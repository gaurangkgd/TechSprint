Build2Skill 3.0 - Advanced Hackathon Platform

A modern hackathon platform built with Next.js 14, TypeScript, Firebase, and TailwindCSS featuring role-based dashboards and real-time event management.

## Features
- **Event Management:** Create, edit, delete events with status workflow (Draft → Published → Ongoing → Completed)
- **Role-Based Access:** Organizer, Participant, and Judge dashboards with different capabilities
- **Real-time Database:** Firebase Firestore integration with instant updates
- **Modern UI:** Dark theme with responsive design and interactive card system
- **Event Cards:** Simplified cards with detailed popup modals for complete information

## Tech Stack
- **Frontend:** Next.js 14 + TypeScript + TailwindCSS
- **Database:** Firebase Firestore
- **Authentication:** localStorage-based role system
- **Styling:** Custom dark theme with slate color palette

## Quick Setup

### Install Dependencies

```bash
cd frontend
npm install
```

### Environment Setup
Copy `.env.example` to `.env.local` and add your Firebase config:

```
NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_domain
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_bucket
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id
NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID=your_measurement_id
```

### Run Development Server

```bash
npm run dev
```

Access at http://localhost:3000

## Demo Login Credentials

- **Organizer:** organizer@build2skill.com / organizer123
- **Participant:** participant@build2skill.com / participant123
- **Judge:** judge@build2skill.com / judge123

## Project Structure

```
frontend/
├── src/
│   ├── app/                    # Next.js App Router pages
│   │   ├── page.tsx           # Landing page
│   │   ├── login/             # Authentication
│   │   └── dashboard/         # Role-based dashboards
│   ├── components/
│   │   ├── CreateEventForm.tsx # Event creation/editing
│   │   └── dashboards/        # Role-specific components
│   └── lib/
│       ├── firebase.ts        # Firebase configuration
│       └── eventService.ts    # Event CRUD operations
└── package.json
```

## Usage

### For Organizers
- Login and access organizer dashboard
- Create events with title, description, theme, dates, fees, etc.
- Manage event status (draft/published/ongoing/completed)
- Edit or delete existing events

### For Participants
- Login and browse available events
- View event details in popup modals
- Register for published/ongoing events

## Event Status Workflow

- **Draft:** Being created (hidden from participants)
- **Published:** Open for registration ✅
- **Ongoing:** Currently happening ✅
- **Completed:** Finished (registration closed)
- **Cancelled:** Event cancelled

## Firebase Setup

1. Create Firebase project
2. Enable Firestore Database
3. Add your web app and get config
4. Update `.env.local` with your credentials

Configure Firebase Storage CORS settings (required for certificate uploads):

```bash
# Install Google Cloud SDK if not already installed
# https://cloud.google.com/sdk/docs/install

# Authenticate with Google Cloud
gcloud auth login

# Set your project
gcloud config set project your-project-id

# Apply CORS configuration
gsutil cors set cors.json gs://your-storage-bucket-name
```

## Development

Build for production:

```bash
npm run build
```

Start production server:

```bash
npm start
```

## Deployment

Deploy to Vercel (recommended):

```bash
npm run build
vercel --prod
```

Remember to set environment variables in your deployment platform.

Built for hackathon organizers and participants
