# MedicalBlocks: Patient Management System with React & PGlite

A modern patient management system that runs entirely in your browser using PGlite (WebAssembly PostgreSQL).

## 📋 Features

- **In-Browser Database**: Full PostgreSQL database running directly in the browser with PGlite
- **Offline Support**: Works without an internet connection, with data persisted in IndexedDB
- **Multi-Tab Support**: Share database state across multiple browser tabs
- **Patient Registration**: Complete form for adding patients with comprehensive medical information
- **Patient Search**: Search and filter patients by name and other attributes
- **Custom SQL Queries**: Advanced interface for querying the database directly with SQL
- **Modern UI**: Clean, responsive interface built with React

## 🚀 Demo

https://medblocks.netlify.app/

## 📦 Installation

### Prerequisites

- Node.js (v16 or higher)
- npm (v7 or higher)

### Setup Steps

1. Clone the repository:

```bash
git clone https://github.com/rishgupta2301/medbblocks_task
cd vite-project
```

2. Install dependencies:

```bash
npm install
```

3. Start the development server:

```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:5173`

## 🛠️ Project Structure

```
patient-system-pglite/
├── public/
│   └── pglite-worker.js     # PGlite worker for multi-tab support
├── src/
│   ├── components/          # Reusable UI components
│   ├── context/             # React context providers
│   │   └── DatabaseContext.tsx
│   ├── pages/               # Application pages
│   │   ├── Dashboard.tsx
│   │   ├── PatientList.tsx
│   │   ├── PatientQuery.tsx
│   │   └── PatientRegistration.tsx
│   ├── services/            # Core services
│   │   └── DatabaseService.ts
│   ├── App.tsx              # Main application component
│   ├── main.tsx             # Application entry point
│   └── index.css            # Global styles
├── package.json
├── tsconfig.json
└── vite.config.ts
```

## 🧩 Implementation Details

### PGlite Integration

The project uses PGlite to run PostgreSQL directly in the browser. The database is initialized in a Web Worker to support multi-tab operation and persisted using IndexedDB.

```typescript
// public/pglite-worker.js
import { PGlite } from '@electric-sql/pglite';
import { worker } from '@electric-sql/pglite/worker';

worker({
  async init() {
    return new PGlite('idb://my-pgdata');
  },
});
```

### Database Schema

```sql
CREATE TABLE IF NOT EXISTS patients (
  id SERIAL PRIMARY KEY,
  first_name TEXT NOT NULL,
  last_name TEXT NOT NULL,
  date_of_birth TEXT NOT NULL,
  gender TEXT NOT NULL,
  email TEXT,
  phone TEXT,
  address TEXT,
  medical_notes TEXT,
  insurance_provider TEXT,
  insurance_id TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX IF NOT EXISTS idx_patient_name ON patients (last_name, first_name);
```

## 🔧 Available Scripts

In the project directory, you can run:

- `npm run dev` - Starts the development server
- `npm run build` - Builds the app for production
- `npm run lint` - Runs ESLint to check code quality
- `npm run preview` - Previews the production build locally

## 📱 Usage Guide

### Adding a New Patient

1. Navigate to the "Register" page using the dashboard or navigation menu
2. Fill in the required patient information
3. Click "Register Patient" to save the record

### Searching for Patients

1. Go to the "Patients" page
2. Use the search bar to find patients by name
3. Click on a patient to view their details

### Running Custom Queries

1. Navigate to the "Query" page
2. Enter your SQL query in the editor
3. Click "Execute" to run the query and view results

## 🧪 Technologies Used

- **React** - UI library
- **TypeScript** - Type safety and better developer experience
- **PGlite** - In-browser PostgreSQL database
- **React Router** - Application routing
- **Lucide React** - Icon library
- **Vite** - Build tool and development server

## 🤝 Contributing

Contributions are always welcome!

1. Fork the repository
2. Create a new branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Commit your changes (`git commit -m 'Add some amazing feature'`)
5. Push to the branch (`git push origin feature/amazing-feature`)
6. Open a Pull Request

Please make sure to update tests as appropriate.


## 🙏 Acknowledgements

- [Pglite Docs]([https://electric-sql.com/](https://pglite.dev/docs/)) for developing PGlite
- [Vite](https://vitejs.dev/) for the blazing fast build tool
- [React](https://reactjs.org/) for the UI library

---