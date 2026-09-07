# Project Information

## 1. Stack

- **Framework & Runtime** — React 18.2.0 (Create React App / react-scripts 5.0.1) & Electron 25.4.0 (Desktop Container)
- **UI Components & Styling** — Material UI v5 (`@mui/material`, `@mui/icons-material`), Ant Design 5.8.2 (`antd`), React-Bootstrap 2.8.0 / Bootstrap 5.3.1, Emotion
- **Routing** — React Router DOM v6.14.2 (`BrowserRouter`, `Routes`, `Route`, `Navigate`)
- **Forms & Validation** — Formik 2.4.3 + Yup 1.2.0
- **HTTP Client** — Axios 1.4.0 (`src/api/apiInterceptor.js` with bearer token injection)
- **Date & Time** — Day.js 1.11.9, Moment.js 2.29.4, Moment Timezone 0.5.43
- **Language** — JavaScript (ES6+ / JSX)
- **Package Manager** — Yarn (v1.22.22) / npm
- **Build & Packaging** — Webpack (react-scripts), electron-builder 24.6.3, electronmon 2.0.2

## 2. Commands

| Command | Action |
| --- | --- |
| `yarn start` / `npm start` | Run React web app in development mode (port 3000) |
| `yarn build` / `npm run build` | Build production React bundle to `build/` |
| `yarn electron:dev` | Start React dev server (port 3001) + Electron in watch mode |
| `yarn electron:start` | Start React dev server (port 3000) + Electron with electronmon |
| `yarn electron:test` | Build and serve production bundle in Electron test mode |
| `yarn electron:package:linux` | Package Electron desktop app for Linux (`.deb`) |
| `yarn electron:package:win` | Package Electron desktop app for Windows (`.exe` / NSIS) |
| `yarn electron:package:mac` | Package Electron desktop app for macOS (`.dmg`) |
| `../start.sh` | Run both backend and frontend concurrently from workspace root |

## 3. Folder Structure

```
[frontend]/
├── public/                  # Static assets, HTML shell, Electron main process & preload
│   ├── electron.js          # Electron main process window management & IPC
│   ├── preload.js           # Electron context isolation & preload scripts
│   └── index.html           # HTML5 template entry point
├── src/
│   ├── Common/              # Shared components (Loader), base config, Material Icons
│   ├── activityLogs/        # Audit & system activity logs viewer, filters & detail modal
│   ├── api/                 # Centralized Axios interceptor & HTTP request handling
│   ├── apiUrlPage/          # Backend API host/port configuration settings UI
│   ├── assets/              # CSS stylesheets, static images & icons
│   ├── auth/                # User login, authentication states & auth event services
│   ├── dashboard/           # Operational dashboard metrics, series breakdown & status tables
│   ├── downloadReport/      # Excel & PDF audit report generation and export
│   ├── faq/                 # In-app user manual, workflows & troubleshooting guide
│   ├── layout/              # App layout shell: Topbar, Sidebar navigation & route Outlet
│   ├── manageAMKQuantity/   # Master AMK ammunition inventory ledger & Excel upload
│   ├── manageDriver/        # Convoy driver & vehicle gate pass check-in management
│   ├── manageFormation/     # Military unit & formation administration
│   ├── manageLts/           # Load Tally Sheet (LTS) voucher allocation & SKT packages
│   ├── manageQRCodes/       # Variety lot encrypted QR code generation & label printing
│   ├── manageSeriesTime/    # Operational shift intervals and time series management
│   ├── manageUser/          # User accounts, RBAC permissions & role assignments
│   ├── routing/             # App route declarations, route constants & PrivateRoute guards
│   ├── settings/            # System settings (database backup & snapshots)
│   ├── track/               # Live cargo loading scanner, barcode verification & gate pass
│   ├── App.js               # Top-level React component & routing wrapper
│   ├── index.js             # React DOM entry point
│   └── index.css            # Global CSS styles
```

## 4. Code Conventions

### 4.1 File Length
- **Max 200 lines** for simple files
- **Max 500 lines** for complex files

### 4.2 Naming
| Type | Pattern | Example |
| --- | --- | --- |
| Component file | `PascalCase.jsx` | `ManageLts.jsx`, `DriverForm.jsx` |
| Event / Service file | `camelCase.js` or `camelCaseEvent.js` | `event.js`, `dashboardEvent.js` |
| State / Schema file | `camelCase.js` or `camelCaseStates.js` | `commonState.js`, `manageLtsStates.js` |
| Route constants | `camelCase.js` | `routeConstants.js` |
| Interceptor | `camelCase.js` | `apiInterceptor.js` |

### 4.3 Splitting Rules
- If a component file approaches 200 lines → extract sub-components (modals, forms, tables, filters)
- Place all API calls and network operations in module `event.js` files rather than inside UI components
- Extract Formik validation schemas and initial values into `commonStates.js` or `manage<Module>States.js`
- No comments in code files
- Always use `apiInterceptor.js` for HTTP requests to ensure JWT token attachment and error trapping
