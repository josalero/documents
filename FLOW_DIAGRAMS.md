# Job Posting Application - Flow Diagrams

This document contains visual diagrams for the four main flows in the Job Posting Application.

## 1. Add a Featured Job Flow

### High-Level Process Flow
```mermaid
flowchart TD
    A[Recruiter Login] --> B[Access Create Featured Job]
    B --> C[Fill Job Information Form]
    C --> D[Submit Job Creation Request]
    D --> E[Validate User Permissions]
    E --> F[Create Job Entity]
    F --> G[Generate Short URL]
    G --> H[Process Skills]
    H --> I[Schedule Job Promotion]
    I --> J[Send Confirmation]
    J --> K[Job Published & Visible]
```

### Detailed Technical Flow
```mermaid
sequenceDiagram
    participant U as User (Recruiter)
    participant C as JobController
    participant S as JobService
    participant R as JobRepository
    participant URL as URLShortenerService
    participant SK as SkillService
    participant SCH as FeaturedJobScheduler
    participant N as NotificationService

    U->>C: POST /featured/jobs
    C->>S: createFeaturedJob(request)
    S->>S: validateUserPermissions()
    S->>S: buildJobFromRequest()
    S->>R: save(job)
    R-->>S: savedJob
    S->>URL: generateShortURL(job)
    URL-->>S: shortURL
    S->>S: setShortURL(shortURL)
    
    alt Skills provided
        S->>SK: saveSkills(skills)
        SK-->>S: skillsMap
        S->>S: processSkillsAndRecommendations()
    end
    
    S->>SCH: schedule(job)
    SCH->>SCH: createCronExpression()
    SCH->>SCH: saveSchedule()
    SCH->>N: setupNotifications()
    
    S-->>C: Job
    C-->>U: 200 OK + Job details
```

## 2. Apply to a Featured Job Flow

### High-Level Process Flow
```mermaid
flowchart TD
    A[Candidate Browses Jobs] --> B[Select Featured Job]
    B --> C[Click Apply Now]
    C --> D[Fill Application Form]
    D --> E[Upload Resume]
    E --> F[Submit Application]
    F --> G[Validate Application]
    G --> H[Process Resume]
    H --> I[Extract Skills]
    I --> J[Calculate Relevance]
    J --> K[Create/Update Candidate]
    K --> L[Send Notifications]
    L --> M[Application Complete]
```

### Detailed Technical Flow
```mermaid
sequenceDiagram
    participant C as Candidate
    participant JC as JobApplicationController
    participant JAS as JobApplicationService
    participant JS as JobService
    participant CS as CandidateService
    participant RS as ResumeService
    participant SK as SkillService
    participant N as NotificationService
    participant DB as Database

    C->>JC: POST /job-applications/apply
    JC->>JAS: applyToFeatureJob(request, file)
    JAS->>JAS: validateJobApplicationRequest()
    JAS->>JS: getJobById(jobId)
    JS-->>JAS: job
    
    JAS->>JAS: validateJobForApplication()
    JAS->>CS: getCandidate(email, companyId)
    CS-->>JAS: candidate (optional)
    
    JAS->>JAS: createAndSaveFile(file)
    JAS->>JAS: createJobApplicationFromRequest()
    JAS->>JS: addJobApplication(jobApplication)
    JS->>DB: save(job)
    DB-->>JS: savedJob
    JS-->>JAS: savedJobApplication
    
    JAS->>JAS: createInitialJobApplicationStatus()
    JAS->>JAS: processCandidateAndCalculateRelevance()
    
    par Async Processing
        JAS->>CS: createCandidateFromJobApplication()
        CS->>RS: extractPersonalInfo(resume)
        RS-->>CS: personalInfo
        CS->>SK: extractSkills(resume)
        SK-->>CS: skills
        CS->>DB: save(candidate)
        DB-->>CS: savedCandidate
        CS-->>JAS: candidateId
        
        JAS->>JAS: calculateRelevance(job, candidate)
        JAS->>JAS: setRelevance(score)
        JAS->>DB: save(jobApplication)
        
        JAS->>N: sendInitialNotification()
    end
    
    JAS-->>JC: JobApplication
    JC-->>C: 200 OK + Application details
```

## 3. Candidate Skill Extraction Flow

### High-Level Process Flow
```mermaid
flowchart TD
    A[Resume Upload] --> B[Extract Content]
    B --> C[Select AI Provider]
    C --> D[AI Analysis]
    D --> E[Extract Skills]
    E --> F[Categorize by Level]
    F --> G[Normalize Skill Names]
    G --> H[Save to Database]
    H --> I[Update Candidate Profile]
    I --> J[Enable Job Matching]
```

### Detailed Technical Flow
```mermaid
sequenceDiagram
    participant F as File Upload
    participant RS as ResumeService
    participant CR as ContentReader
    participant TPP as ThirdPartyProvider
    participant SK as SkillService
    participant SR as SkillRepository
    participant CS as CandidateService
    participant DB as Database

    F->>RS: uploadResume(file)
    RS->>CR: extractContent(file)
    CR-->>RS: resumeContent
    
    RS->>TPP: extractSkills(resumeContent)
    TPP->>TPP: processWithAI(resumeContent)
    TPP-->>RS: ExtractedSkill
    
    RS->>SK: processExtractedSkills(extractedSkill)
    SK->>SK: normalizeSkillNames()
    
    loop For each skill level
        SK->>SR: findByName(skillName)
        alt Skill exists
            SR-->>SK: existingSkill
        else Skill doesn't exist
            SK->>SR: save(newSkill)
            SR-->>SK: newSkill
        end
    end
    
    SK->>SK: categorizeSkillsByLevel()
    SK-->>RS: Map<SkillLevel, List<Skill>>
    
    RS->>CS: updateCandidateSkills(candidate, skills)
    CS->>DB: save(candidate)
    DB-->>CS: updatedCandidate
    
    RS-->>F: ExtractedSkill + Success
```

### AI Provider Selection Flow
```mermaid
flowchart TD
    A[Skill Extraction Request] --> B{Check Feature Flag}
    B -->|IA_FF Active| C[Use OpenRouter Service]
    B -->|IA_FF Inactive| D[Use DeepSeek Service]
    C --> E[Process with OpenRouter AI]
    D --> F[Process with DeepSeek AI]
    E --> G[Parse JSON Response]
    F --> G
    G --> H[Return ExtractedSkill]
```

## 4. Resume Improvement Flow

### High-Level Process Flow
```mermaid
flowchart TD
    A[Resume Upload] --> B[Extract Content]
    B --> C[AI Analysis]
    C --> D[Enhance Content]
    D --> E[Generate LaTeX]
    E --> F[Compile to PDF]
    F --> G{Compilation Success?}
    G -->|No| H[Retry Compilation]
    H --> G
    G -->|Yes| I[Return Enhanced PDF]
```

### Detailed Technical Flow
```mermaid
sequenceDiagram
    participant C as Candidate
    participant RC as ResumeController
    participant RS as ResumeService
    participant CR as ContentReader
    participant TPP as ThirdPartyProvider
    participant LC as LaTeXCompiler
    participant F as FileSystem

    C->>RC: POST /public/resumes/improve
    RC->>RS: improveResume(file)
    RS->>CR: extractContent(file)
    CR-->>RS: resumeContent
    
    RS->>TPP: improveResume(resumeContent)
    TPP->>TPP: processWithAI(resumeContent)
    Note over TPP: Uses specialized resume improvement prompts
    TPP-->>RS: LaTeXContent
    
    RS->>LC: generatePdfFromLatex(latexCode)
    LC->>LC: compileLaTeX()
    alt Compilation Success
        LC-->>RS: pdfBytes
    else Compilation Error
        LC->>LC: retryCompilation()
        LC-->>RS: pdfBytes
    end
    
    RS->>RS: prepareFileResponse()
    RS-->>RC: byte[] (PDF)
    RC->>RC: setHeaders(filename, contentType)
    RC-->>C: 200 OK + PDF file
```

### Resume Enhancement Process
```mermaid
flowchart TD
    A[Original Resume] --> B[Content Analysis]
    B --> C[Identify Improvements]
    C --> D[Add Keywords]
    D --> E[Improve Formatting]
    E --> F[Optimize Sections]
    F --> G[Generate LaTeX]
    G --> H[Apply ModernCV Template]
    H --> I[Compile to PDF]
    I --> J[Enhanced Resume]
```

## 5. System Architecture Overview

### Component Interaction Diagram
```mermaid
graph TB
    subgraph "Presentation Layer"
        JC[JobController]
        JAC[JobApplicationController]
        RC[ResumeController]
    end
    
    subgraph "Service Layer"
        JS[JobService]
        JAS[JobApplicationService]
        CS[CandidateService]
        RS[ResumeService]
        SK[SkillService]
        NS[NotificationService]
    end
    
    subgraph "AI Services"
        ORS[OpenRouterService]
        DSS[DeepSeekService]
        TPP[ThirdPartyProvider]
    end
    
    subgraph "Infrastructure"
        DB[(Database)]
        FS[FileSystem]
        LC[LaTeXCompiler]
        URL[URLShortener]
    end
    
    JC --> JS
    JAC --> JAS
    RC --> RS
    
    JS --> DB
    JAS --> CS
    JAS --> RS
    CS --> DB
    RS --> TPP
    SK --> DB
    
    TPP --> ORS
    TPP --> DSS
    
    RS --> LC
    RS --> FS
    JS --> URL
```

## 6. Data Flow Summary

### Entity Relationships
```mermaid
erDiagram
    Job ||--o{ JobApplication : "has many"
    Job ||--o{ JobSkill : "requires"
    Job ||--|| ShortURL : "has one"
    Job ||--o{ JobMetric : "tracks"
    
    Candidate ||--o{ JobApplication : "submits"
    Candidate ||--o{ CandidateSkill : "has"
    Candidate ||--o{ CandidateFile : "uploads"
    
    JobApplication ||--o{ JobApplicationStatus : "has"
    JobApplication ||--o{ JobApplicationSkill : "includes"
    JobApplication ||--|| File : "attaches"
    
    Skill ||--o{ JobSkill : "used in"
    Skill ||--o{ CandidateSkill : "possessed by"
    Skill ||--o{ JobApplicationSkill : "mentioned in"
    
    Company ||--o{ Job : "posts"
    Company ||--o{ Candidate : "manages"
    User ||--o{ Job : "creates"
```

These diagrams provide a comprehensive visual representation of the four main flows in the Job Posting Application, showing both high-level processes and detailed technical interactions between components.
