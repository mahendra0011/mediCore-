# 🏥 MediCore — Full-Stack HMS

A complete Hospital Management System built with **React + Vite** (frontend) and **Node.js + Express + MongoDB** (backend).

---

## 📁 Project Structure

```
medicore/
├── client/          # React + Vite frontend
│   ├── src/
│   │   ├── components/      # AppSidebar, DashboardLayout, StatCard, UI
│   │   ├── context/         # AuthContext (JWT auth state)
│   │   ├── lib/             # api.js (fetch wrapper)
│   │   └── pages/           # Login, Dashboard, Doctors, Patients,
│   │                        # Appointments, MedicalRecords, Billing, Settings
│   │                        # PDFReports, ImportExport, FileUpload
│   └── .env.example
└── server/          # Node.js + Express + MongoDB API
    ├── models/      # User, Doctor, Patient, Appointment, Record, Billing
    ├── routes/      # auth, doctors, patients, appointments, records, billing, dashboard
    ├── services/   # pdfService, notificationService
    ├── utils/      # imageUtils, excelUtils
    ├── middleware/  # JWT protect, adminOnly
    ├── seed.js      # Demo data seeder
    └── .env.example
```

---

## ⚡ Quick Start

### Prerequisites
- **Node.js** v18+
- **MongoDB** (local or [MongoDB Atlas](https://cloud.mongodb.com))

### 1 — Install dependencies

```bash
# From root
npm install
npm run install:all
```

### 2 — Configure environment

```bash
# Server
cp server/.env.example server/.env
# Edit server/.env — set MONGO_URI and JWT_SECRET

# Client
cp client/.env.example client/.env
# VITE_API_URL=http://localhost:5000/api  (default — no change needed for local dev)
```

### 3 — Seed demo data

```bash
npm run seed
```

This creates:

| Role    | Email                         | Password   |
|---------|-------------------------------|------------|
| Admin   | `admin@medicore.com`          | `password` |
| Doctor  | `sarah.smith@medicore.com`    | `password` |
| Patient | `patient@medicore.com`        | `password` |

### 4 — Run (both servers)

```bash
npm run dev
```

| Service  | URL                        |
|----------|----------------------------|
| Frontend | http://localhost:8080       |
| Backend  | http://localhost:5000       |
| API docs | http://localhost:5000/api/health |

---

## 🔌 API Reference

All endpoints require `Authorization: Bearer <token>` except `/api/auth/login` and `/api/auth/register`.

### Auth
| Method | Path                  | Description              |
|--------|-----------------------|--------------------------|
| POST   | `/api/auth/login`     | Login → returns JWT      |
| POST   | `/api/auth/register`  | Register new user        |
| GET    | `/api/auth/me`        | Get current user profile |
| PUT    | `/api/auth/profile`   | Update name / phone      |

### Doctors
| Method | Path                | Description         |
|--------|---------------------|---------------------|
| GET    | `/api/doctors`      | List (search, available filter) |
| POST   | `/api/doctors`      | Create doctor       |
| PUT    | `/api/doctors/:id`  | Update doctor       |
| DELETE | `/api/doctors/:id`  | Delete doctor       |

### Patients
| Method | Path                 | Description          |
|--------|----------------------|----------------------|
| GET    | `/api/patients`      | List (search, status)|
| POST   | `/api/patients`      | Create patient       |
| PUT    | `/api/patients/:id`  | Update patient       |
| DELETE | `/api/patients/:id`  | Delete patient       |

### Appointments
| Method | Path                      | Description                |
|--------|---------------------------|----------------------------|
| GET    | `/api/appointments`       | List (status, date, search)|
| POST   | `/api/appointments`       | Book appointment           |
| PUT    | `/api/appointments/:id`   | Update / change status     |
| DELETE | `/api/appointments/:id`   | Cancel & delete            |

### Medical Records
| Method | Path               | Description            |
|--------|--------------------|------------------------|
| GET    | `/api/records`     | List (search, type)    |
| POST   | `/api/records`     | Create record          |
| DELETE | `/api/records/:id` | Delete record          |

### Billing
| Method | Path               | Description              |
|--------|--------------------|--------------------------|
| GET    | `/api/billing`     | List + summary totals    |
| POST   | `/api/billing`     | Create invoice           |
| PUT    | `/api/billing/:id` | Update invoice / mark paid|
| DELETE | `/api/billing/:id` | Delete invoice           |

### Dashboard
| Method | Path                   | Description                          |
|--------|------------------------|--------------------------------------|
| GET    | `/api/dashboard/stats` | Stats, charts, recent appointments   |

### Reports (PDF Generation)
| Method | Path                              | Description                    |
|--------|-----------------------------------|--------------------------------|
| POST   | `/api/reports/generate-prescription`   | Generate prescription PDF      |
| POST   | `/api/reports/generate-lab-report`    | Generate lab report PDF        |
| POST   | `/api/reports/generate-discharge-summary` | Generate discharge summary |

### Email Notifications
| Method | Path                          | Description              |
|--------|-------------------------------|--------------------------|
| POST   | `/api/reports/email/appointment-reminder` | Send appointment reminder |
| POST   | `/api/reports/email/otp`     | Send OTP verification    |
| POST   | `/api/reports/email/prescription` | Email prescription with PDF |
| POST   | `/api/reports/email/lab-result` | Send lab result alert    |

### SMS Notifications
| Method | Path                          | Description              |
|--------|-------------------------------|--------------------------|
| POST   | `/api/reports/sms/appointment-reminder` | Send SMS reminder |
| POST   | `/api/reports/sms/otp`       | Send OTP via SMS         |

### File Upload
| Method | Path                    | Description                  |
|--------|-------------------------|------------------------------|
| POST   | `/api/reports/upload/image`  | Upload/compress medical image |
| POST   | `/api/reports/upload/xray`  | Upload X-ray (high-res)      |
| POST   | `/api/reports/upload/document` | Upload PDF/documents       |

### Import/Export
| Method | Path                    | Description                  |
|--------|-------------------------|------------------------------|
| POST   | `/api/reports/import/patients` | Bulk import patients      |
| POST   | `/api/reports/import/doctors`  | Bulk import doctors       |
| POST   | `/api/reports/import/billing`  | Bulk import billing       |
| GET    | `/api/reports/export/patients` | Export patients (xlsx/csv) |
| GET    | `/api/reports/export/doctors`  | Export doctors            |
| GET    | `/api/reports/export/billing`  | Export billing records   |
| GET    | `/api/reports/export/appointments` | Export appointments   |

---

## 🎨 Tech Stack

| Layer     | Technology                          |
|-----------|-------------------------------------|
| Frontend  | React 18, Vite, Tailwind CSS        |
| UI        | shadcn/ui, Radix UI, Lucide Icons   |
| Charts    | Recharts                            |
| Animation | Framer Motion                       |
| State     | TanStack Query v5                   |
| Routing   | React Router v6                     |
| Backend   | Node.js, Express                    |
| Database  | MongoDB, Mongoose                   |
| Auth      | JWT (jsonwebtoken), bcryptjs        |
| PDF       | PDFKit                               |
| Email     | Nodemailer (SMTP)                   |
| Images    | Sharp (resize, compress)            |
| Excel     | xlsx, json2csv                       |
| Upload    | Multer                               |

---

## 🚀 Production Deployment

### Build frontend
```bash
npm run build
# Output: client/dist/
```

### Environment (production server)
```env
PORT=5000
MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/medicore
JWT_SECRET=a_very_long_random_secret_string
CLIENT_URL=https://your-frontend-domain.com

# SMTP Configuration (for email notifications)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password
SMTP_FROM="MediCore Hospital" <noreply@medicorehospital.com>
```

### Serve with PM2
```bash
npm install -g pm2
cd server && pm2 start index.js --name medicore-api
```

---

## 📱 New Features Added

### PDF Report Generation
- Generate professional prescriptions, lab reports, and discharge summaries
- Hospital letterhead with patient data
- Download as PDF or send via email

### Email & SMS Notifications
- Appointment reminders
- OTP verification via email
- Prescription emails with PDF attachment
- Lab result alerts

### Medical File Handling
- Resize and compress uploaded images
- X-ray high-resolution processing
- Document upload (PDF, JPEG, PNG)
- Automatic validation and optimization

### Excel / CSV Import-Export
- Bulk import patients, doctors, billing records
- Export reports and payment history
- Support for both Excel and CSV formats

---

## 📄 License
MIT — free to use and modify.
