# User Story Reviewer UI - Updated for Dual Modes

## 📋 Langflow Flow Architecture Understanding

### **What Langflow Actually Does:**

The Langflow "User Story Review Agent" has **4 integrated steps**:

```
Step 1: API Request
   └─→ Fetches user story from Jira
   └─→ Output: Raw Jira story JSON

Step 2: Parser Component
   └─→ Parses and extracts Jira response
   └─→ Output: Structured data

Step 3: Groq Model (First LLM)
   └─→ Beautifies and extracts specific content
   └─→ Makes content more readable and structured
   └─→ Output: Cleaned-up user story

Step 4: Prompt Template + Groq Model (Second LLM)
   └─→ Takes beautified story
   └─→ Generates quality score
   └─→ Provides detailed assessment
   └─→ Output: Score (X/10) + Assessment
```

---

## 🎯 UI Implementation - Two Operating Modes

The updated UI now supports **two distinct modes** based on your requirements:

### **Mode 1: Manual Input Mode (Direct Scoring)**
**What it does:** Skips Steps 1-2, performs Steps 3-4 only

```
User Input (User Story Text)
    ↓
Step 3: Groq Model (Beautify)
    └─→ Beautifies the input story
    └─→ Extracts key content
    ↓
Step 4: Groq Model (Score)
    └─→ Generates quality score
    └─→ Returns assessment
    ↓
Output: Score + Detailed Assessment
```

**When to use:** 
- When you already have user story text and just want scoring
- For quick testing and validation
- When Jira integration isn't available

**Workflow:**
1. Select "Manual Input Mode"
2. Paste or type your user story
3. Click "Get Score"
4. View score and assessment

---

### **Mode 2: Jira Integration Mode (Full Flow)**
**What it does:** Performs all Steps 1-4

```
Jira Issue Key (e.g., PROJ-123)
    ↓
Step 1: API Request
    └─→ Fetches from Jira
    └─→ Gets full issue details
    ↓
Step 2: Parser
    └─→ Extracts issue data
    └─→ Structures the response
    ↓
Step 3: Groq Model (Beautify)
    └─→ Beautifies the story
    └─→ Makes it more readable
    ↓
Step 4: Groq Model (Score)
    └─→ Generates quality score
    └─→ Returns assessment
    ↓
Output: 
  - Fetched Story (from Jira)
  - Beautified Story
  - Quality Score
  - Detailed Assessment
```

**When to use:**
- When you want to fetch directly from Jira
- For automated workflow integration
- When using Jira as your single source of truth

**Workflow:**
1. Select "Jira Integration Mode"
2. Enter Jira Issue Key (e.g., PROJ-123)
3. Enter Jira API URL (if different from default)
4. Click "Fetch from Jira & Get Score"
5. View fetched story and score

---

## 🔄 Comparison: Mode 1 vs Mode 2

| Feature | Manual Input Mode | Jira Integration Mode |
|---------|------|------|
| **Steps Used** | 3 & 4 only (Beautify + Score) | 1, 2, 3 & 4 (Full flow) |
| **Input Source** | User pastes story manually | Jira API (Issue Key) |
| **Setup Required** | None | Jira API credentials |
| **Processing Time** | ~5-15 seconds | ~15-30 seconds |
| **Use Case** | Quick testing, testing mode | Production automation |
| **Workflow** | Manual copy-paste | Automated fetch |
| **Story Details** | User input only | Full Jira issue data |
| **Configuration** | No extra config needed | Jira URL + API Key needed |

---

## 📖 UI Sections Explained

### **Mode Selection (Always Visible)**
- Two prominent buttons to switch modes
- Shows which mode is currently active
- Describes each mode's purpose

### **Pro Tips Section (Mode-Specific)**
- **Manual Mode Tips:**
  - Enter or paste user story content manually
  - Groq beautifies and generates score
  - Copy results for documentation

- **Jira Mode Tips:**
  - Enter Jira issue key
  - Langflow fetches from Jira
  - Groq beautifies and scores
  - View full issue details

### **API Status (Always Visible)**
- "Test Connection" button
- Real-time connection status
- Works for both modes

### **Input Section (Mode-Specific)**

**Manual Input Mode:**
- Sample user story with "Use This Sample" button
- Text area for manual input
- "Get Score" button
- "Clear All" button

**Jira Integration Mode:**
- Jira Issue Key input field
- Jira API URL field
- "Fetch from Jira & Get Score" button
- "Clear All" button

### **Results Section (Both Modes)**
- Shows reviewed/fetched user story
- Quality assessment score card
- Score interpretation (Excellent/Good/Fair/Poor)
- Detailed assessment from Groq
- Copy buttons for all results

### **Debug Console (Always Visible)**
- Shows step-by-step processing
- Logs for troubleshooting
- Visible for both modes

---

## 🚀 Quick Start Guide

### **Manual Input Mode (Recommended for Testing)**

```
1. Open user-story-reviewer-ui.html in browser
2. Verify "✏️ Manual Input Mode" is selected
3. Click "Test Connection" to verify Langflow
4. Click "Use This Sample" to load example
5. Click "Get Score"
6. View score and assessment
7. Click "Copy" to save results
```

### **Jira Integration Mode**

```
1. Open user-story-reviewer-ui.html in browser
2. Click "🔗 Jira Integration Mode" button
3. Enter Jira Issue Key (e.g., PROJ-123)
4. Enter Jira API URL if different
5. Click "Test Connection"
6. Click "Fetch from Jira & Get Score"
7. View fetched story, score, and assessment
8. Click "Copy" to save results
```

---

## 🔑 Configuration for Jira Mode

### **Required:**
- **Jira Issue Key**: The ticket identifier (e.g., PROJ-123, SCRUM-45)
- **Jira API Base URL**: Your Jira instance URL (e.g., https://your-company.atlassian.net)

### **Optional:**
- **Jira API Authentication**: 
  - For cloud Jira: API token
  - For on-premise: Username/password or API token
  - Configure in Langflow Jira component

### **How Langflow Handles Jira:**
- The APIRequest component in Langflow calls Jira REST API
- Uses the issue key to fetch full issue details
- Extracts description, summary, and other fields
- Passes to Parser for structuring

---

## 💡 Usage Examples

### **Example 1: Manual Input - Quick Test**
```
User Story: "As a user, I want to log in with email and password 
            so I can access my account securely."

Mode: Manual Input
Button: Get Score
Result: Score 8.5/10 - Excellent Quality
```

### **Example 2: Jira Integration - Production Use**
```
Issue Key: PROJ-123
URL: https://mycompany.atlassian.net

Steps:
1. Langflow fetches PROJ-123 from Jira
2. Gets full issue data (summary, description, fields)
3. Beautifies the content
4. Generates score: 7.2/10
5. Provides detailed assessment
```

---

## 🔧 Debugging Tips

### **Manual Input Mode Issues:**
1. Click 🔧 Debug Console
2. Check if "Extracted Score" shows a number
3. Verify Langflow is running (Test Connection)
4. Check if score patterns are recognized

### **Jira Integration Mode Issues:**
1. Click 🔧 Debug Console
2. Look for "Fetch from Jira" messages
3. Check Jira API credentials in Langflow
4. Verify issue key is correct (uppercase)
5. Ensure Jira API URL is accessible

---

## 📊 Score Interpretation (Both Modes)

```
Score Range    | Level              | Status
80-100        | Excellent Quality  | ✓ Ready for Testing
60-79         | Good Quality       | ◐ Minor Improvements
40-59         | Fair Quality       | ◔ Significant Improvements
0-39          | Poor Quality       | ✗ Needs Major Revision
```

---

## 🔐 Security Considerations

### **Manual Input Mode:**
- No external API calls except to Langflow
- No sensitive data fetched
- Safe for testing

### **Jira Integration Mode:**
- Requires Jira API credentials (in Langflow)
- API tokens should be kept secure
- Recommend using environment variables in Langflow
- No credentials stored in UI

---

## 📝 Advanced Configuration

### **Custom Jira Fields:**
Edit Langflow's APIRequest component to fetch custom fields:
```
GET /rest/api/3/issues/{issueKey}?fields=customfield_12345
```

### **Multiple Jira Instances:**
Store Jira URLs in a config:
```javascript
const JIRA_INSTANCES = {
    'prod': 'https://prod.atlassian.net',
    'staging': 'https://staging.atlassian.net'
};
```

### **Score Thresholds:**
Modify score interpretation in `displayResults()`:
```javascript
if (score >= 85) { // Custom threshold
    scoreDetailsElement.textContent = 'Production Ready';
}
```

---

## 🎯 Next Steps

1. ✅ Choose your mode based on use case
2. ✅ Test connection
3. ✅ Try sample or enter data
4. ✅ Get score
5. ✅ Copy and use results
6. ✅ Refer to Advanced Response Parsing Guide if needed

---

## 📞 Quick Reference

| Need | Solution |
|------|----------|
| Quick test | Use Manual Input Mode + Sample |
| Production automation | Use Jira Integration Mode |
| Troubleshoot | Open Debug Console (🔧) |
| Test connection | Click "Test Connection" button |
| Clear data | Click "Clear All" button |
| Change mode | Click mode selection buttons |
| Save results | Click "Copy" buttons |

---

**Version**: 2.0 (Dual Mode Support)  
**Last Updated**: June 7, 2026  
**Status**: Production Ready  
