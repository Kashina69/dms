# Routes Index (Frontend)

| Constant | Path | Protected | Component | Tags (Keywords) | Description |
| --- | --- | --- | --- | --- | --- |
| `API_URL_PAGE` | `/api_url` | No | `Config` | api-url, config, backend-host, settings | Backend API connection configuration & testing screen |
| `LOGIN` | `/login` | No | `Login` | login, auth, session, credentials | User authentication login form |
| `DASHBOARD` | `/dashboard` | Yes | `Dashboard` (Layout) | dashboard, home, metrics, overview | Main operations dashboard with metric widgets and shift status |
| `DASHBOARD_VIEW` | `/dashboard-view` | Yes | `DashboardTable` | dashboard-table, full-view, series-grid | Full-screen table view of vehicle loading by operational series |
| `MANAGE_LTS` | `/manage-lts` | Yes | `ManageLts` (Layout) | lts, vouchers, dispatch-list, tally-sheet | LTS voucher management and listing view |
| `ADD_LTS` | `/manage-lts/add` | Yes | `AddLts` (Layout) | create-lts, add-voucher, new-lts | Step-by-step form to create new LTS vouchers and varieties |
| `EDIT_LTS` | `/manage-lts/edit` | Yes | `EditLts` (Layout) | edit-lts, modify-voucher, update-lts | Form to update existing LTS voucher packages and allocations |
| `PRINT_LTS_DETAILS` | `/print-lts-details/:id` | Yes | `PrintLtsDetils` | print-lts, voucher-slip, issue-sheet | Printable view for a single LTS issue voucher |
| `PRINT_MULTIPLE_DRIVER_LTS_DATA` | `/print-multiple-driver-lts-data` | Yes | `PrintMultipleDriverLtsData` | print-lts-batch, driver-lts, convoy-slips | Batch printable slip layout for multiple driver LTS vouchers |
| `TRACK` | `/track-loading` | Yes | `TrackLoading` (Layout) | track, cargo-loading, barcode-scan, verification | Real-time cargo loading tracking and barcode scanner interface |
| `TRACKBYID` | `/track-loading/:id` | Yes | `TrackLoadingByID` (Layout) | track-vehicle, vehicle-loading, ba-track | Loading progress and scanned lot verification for a specific vehicle |
| `PRINT_PAGE` | `/print-page/:id` | No | `PrintEvent` | print-gatepass, loading-summary, slip | Printable vehicle loading pass and audit slip |
| `MANAGE_DRIVER` | `/manage-driver` | Yes | `ManageDriver` (Layout) | drivers, vehicles, convoy, check-in | Vehicle & driver check-in management and convoy roster |
| `ADD_DRIVER` | `/manage-driver/add` | Yes | `AddDriver` (Layout) | add-driver, register-vehicle, check-in-form | Form to check-in new vehicle, driver, and escort details |
| `EDIT_DRIVER` | `/manage-driver/edit` | Yes | `EditDriver` (Layout) | edit-driver, update-vehicle, driver-modify | Form to edit driver registration and vehicle capacity details |
| `PRINT_DRIVER_DETAILS` | `/print-driver-details/:id` | Yes | `PrintDriverDetails` | print-driver, single-gatepass, vehicle-slip | Printable gate check-in pass for a single vehicle |
| `PRINT_MULTIPLE_DRIVER_DATA` | `/print-multiple-driver-data` | Yes | `PrintMultipleDriverData` | print-drivers-batch, convoy-gatepasses | Batch printable gate check-in passes for convoy vehicles |
| `MANAGE_FORMATION` | `/manage-formation` | Yes | `ManageFormation` (Layout) | formation, unit, brigade, military-unit | Administration of military units and formations |
| `MANAGEAMKQUANTITY` | `/manage-amk-quantity` | Yes | `ManageAmkQuantity` (Layout) | amk, inventory, stock-ledger, ammunition | Master ammunition stock ledger and Excel sheet upload |
| `MANAGEQRCODES` | `/manage-qr-codes` | Yes | `ManageQR` (Layout) | qr-codes, barcodes, lot-hashes, qr-manager | Variety lot QR code generation, search, and validation |
| `PRINTQRCODES` | `/print-lot-qr-details/:id` | Yes | `PrintQrCodes` | print-qr, lot-labels, barcode-stickers | Printable QR code label sheet for ammunition lot batches |
| `MANAGESERIES` | `/manage-series` | Yes | `ManageSeries` (Layout) | series, shifts, operational-hours, series-time | Shift time configuration and series numbering |
| `DOWNLOAD` | `/download` | Yes | `DownloadReport` (Layout) | download, reports, excel-export, pdf-export | System data export and audit report generation |
| `ACTIVITY_LOGS` | `/activity-logs` | Yes | `ActivityLogs` (Layout) | activity-logs, audit, security-logs, user-actions | Audit log viewer with user/action filtering and payload modals |
| `MANAGE_USER` | `/manage-user` | Yes | `ManageUser` (Layout) | users, accounts, rbac, user-list | System user accounts and role administration |
| `CREATE_USER` | `/manage-user/create` | Yes | `AddUser` (Layout) | create-user, new-user, add-account | Form to register a new user account with role selection |
| `EDIT_USER` | `/manage-user/edit` | Yes | `EditUser` (Layout) | edit-user, update-user, modify-account | Form to update user profile and permissions |
| `MANAGE_BACKUP` | `/backup` | Yes | `Backup` (Layout) | backup, restore, database-dump, snapshots | Database snapshot creation, listing, and recovery |
| `FAQ` | `/faq` | Yes | `FaqModule` (Layout) | faq, help, user-manual, troubleshooting | In-app user manual and troubleshooting FAQ |
| `ARMY_UNITS` | `/army-units` | Yes | `ManageArmyUnits` (Layout) | army-units, units, military-units, unit-data | Army unit management, Excel data import, and list view |
| `EXPORT_SYNC_HISTORY` | `/export-sync-history` | Yes | `ExportSyncHistory` (Layout) | export-sync, sync-history, nfc-export, parent-depot | Export sync history log viewer with filtering, payload modal, and AMK details |

