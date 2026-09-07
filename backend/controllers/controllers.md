# Controllers Index

| Name | File | Tags (Keywords) | Description |
| --- | --- | --- | --- |
| AmkQuantityController | `amkQuantityControllers.js` | amk, quantity, stock, inventory, calculation, balance | Manages AMK ammunition quantity updates, allocations, and stock status |
| AssignedLtsController | `assignedLtsController.js` | assigned, lts, vehicle, driver, assignment, allocation | Handles LTS voucher assignment to vehicles/drivers, reassignment, and status |
| AuthController | `authController.js` | auth, login, token, session, jwt, user, credentials, ap | Handles user authentication, credential validation, Ammunition Point (AP) session verification, and JWT token issuance |
| BackupController | `backupController.js` | backup, database, restore, dump, sql, snapshot | Manages database backup generation, download, and restore procedures |
| DashboardListViewController | `dashboardListViewController.js` | dashboard, list, view, summary, metrics, overview, chart | Aggregates summary and list metrics for dashboard and DRAWAL progress views |
| DriverController | `driverController.js` | driver, crud, profile, status, driver-details, amk-tonnage, download_amk, excel-export | CRUD management and status tracking for registered drivers, Drawal Excel generation, and AMK Tonnage report export |
| DriverVehicleController | `driverVehicleController.js` | driver-vehicle, mapping, assignment, gate, load, checkout, convoy | Manages vehicle-driver associations, vehicle loading status, and checkout flows |
| ExportSyncController | `exportSyncController.js` | export-sync, locations, data-sync, history, auto-import, nfc | Handles mobile export unique locations lookup, NFC lot data auto-import into AMK inventory, and export sync history listing |
| FormationDetailsController | `formationDetails.js` | formation, unit, brigade, fleet, military, fmn, unit-assignment | Manages formation CRUD operations, Army Unit assignments, validations, and eager loading of units |
| GateCheckoutController | `gateCheckoutController.js` | gate, checkout, security, exit, verification, pass | Handles gate checkout validation, exit timestamps, and pass verification |
| ImportDataController | `importDataController.js` | import, excel, upload, data-import, bulk, xlsx | Handles Excel spreadsheet uploading and data ingestion for LTS, AMK, and SKT |
| LogController | `logController.js` | logs, audit, history, activity, system-events, audit-trail | Fetches and filters system audit and user activity logs |
| LtsDetailsController | `ltsDetailsController.js` | lts, details, storage, ammunition-records, voucher, issue-voucher | Manages LTS record lifecycle, varieties, quantities, and status |
| ManageSeriesController | `manageSeriesControllers.js` | series, sequence, numbering, lot, intervals, shift | Manages series configuration, batch time intervals, and sequence generation |
| RolesController | `rolesController.js` | roles, permissions, rbac, user-roles | Lists and manages system roles and permission access levels |
| SyncDriverVehicleController | `syncDriverVehicleController.js` | sync-driver, driver-vehicle-sync, offline-driver, mobile-sync | Synchronizes driver and vehicle state between mobile devices and central server |
| UsersController | `usersController.js` | users, user-crud, manage-users, accounts, passwords | CRUD management of user accounts, passwords, and profile details |
| VarietiesLotsController | `varietiesLotsController.js` | variety-lots, lot-qr, lot-list, qr-code, generate-lot | Manages ammunition lot details, QR code generation, updates, and variety lot queries |
| VehicleCapacityController | `vehicleCapacityController.js` | vehicle-capacity, tonnage, weight-limit, load-capacity | Manages vehicle capacity constraints and specifications |
| VehicleTypeController | `vehicleTypeController.js` | vehicle-type, classification, fleet-types, 3-ton, 5-ton | Manages vehicle types, categories, and payload configurations |
