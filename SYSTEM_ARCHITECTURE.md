# Synaphack Platform - System Architecture Diagram

```mermaid
graph TB
    subgraph "Frontend Layer"
        NextJS[Next.js 14<br/>React + TypeScript]
        UI[User Interface]
        Components[Components Layer]
        NextJS --> UI
        UI --> Components
    end
    
    subgraph "User Roles"
        Org[🎯 Organizer<br/>Dashboard]
        Part[👨‍💻 Participant<br/>Dashboard]
        Jdg[⚖️ Judge<br/>Dashboard]
    end
    
    subgraph "Service Layer"
        AuthSvc[Auth Service]
        EventSvc[Event Service]
        SubSvc[Submission Service]
        JudgeSvc[Judge Invite Service]
        TeamSvc[Team Invite Service]
        CertSvc[Certificate Service]
        CommSvc[Communication Service]
        LeadSvc[Leaderboard Service]
        EmailSvc[Email Service]
        GitMCP[Git MCP Service]
        CloudSvc[Cloudinary Service]
    end
    
    subgraph "Firebase Backend"
        FireAuth[Firebase Auth<br/>Authentication]
        Firestore[(Firestore<br/>Database)]
        FireStorage[Firebase Storage]
    end
    
    subgraph "External Services"
        Cloudinary[Cloudinary<br/>Media Storage]
        Gemini[Google Gemini AI<br/>Code Analysis]
        Email[Email Service<br/>Notifications]
    end
    
    %% Frontend to Roles
    Components --> Org
    Components --> Part
    Components --> Jdg
    
    %% Roles to Services
    Org --> EventSvc
    Org --> JudgeSvc
    Org --> CertSvc
    Org --> CommSvc
    
    Part --> EventSvc
    Part --> SubSvc
    Part --> TeamSvc
    Part --> CommSvc
    
    Jdg --> JudgeSvc
    Jdg --> SubSvc
    Jdg --> LeadSvc
    
    %% Services to Firebase
    AuthSvc --> FireAuth
    EventSvc --> Firestore
    SubSvc --> Firestore
    JudgeSvc --> Firestore
    TeamSvc --> Firestore
    CertSvc --> Firestore
    CommSvc --> Firestore
    LeadSvc --> Firestore
    
    %% Services to External
    EmailSvc --> Email
    CloudSvc --> Cloudinary
    GitMCP --> Gemini
    SubSvc --> CloudSvc
    CertSvc --> CloudSvc
    
    %% Cross-service Communication
    EventSvc -.->|notify| EmailSvc
    SubSvc -.->|analyze| GitMCP
    JudgeSvc -.->|notify| EmailSvc
    TeamSvc -.->|notify| EmailSvc
    SubSvc -.->|update| LeadSvc
    
    style NextJS fill:#000,stroke:#0070f3,stroke-width:3px,color:#fff
    style Org fill:#ff6b6b,stroke:#c92a2a,stroke-width:2px,color:#fff
    style Part fill:#4dabf7,stroke:#1971c2,stroke-width:2px,color:#fff
    style Jdg fill:#a78bfa,stroke:#7c3aed,stroke-width:2px,color:#fff
    style Firestore fill:#ffa94d,stroke:#f76707,stroke-width:2px
    style Cloudinary fill:#51cf66,stroke:#2b8a3e,stroke-width:2px
    style Gemini fill:#da77f2,stroke:#9c36b5,stroke-width:2px
```

## Technology Stack

### 🎨 Frontend
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **UI Library**: React 18
- **Styling**: Tailwind CSS
- **3D Graphics**: Three.js
- **Animation**: Custom CSS animations

### 🔧 Backend Services
- **Authentication**: Firebase Auth (Email + Google OAuth)
- **Database**: Firebase Firestore (NoSQL)
- **File Storage**: Cloudinary (Images/Files) + Firebase Storage
- **Real-time**: Firestore real-time listeners

### 🤖 AI/ML Integration
- **Code Analysis**: Google Gemini AI via Git MCP
- **Use Case**: Automated code quality assessment

### 📧 Communication
- **Email Service**: Custom email service for notifications
- **In-app Messaging**: Event communication system

## Data Models

### Core Collections
```
users/
├── {userId}
│   ├── email
│   ├── name
│   ├── role (organizer|participant|judge)
│   └── createdAt

events/
├── {eventId}
│   ├── title
│   ├── description
│   ├── theme
│   ├── timeline
│   ├── prizes[]
│   ├── sponsors[]
│   ├── organizerId
│   └── status

submissions/
├── {submissionId}
│   ├── eventId
│   ├── participantEmail
│   ├── projectName
│   ├── githubLink
│   ├── files[]
│   ├── status
│   └── scores[]

registrations/
├── {registrationId}
│   ├── eventId
│   ├── participantEmail
│   ├── teamName
│   └── registeredAt

judgeAssignments/
├── {assignmentId}
│   ├── eventId
│   ├── judgeEmail
│   └── inviteCode

certificates/
├── {certificateId}
│   ├── eventId
│   ├── participantEmail
│   ├── certificateUrl
│   └── issuedAt
```

## Key Features Implementation

### 🔐 Authentication Flow
```
User → Select Role → Email/Google Auth → Firebase Auth
→ Create User Profile → Store in Firestore → Redirect to Dashboard
```

### 📝 Event Lifecycle
```
Create → Draft → Publish → Registration → Ongoing
→ Submission → Evaluation → Completed → Certificates
```

### 🏆 Scoring System
```
Judge Evaluates → Submit Scores → Aggregate Scores
→ Calculate Ranking → Update Leaderboard → Real-time Update
```

### 📨 Notification System
```
Trigger Event → Email Service → Generate Email
→ Send via SMTP → Log Notification → User Receives
```

## Security Features
- ✅ Firebase Authentication
- ✅ Role-based Access Control (RBAC)
- ✅ Invite Code Validation
- ✅ Secure File Upload (Cloudinary)
- ✅ Environment Variables for Secrets
- ✅ Client-side Authorization Checks

## Performance Optimizations
- ⚡ Next.js Server-Side Rendering (SSR)
- ⚡ Code Splitting
- ⚡ Image Optimization (Cloudinary)
- ⚡ Firestore Query Optimization
- ⚡ Real-time Updates (Efficient Listeners)

## Deployment Architecture
```
GitHub → Vercel (Frontend) → Firebase (Backend)
                           → Cloudinary (Media)
                           → Email Service
```
