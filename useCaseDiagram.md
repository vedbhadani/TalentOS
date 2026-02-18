# Use Case Diagram – HireLens AI

```mermaid
flowchart LR

%% Actors
Candidate([Candidate])
Recruiter([Recruiter])
Admin([Admin])

%% System Boundary
subgraph "HireLens AI System"

UC1((Register / Login))
UC2((Upload Resume))
UC3((Resume Parsing & Skill Extraction))
UC4((View Structured Resume Analysis))
UC5((View Job Match Scores))
UC6((Skill Gap Analysis))
UC7((Generate Learning Roadmap))
UC8((Compare Resume Versions))

UC9((Upload Job Description))
UC10((JD Parsing & Skill Extraction))
UC11((View Ranked Candidates))
UC12((View Match Explanation))
UC13((Provide Feedback))
UC14((View Hiring Analytics))

UC15((Monitor System Analytics))
UC16((Adjust Scoring Weights))
UC17((View Model Performance Metrics))
UC18((Monitor Bias Indicators))
UC19((Manage Model Versions))

UC20((Compute Match Score))
UC21((Generate Embeddings))
UC22((Adaptive Scoring Update))

end

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

%% Internal Includes
UC2 --> UC3
UC3 --> UC21
UC9 --> UC10
UC10 --> UC21
UC5 --> UC20
UC11 --> UC20
UC13 --> UC22
```
