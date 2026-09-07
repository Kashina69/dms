# Services Index

| Name | File | Tags (Keywords) | Description |
| --- | --- | --- | --- |
| AmkQuantityService | `amkQuantityService.js` | amk, quantity, stock-service, calculate, balance | Handles business logic and DB queries for AMK inventory quantities |
| AssignedLTSServices | `assignedLTSServices.js` | assigned-lts, lts-allocation, driver-assignment | Provides database operations for assigning and updating LTS items |
| BackupService | `backupService.js` | backup, mysqldump, database-snapshot, restore | Executes database backup export commands and restore routines |
| DriverVehicleAllServices | `driverVehicleAllServices.js` | driver-vehicle, bulk-driver, batch-ops | Bulk query and status update operations for driver-vehicle pairings |
| DriverVehicleServices | `driverVehicleServices.js` | driver-vehicle, vehicle-mapping, driver-crud | Core operations for driver and vehicle records and check-in |
| ExportSyncService | `exportSyncService.js` | export-sync, unique-locations, auto-import, sync-history | Retrieves unique storage locations, auto-imports batch lots, and queries paginated sync history |
| FetchRecordsServices | `fecthRecordsServices.js` | fetch-records, complex-queries, multi-table, joins, sp_amk_report, fetchAmkListrecords | Complex join queries, aggregated driver-vehicle records, and sp_amk_report invocation for Tonnage report |
| FetchRecordID | `fetchRecordID.js` | record-id, id-resolver, lookup | Helper service to resolve database entity IDs by attributes |
| GateCheckoutSyncServices | `gateCheckoutSyncServices.js` | gate-checkout, checkout-sync, exit-status | Service logic for gate checkout processing and offline sync |
| ImportExcelFileDataServices | `importExcelFIleDataServices.js` | excel-parser, bulk-import, sheet-reader, ingest | Ingests parsed Excel rows and creates database records with validation |
| LogMessageResolver | `logMessageResolver.js` | log-message, audit-text, format-log | Translates system actions and payload diffs into human-readable audit messages |
| LtsServices | `ltsServices.js` | lts, storage-records, lts-db, issue-voucher | LTS database operations, lifecycle management, and status updates |
| ManageAmkQuantityServices | `manageAmkQuantityServices.js` | amk-manage, inventory-levels, stock, ledger | Ammunition quantity allocation and balance updates |
| ModuleNameResolver | `moduleNameResolver.js` | module-name, module-id, resolver | Resolves numeric module IDs to descriptive string identifiers |
| SoftDeleteAllTableEntries | `softDeleteAllTableEntries.js` | soft-delete, cleanup, table-wipe | Handles soft-deletion across multiple entities during reset operations |
| SoftDeleteDriverDataServices | `softDeleteDriverDataServices.js` | soft-delete-driver, purge-driver | Soft delete routines for driver-vehicle records |
| SyncDriverDataServices | `syncDriverDataServices.js` | sync-driver, driver-state-sync, mobile-sync | Synchronizes driver state and assigned vehicle status |
| TimeFormatServices | `timeFormatServices.js` | time-format, date-helper, timestamps | Date and time formatting helpers for logs and database records |
| UpdatedAssignedLTSServices | `updatedAssignedLTSServices.js` | update-assigned-lts, reassign | Reassignment and modification logic for assigned LTS items |
| VarietiesLotsServices | `varietiesLotsServices.js` | variety-lots-service, lot-queries, qr-service, lot-filter | Queries, creates, updates, and deletes lot details and LTS variety mappings |
