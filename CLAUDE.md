# CLAUDE.md - AI Assistant Guide for Job Search Assistant

## Project Overview

**Job Search Assistant** is a single-page web application that helps job seekers match their profiles with job postings using AI-powered analysis. The application provides intelligent resume parsing, job matching analysis, and generates tailored resumes and cover letters using Claude AI.

### Key Capabilities
- Profile setup via manual entry or document upload (PDF, DOCX, TXT)
- Intelligent resume/CV parsing and extraction
- Job description analysis and compatibility scoring
- AI-powered resume generation tailored to specific jobs
- AI-powered cover letter generation
- Document management and download (DOCX format)
- Persistent storage of user profiles and generated documents

## Architecture

### Technology Stack
This is a **monolithic single-page application** with all code contained in `index.html`:
- **HTML5**: Structure and markup
- **CSS3**: Embedded styles with gradient themes and responsive design
- **Vanilla JavaScript**: No frameworks - pure ES6+ JavaScript
- **External CDN Libraries**:
  - PDF.js v3.11.174 - PDF parsing
  - Mammoth.js v1.6.0 - DOCX parsing
  - JSZip v3.10.1 - ZIP file handling for DOCX download

### File Structure
```
job-search-assistant/
├── .git/                    # Git repository
├── index.html              # Entire application (2989 lines)
└── CLAUDE.md              # This documentation file
```

### Application Architecture
The application follows a **state-machine pattern** with five main sections:
1. **Setup Section** (`setup-section`) - Profile creation entry point
2. **Review Section** (`review-section`) - Profile validation
3. **Job Analysis Section** (`job-analysis-section`) - Job posting input
4. **Results Section** (`results-section`) - Analysis and generation results
5. **Generated Files Section** (`generated-files-section`) - File management

## Core Functionality

### 1. Profile Management

#### Manual Entry (index.html:318-368)
Form fields for user input:
- Full Name, Email, Phone (index.html:321-332)
- Location, LinkedIn Profile (index.html:334-342)
- Work Experience, Skills (index.html:344-352)
- Education, Certifications (index.html:354-362)

#### Document Upload (index.html:370-382)
- File picker for PDF, DOCX, or TXT files
- Drag-and-drop interface
- Multi-file support

#### Resume Parsing Pipeline
```javascript
handleFileUpload() -> extractTextFromPDF()/extractTextFromDOCX()
  -> parseExtractedText() -> parseResumeWithPatterns()
  -> displayProfileForReview()
```

**Key Functions**:
- `extractTextFromPDF(file)` (index.html:872-885) - Uses PDF.js to extract text
- `extractTextFromDOCX(file)` (index.html:887-891) - Uses Mammoth.js for DOCX parsing
- `parseExtractedText(text)` (index.html:893-938) - AI-powered parsing using Claude
- `parseResumeWithPatterns(text)` (index.html:940-1037) - Regex-based fallback parser

### 2. Job Analysis

#### Job Matching (index.html:1125-1215)
The `analyzeJob()` function:
1. Validates job description input
2. Calls Claude API with structured prompt
3. Analyzes match percentage, strengths, gaps, and recommendations
4. Displays color-coded match badge (Excellent/Good/Fair/Poor)

**Match Scoring**:
- 80-100%: Excellent match (green badge)
- 60-79%: Good match (blue badge)
- 40-59%: Fair match (yellow badge)
- 0-39%: Poor match (red badge)

### 3. Document Generation

#### Resume Generation (index.html:1424-1514, 2532-2622)
- Creates ATS-optimized resume tailored to job description
- Uses profile data and job requirements
- Formats with proper sections and keywords
- Generates plain text output for maximum compatibility

#### Cover Letter Generation (index.html:1516-1608, 2624-2716)
- Crafts personalized cover letters
- References specific job requirements
- Highlights relevant experience
- Professional tone and structure

#### DOCX Export (index.html:595-770)
The `downloadFileAsDOCX(fileId)` function:
- Converts plain text to formatted DOCX
- Adds proper styling and structure
- Uses JSZip to create valid .docx files
- Triggers browser download

### 4. Storage and State Management

#### Storage Abstraction Layer (index.html:452-490)
Three wrapper functions provide fallback capability:
- `safeStorageGet(key)` - Tries window.storage API, falls back to localStorage
- `safeStorageSet(key, value)` - Persists data with fallback
- `safeStorageDelete(key)` - Removes data with fallback

#### Stored Data
- `profile` - User profile object
- `generated_files` - Array of generated documents
- `current_job` - Current job description being analyzed
- `current_analysis` - Latest analysis results

#### State Variables (index.html:493-497)
```javascript
let profileData = null;           // Current user profile
let currentJobDescription = null; // Active job description
let currentAnalysis = null;       // Latest analysis results
let previousSection = null;       // Navigation history
let generatedFiles = [];          // Generated documents array
```

### 5. Claude API Integration

#### API Proxy (index.html:2964-2986)
```javascript
function callClaudeAPI(systemPrompt, userMessage)
```
- **Endpoint**: `https://curious-rugelach-e5ffb8.netlify.app/.netlify/functions/claude-proxy`
- **Method**: POST
- **Payload**: `{ systemPrompt, userMessage, maxTokens: 4000 }`
- **Response**: Returns content[0].text from Claude API response

#### API Usage Patterns
The app makes Claude API calls for:
1. **Resume Parsing** (index.html:920, 2097) - Structured extraction of profile data
2. **Job Analysis** (index.html:1207, 2384) - Match scoring and recommendations
3. **Gap Analysis** (index.html:1378) - Identifying profile weaknesses
4. **Resume Generation** (index.html:1489, 2597) - Creating tailored resumes
5. **Cover Letter Generation** (index.html:1532, 2640) - Writing cover letters

#### Response Processing (index.html:2956-2962)
```javascript
function stripMarkdownCodeFences(text)
```
Removes markdown code fences (```json, ```) that Claude sometimes adds to responses.

## Code Patterns and Conventions

### Naming Conventions
- **Functions**: camelCase (e.g., `analyzeJob`, `generateResume`)
- **Variables**: camelCase (e.g., `profileData`, `currentJobDescription`)
- **CSS Classes**: kebab-case (e.g., `.btn-primary`, `.form-group`)
- **IDs**: kebab-case (e.g., `#setup-section`, `#job-description`)

### Function Organization
Functions are organized by feature area:
1. **Storage functions** (index.html:453-490)
2. **File management** (index.html:520-770)
3. **Navigation** (index.html:772-810)
4. **Profile setup** (index.html:811-1123)
5. **Job analysis** (index.html:1125-1422)
6. **Document generation** (index.html:1424-2954)
7. **API utilities** (index.html:2956-2986)

### Error Handling Pattern
```javascript
try {
    // Operation
    const result = await apiCall();
    // Success handling
} catch (error) {
    // Display error to user
    alert('Error: ' + error.message);
    console.error(error);
}
```

### UI State Management
- Sections use `.hidden` class for visibility
- Active section has `.active` class
- `showSection(sectionId)` function handles navigation
- Previous section tracked for back navigation

## Development Workflow

### Current Git Workflow
Based on git history, the project follows a simple workflow:
1. Edit `index.html` locally
2. Commit with message "Add files via upload"
3. Push to repository
4. Sometimes followed by "Delete index.html" commits (likely cleanup/iteration)

### Branch Strategy
- **Main branch**: Not specified in git status
- **Current branch**: `claude/claude-md-mkshuhgkjywtzu7m-liXdx` (feature branch)
- Development happens on feature branches with `claude/` prefix

### Deployment
- Hosted on Netlify (evidence: Netlify function URL in code)
- Static site deployment (single HTML file)
- Serverless function for Claude API proxy

## Key Implementation Details

### Resume Parsing Strategy
The app uses a **two-tier parsing approach**:
1. **Primary**: AI-powered parsing via Claude API (index.html:893-938)
   - More accurate and context-aware
   - Handles various resume formats
   - Extracts structured data from unstructured text

2. **Fallback**: Regex-based pattern matching (index.html:940-1037)
   - Used if AI parsing fails
   - Looks for common patterns (email, phone, sections)
   - Less accurate but more reliable

### Section Headers for Parsing
The regex parser looks for these section markers:
- Experience: "EXPERIENCE", "WORK HISTORY", "EMPLOYMENT"
- Skills: "SKILLS", "TECHNICAL SKILLS", "COMPETENCIES"
- Education: "EDUCATION", "ACADEMIC", "QUALIFICATIONS"
- Certifications: "CERTIFICATIONS", "CERTIFICATES", "LICENSES"

### Match Score Calculation
Claude is prompted to return a structured JSON response with:
```json
{
  "matchPercentage": 85,
  "matchLevel": "Excellent",
  "strengths": ["strength1", "strength2"],
  "gaps": ["gap1", "gap2"],
  "recommendations": ["rec1", "rec2"]
}
```

### Document Format Standards
**Resume Format**:
- ATS-optimized (no tables, columns, or complex formatting)
- Clear section headers
- Bullet points for experience
- Keywords from job description
- Plain text for maximum compatibility

**Cover Letter Format**:
- Professional business letter format
- 3-4 paragraphs
- Opening: Position and excitement
- Body: Relevant experience and achievements
- Closing: Call to action

## AI Assistant Guidelines

### When Making Changes

#### ✅ DO:
1. **Read the entire section** you're modifying first
2. **Test locally** before committing (open in browser)
3. **Preserve the single-file architecture** - don't split into multiple files
4. **Maintain backward compatibility** with stored data
5. **Keep the UI/UX consistent** with existing patterns
6. **Add error handling** for new API calls or file operations
7. **Update comments** when adding complex logic
8. **Use the existing utility functions** (safeStorage*, stripMarkdownCodeFences, etc.)
9. **Follow the existing naming conventions**
10. **Test with different file types** (PDF, DOCX, TXT) if modifying upload logic

#### ❌ DON'T:
1. **Don't split into multiple files** - this is intentionally a single-file app
2. **Don't add frameworks** (React, Vue, etc.) - keep it vanilla JS
3. **Don't change the CDN library versions** without testing thoroughly
4. **Don't modify the storage schema** without migration logic
5. **Don't hardcode API keys** - they should stay in the Netlify function
6. **Don't remove fallback logic** (storage, parsing) - it ensures robustness
7. **Don't change the color scheme** without explicit request
8. **Don't add dependencies** that require build steps
9. **Don't modify the Netlify function URL** without updating the actual function
10. **Don't remove console.log statements** - they're useful for debugging

### Common Modification Scenarios

#### Adding a New Field to Profile
1. Add form input in manual entry section (index.html:318-368)
2. Update `saveManualProfile()` to capture new field
3. Update `parseExtractedText()` prompt to extract new field
4. Update `parseResumeWithPatterns()` fallback parser
5. Update `displayProfileForReview()` to show new field
6. Update resume/cover letter generation prompts to use new field

#### Modifying AI Prompts
1. Locate the relevant function (analyze, generate, parse)
2. Find the `systemPrompt` variable
3. Modify the prompt text
4. Test with various inputs
5. Ensure JSON response format is preserved for parsing

#### Adding a New Document Type
1. Add new button/section in results (index.html:425-433)
2. Create new `generate[DocumentType]()` function
3. Add to `generatedFiles` array with appropriate type
4. Update `displayGeneratedFiles()` if needed
5. Ensure DOCX download works with new format

#### Fixing UI Issues
1. Locate CSS classes (index.html:10-297)
2. Make changes preserving the gradient theme (#667eea, #764ba2)
3. Test responsive behavior (max-width: 900px)
4. Verify modal/section transitions

### Testing Checklist

Before committing changes:
- [ ] Open `index.html` in a modern browser (Chrome, Firefox, Safari)
- [ ] Test profile creation (manual entry)
- [ ] Test document upload (PDF and DOCX)
- [ ] Test job analysis with sample job description
- [ ] Test resume generation
- [ ] Test cover letter generation
- [ ] Test file download (DOCX)
- [ ] Test browser back/forward navigation
- [ ] Check browser console for errors
- [ ] Test with localStorage disabled (should still work)
- [ ] Verify mobile responsiveness (if UI changes)

### Debugging Tips

#### Common Issues:
1. **API Errors**: Check Netlify function status and Claude API quota
2. **Parsing Failures**: Check console for PDF.js/Mammoth errors
3. **Storage Issues**: Check localStorage quota and permissions
4. **UI Not Updating**: Verify `.hidden` and `.active` class management
5. **DOCX Download Fails**: Check JSZip console errors, verify XML structure

#### Console Commands for Testing:
```javascript
// Check current state
console.log(profileData);
console.log(generatedFiles);

// Test storage
await safeStorageGet('profile');
await safeStorageSet('test', 'value');

// Force section display
showSection('job-analysis-section');

// Test API
const result = await callClaudeAPI('You are helpful', 'Say hi');
```

## Security Considerations

### Current Security Posture
- ✅ API key hidden in Netlify serverless function
- ✅ No direct API key exposure in client code
- ✅ CORS handled by Netlify function
- ⚠️ No input sanitization on user data
- ⚠️ No rate limiting on API calls
- ⚠️ All data stored client-side (privacy concern)

### Recommendations for Enhancements
1. Add input sanitization for XSS prevention
2. Implement rate limiting in Netlify function
3. Add user authentication for multi-device sync
4. Encrypt sensitive data in localStorage
5. Add CSRF protection if adding server-side state
6. Validate file types server-side (current validation is client-only)

## Performance Considerations

### Current Performance Characteristics
- **Initial Load**: Fast (single HTML file, ~135KB)
- **CDN Dependencies**: Adds ~500KB total
- **API Calls**: 2-4 seconds per Claude API request
- **File Parsing**: 1-3 seconds for typical resumes
- **State Management**: Instant (in-memory)

### Optimization Opportunities
1. Consider minifying HTML/CSS/JS for production
2. Add loading states for all async operations
3. Implement request debouncing for real-time features
4. Cache API responses for identical requests
5. Lazy-load PDF.js/Mammoth.js only when needed
6. Use Web Workers for heavy parsing operations

## Future Enhancement Ideas

### Potential Features
1. **Multi-language Support**: i18n for global users
2. **Template Selection**: Multiple resume/cover letter styles
3. **LinkedIn Integration**: Auto-import profile data
4. **Job Board Integration**: Search and apply directly
5. **Application Tracking**: Track submitted applications
6. **Interview Prep**: Generate interview questions/answers
7. **Salary Insights**: Research and recommendations
8. **Skills Gap Analysis**: Learning path recommendations
9. **Network Analysis**: LinkedIn connection insights
10. **Email Integration**: Direct sending of applications

### Technical Improvements
1. **TypeScript Migration**: For better type safety
2. **Unit Tests**: Jest or Vitest for core functions
3. **E2E Tests**: Playwright or Cypress
4. **CI/CD Pipeline**: Automated testing and deployment
5. **Analytics**: Track usage patterns and success rates
6. **A/B Testing**: Optimize prompts and UI
7. **Offline Support**: Service Worker and PWA
8. **Version Control**: Semantic versioning for releases

## Glossary

### Key Terms
- **ATS**: Applicant Tracking System - software used by employers to filter resumes
- **DOCX**: Microsoft Word document format (.docx)
- **PDF**: Portable Document Format
- **SPA**: Single-Page Application
- **CDN**: Content Delivery Network
- **API**: Application Programming Interface
- **JSON**: JavaScript Object Notation
- **localStorage**: Browser storage API for persistent data

### Component References
- **Sections**: Major UI views (setup, review, analysis, results, files)
- **Profile Data**: User's resume/CV information
- **Generated Files**: AI-created documents (resumes, cover letters)
- **Match Analysis**: AI assessment of job fit
- **Storage Layer**: Persistence abstraction (localStorage/window.storage)

## Contact and Support

### Repository Information
- **Repository**: charissemorton/job-search-assistant
- **Current Branch**: claude/claude-md-mkshuhgkjywtzu7m-liXdx
- **Primary File**: index.html (2989 lines)

### For AI Assistants
When working on this codebase:
1. Always read index.html before making changes
2. Understand the full context of the section you're modifying
3. Test changes thoroughly before committing
4. Preserve the single-file architecture
5. Follow existing patterns and conventions
6. Document complex changes in code comments
7. Update this CLAUDE.md if making architectural changes

---

**Last Updated**: 2026-01-24
**Document Version**: 1.0
**Codebase Version**: Latest commit 46a4d68
