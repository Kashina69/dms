# UI Components & Sub-Components Index

| Component | File Path | Tags (Keywords) | Description |
| --- | --- | --- | --- |
| `Loader` | `src/Common/Loader.jsx` | loader, spinner, loading-overlay, progress | Full-screen and inline loading overlay spinner |
| `LayoutPage` | `src/layout/LayoutPage.jsx` | layout, sidebar, header, topbar, navigation | Master application layout containing responsive sidebar, navigation menu, and user header |
| `PrivateRoutes` | `src/routing/PrivateRoutes.jsx` | private-route, route-guard, auth-guard, protection | Route wrapper checking authentication token before rendering protected child routes |
| `ActivityLogsForm` | `src/activityLogs/ActivityLogsForm.jsx` | logs-filter, search-logs, date-filter, audit-form | Filter toolbar for searching audit logs by date range, user, and module |
| `ActivityLogsModel` | `src/activityLogs/ActivityLogsModel.jsx` | log-details-modal, payload-view, audit-modal | Modal displaying detailed request payload and response metadata for a selected log entry |
| `ActivityLogsTable` | `src/activityLogs/ActivityLogsTable.jsx` | logs-table, audit-grid, paginated-logs | Paginated table rendering audit trail entries with status tags |
| `CreateLtsForm` | `src/manageLts/CreateLtsForm.jsx` | create-lts-form, voucher-form, skt-form, lot-picker | Multi-step form for configuring LTS vouchers, SKT groups, varieties, and lot assignments |
| `ConfirmationDialog` | `src/manageLts/ConfirmationDialog.jsx` | confirm-modal, prompt-dialog, lts-confirm | General-purpose confirmation prompt modal for LTS actions |
| `ConfirmationUpdateFormation` | `src/manageLts/ConfirmationUpdateFormation.jsx` | formation-confirm, update-unit-modal | Confirmation dialog when modifying assigned military formation on an existing voucher |
| `DeleteLtsModal` | `src/manageLts/DeleteLtsModal.jsx` | delete-lts, remove-voucher-modal | Confirmation modal for soft-deleting an LTS issue voucher |
| `lotConfirmationDialog` | `src/manageLts/lotConfirmationDialog.jsx` | lot-confirm, select-lot-modal | Modal verifying lot selection and quantity sufficiency before allocation |
| `PaginationFooter` | `src/manageLts/PaginationFooter.jsx` | pagination, pager, table-footer | Reusable pagination controls with page size selector and item counter |
| `DriverForm` | `src/manageDriver/DriverForm.jsx` | driver-form, vehicle-form, checkin-inputs | Form for registering driver identity, vehicle registration (BA number), escort, and tonnage capacity |
| `DriverList` | `src/manageDriver/DriverList.jsx` | driver-table, vehicle-roster, convoy-list | Table listing registered convoy vehicles, driver names, and gate status |
| `FormationFormModal` | `src/manageFormation/FormationFormModal.jsx` | formation-modal, unit-form, add-fmn, unit-multiselect | Modal form for creating and editing military formation records with Army Unit multiselect dropdown |
| `FormationList` | `src/manageFormation/FormationList.jsx` | formation-table, fmn-list, assigned-units, units-modal | Paginated table rendering military formations with assigned units eye button and popup modal with unit chips |
| `FormationDeleteModal` | `src/manageFormation/FormationDeleteModal.jsx` | formation-delete, remove-unit-modal | Confirmation modal for deleting military formations |
| `ManageAmkLotModal` | `src/manageAMKQuantity/ManageAmkLotModal.jsx` | amk-lot-modal, edit-lots, condition-editor | Modal for viewing and updating lot batch numbers and condition states (SER, UNSE, RMJ, SEG) |
| `ManageAMKQuantityDeleteModal` | `src/manageAMKQuantity/ManageAMKQuantityDeleteModal.jsx` | amk-delete-modal, remove-stock-modal | Confirmation dialog for removing ammunition stock items |
| `ManageAMKQuantityFile` | `src/manageAMKQuantity/ManageAMKQuantityFile.jsx` | upload-modal, excel-dropzone, file-import | File upload component for ingesting headquarters Excel ammunition stock spreadsheets |
| `manageAMKQuantityModal` | `src/manageAMKQuantity/manageAMKQuantityModal.jsx` | amk-form-modal, add-stock-modal | Modal dialog for creating or updating master AMK item records |
| `ManageAMKQuantitySearch` | `src/manageAMKQuantity/ManageAMKQuantitySearch.jsx` | amk-search, filter-stock, inventory-search | Search toolbar and filter dropdowns for ammunition inventory ledger |
| `QRCodesForm` | `src/manageQRCodes/QRCodesForm.jsx` | qr-form, generate-barcode-form, lot-qr-inputs | Form for generating encrypted variety lot QR code batches with IPQ and series parameters |
| `LotDetailsModal` | `src/manageQRCodes/LotDetailsModal.jsx` | qr-lot-modal, decoded-qr-view | Modal displaying decoded lot metadata, signature verification status, and batch details |
| `DeleteConfirmation` | `src/manageQRCodes/DeleteConfirmation.jsx` | delete-qr-modal, remove-barcode-modal | Confirmation dialog for deleting QR code batches |
| `DuplicatePopover` | `src/track/DuplicatePopover.jsx` | duplicate-popover, scan-warning, duplicate-alert | Warning popover alerting loader operator when a barcode has already been scanned |
| `AssignedLtsDetails` | `src/track/AssignedLtsDetails.jsx` | track-lts-card, variety-progress, cargo-progress | Progress card showing ammunition varieties assigned to a vehicle and real-time loading count |
| `BackupList` | `src/settings/backup/BackupList.jsx` | backup-table, snapshot-list, restore-table | Table listing available database snapshots with download and restore action buttons |
| `ArmyUnitList` | `src/manageArmyUnits/ArmyUnitList.jsx` | army-unit-table, units-list, unit-grid | Paginated table rendering army units with serial numbers, formation tags, and edit/delete actions |
| `ArmyUnitFormModal` | `src/manageArmyUnits/ArmyUnitFormModal.jsx` | army-unit-modal, add-unit, edit-unit | Form modal for creating single or comma-separated army units and editing unit details with formation selector |
| `ArmyUnitDeleteModal` | `src/manageArmyUnits/ArmyUnitDeleteModal.jsx` | delete-unit-modal, confirm-delete-unit | Confirmation dialog modal for soft-deleting army unit records |
| `DuplicateUnitModal` | `src/manageArmyUnits/DuplicateUnitModal.jsx` | duplicate-unit-modal, conflict-error, unit-validation | Modal displaying existing duplicate Army Units and their assigned formations when creation or update fails |
| `ExcelImportErrorModal` | `src/manageArmyUnits/ExcelImportErrorModal.jsx` | excel-error-modal, invalid-formations, import-abort | Modal displaying validation errors and non-existing formations from Excel sheets |
| `ExcelImportConfirmModal` | `src/manageArmyUnits/ExcelImportConfirmModal.jsx` | excel-confirm-modal, import-preview, diff-table | Modal displaying bulk import preview diff (creations, formation updates, unassigned) with confirmation |
