# Job Posting Application - Detailed Scenarios

This document provides comprehensive scenarios for each of the four main flows in the Job Posting Application, including edge cases, error handling, and user interactions.

## Table of Contents
1. [Add a Featured Job Scenarios](#add-a-featured-job-scenarios)
2. [Apply to a Featured Job Scenarios](#apply-to-a-featured-job-scenarios)
3. [Candidate Skill Extraction Scenarios](#candidate-skill-extraction-scenarios)
4. [Resume Improvement Scenarios](#resume-improvement-scenarios)

---

## Add a Featured Job Scenarios

### Scenario 1: Successful Featured Job Creation

**Actor:** Sarah (Company Recruiter)
**Context:** Sarah needs to post a new Senior Software Engineer position
**Preconditions:** Sarah is logged in with COMPANY_RECRUITER role

#### Main Flow:
1. Sarah navigates to the "Create Featured Job" page
2. She fills out the job form with:
   - Title: "Senior Software Engineer"
   - Description: "We are looking for an experienced software engineer..."
   - Location: "Remote"
   - Category: "Software Development"
   - Sub-category: "Full Stack"
   - Min Salary: $100,000
   - Max Salary: $150,000
   - Currency: USD
   - Skills: ["Java", "Spring Boot", "React", "AWS"]
3. Sarah clicks "Create Job"
4. System validates the form data
5. System creates the job with `featured = true`
6. System generates a short URL: `https://jobs.ly/abc123`
7. System schedules the job for automated promotion
8. Sarah receives confirmation: "Featured job created successfully"
9. Job appears in the featured jobs list

#### Expected Result:
- Job is created and marked as featured
- Short URL is generated for easy sharing
- Job is scheduled for automated promotion
- Sarah can view and manage the job

### Scenario 2: Job Creation with Missing Required Fields

**Actor:** Mike (Company Admin)
**Context:** Mike tries to create a job but forgets required information

#### Main Flow:
1. Mike navigates to "Create Featured Job"
2. He fills out only the job title: "Data Scientist"
3. He leaves description, location, and salary fields empty
4. Mike clicks "Create Job"
5. System validates the form and finds missing required fields
6. System returns validation errors:
   - "Description is required"
   - "Location is required"
   - "Minimum salary is required"
7. Mike corrects the form and resubmits
8. Job is created successfully

#### Expected Result:
- Validation errors are displayed clearly
- User can correct errors and resubmit
- Job is created only after all validations pass

### Scenario 3: Unauthorized Job Creation Attempt

**Actor:** John (Regular User)
**Context:** John tries to create a featured job without proper permissions

#### Main Flow:
1. John (with USER role) navigates to "Create Featured Job"
2. System checks John's permissions
3. System determines John lacks required role (COMPANY_RECRUITER, ADMIN, etc.)
4. System returns 403 Forbidden error
5. John is redirected to an access denied page

#### Expected Result:
- Access is denied for unauthorized users
- Clear error message is displayed
- User is redirected appropriately

### Scenario 4: Job Creation with Skills Processing

**Actor:** Lisa (Company Recruiter)
**Context:** Lisa creates a job with specific technical skills

#### Main Flow:
1. Lisa creates a job for "DevOps Engineer"
2. She specifies skills: ["Docker", "Kubernetes", "Terraform", "AWS"]
3. System processes the skills:
   - Normalizes skill names
   - Categorizes by skill level (if provided)
   - Creates new skills if they don't exist
   - Links skills to the job
4. System generates skill-based recommendations
5. Job is created with associated skills

#### Expected Result:
- Skills are properly processed and stored
- New skills are created in the database
- Job is linked to all specified skills

---

## Apply to a Featured Job Scenarios

### Scenario 1: Successful Job Application

**Actor:** Alex (Job Candidate)
**Context:** Alex wants to apply for a Software Developer position
**Preconditions:** Featured job exists and is accepting applications

#### Main Flow:
1. Alex browses featured jobs and finds "Software Developer" position
2. He clicks "Apply Now"
3. Alex fills out the application form:
   - First Name: "Alex"
   - Last Name: "Johnson"
   - Email: "alex.johnson@email.com"
   - Phone: "+1-555-0123"
   - Expected Salary: $120,000
   - Uploads resume: "Alex_Johnson_Resume.pdf"
4. Alex clicks "Submit Application"
5. System validates the application data
6. System checks for duplicate applications (none found)
7. System creates JobApplication entity
8. System processes the resume asynchronously:
   - Extracts personal information
   - Extracts technical skills
   - Creates/updates candidate profile
   - Calculates relevance score
9. System sends confirmation email to Alex
10. System notifies the recruiter of new application

#### Expected Result:
- Application is successfully submitted
- Candidate profile is created/updated
- Skills are extracted and categorized
- Relevance score is calculated
- Notifications are sent to both parties

### Scenario 2: Duplicate Application Attempt

**Actor:** Maria (Job Candidate)
**Context:** Maria tries to apply for the same job twice

#### Main Flow:
1. Maria applies for "Product Manager" position
2. Application is successfully submitted
3. Maria tries to apply again for the same position
4. System checks for existing applications with same email and job ID
5. System finds duplicate application
6. System returns error: "You have already applied for this position"
7. Maria is redirected to application status page

#### Expected Result:
- Duplicate applications are prevented
- Clear error message is displayed
- User is redirected to appropriate page

### Scenario 3: Application to Closed Job

**Actor:** David (Job Candidate)
**Context:** David tries to apply for a job that has been closed

#### Main Flow:
1. David finds a job posting for "Marketing Manager"
2. He fills out the application form
3. He clicks "Submit Application"
4. System validates the job status
5. System finds that the job is closed
6. System returns error: "This job is no longer accepting applications"
7. David is redirected to the job details page with status message

#### Expected Result:
- Applications to closed jobs are rejected
- Clear status message is displayed
- User understands why application was not accepted

### Scenario 4: Application with Resume Processing Error

**Actor:** Sarah (Job Candidate)
**Context:** Sarah uploads a corrupted resume file

#### Main Flow:
1. Sarah applies for "Data Analyst" position
2. She uploads a corrupted PDF file
3. System attempts to process the resume
4. Content extraction fails due to file corruption
5. System logs the error but continues processing
6. Application is created without skill extraction
7. System sends notification to admin about processing error
8. Sarah receives confirmation but with limited functionality

#### Expected Result:
- Application is still created
- Error is logged for investigation
- Admin is notified of processing issues
- User receives appropriate feedback

---

## Candidate Skill Extraction Scenarios

### Scenario 1: Successful Skill Extraction

**Actor:** System (AI Service)
**Context:** Processing a well-formatted resume with clear technical skills

#### Main Flow:
1. Resume file is uploaded: "John_Doe_Resume.pdf"
2. System extracts text content successfully
3. AI service (OpenRouter) analyzes the content
4. AI identifies skills:
   - Beginner: ["HTML", "CSS"]
   - Intermediate: ["JavaScript", "React"]
   - Advanced: ["Java", "Spring Boot"]
   - Expert: ["System Design", "Microservices"]
5. System normalizes skill names
6. System checks existing skills in database
7. New skills are created for those not found
8. Skills are categorized and linked to candidate
9. Candidate profile is updated with extracted skills

#### Expected Result:
- All skills are accurately extracted
- Skills are properly categorized by level
- New skills are created in the database
- Candidate profile is updated successfully

### Scenario 2: Skill Extraction from Poorly Formatted Resume

**Actor:** System (AI Service)
**Context:** Processing a resume with poor formatting and unclear skill descriptions

#### Main Flow:
1. Resume file is uploaded: "Jane_Smith_Resume.pdf"
2. System extracts text content (some formatting issues)
3. AI service analyzes the content
4. AI identifies some skills but with lower confidence:
   - Intermediate: ["Programming", "Database"]
   - Advanced: ["Software Development"]
5. System attempts to normalize unclear skill names
6. Some skills are categorized as "OTHER" due to ambiguity
7. System creates skills with best-guess categorization
8. Candidate profile is updated with available skills

#### Expected Result:
- Skills are extracted with available information
- Ambiguous skills are categorized appropriately
- System handles poor formatting gracefully
- Candidate profile is updated with extracted data

### Scenario 3: AI Service Failure and Fallback

**Actor:** System (AI Service)
**Context:** Primary AI service (OpenRouter) is unavailable

#### Main Flow:
1. Resume file is uploaded for processing
2. System attempts to use OpenRouter service
3. OpenRouter service returns error (timeout/API failure)
4. System checks feature flags and switches to DeepSeek service
5. DeepSeek service processes the resume successfully
6. Skills are extracted and categorized
7. Candidate profile is updated
8. System logs the service switch for monitoring

#### Expected Result:
- Fallback mechanism works correctly
- Skills are still extracted successfully
- System maintains high availability
- Service switch is logged for analysis

### Scenario 4: Resume with No Technical Skills

**Actor:** System (AI Service)
**Context:** Processing a resume for a non-technical position

#### Main Flow:
1. Resume file is uploaded: "Marketing_Manager_Resume.pdf"
2. System extracts text content
3. AI service analyzes the content
4. AI finds no technical skills, only soft skills and experience
5. System creates empty skill set
6. Candidate profile is updated with no technical skills
7. Job matching algorithms handle non-technical profiles appropriately

#### Expected Result:
- System handles non-technical resumes gracefully
- Empty skill set is created appropriately
- Job matching works for non-technical positions
- No errors occur due to missing technical skills

---

## Resume Improvement Scenarios

### Scenario 1: Successful Resume Enhancement

**Actor:** Michael (Job Candidate)
**Context:** Michael wants to improve his resume for better ATS compatibility

#### Main Flow:
1. Michael uploads his current resume: "Michael_Resume.pdf"
2. System extracts text content from the PDF
3. AI service analyzes the resume structure and content
4. AI identifies areas for improvement:
   - Missing keywords for his target role
   - Poor section organization
   - Unclear achievement descriptions
5. AI generates enhanced LaTeX code:
   - Adds relevant keywords
   - Improves section headings
   - Quantifies achievements
   - Uses moderncv template
6. System compiles LaTeX to PDF successfully
7. Enhanced resume is generated: "ModernCv_Michael_Resume.pdf"
8. Michael downloads the improved resume

#### Expected Result:
- Resume is significantly improved
- All original content is preserved
- ATS compatibility is enhanced
- Professional formatting is applied

### Scenario 2: LaTeX Compilation Error

**Actor:** Lisa (Job Candidate)
**Context:** AI generates LaTeX code with syntax errors

#### Main Flow:
1. Lisa uploads her resume for improvement
2. AI generates LaTeX code with some syntax issues
3. System attempts to compile LaTeX to PDF
4. Compilation fails due to syntax errors
5. System retries compilation (up to 3 attempts)
6. On second attempt, compilation succeeds
7. Enhanced resume is generated successfully
8. Lisa receives the improved resume

#### Expected Result:
- Retry mechanism handles compilation errors
- Resume is eventually generated successfully
- System maintains reliability through retries

### Scenario 3: Resume with Complex Formatting

**Actor:** Robert (Job Candidate)
**Context:** Robert's resume has complex tables and graphics

#### Main Flow:
1. Robert uploads a resume with complex formatting
2. System extracts text content (graphics and tables are simplified)
3. AI processes the simplified content
4. AI generates clean LaTeX code without complex formatting
5. System compiles LaTeX successfully
6. Enhanced resume is generated with clean, ATS-friendly formatting
7. Robert receives the improved resume

#### Expected Result:
- Complex formatting is simplified appropriately
- ATS compatibility is improved
- Clean, professional output is generated
- All important content is preserved

### Scenario 4: AI Service Timeout

**Actor:** Jennifer (Job Candidate)
**Context:** AI service takes too long to process the resume

#### Main Flow:
1. Jennifer uploads a very long resume (10+ pages)
2. System extracts text content
3. AI service processes the content but takes longer than expected
4. System implements timeout mechanism
5. AI service returns partial results before timeout
6. System uses available results to generate LaTeX
7. Enhanced resume is generated with available improvements
8. Jennifer receives the partially improved resume

#### Expected Result:
- Timeout mechanism prevents system hanging
- Partial improvements are still applied
- System maintains responsiveness
- User receives feedback about processing

---

## Error Handling Scenarios

### Scenario 1: Database Connection Failure

**Context:** Database is temporarily unavailable during job creation

#### Main Flow:
1. User submits job creation request
2. System attempts to save job to database
3. Database connection fails
4. System catches database exception
5. System returns 500 Internal Server Error
6. User sees error message: "Service temporarily unavailable"
7. System logs error for investigation

#### Expected Result:
- Graceful error handling
- User receives appropriate feedback
- Error is logged for monitoring
- System remains stable

### Scenario 2: File Upload Size Limit Exceeded

**Context:** User tries to upload a resume larger than allowed limit

#### Main Flow:
1. User uploads 50MB resume file (limit is 10MB)
2. System validates file size
3. System rejects the file
4. System returns error: "File size exceeds maximum allowed size"
5. User is prompted to upload smaller file

#### Expected Result:
- File size validation works correctly
- Clear error message is displayed
- User can retry with appropriate file size

### Scenario 3: Invalid File Format

**Context:** User uploads non-PDF file for resume processing

#### Main Flow:
1. User uploads .docx file for resume improvement
2. System validates file format
3. System accepts .docx and converts to text
4. Processing continues normally
5. Enhanced resume is generated successfully

#### Expected Result:
- Multiple file formats are supported
- Conversion happens transparently
- Processing continues normally

---

## Performance Scenarios

### Scenario 1: High Volume Job Applications

**Context:** Popular job posting receives 100+ applications in one hour

#### Main Flow:
1. Multiple candidates apply simultaneously
2. System processes applications in parallel
3. Async processing handles resume analysis
4. Database handles concurrent writes
5. All applications are processed successfully
6. System maintains response times

#### Expected Result:
- System handles high volume gracefully
- Performance remains acceptable
- All applications are processed
- No data loss occurs

### Scenario 2: Large Resume File Processing

**Context:** User uploads 8MB resume with complex formatting

#### Main Flow:
1. Large resume file is uploaded
2. System processes file in chunks
3. AI service handles large content
4. Processing takes longer but completes
5. Enhanced resume is generated successfully

#### Expected Result:
- Large files are handled appropriately
- Processing completes successfully
- Memory usage is managed efficiently
- User receives feedback on progress

These scenarios provide comprehensive coverage of the main flows, edge cases, and error conditions in the Job Posting Application, ensuring robust and user-friendly operation across all use cases.
