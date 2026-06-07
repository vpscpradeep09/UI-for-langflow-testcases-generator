# UI Layout Guide - Visual Reference

## 🎨 Application Layout Structure

### **Header Section (Always Visible)**
```
╔════════════════════════════════════════════════════════╗
║                 🚀 User Story Reviewer                 ║
║      AI-Powered Assessment for Test Case Generation    ║
╚════════════════════════════════════════════════════════╝
```

---

### **Mode Selection Section (Always Visible)**
```
┌────────────────────────────────────────────────────────┐
│ ⚙️ Operating Mode                                       │
├────────────────────────────────────────────────────────┤
│                                                         │
│ ┌──────────────────┐  ┌──────────────────┐           │
│ │ ✏️ Manual Input   │  │ 🔗 Jira Integ.   │           │
│ │ Skip Jira...     │  │ Fetch & process  │           │
│ │                  │  │                  │           │
│ │   [ACTIVE]       │  │   [INACTIVE]     │           │
│ └──────────────────┘  └──────────────────┘           │
│                                                         │
└────────────────────────────────────────────────────────┘
```

---

### **Pro Tips Section (Dynamic - Changes by Mode)**

#### **When Manual Input Mode is Active:**
```
┌────────────────────────────────────────────────────────┐
│ 💡 How It Works                                         │
├────────────────────────────────────────────────────────┤
│ ✓ Enter or paste user story content manually           │
│ ✓ Click "Get Score" to analyze with Groq AI            │
│ ✓ Groq beautifies and generates quality score          │
│ ✓ Copy results for further use or documentation        │
│ ✓ Use the Clear button to reset and start fresh        │
└────────────────────────────────────────────────────────┘
```

#### **When Jira Integration Mode is Active:**
```
┌────────────────────────────────────────────────────────┐
│ 💡 How It Works                                         │
├────────────────────────────────────────────────────────┤
│ ✓ Enter your Jira issue key (e.g., PROJ-123)          │
│ ✓ Click "Fetch from Jira & Get Score" button          │
│ ✓ Langflow fetches story from Jira                     │
│ ✓ Groq beautifies and generates quality score          │
│ ✓ View fetched story and score results                 │
└────────────────────────────────────────────────────────┘
```

---

### **API Status Section (Always Visible)**
```
┌────────────────────────────────────────────────────────┐
│ 🔗 API Status                                           │
├────────────────────────────────────────────────────────┤
│                                                         │
│ [Test Connection]  ⚪ Status: Not tested yet           │
│                                                         │
│ OR (after testing)                                     │
│                                                         │
│ [Test Connection]  ✅ Connection Successful!          │
│                                                         │
│ OR (if error)                                          │
│                                                         │
│ [Test Connection]  ❌ Connection Failed: ...          │
│                                                         │
└────────────────────────────────────────────────────────┘
```

---

## 📋 MANUAL INPUT MODE - Complete Layout

```
┌────────────────────────────────────────────────────────┐
│ 🚀 User Story Reviewer                                 │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ ⚙️ Operating Mode                                       │
│ [✏️ Manual Input (ACTIVE)] [🔗 Jira Integration]      │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ 💡 How It Works (Manual Mode Tips)                     │
│ ✓ Enter or paste user story content manually           │
│ ✓ Click "Get Score" to analyze with Groq AI            │
│ ✓ Groq beautifies and generates quality score          │
│ ✓ Copy results for further use or documentation        │
│ ✓ Use the Clear button to reset and start fresh        │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ 🔗 API Status                                           │
│ [Test Connection]  ✅ Connection Successful!           │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ Sample User Story                                       │
├────────────────────────────────────────────────────────┤
│ 📌 Example User Story                                  │
│                                                         │
│ As a user, I want to be able to log in with my email   │
│ and password so that I can access my account securely. │
│ The login form should validate empty fields and show   │
│ error messages for invalid credentials. After          │
│ successful login, I should be redirected to the        │
│ dashboard.                                             │
│                                                         │
│ [Use This Sample]                                      │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ Review User Story                                       │
├────────────────────────────────────────────────────────┤
│ 📝 Enter or Paste Your User Story                      │
│                                                         │
│ ┌──────────────────────────────────────────────────┐  │
│ │                                                  │  │
│ │  [User pastes their story here...]              │  │
│ │                                                  │  │
│ │                                                  │  │
│ └──────────────────────────────────────────────────┘  │
│                                                         │
│ [Get Score]  [Clear All]                              │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ Review Results                                          │
├────────────────────────────────────────────────────────┤
│                                                         │
│ ┌──────────────────────────────────────────────────┐  │
│ │ [Copy]  📖 Reviewed User Story                   │  │
│ │                                                  │  │
│ │ [User story text here...]                        │  │
│ │                                                  │  │
│ └──────────────────────────────────────────────────┘  │
│                                                         │
│ ╔══════════════════════════════════════════════════╗  │
│ ║   Quality Assessment Score                       ║  │
│ ║                  8.5                             ║  │
│ ║  ✓ Excellent Quality - Ready for Testing        ║  │
│ ╚══════════════════════════════════════════════════╝  │
│                                                         │
│ ┌──────────────────────────────────────────────────┐  │
│ │ [Copy]  📊 Detailed Assessment                   │  │
│ │                                                  │  │
│ │ [Assessment text from Groq here...]             │  │
│ │ [Score details...]                              │  │
│ │                                                  │  │
│ └──────────────────────────────────────────────────┘  │
│                                                         │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ 🔧 Debug Console                                        │
│ [Toggle]                                               │
│                                                         │
│ ┌──────────────────────────────────────────────────┐  │
│ │ [15:30:45] User Story:                           │  │
│ │ [15:30:45] As a user, I want to...              │  │
│ │ [15:30:45] Calling Langflow API...              │  │
│ │ [15:31:10] Raw Response: {...}                  │  │
│ │ [15:31:10] Found outputs array, length: 1       │  │
│ │ [15:31:10] Extracted Score: 85                  │  │
│ │ ✅ User story reviewed successfully!            │  │
│ └──────────────────────────────────────────────────┘  │
│                                                         │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ Powered by Langflow AI | User Story Review Agent v1.0  │
└────────────────────────────────────────────────────────┘
```

---

## 🔗 JIRA INTEGRATION MODE - Complete Layout

```
┌────────────────────────────────────────────────────────┐
│ 🚀 User Story Reviewer                                 │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ ⚙️ Operating Mode                                       │
│ [✏️ Manual Input] [🔗 Jira Integration (ACTIVE)]      │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ 💡 How It Works (Jira Mode Tips)                       │
│ ✓ Enter your Jira issue key (e.g., PROJ-123)          │
│ ✓ Click "Fetch from Jira & Get Score" button          │
│ ✓ Langflow fetches story from Jira                     │
│ ✓ Groq beautifies and generates quality score          │
│ ✓ View fetched story and score results                 │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ 🔗 API Status                                           │
│ [Test Connection]  ✅ Connection Successful!           │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ Fetch from Jira                                         │
├────────────────────────────────────────────────────────┤
│ 🔑 Jira Issue Key                                      │
│ ┌──────────────────────────────────────────────────┐  │
│ │ e.g., PROJ-123                                   │  │
│ │ [PROJ-123                              ]         │  │
│ │ 📌 Enter your Jira issue key                     │  │
│ └──────────────────────────────────────────────────┘  │
│                                                         │
│ 🔗 Jira API Base URL                                   │
│ ┌──────────────────────────────────────────────────┐  │
│ │ https://your-jira.atlassian.net                  │  │
│ │ [https://your-jira.atlassian.net        ]        │  │
│ │ 💡 Tip: This will be used to construct...       │  │
│ └──────────────────────────────────────────────────┘  │
│                                                         │
│ [Fetch from Jira & Get Score]  [Clear All]            │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ Jira Story Details                                      │
├────────────────────────────────────────────────────────┤
│ ┌──────────────────────────────────────────────────┐  │
│ │ [Copy]                                           │  │
│ │ 📋 Fetched from Jira                             │  │
│ │                                                  │  │
│ │ Issue Key: PROJ-123                              │  │
│ │                                                  │  │
│ │ Fetched from Jira API                            │  │
│ │                                                  │  │
│ │ [Full issue details from Jira...]               │  │
│ │ [Summary, description, fields...]               │  │
│ │                                                  │  │
│ └──────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ Review Results                                          │
├────────────────────────────────────────────────────────┤
│                                                         │
│ ┌──────────────────────────────────────────────────┐  │
│ │ [Copy]  📖 Reviewed User Story                   │  │
│ │                                                  │  │
│ │ [Fetched and beautified story from Jira...]     │  │
│ │                                                  │  │
│ └──────────────────────────────────────────────────┘  │
│                                                         │
│ ╔══════════════════════════════════════════════════╗  │
│ ║   Quality Assessment Score                       ║  │
│ ║                  8.5                             ║  │
│ ║  ✓ Excellent Quality - Ready for Testing        ║  │
│ ╚══════════════════════════════════════════════════╝  │
│                                                         │
│ ┌──────────────────────────────────────────────────┐  │
│ │ [Copy]  📊 Detailed Assessment                   │  │
│ │                                                  │  │
│ │ [Assessment from Groq Model...]                 │  │
│ │ [Score analysis and recommendations...]         │  │
│ │                                                  │  │
│ └──────────────────────────────────────────────────┘  │
│                                                         │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ 🔧 Debug Console                                        │
│ [Toggle]                                               │
│                                                         │
│ ┌──────────────────────────────────────────────────┐  │
│ │ [15:35:20] Jira Issue Key: PROJ-123             │  │
│ │ [15:35:20] Jira API Endpoint: https://...       │  │
│ │ [15:35:20] Calling Langflow full flow...        │  │
│ │ [15:35:40] Langflow Response received           │  │
│ │ [15:35:40] Found outputs array, length: 1       │  │
│ │ [15:35:40] Extracted Score: 85                  │  │
│ │ ✅ Jira story fetched and scored successfully!  │  │
│ └──────────────────────────────────────────────────┘  │
│                                                         │
└────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────┐
│ Powered by Langflow AI | User Story Review Agent v1.0  │
└────────────────────────────────────────────────────────┘
```

---

## 🎯 Key UI Elements

### **Active Mode Indicator**
```
When Manual Input Mode is active:
┌─────────────┐  ┌─────────────┐
│ ✏️ ACTIVE   │  │ 🔗 inactive │
│ (blue/pink) │  │ (gray)      │
└─────────────┘  └─────────────┘

When Jira Integration Mode is active:
┌─────────────┐  ┌─────────────┐
│ ✏️ inactive │  │ 🔗 ACTIVE   │
│ (gray)      │  │ (blue/pink) │
└─────────────┘  └─────────────┘
```

### **Score Card Display**
```
╔═════════════════════════════════════╗
║  Quality Assessment Score           ║
║              9.2                    ║
║  ✓ Excellent Quality               ║
║    Ready for Testing               ║
╚═════════════════════════════════════╝

Scores:
- 9.2 (displayed large)
- Status message (changes by score)
```

### **Results Display**
```
Manual Mode:
┌─────────────────────────────────────┐
│ [Copy] 📖 Reviewed User Story      │
│ [User input story text]             │
└─────────────────────────────────────┘

Jira Mode:
┌─────────────────────────────────────┐
│ [Copy] 📖 Reviewed User Story      │
│ Issue Key + Fetched Story + Details │
└─────────────────────────────────────┘
```

---

## 🎨 Color Scheme

```
Primary Gradient:    Purple to Pink (#667eea → #764ba2)
Secondary Gradient:  Pink to Red (#f093fb → #f5576c)
Success Green:       #10b981
Error Red:           #f5576c
Neutral Gray:        #f0f0f0, #ddd, #999

Backgrounds:
- Header:           Gradient (Purple-Pink)
- Alert Success:    Light green
- Alert Error:      Light red
- Debug Console:    Dark (#1e1e1e) with bright text
```

---

## 📱 Responsive Breakpoints

```
Desktop (> 768px):
- Full layout with side-by-side options
- Large buttons and text areas
- All sections visible

Tablet (768px):
- Stacked buttons
- Full-width inputs
- Touch-friendly sizing

Mobile (< 768px):
- Single column layout
- Stacked buttons
- Larger touch targets
- Readable font sizes
```

---

## ✨ Visual Feedback

```
Loading State:
[🔄 Loading...]  Button shows spinner

Success:
✅ Green checkmark + Message
✓ Copied! confirmation on copy buttons

Error:
❌ Red X + Error message
Connection failed indicators

Status:
⚪ Not tested
✅ Connected
❌ Failed
```

---

**This visual guide helps understand the complete UI layout for both operating modes!**
