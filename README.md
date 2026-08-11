# AbleSpace — IEP Special Education Caseload & Task Platform

[![GitHub](https://img.shields.io/badge/GitHub-rammane20%2FAbleSpace--assignment-blue?logo=github)](https://github.com/rammane20/AbleSpace-assignment)

> 📖 **[Full Walkthrough & API Reference →](./WALKTHROUGH.md)**  
> 🌐 **Live Demo**: *(deploy to Vercel/Render — see [WALKTHROUGH.md](./WALKTHROUGH.md#-live-deployment))*

## 📌 What This App Does

The project consists of two core full-stack modules:

1. **Caseload & IEP Goal Data Tracking** — Single-click "Take Data" trial counter workspace, visual compliance deadline urgency flags (Overdue, Warning < 30d,Compliant), service minute completion tracking, and multi-disciplinary team collaborator tooltips.
2. **Integrated Task Management Engine** — Grouped List view and 3-column Kanban Board view with drag/interactive controls, field visibility toggles, and persistent light/dark/blue themes.

---

## Project Structure

```text
AbleSpace/
├── client/    
│   ├── app/
│   │   ├── caseload/     
│   │   ├── data/         
│   │   ├── tasks/        
│   │   ├── components/ui/   
│   │   └── lib/          
│   └── styles/globals.css  
│
├── server/              
│   ├── prisma/
│   │   └── schema.prisma   
│   └── src/
│       ├── students/     
│       ├── data-sessions/  
│       ├── auth/         
│       └── users/        
│
├── install.bat           
├── install.sh            
├── uninstall.bat        
├── uninstall.sh          
├── docker-compose.yml    
└── README.md
```

---

## Prerequisites

| Tool    | Minimum Version   | Download                        |
| ------- | ----------------- | ------------------------------- |
| Node.js | **v18.0.0** | [nodejs.org](https://nodejs.org) |
| npm     | **v9.0.0**  | Included with Node.js           |

---

## Getting Started — Step by Step

### Step 1: Clone the Repository

```bash
git clone <your-repo-url>
cd AbleSpace
```

---

### Step 2A: Install All Dependencies

Choose your OS:

**Windows PowerShell:**

```powershell
.\install.bat
```

 **Windows CMD (Command Prompt):**

```cmd
install.bat
```

**Mac / Linux / Git Bash:**

```bash
bash install.sh
```

>  **PowerShell note**: PowerShell requires `.\ ` prefix to run scripts in the current directory. CMD does not. You can also just double-click `install.bat` in File Explorer.

The installer automatically:

1. Installs backend (`server/`) npm dependencies
2. Generates the Prisma client and creates the SQLite database
3. Installs frontend (`client/`) npm dependencies

> **Or install manually** — skip to Step 2b below.

---

### Step 2B: Manual Install (without the script)

**Backend:**

```bash
cd server
npm install
#Generate Prisma client and apply DB migration (creates SQLite dev.db)
npx prisma generate
npx prisma migrate dev --name init

cd ..
```

**Frontend:**

```bash
cd client
npm install
cd ..
```

---

### Step 3: Start the Backend API

Open a terminal in the project root:

```bash
cd server
npm run start:dev
# Backend API running at http://localhost:3001
```

---

### Step 4: Start the Frontend

Open a **second terminal** in the project root:

```bash
cd client
npm run dev
# Web app running at http://localhost:3000
```

## Backend API Endpoints

The NestJS server listens on port **3001** by default.

| Method | Endpoint        | Auth Required | Description                       |
| ------ | --------------- | ------------- | --------------------------------- |
| POST   | `/auth/guest` | No            | Returns`{ access_token, user }` |
| GET    | `/tasks`      | Bearer        | List all tasks                    |
| POST   | `/tasks`      | Bearer        | Create a task`{ title }`        |

**JWT Secret**: Defaults to the "JWT_SECRETE" environment variable, or `'changeme'` for local development. Always override in production.

## Build & Test

### Build (verify zero compile errors)

```bash
# Backend build
cd server && npm run build

# Frontend build
cd client && npm run build
```

### Run Tests (Backend)

```bash
cd server

# Unit tests
npm run test

# End-to-end tests
npm run test:e2e

# Test coverage
npm run test:cov
```

## Database Inspection

To browse the SQLite database visually in your browser:

```bash
cd server
npx prisma studio
# → Opens Prisma Studio at http://localhost:5555
```

## Alternative: Docker Compose (One Command)

If you have Docker installed, spin up all containers (PostgreSQL 15 + NestJS API + Next.js Frontend):

```bash
docker-compose up --build -d
```

## Uninstall / Clean Up

To remove all installed files ("node_module" ,"dist", ".next", database) and restore the repo to its clean state:

  **Windows PowerShell:**

```powershell
.\uninstall.bat
```

 **Windows CMD (Command Prompt):**

```cmd
uninstall.bat
```

**Mac / Linux / Git Bash:**

```bash
bash uninstall.sh
```

> **PowerShell note**: Use `.\ ` prefix in PowerShell. Or just double-click `uninstall.bat` in File Explorer.

> Your source code files are **never deleted**. Run `install.bat` / `install.sh` again to reinstall.
