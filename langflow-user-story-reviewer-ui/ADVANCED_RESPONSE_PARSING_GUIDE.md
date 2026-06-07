# Advanced API Response Parsing Guide

## Understanding Langflow Response Structure

This document explains how the User Story Reviewer UI parses Langflow API responses and extracts scoring information.

---

## 📊 Response Format Analysis

### Standard Langflow Response Structure

```json
{
    "outputs": [
        {
            "outputs": [
                {
                    "results": {
                        "message": {
                            "text": "Quality Score: 8.5/10\n\nAssessment..."
                        }
                    }
                }
            ]
        }
    ]
}
```

### Response Parsing Flow

```
Raw Response (JSON)
    ↓
Extract outputs[0]
    ↓
Extract outputs[0].outputs[0]
    ↓
Try multiple text extraction paths:
  - results.message.text
  - results.text
  - message.text
  - Plain string
    ↓
Extract Score from Text
    ↓
Display Results
```

---

## 🔍 Score Extraction Patterns

The UI supports multiple score formats. The following patterns are tried in order:

### Pattern 1: Score with Context
```
Score: 8.5/10
Score: 8.5 out of 10
Score: 8.5
```
**Regex**: `/score[\s:]*(\d+(?:\.\d+)?)\s*(?:out of|\/|%)?[\s]*(?:10)?/i`

### Pattern 2: Rating Format
```
Rating: 8.5
Overall Rating: 8.5
```
**Regex**: `/rating[\s:]*(\d+(?:\.\d+)?)/i`

### Pattern 3: Out of Format
```
8.5 out of 10
8.5/10
```
**Regex**: `/(\d+(?:\.\d+)?)\s*(?:out of|\/)\s*10/i`

### Pattern 4: Percentage Format
```
85%
```
**Regex**: `/(\d+(?:\.\d+)?)%/`

### Pattern 5: Quality Score
```
Quality Score: 8.5
Test Score: 8.5
Assessment: 8.5
```
**Regex**: `/quality\s*score[\s:]*(\d+(?:\.\d+)?)/i`

### Pattern 6: Context-based
```
Score is 8.5
Quality is 8.5
Rating is 8.5
```
**Regex**: `/(?:score|rating|quality)[\s]*(?:is|:)[\s]*(\d+(?:\.\d+)?)/i`

---

## 🔄 Score Normalization

All scores are normalized to a 0-100 scale:

```javascript
// If score is 0-10, multiply by 10
if (score <= 10) {
    score = (score / 10) * 100;
}

// Clamp between 0-100
score = Math.min(Math.max(score, 0), 100);
```

**Examples:**
- Input: 8.5 → Output: 85
- Input: 85 → Output: 85
- Input: 0.85 → Output: 8.5
- Input: 95.5 → Output: 95.5

---

## 📝 Example Responses & Parsing

### Example 1: Standard Response

**Raw Response:**
```json
{
    "outputs": [
        {
            "outputs": [
                {
                    "results": {
                        "message": {
                            "text": "User Story Analysis:\n\nScore: 8.5/10\n\nAssessment:\n- Clear user role (As a user)\n- Well-defined action\n- Clear business value\n- Good acceptance criteria"
                        }
                    }
                }
            ]
        }
    ]
}
```

**Parsing Steps:**
1. ✅ Access outputs[0] - exists
2. ✅ Access outputs[0].outputs[0] - exists
3. ✅ Extract from results.message.text - found
4. ✅ Search for score pattern - found "8.5"
5. ✅ Normalize: 8.5 → 85
6. ✅ Extract assessment text

**Result:**
- Score: 85/100
- Assessment: Full text displayed

### Example 2: Alternative Structure

**Raw Response:**
```json
{
    "outputs": [
        {
            "message": {
                "text": "Rating: 9.2 - Excellent user story with clear objectives"
            }
        }
    ]
}
```

**Parsing Steps:**
1. ✅ Access outputs[0] - exists
2. ❌ Access outputs[0].outputs[0] - doesn't exist
3. ✅ Try output.message.text - found
4. ✅ Search for score pattern - found "9.2"
5. ✅ Normalize: 9.2 → 92
6. ✅ Extract assessment text

**Result:**
- Score: 92/100
- Assessment: Full text displayed

### Example 3: Simple Text Response

**Raw Response:**
```json
{
    "outputs": [
        "Quality Score: 7.8/10\n\nThis user story is well-structured..."
    ]
}
```

**Parsing Steps:**
1. ✅ Access outputs[0] - exists (string)
2. ❌ No nested outputs
3. ✅ Use string directly as assessment
4. ✅ Search for score pattern - found "7.8"
5. ✅ Normalize: 7.8 → 78
6. ✅ Extract assessment text

**Result:**
- Score: 78/100
- Assessment: Full text displayed

---

## 🐛 Common Response Issues & Solutions

### Issue 1: Score Not Extracted

**Problem:**
```
Assessment text found: "The user story score is good"
No numeric score detected
```

**Debug:**
1. Open Debug Console (🔧)
2. Look for "Extracted Score: 0"
3. Check raw response for score format
4. Add custom pattern if needed

**Solution:**
If your Langflow flow outputs scores differently, add a custom regex pattern:

```javascript
// In the extractScoreFromText function, add:
const customPattern = /your_custom_pattern[\s:]*(\d+(?:\.\d+)?)/i;
const match = text.match(customPattern);
if (match) {
    return parseFloat(match[1]);
}
```

### Issue 2: Duplicate Extraction

**Problem:**
```
Text: "Initial score: 5, Final score: 8.5"
Extracted: 5 (first match)
```

**Expected:**
```
Extracted: 85 (final score)
```

**Solution:**
Use regex that captures the most relevant score:
```javascript
// Prefer "Final score" or "Overall score"
/(?:final|overall|assessment)\s*score[\s:]*(\d+(?:\.\d+)?)/i
```

### Issue 3: Percentage vs. Decimal

**Problem:**
```
Input: "85" (already 0-100 scale)
Normalized: 850 (incorrect)
```

**Current Fix:**
```javascript
// Only multiply if score is 0-10
if (score <= 10) {
    score = (score / 10) * 100;
}
```

---

## 🧪 Testing Different Response Formats

### Using Debug Console

1. Open Debug Console (🔧)
2. Check log entries for:
   - "Found outputs array, length: X"
   - "Found text in results.message.text" (or alternative path)
   - "Extracted Score: X"

### Example Debug Output

```
[15:30:45] User Story:
[15:30:45] As a user, I want to log in...
[15:30:45] Calling API: http://localhost:7860/api/v1/run/3fca058a...
[15:30:45] Payload: {"output_type":"text",...}
[15:31:10] Raw Response: {"outputs":[...]...
[15:31:10] Found outputs array, length: 1
[15:31:10] Found inner outputs, length: 1
[15:31:10] Found text in results.message.text
[15:31:10] Extracted Score: 85
[15:31:10] Assessment (first 150 chars): Quality Score: 8.5/10...
✅ User story reviewed successfully!
```

---

## 🔧 Customizing Response Parsing

### If Langflow Flow Changes

If you modify the Langflow flow and it returns a different structure:

**Step 1:** Test with Postman first
```bash
curl -X POST 'http://localhost:7860/api/v1/run/3fca058a-15dd-43a1-8d4c-b5f576246de7' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: sk-l7XYkwdxkUmrTea_PvIcA0OwkCfb6AR3tEJ4WtiiIls' \
  -d '{"output_type":"text","input_type":"text","input_value":"test story"}'
```

**Step 2:** Copy the response

**Step 3:** Add debug to HTML:
```javascript
// In reviewUserStory() function
console.log('Full response:', JSON.stringify(data, null, 2));
```

**Step 4:** Update parsing logic based on actual structure

### Example: Custom Response Path

```javascript
// If response is: { data: { assessment: "...", score: 8.5 } }
if (data.data?.assessment) {
    assessment = data.data.assessment;
}
if (data.data?.score) {
    parsedScore = (data.data.score / 10) * 100;
}
```

---

## 📊 Score Interpretation

### Quality Levels

| Score Range | Level | Interpretation | Emoji |
|------------|-------|-----------------|-------|
| 80-100 | Excellent | Ready for testing, no revisions needed | ✓ |
| 60-79 | Good | Minor improvements recommended | ◐ |
| 40-59 | Fair | Significant improvements needed | ◔ |
| 0-39 | Poor | Needs major revision | ✗ |

### What Affects Score

**High Scores (80+):**
- Clear role definition ("As a ...")
- Specific action ("want to ...")
- Clear business value ("so that ...")
- Complete acceptance criteria
- No ambiguity
- Testable and measurable

**Low Scores (0-39):**
- Vague role definition
- Unclear actions
- Missing business value
- No acceptance criteria
- Ambiguous requirements
- Not testable

---

## 🚀 Performance Considerations

### Response Processing Time
- **API Call**: 5-30 seconds (depends on Langflow server)
- **Response Parsing**: < 100ms
- **UI Update**: < 50ms

### Large Response Handling
```javascript
// Debug console limits output to first 200 chars
const preview = JSON.stringify(data).substring(0, 200);
```

If Langflow returns very large responses:
```javascript
// Sample from the middle instead of beginning
const mid = Math.floor(JSON.stringify(data).length / 2);
const sample = JSON.stringify(data).substring(mid, mid + 200);
```

---

## 📚 Additional Resources

### Response Structure Debugging
1. Use browser DevTools (F12)
2. Network tab → Find Langflow API call
3. Preview or Response tab → See full JSON
4. Copy response and format with JSONFormatter

### Postman for Testing
1. Import Postman collection
2. Modify request payload
3. Send and inspect response
4. Copy working response to test parsing

---

## 🔗 Related Documentation

- Main Setup Guide: `SETUP_AND_USAGE_GUIDE.md`
- Langflow Docs: https://docs.langflow.org/api-reference
- Flow Definition: `User Story Review Agent_Langflow-export-File.json`

---

**Version**: 1.0  
**Last Updated**: June 7, 2026  
