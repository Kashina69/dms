# Routes Index

| Name | File | Tags (Keywords) | Description |
| --- | --- | --- | --- |
| AmkQuantityRoutes | `amkQuantityRoutes.js` | amk, quantity, stock, inventory, balance | Endpoints for fetching, updating, and recalculating AMK quantities and balances |
| ArmyUnitRoutes | `armyUnitRoutes.js` | unit, army-unit, formation-unit, bulk-upload, army_units | Army unit creation, updating, listing, soft-deletion, and bulk Excel upload |
| AssignedLtsRoutes | `assignedLtsRoutes.js` | assigned-lts, lts-allocation, driver-lts, vehicle-lts | Endpoints for assigning LTS vouchers to vehicles and drivers, reassigning, and loading status |
| AuthRoutes | `authRoutes.js` | auth, login, jwt, authenticate, access-token, ap | Authentication endpoints (POST `/login` with credentials, AP validation, and JWT issuance) |
| BackupRoutes | `backupRoutes.js` | backup, restore, database-dump, sql, snapshot | Endpoints for generating, listing, and restoring database backups |
| CheckConnectionRoutes | `checkConnectionRoutes.js` | ping, health, db-check, status, connection | Endpoint for verifying database connection and service health |
| DashboardListViewRoutes | `dashboardListViewRoutes.js` | dashboard, list-view, stats, counts, drawal-progress | Endpoints for dashboard summary statistics, metrics, and DRAWAL progress chart data |
| DriverVehicleRoutes | `driverVehicleRoutes.js` | driver, vehicle, vehicle-assignment, trip, convoy | Endpoints for driver registration, vehicle check-in, convoy tracking, and status |
| ExportSyncRoutes | `exportSyncRoutes.js` | export, locations, data-sync, sync-history, nfc-export | Endpoints for mobile NFC export locations lookup, auto-sync/import AMK lots, and sync history logs |
| FetchDetailsRoutes | `fetchDetailsRoutes.js` | fetch-all, lookup, batch-fetch, details, records | Endpoints for aggregated entity data, tracking loading details, and ID lookups |
| FormationRoutes | `formationRoutes.js` | formation, unit, brigade, military-unit, fmn, unit_ids | Endpoints for creating, updating, listing (with associated units), and soft-deleting military formations |
| GateCheckoutSyncRoutes | `gateCheckoutSyncRoutes.js` | gate, checkout, gate-sync, security, departure | Endpoints for gate checkout status updates, vehicle exit timestamps, and offline sync |
| ImportDataRoute | `importDataRoute.js` | import, excel-upload, parse-excel, ingest, bulk-upload | Endpoints for uploading and ingesting Excel spreadsheets for LTS and AMK datasets |
| LogRoutes | `logRoutes.js` | logs, audit-trail, activity-log, audit, security-log | Endpoints for querying system activity, user actions, and audit logs |
| LtsDetailsRoutes | `ltsDetailsRoutes.js` | lts, lts-details, ammunition-records, voucher, issue-voucher | Endpoints for CRUD operations on LTS issue vouchers, SKT items, and varieties |
| RoleRoutes | `roleRoutes.js` | roles, rbac, user-roles, permissions | Endpoints for listing available user roles and permissions |
| SeriesRouter | `seriesRouter.js` | series, numbering, sequence, series-config, intervals | Endpoints for managing time-series shift intervals and series generation |
| SyncDriverDataRoutes | `syncDriverDataRoutes.js` | sync-driver, driver-sync, unloaded-drivers, mobile-control | Endpoints for synchronizing driver vehicle loading state with mobile control center |
| UserRoutes | `userRoutes.js` | users, user-crud, manage-users, accounts, password-reset | Endpoints for user account CRUD, status toggling, and role assignments |
| VarietiesLotsRoutes | `varietiesLotsRoutes.js` | lot-qr, varieties-lots, lot-details, qr-details, lot-management | Endpoints for generating, listing, updating, and deleting variety lot QR codes and details |
| VehicleCapacityRoutes | `vehicleCapacityRoutes.js` | vehicle-capacity, tonnage, weight-limits, payload | Endpoints for vehicle load capacity configurations and limits |
| VehicleTypeRoutes | `vehicleTypeRoutes.js` | vehicle-type, categories, fleet-types, 3-ton, 5-ton | Endpoints for vehicle type listings, fleet classifications, and configurations |
