# Project Information

## 1. Stack

- **Framework** — Express.js 4.18.2 (REST API)
- **Database / ORM** — MySQL 2 / Sequelize 6.32.1
- **Language** — Node.js / JavaScript (CommonJS)
- **Authentication & Security** — JWT (`jsonwebtoken`), bcryptjs, AES-256-GCM crypto, express-validator, CORS
- **File & Data Processing** — exceljs, xlsx, multer
- **Package Manager** — npm
- **Dev Tools** — nodemon, sequelize-cli

## 2. Commands

| Command | Action |
| --- | --- |
| `npm run dev` | Dev server with nodemon |
| `npm start` | Production server (`node index.js`) |
| `npm test` | Test server environment (`PORT=8081`) |
| `../start.sh` | Run both backend & frontend concurrently from root |

## 3. Folder Structure

```
[root]/
├── config/              # Database connection & Sequelize config
├── context/             # Business logic & project memory
├── controllers/         # Express request handlers & controller logic
├── helpers/             # Utility helpers (excelToJson, ipHandler, responseHandler, qrCodeGenerator)
├── middleware/          # Express middlewares (authMiddleware, logger)
├── migrations/          # Sequelize schema migrations
├── models/              # Sequelize database models and relations
├── modules/             # System modules & action definition mappings
├── routes/              # Express API route declarations
├── seeders/             # Database seeders
├── services/            # Business logic, query builders & sync services
├── templates/           # Static templates & upload storage
├── uploads/             # Ammunition spreadsheet uploads
└── index.js             # Application entry point & server bootstrap
```

## 4. Code Conventions

### 4.1 File Length
- **Max 200 lines** for simple files
- **Max 500 lines** for complex files

### 4.2 Naming
| Type | Pattern | Example |
| --- | --- | --- |
| Route file | `camelCaseRoutes.js` | `authRoutes.js` |
| Controller file | `camelCaseController.js` | `authController.js` |
| Model file | `lowercase.js` | `user.js` |
| Service file | `camelCaseServices.js` | `syncDriverDataServices.js` |
| Middleware file | `camelCase.js` | `authMiddleware.js` |
| Helper file | `camelCase.js` | `responseHandler.js` |

### 4.3 Splitting Rules
- If a controller or service approaches 200 lines → extract helper functions or dedicated sub-services
- Keep route definitions lean; place validation in routes and business logic in controllers/services
- No comments in code files
