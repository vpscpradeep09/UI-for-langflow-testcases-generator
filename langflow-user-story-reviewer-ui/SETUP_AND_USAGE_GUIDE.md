# User Story Reviewer UI - Setup & Usage Guide

## Overview
The **User Story Reviewer UI** is a web-based interface that integrates with Langflow to analyze and score user stories using AI-powered assessment. It provides quality ratings and detailed feedback for test case generation.

---

## 📋 Prerequisites

### 1. **Langflow Installation**
- Langflow must be running on `http://localhost:7860`
- [Install Langflow](https://docs.langflow.org/getting-started) if not already installed

### 2. **User Story Review Agent Flow**
- The flow must be imported into Langflow
- Flow ID: `3fca058a-15dd-43a1-8d4c-b5f576246de7`
- Import file: `User Story Review Agent_Langflow-export-File.json`

### 3. **API Credentials**
- API Key: `sk-l7XYkwdxkUmrTea_PvIcA0OwkCfb6AR3tEJ4WtiiIls`
- These are already configured in the HTML file

---

## 🚀 Getting Started

### Step 1: Open the HTML File
```bash
# Open the file in your browser
open user-story-reviewer-ui.html

# Or use your preferred browser
# File path: langflow-user-story-reviewer-ui/user-story-reviewer-ui.html
```

### Step 2: Test the Connection
1. Click the **"🔗 Test Connection"** button in the "API Status" section
2. If successful, you'll see: ✅ Connection Successful!
3. If failed, ensure Langflow is running on port 7860

### Step 3: Review Your First User Story
1. **Option A - Use Sample Story**: Click "Use This Sample" button
2. **Option B - Paste Your Own**: Paste a user story into the text area
3. Click **"Review & Score"** button
4. Wait for the API to analyze (typically 5-30 seconds)
5. View the results with quality score and detailed assessment

---

## 📊 Features Explained

### 1. **Pro Tips Section**
- Quick reference guide for using the tool
- Explains the workflow and how scoring works

### 2. **API Status**
- **Test Connection**: Verifies Langflow connectivity
- **Status Display**: Shows connection health
  - ✅ Connected and ready
  - ❌ Connection failed
  - ⚪ Not tested yet

### 3. **Sample User Story**
- Pre-loaded example for testing
- Click "Use This Sample" to populate the input field
- Great for understanding the scoring system

### 4. **Review User Story Section**
- **Input Field**: Paste or type user stories
- **Review & Score**: Analyzes the story and generates score
- **Clear All**: Resets all data and clears results

### 5. **Review Results Section**
- **Reviewed User Story**: Shows the input story with copy button
- **Quality Assessment Score**: Large, prominent score display
  - 80-100: Excellent Quality ✓
  - 60-79: Good Quality ◐
  - 40-59: Fair Quality ◔
  - 0-39: Needs Revision ✗
- **Detailed Assessment**: Full AI-generated review with copy button

### 6. **Copy Buttons**
- Each result section has a copy button
- Shows "✓ Copied!" confirmation when clicked
- Copies full text to clipboard

### 7. **Debug Console**
- **Toggle**: Click "🔧 Debug Console" to open/close
- **Shows**:
  - API request details
  - Response structure parsing
  - Score extraction process
  - Error messages with timestamps
- **Useful for**: Troubleshooting connection issues

---

## 🔧 API Integration Details

### Langflow API Endpoint
```
POST http://localhost:7860/api/v1/run/3fca058a-15dd-43a1-8d4c-b5f576246de7
```

### Request Format
```json
{
    "output_type": "text",
    "input_type": "text",
    "input_value": "Your user story here"
}
```

### Headers Required
```
Content-Type: application/json
x-api-key: sk-l7XYkwdxkUmrTea_PvIcA0OwkCfb6AR3tEJ4WtiiIls
```

### Response Structure (Typical)
```json
{
    "outputs": [
        {
            "outputs": [
                {
                    "results": {
                        "message": {
                            "text": "Quality Score: 8.5/10\nAssessment details..."
                        }
                    }
                }
            ]
        }
    ]
}
```

---

## 📈 How the Langflow Flow Works

The **User Story Review Agent** flow consists of:

1. **API Request Component** - Receives input from the UI
2. **Parser Component** - Extracts and structures the input data
3. **Groq Model (1st)** - Analyzes the user story for completeness and clarity
4. **Prompt Template** - Formats the analysis for final scoring
5. **Groq Model (2nd)** - Generates final quality score and feedback
6. **Text Output** - Returns the assessment to the UI

**Flow**: Input → Parse → Analyze → Format → Score → Output

---

## ✨ Best Practices

### User Stories to Test
1. **Simple Stories**:
   ```
   As a user, I want to log in with email and password so I can access my account.
   ```

2. **Complex Stories**:
   ```
   As a product manager, I want to generate automated test cases from user stories 
   so that the testing team can quickly create comprehensive test coverage without manual effort.
   ```

3. **Jira Stories**: Copy directly from Jira issue descriptions

### Tips for Best Results
- Use complete, well-structured user stories
- Include acceptance criteria for better scoring
- Stories with "As a", "I want", "so that" format score better
- Clear and specific requirements receive higher scores

---

## 🐛 Troubleshooting

### Issue: "Cannot connect to Langflow"
**Solution:**
1. Verify Langflow is running: `http://localhost:7860`
2. Check if port 7860 is not blocked by firewall
3. Try clicking "Test Connection" button
4. Check Debug Console for detailed error

### Issue: "CORS error"
**Solution:**
1. Update Langflow CORS settings
2. Or use a browser extension for CORS (development only)
3. Check Langflow documentation for CORS configuration

### Issue: No score extracted from response
**Solution:**
1. Open Debug Console (🔧 icon)
2. Check the raw response structure
3. Verify Langflow flow is working correctly
4. Test flow directly in Langflow UI

### Issue: API Key not recognized
**Solution:**
1. Verify API key in Langflow settings
2. Update API key in HTML if changed:
   ```javascript
   const API_KEY = 'your-new-key-here';
   ```
3. Ensure API key hasn't expired

---

## 📝 Customization

### Change API Endpoint
Edit the configuration in the HTML:
```javascript
const LANGFLOW_API = 'http://your-langflow-host:port/api/v1/run/FLOW_ID';
```

### Change API Key
```javascript
const API_KEY = 'your-api-key-here';
```

### Customize Sample Story
```javascript
const SAMPLE_STORY = `Your custom sample story here`;
```

### Modify Score Interpretation
Edit the `displayResults()` function score details:
```javascript
if (score >= 80) {
    scoreDetailsElement.textContent = '✓ Excellent Quality - Ready for Testing';
}
```

---

## 📱 Responsive Design

The UI is fully responsive and works on:
- ✅ Desktop browsers (Chrome, Firefox, Safari, Edge)
- ✅ Tablets (iPad, Android tablets)
- ✅ Mobile devices (Responsive layout)

---

## 🔐 Security Notes

1. **API Key Handling**: 
   - Currently in frontend (visible in source)
   - For production, move to backend with proxy

2. **Data Privacy**:
   - User stories sent to Langflow server
   - Ensure compliance with your data policies

3. **CORS Considerations**:
   - UI runs locally or on same domain as Langflow
   - Configure CORS properly for cross-origin requests

---

## 📞 Support & Additional Resources

### Related Files
- `User Story Review Agent_Langflow-export-File.json` - Flow definition
- `User Story Review Agent_Calling-langflow-from-postman.txt` - Postman example

### Documentation Links
- [Langflow Documentation](https://docs.langflow.org/)
- [Langflow API Reference](https://docs.langflow.org/api-reference)
- [Groq API Documentation](https://console.groq.com/docs)

---

## 🎯 Next Steps

1. ✅ Open the HTML file in your browser
2. ✅ Test the connection to Langflow
3. ✅ Try the sample user story
4. ✅ Paste your own user stories for review
5. ✅ Copy results for documentation
6. ✅ Use scores to prioritize test case generation

---

**Version**: 1.0  
**Last Updated**: June 7, 2026  
**Status**: Ready for Production  
