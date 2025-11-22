# Firebase Backend Setup Guide

This guide will help you set up and run the Firebase Emulators for the Chain of Custody application.

## Prerequisites

1. **Node.js 18+** installed
2. **Firebase CLI** installed globally:
   ```bash
   npm install -g firebase-tools
   ```

3. **Firebase Login** (for emulator setup):
   ```bash
   firebase login
   ```

## Installation Steps

### 1. Install Dependencies

```bash
# Install frontend dependencies
npm install

# Install Cloud Functions dependencies
cd functions
npm install
cd ..
```

### 2. Initialize Firebase (if not already done)

```bash
firebase init emulators
```

Select the following emulators:
- Authentication
- Firestore
- Functions
- Storage

### 3. Start Firebase Emulators

```bash
# Option 1: Using npm script
npm run emulators

# Option 2: Direct command
firebase emulators:start
```

The emulators will start on:
- **Auth**: http://localhost:9099
- **Firestore**: http://localhost:8081
- **Functions**: http://localhost:5001
- **Storage**: http://localhost:9199
- **UI**: http://localhost:4000

### 4. Seed Test Users

In a **new terminal** (while emulators are running):

```bash
npm run seed
```

This will create 3 test users:
- `constable@tspolice.gov.in` (Role: constable)
- `investigator@tspolice.gov.in` (Role: investigator)
- `seniorofficer@tspolice.gov.in` (Role: senior)

**Password for all:** `TSPolice@2024`

### 5. Build Cloud Functions

```bash
cd functions
npm run build
cd ..
```

### 6. Start Frontend Development Server

In another terminal:

```bash
npm run dev
```

The app will be available at `http://localhost:5173` (or the port Vite assigns).

## Firebase Configuration

### Emulator Configuration

The app is configured to use **local emulators only**. No real Firebase project credentials are needed.

The configuration in `src/lib/firebase.ts` uses demo credentials:
- Project ID: `demo-project`
- All services connect to localhost emulators

### For Production Deployment

When deploying to production, you'll need:

1. **Create a Firebase Project** at https://console.firebase.google.com
2. **Get Firebase Config** from Project Settings
3. **Update `src/lib/firebase.ts`** with real credentials
4. **Deploy Functions**: `cd functions && npm run deploy`
5. **Deploy Firestore Rules**: `firebase deploy --only firestore:rules`
6. **Deploy Storage Rules**: `firebase deploy --only storage:rules`

## Project Structure

```
.
├── firebase.json          # Emulator configuration
├── firestore.rules        # Firestore security rules
├── storage.rules          # Storage security rules
├── functions/             # Cloud Functions
│   ├── src/
│   │   └── index.ts      # Functions implementation
│   ├── package.json
│   └── tsconfig.json
├── scripts/
│   └── seed-emulators.js # User seeding script
└── src/
    ├── lib/
    │   └── firebase.ts    # Firebase client config
    └── services/
        └── RealEncryptionService.ts  # Encryption service
```

## Troubleshooting

### Emulators won't start
- Make sure ports 9099, 8080, 5001, 9199, and 4000 are not in use
- Check if Firebase CLI is installed: `firebase --version`

### Seed script fails
- Ensure emulators are running before seeding
- Check that `firebase-admin` is installed: `npm install firebase-admin`

### Functions not working
- Build functions first: `cd functions && npm run build`
- Check Functions emulator logs in the Firebase UI (http://localhost:4000)

### Authentication errors
- Make sure you've run the seed script to create test users
- Check that Auth emulator is running on port 9099

## Security Notes

⚠️ **Important**: The current setup uses a **demo encryption key** stored in the Cloud Functions code. 

For production:
1. Use **Google Cloud KMS** or **Secret Manager** for the server KEK
2. Store the KEK securely, never in code
3. Rotate keys regularly
4. Enable audit logging

## Testing the Application

1. **Login Test**: Use any of the test credentials to log in
2. **File Upload**: Create a case via the Public Grievance Portal
3. **RBAC Test**: Login as constable and try to access sensitive files (should be denied)
4. **Audit Log**: Login as senior officer to view complete audit logs

## Next Steps

- [ ] Set up production Firebase project
- [ ] Configure Google Cloud KMS for encryption keys
- [ ] Set up CI/CD pipeline
- [ ] Configure custom domain
- [ ] Set up monitoring and alerts

