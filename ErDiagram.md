# ER Diagram – HireLens AI

```mermaid
erDiagram

%% =========================
%% 1️⃣ Identity & Access Layer
%% =========================

USER {
    string _id PK
    string name
    string email UNIQUE
    string passwordHash
    string role  "CANDIDATE | RECRUITER | ADMIN"
    boolean isActive
    date createdAt
    date updatedAt
}

REFRESH_TOKEN {
    string _id PK
    string userId FK
    string token
    date expiresAt
    boolean isRevoked
}

USER ||--o{ REFRESH_TOKEN : owns


%% =========================
%% 2️⃣ Candidate Domain
%% =========================

CANDIDATE_PROFILE {
    string _id PK
    string userId FK
    string headline
    string location
    number totalExperienceYears
    date createdAt
}

RESUME {
    string _id PK
    string candidateId FK
    string version
    string rawText
    vector embeddingVector
    number experienceYears
    date createdAt
}

RESUME_SKILL {
    string _id PK
    string resumeId FK
    string skillName
    number proficiencyScore
}

RESUME_PROJECT {
    string _id PK
    string resumeId FK
    string title
    string description
    string techStack
}

CANDIDATE_PROFILE ||--|| USER : belongs_to
CANDIDATE_PROFILE ||--o{ RESUME : has
RESUME ||--o{ RESUME_SKILL : contains
RESUME ||--o{ RESUME_PROJECT : includes


%% =========================
%% 3️⃣ Recruiter Domain
%% =========================

RECRUITER_PROFILE {
    string _id PK
    string userId FK
    string companyName
    string designation
    date createdAt
}

JOB_DESCRIPTION {
    string _id PK
    string recruiterId FK
    string title
    string description
    number experienceRequired
    vector embeddingVector
    date createdAt
}

JOB_REQUIRED_SKILL {
    string _id PK
    string jobId FK
    string skillName
    number importanceWeight
}

RECRUITER_PROFILE ||--|| USER : belongs_to
RECRUITER_PROFILE ||--o{ JOB_DESCRIPTION : posts
JOB_DESCRIPTION ||--o{ JOB_REQUIRED_SKILL : requires


%% =========================
%% 4️⃣ Matching Engine Layer
%% =========================

MATCH_RESULT {
    string _id PK
    string resumeId FK
    string jobId FK
    number overallScore
    number skillScore
    number experienceScore
    number projectScore
    string explanation
    string scoringStrategy
    date createdAt
}

RESUME ||--o{ MATCH_RESULT : evaluated_in
JOB_DESCRIPTION ||--o{ MATCH_RESULT : produces


%% =========================
%% 5️⃣ Feedback & Adaptive Learning Layer
%% =========================

FEEDBACK {
    string _id PK
    string matchResultId FK
    string recruiterId FK
    string decision  "SELECTED | REJECTED | STRONG_MATCH"
    number rating
    string comments
    date createdAt
}

MODEL_VERSION {
    string _id PK
    string versionName
    number skillWeight
    number experienceWeight
    number projectWeight
    number domainWeight
    date createdAt
}

MODEL_PERFORMANCE {
    string _id PK
    string modelVersionId FK
    number precision
    number recall
    number accuracy
    number falsePositiveRate
    date evaluatedAt
}

MATCH_RESULT ||--o{ FEEDBACK : receives
MODEL_VERSION ||--o{ MATCH_RESULT : influences
MODEL_VERSION ||--o{ MODEL_PERFORMANCE : evaluated_by


%% =========================
%% 6️⃣ Analytics & Logging Layer
%% =========================

ANALYTICS_EVENT {
    string _id PK
    string userId FK
    string eventType
    string metadata
    date createdAt
}

SYSTEM_LOG {
    string _id PK
    string level
    string message
    string source
    date createdAt
}

USER ||--o{ ANALYTICS_EVENT : generates
```
