# Synaphack Platform - Process Flow Diagram

```mermaid
flowchart TD
    Start([User Visits Platform]) --> Login{Login/Register}
    
    Login --> RoleSelect[Select Role]
    RoleSelect --> Participant[👨‍💻 Participant]
    RoleSelect --> Organizer[🎯 Organizer]
    RoleSelect --> Judge[⚖️ Judge]
    
    %% ORGANIZER FLOW
    Organizer --> OrgDash[Organizer Dashboard]
    OrgDash --> CreateEvent[Create Event]
    CreateEvent --> EventDetails[Add Details:<br/>Title, Theme, Timeline,<br/>Prizes, Sponsors]
    EventDetails --> SaveDraft{Save as Draft<br/>or Publish?}
    SaveDraft -->|Draft| Draft[Draft Event]
    SaveDraft -->|Publish| Published[Published Event]
    Published --> InviteJudge[Invite Judges]
    InviteJudge --> GenCode[Generate Invite Code]
    GenCode --> ShareCode[Share with Judges]
    Published --> ManageEvent[Manage Event]
    ManageEvent --> ViewParticipants[View Participants]
    ManageEvent --> ViewSubmissions[Review Submissions]
    ManageEvent --> SendAnnounce[Send Announcements]
    ManageEvent --> ManageLeaderboard[Update Leaderboard]
    ManageEvent --> GenCert[Generate Certificates]
    
    %% PARTICIPANT FLOW
    Participant --> PartDash[Participant Dashboard]
    PartDash --> BrowseEvents[Browse Events]
    BrowseEvents --> ViewEvent[View Event Details]
    ViewEvent --> Register[Register for Event]
    Register --> EmailConf[Receive Email<br/>Confirmation]
    EmailConf --> TeamDecision{Create/Join Team?}
    TeamDecision -->|Create| CreateTeam[Create Team]
    TeamDecision -->|Join| JoinTeam[Accept Team Invite]
    CreateTeam --> SendInvite[Send Team Invites]
    SendInvite --> TeamFormed[Team Formed]
    JoinTeam --> TeamFormed
    TeamFormed --> SubmitProject[Submit Project]
    SubmitProject --> UploadFiles[Upload Files/<br/>GitHub Link]
    UploadFiles --> TrackStatus[Track Submission<br/>Status]
    TrackStatus --> ViewLeaderboard[View Leaderboard]
    ViewLeaderboard --> GetCert[Receive Certificate]
    
    %% JUDGE FLOW
    Judge --> JudgeDash[Judge Dashboard]
    ShareCode --> AcceptInvite[Judge Accepts<br/>Invite via Code]
    AcceptInvite --> JudgeAssigned[Assigned to Event]
    JudgeAssigned --> JudgeDash
    JudgeDash --> ViewAssigned[View Assigned Events]
    ViewAssigned --> AccessSubs[Access Submissions]
    AccessSubs --> Evaluate[Evaluate Projects]
    Evaluate --> Score[Score & Feedback]
    Score --> UpdateBoard[Leaderboard Updates]
    
    %% SYSTEM INTERACTIONS
    Register -.->|Email Service| EmailConf
    GenCode -.->|Firebase| ShareCode
    SubmitProject -.->|Cloudinary| UploadFiles
    Score -.->|Firebase| UpdateBoard
    GenCert -.->|Certificate Service| GetCert
    
    style Organizer fill:#ff6b6b,stroke:#c92a2a,stroke-width:3px,color:#fff
    style Participant fill:#4dabf7,stroke:#1971c2,stroke-width:3px,color:#fff
    style Judge fill:#a78bfa,stroke:#7c3aed,stroke-width:3px,color:#fff
    style Published fill:#51cf66,stroke:#2b8a3e,stroke-width:2px
    style GetCert fill:#ffd43b,stroke:#f59f00,stroke-width:2px
```

## Key Process Stages

### 🎯 Organizer Journey
1. **Event Creation** → Details Entry → Publish/Draft
2. **Judge Management** → Generate Invite Codes → Share
3. **Event Monitoring** → View Participants → Review Submissions
4. **Communication** → Announcements → Leaderboard → Certificates

### 👨‍💻 Participant Journey
1. **Discovery** → Browse Events → Register
2. **Team Formation** → Create/Join Team → Invite Members
3. **Submission** → Upload Project → Track Status
4. **Recognition** → View Leaderboard → Get Certificate

### ⚖️ Judge Journey
1. **Onboarding** → Accept Invite → Assignment
2. **Evaluation** → View Submissions → Score Projects
3. **Feedback** → Provide Comments → Update Rankings

## System Services
- **Firebase Auth** - User authentication
- **Firestore** - Data storage
- **Email Service** - Notifications
- **Cloudinary** - File uploads
- **Certificate Service** - Auto-generation
- **Git MCP** - AI code analysis
