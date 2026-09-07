# Models Index

| Name | File | Tags (Keywords) | Description |
| --- | --- | --- | --- |
| AmkExcelSheets | `amkexcelsheets.js` | amk, excel, uploads, files, sheet-metadata, tonnage | Tracks uploaded AMK Excel file metadata, upload timestamps, and total tonnage |
| AmkLotDetails | `amklotdetails.js` | amk-lot, lot-number, batch, condition, qr-code, ser-unse | Model for lot-level AMK ammunition batches, QR codes, and serviceability conditions (SER, UNSE, RMJ, SEG) |
| ArmyUnit | `armyunits.js` | unit, army-unit, formation-unit, army_units | Stores army units linked to military formations (1:N) |
| AssignedLtsDetail | `assignedltsdetail.js` | assigned, lts, driver, vehicle, allocation-model, is-loaded | Model for assigned LTS records linking vehicles, drivers, and LTS issue vouchers |
| BackupDetails | `backupdetails.js` | backup, snapshot, sql-dump, metadata | Stores DB backup metadata, timestamps, and file locations |
| DriverVehicleDetail | `drivervehicledetail.js` | driver, vehicle, trip, load, status-model, ba-number, convoy | Stores driver and vehicle association, loading status, gate check-in/out timestamps |
| ExportSyncHistory | `exportsynchistory.js` | export, sync-history, nfc-sync, parent-depot, auto-import | Stores export gate sync transactions, structured payload, import summary, and user |
| FormationDetails | `formationdetails.js` | formation, unit, brigade, organization, fmn | Stores military/fleet formation unit details |
| Index | `index.js` | sequelize, connection, db, associations, models-init | Sequelize initialization, database connection, model loading, and association setup |
| Log | `log.js` | log, audit, activity, user-action, events, security-log | Stores audit trail entries for user operations across all modules |
| LtsDetail | `ltsdetail.js` | lts, storage, ammunition, stock-record, voucher, issue-voucher | Core LTS details model representing ammunition dispatch issue vouchers |
| ManageAmkQuantity | `manageamkquantity.js` | amk, inventory, quantity, stock-levels, location, 33-fad | Model tracking AMK ammunition quantity allocations and balances by location |
| Role | `role.js` | role, rbac, auth, permissions | Stores user role definitions (Administrator, Gate Operator, Dispatch Clerk, etc.) |
| Series | `series.js` | series, sequence, lot-number, numbering, shift-interval | Manages operational shift time series intervals and sequence numbering |
| SktDetails | `sktdetails.js` | skt, specification, item-details, package-section | Stores SKT base item definitions and package container sections within a voucher |
| SktVarieties | `sktvarieties.js` | skt, variety, item-varieties, types, bridge | Bridge model linking SKT package sections to specific ammunition variety specifications |
| User | `user.js` | user, account, auth, credentials, password, refresh-token | Stores user credentials, hashed passwords, role associations, and active status |
| VarietyDetail | `varietydetail.js` | variety, ammunition-type, specification, ipq, weight | Details for distinct ammunition varieties (IPQ, package weight, loading point) |
| VarietyLoadDetails | `varietyloaddetails.js` | variety-load, lot-load, vehicle-loading-status, load-status | Granular lot-level vehicle loading status (Pending, Partially Loaded, Loaded), condition, and timestamps |
| VehicleType | `vehicletype.js` | vehicle-type, fleet, vehicle-category, 3-ton, 5-ton | Defines vehicle classifications and payload capacity configurations |
