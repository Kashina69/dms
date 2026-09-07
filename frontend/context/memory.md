# Frontend Memory & Architectural Context

## 1. Frontend Architecture Overview

The **DMS Frontend** is a desktop-ready React 18 single-page application packaged inside an Electron 25 shell. It provides a secure, high-throughput user interface for depot operators to manage ammunition inventories, issue vouchers (LTS), check in convoy vehicles, scan encrypted QR code barcodes during cargo loading, and audit all depot transactions.

---

## 2. Key UI/UX Patterns & State Management

- **Component Organization**:
  - Each major feature resides in its own top-level directory under `src/` (e.g. `src/manageLts/`, `src/track/`).
  - Feature directories contain the main page component (`PascalCase.jsx`), sub-components (modals, tables, filters), form states/schemas (`commonState.js`), and API event services (`event.js`).
- **Form Management**:
  - Forms use Formik + Yup for schema validation.
  - Complex multi-step forms (e.g., `CreateLtsForm.jsx`, `DriverForm.jsx`) maintain state transitions cleanly with validation at each stage.
  - LTS creation allows quantity given to exceed available stock balances without restriction, reflecting negative inventory loans.
- **Inventory Presentation**:
  - `ManageAMKQuantityTable.jsx` highlights rows with negative `actual_quantity` using `.negative-quantity-row` theme styling.
- **HTTP & Authentication**:
  - Centralized Axios instance in `src/api/apiInterceptor.js`.
  - Injects JWT token into `Authorization: Bearer <token>` header on every outgoing request.
  - Login requires Ammunition Point selection (AP 251 - AP 255) alongside credentials.
  - Intercepts 401 Unauthorized responses to clear local storage session and redirect to `/login`.
- **API Host Configuration**:
  - `src/apiUrlPage/Config.jsx` allows operators on standalone depot machines to configure and test the backend server endpoint URL and port.

---

## 3. Real-Time Cargo Tracking & Scanning Flow (`src/track/`)

1. **Vehicle Selection**: Operator selects or enters a vehicle registration / BA number.
2. **LTS Loading Progress**: System loads the assigned LTS voucher, varieties, and target quantities (`AssignedLtsDetails.jsx`).
3. **Barcode Scanning**: Operator scans AES-256 encrypted QR codes on ammunition boxes.
4. **Validation & Duplicate Prevention**:
   - `DuplicatePopover.jsx` flags barcodes already scanned in the current session.
   - Condition states (`SER`, `UNSE`, `RMJ`, `SEG`) are verified in real time.
   - Quantities increment until the variety target is reached.
5. **Completion & Gate Pass**: Once all varieties are loaded (`Loaded` state), the vehicle exit pass (`PrintAssignedLtsDetails.jsx` / `PrintEvent.jsx`) is printed for security gate departure.

---

## 4. Electron Desktop Integration (`public/`)

- **Main Process (`public/electron.js`)**: Manages BrowserWindow lifecycle, hardware window controls (maximize, minimize, close), offline file dialogs, and native printing.
- **Preload Script (`public/preload.js`)**: Exposes safe Electron IPC bridges to the React renderer via context isolation.
- **Print Views**: Specialized printable components (`PrintLtsDetils.jsx`, `PrintDriverDetails.jsx`, `PrintQrCodes.jsx`) render clean, print-optimized layouts suitable for depot thermal/laser printers without UI chrome.

---

## 5. Coding & Contribution Rules

- **Modularity**: Extract tables, modals, and search bars when components exceed 200 lines.
- **Cleanliness**: No comments in code files. Maintain concise and clean JSX.
- **API Calls**: Never invoke `axios` directly in React components; delegate all HTTP interactions to module-level `event.js` files.
- **Icons & Theme**: Use icons from `src/Common/materialIcons.js` or MUI icons. Maintain consistent depot theme styling.
