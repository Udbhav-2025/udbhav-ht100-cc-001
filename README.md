# TG - Chain of Custody Case Management System

A high-security, role-based case management dashboard built for law enforcement with immutable audit trails and AES-256 encryption simulation.

## 🚨 Test Credentials

**Password for ALL accounts:** `TG@2024`

### Test User Accounts:

| Role | Email | Access Level |
|------|-------|--------------|
| **Constable** | `constable@tg.gov.in` | ✅ View cases<br>✅ Access Identity Proof files<br>❌ Cannot access Sensitive Evidence |
| **Investigation Officer** | `investigator@tg.gov.in` | ✅ View cases<br>✅ Access Identity Proof files<br>✅ Access Sensitive Evidence files |
| **Senior Officer** | `seniorofficer@tg.gov.in` | ✅ Full access to all files<br>✅ View complete Audit Logs<br>✅ System administration |

## 🎯 Key Features

### Public Grievance Portal
- **Segmented File Uploads**: Citizens can upload files into distinct categories
  - "Identity Proof" (accessible by all officers)
  - "Sensitive Evidence" (restricted to Investigation Officers and above)
- **Case ID Generation**: Automatic unique case ID upon submission
- **Encrypted Storage**: All files simulated with AES-256 encryption

### Police Dashboard (Internal)
- **Role-Based Access Control (RBAC)**: Three-tier permission system
- **Mock Encryption/Decryption**: Visual simulation of secure file access
- **Real-time Case Management**: View, filter, and manage all cases
- **File Access Restrictions**: Enforced at UI level based on officer role

### Immutable Audit Log
- **Complete Chain of Custody**: Every file access is recorded
- **Timeline View**: Chronological display of all case actions
- **Officer Attribution**: Track who accessed what and when
- **Timestamp Precision**: Down to the second for forensic accuracy

## 🛠 Technology Stack

- **Frontend**: React 18 + TypeScript + Vite
- **Styling**: Tailwind CSS with custom design system
- **UI Components**: Shadcn UI (customized)
- **Routing**: React Router v6
- **Backend**: Firebase Emulators (Auth, Firestore, Storage)
- **Fonts**: Inter (Google Fonts)

## 📦 Installation & Setup

### Prerequisites
- Node.js 18+ and npm/yarn
- Firebase CLI (for emulators)

### Quick Start

```bash
# 1. Install dependencies
npm install

# 2. Start the development server
npm run dev

# 3. (Optional) Start Firebase emulators in a separate terminal
firebase emulators:start
```

The application will be available at `http://localhost:8080`

### Firebase Emulator Configuration

The app is pre-configured to connect to Firebase Emulators running locally:

- **Auth Emulator**: `http://localhost:9099`
- **Firestore Emulator**: `localhost:8080`
- **Storage Emulator**: `localhost:9199`

If emulators are not running, the app will still work with mock data.

## 🗂 Project Structure

```
src/
├── assets/              # Images and static files
│   └── ts-police-logo.png
├── components/          # Reusable UI components
│   ├── ui/             # Shadcn UI components
│   ├── Layout.tsx      # Main layout with sidebar
│   └── NavLink.tsx     # Navigation component
├── data/
│   └── mockData.ts     # Test users and sample cases
├── lib/
│   └── firebase.ts     # Firebase config and types
├── pages/
│   ├── PublicGrievance.tsx   # Citizen complaint form
│   ├── Login.tsx             # Officer authentication
│   ├── Dashboard.tsx         # Case overview
│   └── CaseDetail.tsx        # Individual case view
├── utils/
│   └── encryption.ts   # Mock AES-256 encryption
└── App.tsx             # Root component with routes
```

## 🔐 Security Features

### Encryption Simulation
- **Algorithm**: AES-256-GCM (simulated)
- **Visual Feedback**: "Decrypting..." spinner on file access
- **Processing Delay**: Realistic 1-1.5 second delay to simulate cryptographic operations

### Access Control Matrix

| File Category | Constable | Investigation Officer | Senior Officer |
|--------------|-----------|----------------------|----------------|
| Identity Proof | ✅ View & Download | ✅ View & Download | ✅ View & Download |
| Sensitive Evidence | ❌ Access Denied | ✅ View & Download | ✅ View & Download |
| Audit Logs | ❌ Not Visible | ❌ Not Visible | ✅ Full Access |

### Audit Trail
Every sensitive action is logged:
- Officer name and badge number
- Action type (view, download, decrypt)
- File name (if applicable)
- Precise timestamp
- Role at time of action

## 🎨 Design System

### Color Palette
- **Primary (Royal Blue)**: `hsl(220 80% 45%)` - Trust and authority
- **Background (Deep Slate)**: `hsl(222 47% 11%)` - Professional dark theme
- **Accent (Gold)**: `hsl(45 93% 47%)` - Police badge heritage
- **Success**: `hsl(142 76% 36%)` - Secure operations
- **Warning**: `hsl(38 92% 50%)` - Attention required
- **Info**: `hsl(199 89% 48%)` - Informational states

### Visual Effects
- **Glassmorphism**: Backdrop blur with subtle borders
- **Security Pulse**: Animated ring effect on critical elements
- **Smooth Transitions**: All interactions use `cubic-bezier` easing

## 📱 Responsive Design

- **Mobile**: Single-column layout with collapsible sidebar
- **Tablet**: Adaptive grid system
- **Desktop**: Full multi-column dashboard layout

## 🚀 Deployment

### Build for Production

```bash
npm run build
```

The production build will be in the `dist/` directory.

### Environment Variables

For production deployment, configure these Firebase settings in `src/lib/firebase.ts`:

```typescript
const firebaseConfig = {
  apiKey: "YOUR_PROD_API_KEY",
  authDomain: "YOUR_PROD_DOMAIN",
  projectId: "YOUR_PROD_PROJECT_ID",
  // ... other config
};
```

## 🧪 Testing the Application

### Test Scenario 1: Constable Access
1. Login as `constable@tg.gov.in`
2. Navigate to any case
3. Try to access "Sensitive Evidence" files
4. **Expected**: Access Denied message

### Test Scenario 2: Investigation Officer
1. Login as `investigator@tg.gov.in`
2. Open case TG-XX-1234
3. Click "Decrypt & View" on `cctv_footage.mp4`
4. **Expected**: Decryption spinner → Success toast → New audit log entry

### Test Scenario 3: Senior Officer Audit Review
1. Login as `seniorofficer@tg.gov.in`
2. View the "Chain of Custody Timeline" at bottom of case
3. **Expected**: Complete chronological list of all actions

### Test Scenario 4: Public Complaint Filing
1. Navigate to the home page (Public Grievance Portal)
2. Fill out the complaint form
3. Upload files in both categories
4. **Expected**: Case ID generated (e.g., TG-XX-1234)

## 📄 License

This project is a demonstration/prototype for TG. All rights reserved.

## 🤝 Support

For issues or questions:
- Create an issue in the repository
- Contact the development team

---

**Built with ❤️ for TG**

*"Duty, Honour, Compassion"*
