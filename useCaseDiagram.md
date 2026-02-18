# Use Case Diagram – HireLens AI

```mermaid
%% Actors
actor Candidate
actor Recruiter
actor Admin

%% System Boundary
rectangle "HireLens AI System" {

  %% Candidate Use Cases
  (Register / Login) as UC1
  (Upload Resume) as UC2
  (Resume Parsing & Skill Extraction) as UC3
  (View Structured Resume Analysis) as UC4
  (View Job Match Scores) as UC5
  (Skill Gap Analysis) as UC6
  (Generate Learning Roadmap) as UC7
  (Compare Resume Versions) as UC8

  %% Recruiter Use Cases
  (Upload Job Description) as UC9
  (JD Parsing & Skill Extraction) as UC10
  (View Ranked Candidates) as UC11
  (View Match Explanation) as UC12
  (Provide Feedback) as UC13
  (View Hiring Analytics) as UC14

  %% Admin Use Cases
  (Monitor System Analytics) as UC15
  (Adjust Scoring Weights) as UC16
  (View Model Performance Metrics) as UC17
  (Monitor Bias Indicators) as UC18
  (Manage Model Versions) as UC19

  %% Core Engine Use Cases
  (Compute Match Score) as UC20
  (Generate Embeddings) as UC21
  (Adaptive Scoring Update) as UC22
}

%% Associations

Candidate --> UC1
Candidate --> UC2
Candidate --> UC4
Candidate --> UC5
Candidate --> UC6
Candidate --> UC7
Candidate --> UC8

Recruiter --> UC1
Recruiter --> UC9
Recruiter --> UC11
Recruiter --> UC12
Recruiter --> UC13
Recruiter --> UC14

Admin --> UC15
Admin --> UC16
Admin --> UC17
Admin --> UC18
Admin --> UC19

%% Include Relationships

UC2 --> UC3 : <<include>>
UC3 --> UC21 : <<include>>
UC9 --> UC10 : <<include>>
UC10 --> UC21 : <<include>>
UC5 --> UC20 : <<include>>
UC11 --> UC20 : <<include>>
UC13 --> UC22 : <<include>>

%% Extend Relationships

UC6 --> UC5 : <<extend>>
UC7 --> UC6 : <<extend>>
UC12 --> UC11 : <<extend>>
UC17 --> UC15 : <<extend>>
