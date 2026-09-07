# Project Memory & Business Context

## 1. Domain Overview & Purpose

The **Depot & Ammunition Dispatch Management System (DMS)** manages secure military depot operations for ammunition inventory, batch lot tracking, Load Tally Sheet (LTS) voucher allocation, convoy vehicle check-in, real-time cargo loading validation, gate checkout, and end-to-end audit security.

---

## 2. Key Domain Terminology & Schema Concepts

- **Users & Roles**: `users` (depot staff, gatekeepers, warehouse managers) linked to `roles` (Administrator, Gate Operator, Dispatch Clerk) determining RBAC permissions.
- **Master Ammunition Inventory**:
  - `amk_excel_sheets`: Master spreadsheets uploaded from headquarters containing stock numbers, file IDs, and total tonnages.
  - `amk_quantities` (`ManageAmkQuantity`): Warehouse inventory ledger entry for a specific ammunition type and storage depot location (e.g., 33 FAD).
  - `amk_lot_details`: Specific lot batches with lot numbers, quantities, QR code hashes, and condition flags.
- **Condition States**:
  - `SER` — Serviceable (Ready to use)
  - `UNSE` — Unserviceable (Damaged/Expired)
  - `RMJ` — Repairable Major (Needs depot repair)
  - `SEG` — Segregated (Quarantined/Inspection)
- **Requisition & Dispatch (LTS)**:
  - `formations`: Military brigade, division, or unit requesting supplies.
  - `lts_issue_voucher_details` (`LtsDetail`): Official dispatch order voucher / Load Tally Sheet (LTS).
  - `skt_details`: Grouped dispatch package container section within an LTS voucher.
  - `skt_varieties`: Bridge entity linking an SKT package section to a specific ammunition variety.
  - `variety_details`: Catalog specifications (IPQ / Items Per Quantity, package weight, shelf-life, loading point LP number).
- **Convoy & Vehicle Check-in**:
  - `vehicle_types`: Transport truck category (3-Ton, 5-Ton, Trailer) defining payload weight limits.
  - `driver_vehicle_details`: Gate pass and convoy check-in ticket recording vehicle registration/BA number, driver identity, escort rank, and entry/exit timestamps (`begin`, `end`).
  - `assigned_lts_issue_voucher_details` (`AssignedLtsDetail`): Slip assigning an LTS voucher to a transport vehicle.
- **Physical Loading & Dispatch**:
  - `variety_load_details`: Real-time loading counter tracking ammunition lots placed inside a vehicle, scanner ID, and status (`Pending`, `Partially Loaded`, `Loaded`).
  - `is_loaded`: Flag on `assigned_lts_issue_voucher_details` marked true once all required lots are packed and verified.
- **Shift Intervals & Audit**:
  - `series`: Operational shift time windows and interval configurations.
  - `logs`: Audit trail recording user actions, IP, HTTP method, module name, and status.
  - `backup_details`: Database snapshot history and file locations.

---

## 3. Core Business Flows (6-Flow Lifecycle)

1. **Authentication & RBAC**: Users authenticate via username, password, and designated Ammunition Point (AP 251-255) (POST `/api/login`), verified against server session AP and `authMiddleware.js`.
2. **Inventory Upload & Lot Master**: Headquarters Excel sheets parsed via `excelTojson.js` / `importExcelFIleDataServices.js`, creating `amk_quantities` and `amk_lot_details` with encrypted AES-256-GCM QR codes.
3. **LTS Voucher Preparation**: Military unit order creates LTS vouchers (`lts_issue_voucher_details`), subdivided into `skt_details`, mapped to `skt_varieties` and `variety_details`. Ammunition quantities can exceed current stock balances (negative inventory loan), permitting dispatch and bulk import when balance is depleted/negative.
4. **Convoy Gate Check-in & LTS Assignment**: Transport vehicles register at the gate (`driver_vehicle_details`), vehicle capacity verified (`vehicleCapacityRoutes.js`), and vouchers assigned via `assigned_lts_issue_voucher_details`.
5. **Physical Loading & Gate Checkout**: Loading crew scans ammunition lot QR codes (`variety_load_details`), status progresses `Pending` -> `Partially Loaded` -> `Loaded`. On complete loading, driver checks out at gate with exit timestamp.
6. **System Audit & Shift Logging**: All operations logged to `logs` via `logger.js` and `logMessageResolver.js`. Shift intervals tracked in `series`.

---

## 4. Architecture & Implementation Conventions

- **Module System**: CommonJS (`require` / `module.exports`).
- **Database & ORM**: MySQL 2 + Sequelize 6. Models initialized in `models/index.js`.
- **Standardized API Response**: All controller responses MUST use `helpers/responseHandler.js`:
  ```javascript
  responseHandler(req, res, statusCode, success, error, data, message);
  ```
- **Validation**: Express-validator middleware in route files (`body()`, `param()`, `query()`) before passing to controller.
- **Error Handling**: Controller functions wrap logic in `try ... catch` blocks and return 500 status via `responseHandler`.
- **Soft Deletion**: Multi-entity purge routines handle cascade logic gracefully where required; series updates do not purge or soft-delete formations or module tables.
- **Pagination with Joins**: When using `findAndCountAll` with 1-to-many associations (e.g. `driver_vehicle_details` joined to `assigned_lts_issue_voucher_details`, `skt_details`, `skt_varieties`), ALWAYS specify `distinct: true, col: 'id'` so Sequelize counts distinct parent records rather than multiplied joined rows.
- **Physical Loading & Tonnage Calculation Rule**: `variety_load_details` records start as `load_status = 'Pending'` upon LTS voucher creation/import as unfulfilled requisition targets. Only lots transitioning to `Partially Loaded` or `Loaded` represent cargo actually loaded onto vehicles. Stored procedure `sp_amk_report` and Tonnage Report exports strictly filter `load_status != 'Pending'` with `0` fallback (`COALESCE(SUM(lot_quantity), 0)`), ensuring items with 0 loaded goods report `0.00` quantity and `0.00` tonnage.
- **Code Cleanliness**: No comments in code files. Maintain max 200-500 lines per file.

