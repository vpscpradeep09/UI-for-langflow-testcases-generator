# Quick Reference: User Story Reviewer UI Implementation

## 📦 What's Included

```
langflow-user-story-reviewer-ui/
├── user-story-reviewer-ui.html               # Main application file
├── SETUP_AND_USAGE_GUIDE.md                 # User guide and setup
├── ADVANCED_RESPONSE_PARSING_GUIDE.md       # Technical deep-dive
├── THIS_FILE (QUICK_REFERENCE.md)           # Quick reference
└── source files/
    ├── User Story Review Agent_Langflow-export-File.json
    ├── User Story Review Agent_Calling-langflow-from-postman.txt
    └── user-story-reviewer-ui.md.txt
```

---

## 🚀 Quick Start (30 seconds)

```bash
# 1. Ensure Langflow is running on port 7860
# 2. Open the HTML file in your browser
open user-story-reviewer-ui.html

# 3. Click "Test Connection" to verify API connectivity
# 4. Click "Use This Sample" to load an example
# 5. Click "Review & Score" to analyze
```

---

## 🔑 Key Configuration

All configuration is in the HTML `<script>` section:

```javascript
// API Configuration
const LANGFLOW_API = 'http://localhost:7860/api/v1/run/3fca058a-15dd-43a1-8d4c-b5f576246de7';
const API_KEY = 'sk-l7XYkwdxkUmrTea_PvIcA0OwkCfb6AR3tEJ4WtiiIls';

// Sample Story
const SAMPLE_STORY = 'As a user, I want to...';
```

---

## 🎯 Core Functions

### Main User Flow
```javascript
// User enters story → clicks "Review & Score"
reviewUserStory()
  ├── Validate input
  ├── Call Langflow API
  ├── Parse response
  ├── Extract score
  └── displayResults()
```

### Supporting Functions
```javascript
useSampleStory()          // Load sample into input field
testConnection()          // Verify API is accessible
clearResults()            // Reset all data
extractScoreFromText()    // Parse score from AI response
displayResults()          // Show results on UI
copyToClipboard()         // Copy result to clipboard
toggleDebugPanel()        // Show/hide debug console
addDebugLog()             // Log debug messages
```

---

## 📡 API Call Details

### Endpoint
```
POST http://localhost:7860/api/v1/run/3fca058a-15dd-43a1-8d4c-b5f576246de7
```

### Request
```javascript
{
    "output_type": "text",
    "input_type": "text",
    "input_value": "<user story text>"
}
```

### Headers
```
Content-Type: application/json
x-api-key: sk-l7XYkwdxkUmrTea_PvIcA0OwkCfb6AR3tEJ4WtiiIls
```

### Expected Response
```javascript
{
    outputs: [{
        outputs: [{
            results: {
                message: {
                    text: "Score: X/10\n\nAssessment..."
                }
            }
        }]
    }]
}
```

---

## 🔍 UI Components Breakdown

### Header
- Title and description
- Branding

### Pro Tips
- Quick reference for workflow
- Feature highlights

### API Status
- Connection test button
- Status indicator
- Color-coded feedback

### Sample Story
- Pre-filled example
- "Use This Sample" button
- For testing purposes

### Input Section
- Text area for user stories
- Review & Score button
- Clear All button

### Results Section
- Displays reviewed story with copy button
- Score card with quality level indicator
- Detailed assessment with copy button

### Debug Console
- Toggle button
- Real-time logs
- Timestamps
- Color-coded messages (info/success/error)

---

## 🎨 CSS Structure

```css
/* Main layout */
.container           /* Outer wrapper */
.header             /* Title area */
.content            /* Main content area */
.footer             /* Footer info */

/* Sections */
.section            /* Section wrapper */
.section-title      /* Section heading */

/* Styles */
.pro-tips           /* Callout box */
.btn                /* Button styling */
.btn-primary        /* Primary action */
.btn-danger         /* Destructive action */
.results            /* Results container */
.score-card         /* Score display */
.alert              /* Alert messages */
.debug-panel        /* Debug console */

/* Responsive */
@media (max-width: 768px)  /* Mobile styles */
```

---

## 🔄 Score Extraction Logic

```javascript
// 1. Try regex patterns (in order)
Patterns tried:
  - "score: 8.5/10"
  - "rating: 8.5"
  - "8.5 out of 10"
  - "85%"
  - "Quality Score: 8.5"
  - "score is 8.5"

// 2. Parse number from first match
Score: 8.5

// 3. Normalize to 0-100 scale
if (score <= 10) {
    score = (score / 10) * 100;  // 8.5 → 85
}

// 4. Clamp to range
score = Math.min(Math.max(score, 0), 100);
```

---

## 📊 Score Interpretation

```javascript
if (score >= 80) {
    // ✓ Excellent Quality - Ready for Testing
} else if (score >= 60) {
    // ◐ Good Quality - Minor Improvements
} else if (score >= 40) {
    // ◔ Fair Quality - Significant Improvements
} else {
    // ✗ Needs Major Revision
}
```

---

## 🐛 Debugging Checklist

```
✓ Langflow running? (localhost:7860)
✓ API Key valid? (Check in Langflow settings)
✓ Flow ID correct? (3fca058a-15dd-43a1-8d4c-b5f576246de7)
✓ Input format correct? (JSON with output_type, input_type, input_value)
✓ Response parsing working? (Open Debug Console)
✓ Score extraction working? (Check extracted score in debug log)
```

---

## 🚨 Common Errors & Fixes

| Error | Cause | Fix |
|-------|-------|-----|
| Cannot connect to Langflow | Langflow not running | Start Langflow on port 7860 |
| API Error: 401 | Invalid API key | Update API key in HTML |
| CORS error | Browser blocking request | Configure CORS in Langflow |
| Score: 0 | Score not found in response | Check response format, add pattern |
| No results shown | Response parsing failed | Check debug console for structure |

---

## 📝 Common Customizations

### Change API Endpoint
```javascript
// Line ~110
const LANGFLOW_API = 'http://your-host:port/api/v1/run/FLOW_ID';
```

### Change API Key
```javascript
// Line ~111
const API_KEY = 'your-api-key';
```

### Change Sample Story
```javascript
// Line ~114
const SAMPLE_STORY = 'Your story here';
```

### Add New Score Pattern
```javascript
// In extractScoreFromText() function, add:
const yourPattern = /your_pattern_here[\s:]*(\d+(?:\.\d+)?)/i;
```

### Modify Score Labels
```javascript
// In displayResults() function:
if (score >= 80) {
    scoreDetailsElement.textContent = 'Your custom message';
}
```

---

## 📂 File Organization

```
Main Files:
- user-story-reviewer-ui.html          (Single-file application, 700+ lines)
  ├── Embedded CSS (400+ lines)
  └── Embedded JavaScript (400+ lines)

Documentation:
- SETUP_AND_USAGE_GUIDE.md             (User guide)
- ADVANCED_RESPONSE_PARSING_GUIDE.md   (Technical details)
- QUICK_REFERENCE.md                   (This file)

Source Files:
- User Story Review Agent_Langflow-export-File.json
- User Story Review Agent_Calling-langflow-from-postman.txt
- user-story-reviewer-ui.md.txt
```

---

## 🔗 Quick Links

| Resource | Location |
|----------|----------|
| HTML File | `user-story-reviewer-ui.html` |
| Setup Guide | `SETUP_AND_USAGE_GUIDE.md` |
| Technical Guide | `ADVANCED_RESPONSE_PARSING_GUIDE.md` |
| Langflow Export | `source files/User Story Review Agent_Langflow-export-File.json` |
| Postman Example | `source files/User Story Review Agent_Calling-langflow-from-postman.txt` |

---

## 💡 Pro Tips

1. **Test First**: Always click "Test Connection" when starting
2. **Debug Mode**: Use 🔧 Debug Console for troubleshooting
3. **Copy Results**: Click copy buttons to save assessments
4. **Sample Story**: Test with sample first before production data
5. **Clear Data**: Use "Clear All" between tests to avoid confusion
6. **Browser Console**: Press F12 for additional debugging

---

## ✅ Features Checklist

- [x] ✅ Langflow API integration
- [x] ✅ User story input
- [x] ✅ AI-powered scoring
- [x] ✅ Quality assessment display
- [x] ✅ Copy to clipboard
- [x] ✅ Sample user story
- [x] ✅ Clear all function
- [x] ✅ Connection test
- [x] ✅ Debug console
- [x] ✅ Responsive design
- [x] ✅ Error handling
- [x] ✅ Score parsing

---

## 🎯 Next Steps

1. ✅ Open `user-story-reviewer-ui.html` in browser
2. ✅ Read `SETUP_AND_USAGE_GUIDE.md` for detailed setup
3. ✅ Test connection with "Test Connection" button
4. ✅ Try sample story
5. ✅ Input your own user stories
6. ✅ Refer to `ADVANCED_RESPONSE_PARSING_GUIDE.md` if issues arise

---

**Version**: 1.0  
**Status**: Production Ready  
**Last Updated**: June 7, 2026  

For detailed information, see the full documentation files.
