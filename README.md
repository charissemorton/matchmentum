# MatchMentum

**Build Career Momentum Fast** - AI-powered job application assistant that helps you create tailored resumes and cover letters in minutes.

🔗 **Live Demo:** [https://charissemorton.github.io/matchmentum/](https://charissemorton.github.io/matchmentum/)

---

## What It Does

MatchMentum analyzes your profile against job descriptions and generates:
- ✅ **Tailored resumes** optimized for specific jobs
- ✅ **Custom cover letters** that highlight relevant experience
- ✅ **Match analysis** showing how well you fit the role
- ✅ **ATS compatibility scores** to pass applicant tracking systems

### Key Features

- 📄 **Multi-resume upload** - Merge information from multiple versions of your resume
- 🤖 **AI-powered parsing** - Automatic extraction of work history, skills, certifications
- 🎯 **Job matching** - See your compatibility score before applying
- 📊 **Smart deduplication** - Automatically removes duplicate skills, certifications, and experience
- 💾 **Progress saving** - Your profile is saved locally, no account needed
- 📥 **DOCX export** - Download professional Word documents
- 🔒 **Privacy-first** - All data stays in your browser

---

## Quick Start

### 1. Upload Your Resume(s)
- Supports PDF, DOCX, and TXT files
- Upload multiple versions to combine information
- AI automatically extracts and merges your data

### 2. Review Your Profile
- Edit any parsed information
- Add missing details
- Verify everything is accurate

### 3. Analyze a Job
- Paste the job description
- Get instant compatibility score
- See your strengths and gaps

### 4. Generate Documents
- Create tailored resume for the specific job
- Generate matching cover letter
- Download as Word documents

---

## Technology Stack

**Frontend:**
- HTML5, CSS3, JavaScript (ES6+)
- Single-page application (no build process)
- Responsive design with shadow-based depth

**AI/ML:**
- Claude API (Anthropic) for intelligent parsing and generation
- Pattern-based fallback parser
- OCR support via Tesseract.js for image-based PDFs

**Document Processing:**
- PDF.js for PDF parsing
- Mammoth.js for DOCX parsing
- Custom DOCX generation with proper styling

**Data Storage:**
- LocalStorage for profile persistence
- Claude Projects persistent storage for saved files
- No server-side database

**Deployment:**
- GitHub Pages
- Netlify Functions for API proxy

---

## Features in Detail

### Smart Resume Parsing
- Extracts work experience with achievements and metrics
- Identifies skills, certifications, and education
- Detects projects and technical implementations
- Handles various resume formats and layouts
- OCR fallback for scanned/image-based PDFs

### Intelligent Merging
- Combines multiple resume versions
- Deduplicates skills (Python = Python 3 = Python 3.11)
- Removes duplicate certifications across resumes
- Merges work experience from different versions
- Keeps the most detailed version of each item

### Job Match Analysis
- Calibrated scoring system (70% = good match)
- Identifies your strengths for the role
- Highlights experience gaps
- Provides actionable recommendations
- Privacy controls (optional location inclusion)

### Resume Generation
- Tailored to specific job descriptions
- ATS-optimized formatting
- Anti-fabrication safeguards
- Includes only relevant information
- Professional DOCX formatting with proper styles

### Security Features
- XSS protection with input sanitization
- File size limits (10MB per file)
- File type validation
- Memory leak prevention
- Data validation for stored information

---

## Deployment

### GitHub Pages
1. Upload `matchmentum-final-v2.html` to your repository
2. Rename to `index.html`
3. Enable GitHub Pages in repository settings
4. Access at `https://[username].github.io/matchmentum/`

### Netlify Function (Required)
The application requires a Netlify Function to proxy API calls:

**Repository:** `claude-proxy` function on Netlify
**Endpoint:** `https://[your-netlify-site]/.netlify/functions/claude-proxy`

Update the API endpoint in the HTML file (line ~1569):
```javascript
const netlifyFunctionUrl = 'https://your-site.netlify.app/.netlify/functions/claude-proxy';
```

---

## File Limits

- **File size:** 10MB maximum per file
- **File types:** PDF, DOCX, TXT only
- **Multiple uploads:** No limit on number of files
- **Processing time:** 
  - Text-based PDFs: 2-5 seconds
  - Image-based PDFs (OCR): 30-60 seconds

---

## Browser Support

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+
- ❌ Internet Explorer (not supported)

---

## Privacy & Data

**What data is stored:**
- Your profile information (name, email, work history, skills)
- Generated resumes and cover letters
- Analysis results

**Where it's stored:**
- Locally in your browser (LocalStorage)
- Claude Projects persistent storage (if enabled)
- Never sent to external servers (except Claude API for processing)

**How to clear your data:**
- Use browser's "Clear browsing data" option
- Or clear LocalStorage via developer console
- Data is automatically cleared if you clear cookies

---

## Development

### File Structure
```
matchmentum-final-v2.html (5,300 lines)
├── HTML Structure (~200 lines)
├── CSS Styles (~800 lines)
└── JavaScript (~4,300 lines)
    ├── File Upload & Parsing
    ├── Profile Management
    ├── Job Analysis
    ├── Resume Generation
    ├── Cover Letter Generation
    └── DOCX Export
```

### Key Functions
- `handleMainFileUpload()` - Processes uploaded resumes
- `parseExtractedText()` - AI-powered parsing
- `mergeProfiles()` - Combines multiple resumes
- `analyzeJobMatch()` - Calculates compatibility
- `generateResume()` - Creates tailored resume
- `generateCoverLetter()` - Creates custom cover letter

### Rate Limiting
- Client-side: 50 API calls per hour
- Server-side: Configured in Netlify Function
- Automatic request throttling

---

## Known Limitations

- **Education:** No formal degree normalization (intentional - prevents false matches)
- **Languages:** English only
- **Job descriptions:** Cannot fetch from URLs (paste text instead)
- **Offline mode:** Requires internet for AI processing
- **Large files:** 10MB limit to prevent browser crashes

---

## Troubleshooting

### Issue: "File too large" error
**Solution:** Compress your PDF or use a smaller file (under 10MB)

### Issue: Certifications appearing multiple times
**Solution:** Re-upload resumes - deduplication improved in v2

### Issue: OCR taking too long
**Solution:** Click "Cancel OCR" and try a different file format

### Issue: "Rate limit exceeded"
**Solution:** Wait an hour or contact support to increase limits

### Issue: Resume not generating
**Solution:** Check console for errors, verify profile has required fields (name, email, experience)

---

## Changelog

### Version 2.0 (February 2026)
- ✅ Fixed XSS vulnerabilities (all 7 patched)
- ✅ Added file size limits (10MB max)
- ✅ Fixed memory leaks in PDF/OCR processing
- ✅ Improved deduplication across all fields
- ✅ Fixed blank section handling
- ✅ Enhanced comma-separated list parsing
- ✅ Better error messages and validation

### Version 1.0 (January 2026)
- Initial release
- Basic resume parsing and generation
- Job match analysis
- Cover letter generation

---

## Credits

**Created by:** Charisse Morton  
**AI Assistant:** Claude (Anthropic)  
**Tech Stack:** HTML, CSS, JavaScript, Claude API  

---

## License

This project is open source and available for personal use. Feel free to fork and customize for your own needs.

---

## Support

For issues or questions:
- Open an issue on GitHub
- Contact via LinkedIn: [Your LinkedIn Profile]
- Email: [Your Email]

---

## Acknowledgments

- Anthropic for Claude API
- PDF.js for PDF parsing
- Mammoth.js for DOCX support
- Tesseract.js for OCR capabilities

---

**Built with ❤️ to help job seekers build career momentum fast**
