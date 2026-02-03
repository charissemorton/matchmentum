[README.md](https://github.com/user-attachments/files/25029224/README.md)
# SmartApply - AI-Powered Job Application Assistant

**Version:** 2.0  
**Last Updated:** February 3, 2026  
**Author:** Charisse Morton  

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [How It Works](#how-it-works)
- [Getting Started](#getting-started)
- [Usage Guide](#usage-guide)
- [Technical Details](#technical-details)
- [Recent Updates](#recent-updates)
- [Troubleshooting](#troubleshooting)
- [Privacy & Ethics](#privacy--ethics)
- [License](#license)

---

## 🎯 Overview

SmartApply is an AI-powered job application assistant that helps you create tailored resumes and cover letters for specific job opportunities. Upload your resume, paste a job description, and get professionally formatted, ATS-optimized application materials in under 60 seconds.

### What Makes SmartApply Different?

✅ **Truthful AI** - Only uses information from your actual resume  
✅ **ATS Optimized** - Formats documents for Applicant Tracking Systems  
✅ **Smart Matching** - Analyzes job fit before you apply  
✅ **Fast & Easy** - Complete workflow in under a minute  
✅ **No Data Collection** - Everything stays in your browser  

---

## ✨ Features

### 📄 Resume Parsing
- **Multi-Format Support** - Upload PDF, DOCX, or TXT files
- **OCR Capability** - Extract text from scanned/image-based PDFs
- **AI-Powered Extraction** - Intelligently parses experience, skills, education, certifications
- **Multi-Resume Merging** - Upload multiple resumes at once for comprehensive profile
- **Cumulative Upload** - Add information from additional resumes without losing existing data

### 🎯 Job Analysis
- **Match Score** - Get percentage match between your profile and job requirements
- **Gap Analysis** - Identify missing skills and qualifications
- **Strength Identification** - See where your experience aligns perfectly
- **Strategic Insights** - Understand how to position yourself

### 📝 Document Generation
- **Tailored Resumes** - Custom resume for each job application
- **Custom Cover Letters** - Personalized letters that avoid AI tells
- **DOCX Download** - Professional formatting with proper spacing
- **Copy to Clipboard** - Quick copy for online applications
- **ATS Optimization** - Keyword matching and format compliance

### 🔧 Profile Management
- **Review & Edit** - Full control over extracted information
- **Manual Entry** - Option to enter profile details directly
- **Location Privacy** - Choose whether to include location in documents
- **Profile Persistence** - Auto-saves to browser storage
- **Start Over** - Easy reset to begin fresh

---

## 🚀 How It Works

### 1. **Upload Your Resume**
- Drag & drop or select PDF, DOCX, or TXT file
- Upload multiple resumes to merge into one comprehensive profile
- Or enter information manually

### 2. **Review Your Profile**
- AI extracts and structures your information
- Edit any field directly in-place
- Add more information from additional resumes if needed
- Confirm when ready

### 3. **Analyze Job Match**
- Paste job description
- Get instant match score and analysis
- See strengths, gaps, and strategic positioning advice

### 4. **Generate Documents**
- Create tailored resume in one click
- Generate custom cover letter
- Download as DOCX or copy text
- Apply with confidence

---

## 🏁 Getting Started

### Prerequisites
- Modern web browser (Chrome, Firefox, Safari, Edge)
- JavaScript enabled
- Internet connection (for AI processing)

### Installation

#### Option 1: Use Hosted Version
Visit: **https://charissemorton.github.io/smartapply/**

#### Option 2: Run Locally
```bash
# Clone or download the repository
git clone https://github.com/CharisseMorton/smartapply.git

# Navigate to directory
cd smartapply

# Open in browser
# Simply double-click index.html
# OR serve with local server:
python -m http.server 8000
# Then visit http://localhost:8000
```

### Initial Setup
1. Navigate to the application
2. Click "Get Started"
3. Upload your resume or use manual entry
4. Review extracted information
5. You're ready to analyze jobs!

---

## 📖 Usage Guide

### Uploading Your Resume

**Single Resume:**
1. Go to "Upload Resume" section
2. Click upload box or drag file
3. Wait for processing (10-30 seconds)
4. Review extracted information

**Multiple Resumes:**
1. Select 2-3 resume files at once
2. AI intelligently merges all information
3. Review combined profile

**Adding More Information:**
1. Go to "Review Profile" page
2. Use "📄 Add More Information" box
3. Upload additional resume
4. AI merges with existing profile without overwriting

### Reviewing Your Profile

**Edit Fields:**
- Click directly into any text field
- Make changes as needed
- All edits auto-save when you click "Confirm & Continue"

**Required Fields:**
- Name (required)
- Email (required)
- Experience or Skills (recommended for accurate matching)

**Tips for Better Results:**
- Include specific metrics and achievements
- List technical skills and tools
- Add certifications and education
- Include project details

### Analyzing Job Match

**Best Practices:**
1. Paste the ENTIRE job description (not just a URL)
2. Include requirements, qualifications, responsibilities
3. More detail = better analysis

**Understanding Your Score:**
- **85-100%** - Excellent match, strong candidate
- **70-84%** - Good match, competitive application
- **55-69%** - Moderate match, highlight transferable skills
- **Below 55%** - Consider whether to apply or address gaps

**Gap Addressing:**
- Review identified gaps
- Add context in the gap explanation field
- AI incorporates your explanation into documents

### Generating Documents

**Resume Generation:**
1. Click "Generate Resume"
2. Wait 30-60 seconds
3. Review generated resume
4. Download DOCX or copy text

**Cover Letter Generation:**
1. Click "Generate Cover Letter"
2. Wait 30-60 seconds
3. Review letter (checks for AI tells automatically)
4. Download DOCX or copy text

**Document Quality:**
- ✅ Uses ONLY information from your profile
- ✅ Tailored to specific job requirements
- ✅ Formatted for ATS compatibility
- ✅ No generic AI phrases
- ✅ Professional tone and structure

---

## 🔧 Technical Details

### Architecture
- **Frontend:** Single-page application (SPA)
- **Styling:** Custom CSS with responsive design
- **AI Integration:** Anthropic Claude API via Netlify Functions
- **Storage:** Browser localStorage (no server storage)
- **File Processing:** PDF.js, Mammoth.js, Tesseract.js

### Supported File Types
- **PDF** - Including scanned/image-based PDFs (with OCR)
- **DOCX** - Microsoft Word documents
- **TXT** - Plain text files

### Profile Data Structure (v2.0)
```javascript
{
  "metadata": {"version": "2.0"},
  "name": "string",
  "email": "string",
  "phone": "string",
  "location": "string",
  "linkedin": "string",
  "experience": "string",
  "skills": "string",
  "education": "string",
  "certifications": "string",
  "projects": "string"
}
```

### Browser Compatibility
- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+
- ❌ Internet Explorer (not supported)

### Performance
- **Resume Parsing:** 10-30 seconds (depending on file size and OCR needs)
- **Job Analysis:** 15-20 seconds
- **Resume Generation:** 30-60 seconds
- **Cover Letter Generation:** 30-60 seconds

### Privacy & Security
- **No server storage** - All data stored locally in your browser
- **No tracking** - No analytics or user tracking
- **No data sharing** - Your information stays with you
- **API calls only** - Only AI processing calls go to external servers
- **Clear data option** - "Start Over" deletes all stored information

---

## 🆕 Recent Updates

### Version 2.0 - February 3, 2026

#### 🔴 Critical Bug Fixes
- **Fixed 7 crashes** related to old nested profile format
- Resume DOCX download now works correctly
- Cover letter DOCX download now works correctly
- Location opt-in dialog fixed
- Location handling in document generation fixed

#### ✨ New Features
- **Multi-Resume Upload** - Select multiple resumes at once for intelligent merging
- **Cumulative Upload** - "Add More Information" box on review page
- **Improved Navigation** - Action verb labels (Upload Resume, Review Profile, Analyze Job)
- **Phone Validation** - Now accepts periods in phone numbers (555.123.4567)

#### 🛡️ Improved Validation
- Hard-block on empty profiles (requires name and email)
- Warning when missing experience/skills
- Better error messages
- Profile content checks before job analysis

#### 🔧 Technical Improvements
- Updated profile format migration logic
- Intelligent text field merging
- Better duplicate detection
- Enhanced error handling

### Version 1.0 - Initial Release
- Resume parsing with AI
- Job analysis and matching
- Tailored document generation
- ATS optimization
- Manual profile entry

---

## 🐛 Troubleshooting

### Resume Not Parsing Correctly

**Issue:** AI parsing failed or extracted wrong information

**Solutions:**
1. Try uploading a different file format (PDF → DOCX or vice versa)
2. If resume is scanned/image-based, wait for OCR (may take 30+ seconds)
3. Use manual entry to correct any errors
4. Check console for errors (F12 → Console tab)

### "Profile is Empty" Error

**Issue:** Can't proceed to job analysis

**Solutions:**
1. Ensure you've uploaded a resume OR used manual entry
2. Click "Confirm & Continue" on review page to save profile
3. Add at least name, email, and experience/skills
4. Check that profile fields aren't blank

### DOCX Download Not Working

**Issue:** Error when trying to download documents

**Solutions:**
1. Refresh the page and try again
2. Try "Copy Text" button instead and paste into Word
3. Ensure popup blocker isn't preventing download
4. Check browser console for errors

### Job Analysis Shows Low Match

**Issue:** Match score lower than expected

**Solutions:**
1. Ensure your resume has relevant experience and skills
2. Check that you pasted the FULL job description
3. Add certifications and projects to your profile
4. Use "Add More Information" to upload additional resumes
5. Address gaps in the gap explanation field

### OCR Taking Too Long

**Issue:** Scanned PDF processing is slow

**Solutions:**
1. Wait patiently (can take 30-60 seconds for multi-page PDFs)
2. Convert scanned PDF to searchable PDF using external tool
3. Use DOCX format instead if possible
4. Reduce file size (fewer pages)

### Lost My Profile Data

**Issue:** Profile disappeared after closing browser

**Solutions:**
1. Check if you're in Incognito/Private mode (data doesn't persist)
2. Check if browser cleared localStorage
3. Re-upload resume to recreate profile
4. Use "Download DOCX" to save documents before closing

---

## ⚖️ Privacy & Ethics

### Truthfulness Commitment

SmartApply is committed to **truthful, ethical job applications**. The tool:

✅ **DOES:**
- Help you articulate your real experience effectively
- Format your actual qualifications for maximum impact
- Tailor your genuine skills to job requirements
- Suggest better ways to phrase your accomplishments

❌ **DOES NOT:**
- Create false qualifications
- Fabricate skills you don't have
- Invent experience or achievements
- Generate misleading information

### User Responsibility

**You are responsible for:**
- Ensuring all information is accurate and truthful
- Verifying generated documents before submission
- Maintaining professional and ethical standards
- Using the tool as intended (assistance, not fabrication)

### Data Privacy

- **Local Storage Only** - Your data stays in your browser
- **No Account Required** - No registration or personal data collection
- **No Tracking** - We don't track your usage
- **API Calls** - Only AI processing happens on external servers
- **No Data Retention** - AI provider doesn't store your resume data

### Acknowledgment

Before generating documents, you acknowledge:
1. All information provided is truthful and accurate
2. You've reviewed and verified all details
3. Generated documents are based on your real qualifications
4. You take responsibility for final application materials

---

## 📞 Support & Feedback

### Getting Help

- **Check Troubleshooting Section** - Most common issues covered above
- **Browser Console** - Press F12 to see detailed error messages
- **GitHub Issues** - [Report bugs or request features](https://github.com/CharisseMorton/smartapply/issues)
- **GitHub Repository** - [View source code](https://github.com/CharisseMorton/smartapply)

### Feedback

Your feedback helps improve SmartApply!

- **👍 Like a feature?** - Let us know what's working well
- **👎 Found a bug?** - Report it with steps to reproduce
- **💡 Have an idea?** - Suggest new features or improvements
- **📝 Documentation unclear?** - Tell us what needs clarification

### Contributing

Interested in contributing? We welcome:
- Bug fixes
- Feature enhancements
- Documentation improvements
- UI/UX suggestions

---

## 📄 License

This project is provided as-is for personal and professional use. 

**Permitted Uses:**
- Personal job searching
- Professional career development
- Educational purposes

**Restrictions:**
- Do not use for fraudulent applications
- Do not redistribute without attribution
- Do not use for commercial reselling

---

## 🙏 Acknowledgments

### Technologies Used
- **Anthropic Claude** - AI processing
- **PDF.js** - PDF text extraction
- **Mammoth.js** - DOCX processing
- **Tesseract.js** - OCR capability
- **JSZip** - DOCX generation

### Inspiration
Built to help job seekers present their authentic qualifications effectively while navigating the challenges of modern ATS systems and AI-powered recruitment tools.

---

## 📊 Statistics

- **4,899 lines of code**
- **63 functions**
- **5 main sections** (Upload, Review, Analyze, Generate)
- **3 file formats supported** (PDF, DOCX, TXT)
- **60 second average** processing time
- **Zero data collection** - privacy-first design

---

## 🗺️ Roadmap

### Planned Features
- [ ] LinkedIn profile import
- [ ] Multiple job comparison
- [ ] Application tracking
- [ ] Document version history
- [ ] Export to various formats (Google Docs, Pages, etc.)
- [ ] Template customization
- [ ] Skill gap learning resources
- [ ] Interview preparation based on job analysis

### Under Consideration
- Mobile app version
- Browser extension
- Batch job analysis
- Resume A/B testing
- Industry-specific templates

---

## ⚡ Quick Start

**In under 60 seconds:**

1. **Visit the app** → **https://charissemorton.github.io/smartapply/**
2. **Upload resume** → Click "Upload Resume"
3. **Review profile** → Check extracted info
4. **Paste job description** → Go to "Analyze Job"
5. **Generate documents** → Click "Generate Resume"
6. **Apply!** → Download or copy

**That's it!** You're ready to submit a tailored application.

---

## 🎓 Tips for Success

### Resume Tips
- Include specific metrics and numbers
- List technical skills and tools
- Add certifications with dates
- Include project details and outcomes

### Job Analysis Tips
- Paste the complete job description
- Include requirements and qualifications sections
- Don't just paste the URL
- More detail = better matching

### Document Generation Tips
- Address identified gaps before generating
- Review generated documents carefully
- Customize further if needed
- Save multiple versions for different roles

---

**Ready to streamline your job search? [Get Started →](https://charissemorton.github.io/smartapply/)** 🚀

---

*SmartApply - Because your authentic qualifications deserve authentic presentation.*

**Version 2.0** | Last Updated: February 3, 2026 | Made with ❤️ by Charisse Morton
