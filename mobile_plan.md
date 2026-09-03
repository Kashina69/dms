# Export Gate Flow — Mobile App Implementation & Integration Guide

**Document Purpose**: Handoff specification for the Android Developer and their AI Agent.

---

> [!IMPORTANT]
> ### 🚀 Workspace & Branch Setup (For Android Dev + AI Agent)
> 
> The backend APIs and the desktop **Inventory Receipt** UI are already built and tested.
> 
> 1. **Git Branch**: Ensure your workspace for both the backend (Express/Node.js) and frontend (React/Electron) is checked out to:
>    ```bash
>    git checkout feat/export-sync-history
>    git pull origin feat/export-sync-history
>    ```
> 2. **Run Backend Migrations**:
>    ```bash
>    cd backend
>    npx sequelize-cli db:migrate
>    ```
>    *(Or starting the backend with `npm run dev` will auto-run pending migrations upon initialization).*
> 3. **Database Notice**: By default, there is **no dummy data** in your local database. `GET /api/export/locations` will return locations currently existing in your local `amk_quantities` table (or an empty list `[]` on a fresh database).
> 4. **AI Agent Permission Note**: You have access to the actual mobile codebase and NFC card reading logic that the server team did not have. If your AI agent identifies minor field structure differences between the NFC card and the backend payload, **you are permitted to make minor, surgical adjustments to the backend on `feat/export-sync-history` if strictly necessary**.

---

## 1. Business Flow & User Journey

The DMS mobile app is used at **Place B's entry gate**. When a convoy arrives with an LTS (Load Tally Sheet) from Place A:

1. Gatekeeper opens mobile app → taps **"EXPORT"** on the home/login screen.
2. Enters gate password → taps **"Proceed"**.
3. Taps **"SCAN NFC CARD"** → scans the NFC card physically mounted on or carried by the arriving vehicle.
4. App reads and parses the JSON payload from the NFC card.
5. **NEW UI**: User fills in shipment storage details (Parent Depot Name, New Storage Location dropdowns).
6. Taps **"EXPORT & Auto Sync"** button:
   - Generates and saves the updated Excel file locally.
   - Sends payload to Place B server via `POST /api/export/data-sync`.
   - Place B server auto-imports AMK inventory and logs the transaction.
   - Desktop dashboard updates in real time under **Settings → Inventory Receipt**.

---

## 2. Mobile App UI Changes (After NFC Scan Screen)

Currently, after scanning an NFC card, the screen displays simple vehicle summary boxes (Vehicle Number, Driver Name, Unit, Checkout Time, Scanned At).

### 2.1 Top Section — "Parent Depot Name" Input Field

Add a text input field at the **top** of the screen, above the vehicle info section:

| Element | Type | Label | Required | Details |
|---|---|---|---|---|
| **Parent Depot Name** | `TextInput` | `"Parent Depot Name"` | **Optional** | Free text input (NOT a dropdown). Captures Place A origin name (e.g., *"33 FAD Central Depot"*). |

---

### 2.2 AMK Details Section — Item Cards List

Replace the current single box with a **list of AMK Item Cards**. For each variety/AMK item extracted from the NFC card JSON:

| Field | Source from NFC JSON | UI Element | Details |
|---|---|---|---|
| **AMK Number** | `varieties[].amk_number` | Text Label | e.g. `AMK-556-01` |
| **Nomenclature** | `varieties[].nomenclature` | Text Label | e.g. `5.56mm Ball Cartridge 1A` |
| **Location (Place A)** | `skts[].skt_name` | Text Label | The SKT name **is** the Place A storage location (e.g. `Shed A-3`) |
| **Given Quantity** | `varieties[].qty` | Text Label | Total quantity in this shipment |
| **New Storage Location** | User Selection | **Searchable Dropdown** | Destination storage shed at Place B *(See Section 2.3)* |

---

### 2.3 New Storage Location Dropdown & "+ Add Location" Modal

Each AMK item card contains a dropdown for selecting the Place B storage location:

- **Data Source**: Call `GET /api/export/locations` **once** immediately after scanning the NFC card. Cache this array locally and populate all AMK card dropdowns.
- **Searchable/Autocomplete**: User can type to filter dropdown options.
- **Default State**: Empty / unselected.
- **"+ Add Location" Option**:
  - At the very bottom of the dropdown options, display a button: **`"+ Add Location"`**.
  - Tapping this opens a simple modal/dialog:
    - **Title**: *"Add New Location"*
    - **Input**: Text field for Location Name (e.g., *"Shed Z-14"* or *"Bunker 9"*)
    - **Buttons**: `Save` and `Cancel`
  - When `Save` is tapped:
    1. The new location is added to the local dropdown list in memory for the current session.
    2. It is automatically selected for that AMK item card.
    3. The flag `is_custom_location = true` is set for this item.
    *(No immediate server API call is needed for custom location creation; the server will auto-create it during sync).*

---

### 2.4 Button Renaming & Flow

| Old Button Label | New Button Label | Behavior |
|---|---|---|
| `"EXPORT SELECTED"` | **`"EXPORT & Auto Sync"`** | Triggers confirmation validation → Generates Excel → Calls Sync API |

---

### 2.5 Confirmation Warning Modal Logic

When the user taps **"EXPORT & Auto Sync"**, run these three validation checks:

- **Check 1**: Is `parent_depot_name` empty?
- **Check 2**: Are any AMK item cards missing a `new_location` selection?
- **Check 3**: Were any **custom locations** added via "+ Add Location"?

#### Modal Rules:
1. **If Check 1 OR Check 2 is TRUE**: Display a **Warning Confirmation Modal**:
   ```text
   ┌──────────────────────────────────────────────┐
   │  ⚠️ Missing Information                  [X] │
   │                                              │
   │  The following fields are not filled:        │
   │  • Parent Depot Name: Not provided           │
   │  • AMK-556-01 — New Location: Not selected   │
   │                                              │
   │  (If applicable):                            │
   │  ⚡ You have added custom location(s):       │
   │    - "Bunker Underground U-4" (custom)       │
   │                                              │
   │  Do you want to continue anyway?             │
   │                                              │
   │       [ Cancel ]         [ Continue ]        │
   └──────────────────────────────────────────────┘
   ```
   - **Cancel** or **[X]** or **Android Hardware Back Button**: Closes modal and returns to the form without losing any entered data.
   - **Continue**: Proceeds with Excel export and server sync.

2. **If only Check 3 is TRUE** (all fields filled, but custom locations were used):
   - Show an informational modal mentioning the custom location(s) with `Continue` and `Cancel`.
3. **If all fields are filled and NO custom locations**:
   - Skip modal and proceed directly.

---

### 2.6 Excel Export Location Replacement

In the existing local Excel generation logic:
1. Find the storage location column by matching header names against regex/list: `["loc", "shed_location", "shed_loc", "location"]`.
2. Replace the old Place A location value with the **newly selected storage location** from the dropdown.
3. If the user left the dropdown empty, retain the original Place A location (`skt_name`).
4. Save the Excel file locally as usual.

---

### 2.7 Server Sync API Call (`POST /api/export/data-sync`)

Immediately after the Excel file is generated and saved:

1. Make the HTTP POST request to `http://<server-ip>:8080/api/export/data-sync`.
2. **On HTTP 200 Success**:
   - Show toast: *"Data synced successfully"*.
   - Return to home/export scan screen.
3. **On Network Error / Failure**:
   - Show toast: *"Sync failed. Please try again."*
   - Keep the generated Excel file locally so no data is lost.
   - Allow user to tap *"EXPORT & Auto Sync"* again to retry if needed.

---

## 3. Backend API Contracts (Live on `feat/export-sync-history`)

### 3.1 GET `/api/export/locations`

Returns all existing distinct storage locations from inventory.

- **URL**: `GET /api/export/locations`
- **Headers**:
  ```http
  Authorization: Bearer <token>
  user_id: <user_id>
  password: <password>
  ```
- **Success Response (200 OK)**:
  ```json
  {
    "success": true,
    "data": [
      "33 FAD",
      "Cold Storage 1",
      "Main Store B-1",
      "Shed 4",
      "Shed A-1"
    ],
    "message": "Locations fetched successfully"
  }
  ```

---

### 3.2 POST `/api/export/data-sync`

Atomically auto-imports AMK inventory lots and records shipment history.

- **URL**: `POST /api/export/data-sync`
- **Headers**:
  ```http
  Content-Type: application/json
  Authorization: Bearer <token>
  user_id: <user_id>
  password: <password>
  ```
- **Request Body Payload**:
  ```json
  {
    "parent_depot_name": "33 FAD Central Depot (Place A)",
    "vehicle_number": "BA-21D874512K",
    "driver_name": "Sepoy Rajesh Kumar",
    "unit": "25 Inf Div Ord Unit",
    "checkout_time": "2026-09-01T08:30:00.000Z",
    "scanned_at": "2026-09-01T10:15:30.000Z",
    "lts_name": "LTS/2026/09/001",
    "formation_name": "25 Infantry Division",
    "amk_items": [
      {
        "amk_number": "AMK-556-01",
        "nomenclature": "5.56mm Ball Cartridge 1A",
        "old_location": "Shed A-3",
        "new_location": "Main Store B-1",
        "is_custom_location": false,
        "given_quantity": 5000,
        "amn_shelf_life": "2030",
        "lots": [
          {
            "lot_number": "230510/KGP",
            "lot_quantity": 2500,
            "condition": "SER",
            "pkg_type": "Box"
          },
          {
            "lot_number": "230512/KGP",
            "lot_quantity": 2500,
            "condition": "SER",
            "pkg_type": "Box"
          }
        ]
      }
    ],
    "raw_nfc_json": { }
  }
  ```
- **Field Specifications**:
  - `parent_depot_name` *(string, optional)*: Origin depot name typed by user.
  - `vehicle_number` *(string, required)*: BA number from NFC card.
  - `driver_name` *(string, required)*: Driver name from NFC card.
  - `unit` *(string, optional)*: Unit/formation from NFC card.
  - `checkout_time` *(ISO string, optional)*: When vehicle departed Place A.
  - `scanned_at` *(ISO string, required)*: Current device timestamp when card was scanned at Place B.
  - `lts_name` *(string, optional)*: LTS voucher number from card.
  - `amk_items` *(array, required)*: Flat array of all AMK varieties.
  - `amk_items[].old_location` *(string, optional)*: Place A location (`skt_name` from NFC).
  - `amk_items[].new_location` *(string, optional)*: Selected Place B storage location.
  - `amk_items[].is_custom_location` *(boolean, required)*: `true` if typed via "+ Add Location", `false` if picked from dropdown.
  - `raw_nfc_json` *(object, optional)*: The complete parsed JSON object from the NFC card for auditing.
- **Success Response (200 OK)**:
  ```json
  {
    "success": true,
    "data": {
      "history_id": 1,
      "import_summary": {
        "total_amk_items": 1,
        "total_lots_imported": 2,
        "new_locations_created": 0,
        "success_count": 1,
        "error_count": 0
      }
    },
    "message": "Data synced and imported successfully"
  }
  ```

---

## 4. NFC JSON Structure & Flattening Reference

When the mobile app reads the card, the payload tree is structured as:

```text
root (vehicle_number_ba_number, driver_name, unit, end)
 └── ltsData[] (ltsNo, formation_name)
      └── skts[] (skt_name -> Old Storage Location)
           └── varieties[] (amk_number, nomenclature, qty, amn_shelf_life)
                └── lot_numbers[] (lot_number, lot_quantity, condition, pkg_type)
```

### Flattening Loop:
```kotlin
val amkItemsList = mutableListOf<AmkItemDto>()

for (lts in nfcPayload.ltsData) {
    for (skt in lts.skts) {
        val oldLocation = skt.skt_name // SKT name is the Place A storage location
        
        for (variety in skt.varieties) {
            val lotsList = variety.lot_numbers.map { lot ->
                LotDto(
                    lot_number = lot.lot_number,
                    lot_quantity = lot.lot_quantity,
                    condition = lot.condition ?: "SER",
                    pkg_type = lot.pkg_type ?: "Box"
                )
            }
            
            amkItemsList.add(
                AmkItemDto(
                    amk_number = variety.amk_number,
                    nomenclature = variety.nomenclature,
                    old_location = oldLocation,
                    new_location = userSelectedLocationMap[variety.amk_number] ?: oldLocation,
                    is_custom_location = isCustomLocationMap[variety.amk_number] ?: false,
                    given_quantity = variety.qty,
                    amn_shelf_life = variety.amn_shelf_life,
                    lots = lotsList
                )
            )
        }
    }
}
```

> [!NOTE]
> If the same `amk_number` appears under **multiple SKTs** (different storage locations), treat them as separate item cards in the UI so the user can assign different Place B sheds to each.

---

## 5. End-to-End Verification Checklist

1. [ ] Pull `feat/export-sync-history` on backend and ensure server runs on port 8080.
2. [ ] Open mobile app → tap **EXPORT** → enter password.
3. [ ] Scan NFC card on vehicle.
4. [ ] Verify `GET /api/export/locations` runs once and populates the location dropdowns.
5. [ ] Enter a **Parent Depot Name** (or leave empty).
6. [ ] Test "+ Add Location" modal to add a custom shed (e.g. `"Bunker 9"`).
7. [ ] Tap **"EXPORT & Auto Sync"** → verify confirmation modal pops up if fields are missing or custom locations are used.
8. [ ] Confirm Excel file downloads locally with the new shed location in the location column.
9. [ ] Confirm `POST /api/export/data-sync` succeeds and shows *"Data synced successfully"*.
10. [ ] Open Desktop Web App → navigate to **Settings → Inventory Receipt** and confirm the newly synced record appears with its lots and locations.
