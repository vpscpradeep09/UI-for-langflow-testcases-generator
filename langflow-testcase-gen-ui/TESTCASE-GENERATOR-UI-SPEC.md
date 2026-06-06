# AI-Powered Test Case Generator UI - Complete Specification

## Context

You are creating a fully functional single-page HTML UI for an AI-powered Test Case Generator that integrates with Langflow backend API. This application allows users to input user stories and automatically generate comprehensive test cases using artificial intelligence.

**Target Users:** QA Engineers, Test Analysts, Product Managers  
**Domain Focus:** Banking and Financial Services  
**Technology Stack:** Vanilla HTML5, CSS3, JavaScript (No frameworks)  
**API:** Langflow REST API (Direct integration, not embedded widget)

---

## Project Requirements

### [MANDATORY] Core Features

1. **Fully Functional Single-Page HTML UI**
   - All code in one self-contained HTML file
   - No external npm dependencies
   - No build tools required
   - Open and run directly in browser

2. **User-Friendly Instructions**
   - Short and concise (4 quick steps)
   - Positioned in left sidebar
   - Guide users through the process quickly

3. **Sample Banking User Stories**
   - Pre-populated stories for testing
   - Full user story format (As a customer, I want...)
   - Load via "Load Sample Stories" button
   - Stories:
     1. As a customer, I want to transfer funds between my accounts so that I can manage my money efficiently.
     2. As a customer, I want to view my transaction history for the last 90 days so that I can track my spending.

4. **Clear Chat Option**
   - Button to clear all chat history
   - Confirmation dialog to prevent accidental clearing
   - Shows only once user clicks "Clear Chat"

5. **Copy Chat Output**
   - Copy all generated test cases to clipboard
   - Formatted output with [USER]/[BOT] labels
   - "Copied to clipboard" feedback message

6. **Proper Scrolling**
   - Scrollbars visible on chat display area
   - Auto-scroll to latest message
   - Responsive scrolling on all screen sizes

### [CRITICAL] API Integration

- **Technology:** Direct Langflow REST API (not embedded widget)
- **Host URL:** `http://localhost:7860`
- **Flow ID:** `23500e26-476d-4508-b840-b6902a1d5e69`
- **API Endpoint:** `/api/v1/run/{flowId}`
- **Authentication:** X-API-Key header
- **Request Method:** POST with JSON payload
- **Request Format:**
  ```json
  {
    "input_value": "user message",
    "output_type": "chat",
    "input_type": "chat"
  }
  ```
- **Response Parsing:** Handle nested Langflow response structure

### [CRITICAL] Security

- **API Key Entry Modal**
  - Modal appears on page load
  - User enters API key before accessing chat
  - Minimum 10 character validation
  - Toggle to show/hide API key
  - Session-only storage (not persisted)

- **Credential Handling**
  - API key stored in LANGFLOW_CONFIG object during session
  - Not stored in HTML file
  - Not saved to local storage
  - Session clears on page reload

---

## UI Design Specifications

### Color Theme: Professional Dark Mode

**Primary Backgrounds:**
- Body: Dark gradient (#0f172a → #1a1f3a)
- Sidebar: #1a1f3a → #16213e
- Chat Display: #1a1f3a
- Input Fields: #1e293b

**Text Colors:**
- Primary Text: #e2e8f0
- Secondary Text: #cbd5e0
- Muted Text: #94a3b8

**Semantic Button Colors:**
- Primary Action (Send, Copy): Blue (#3b82f6)
- Destructive (Clear): Red (#ef4444)
- Success (Load Samples): Green (#10b981)

**Message Styling:**
- User Messages: Blue background (#3b82f6), white text
- Bot Messages: Dark background (#1e293b), light text with blue left border

**Accents:**
- Focus States: Bright blue (#3b82f6)
- Borders: Subtle light rgba(255,255,255,0.1)
- Hover States: Slightly lighter shade

### Layout & Responsive Design

**Desktop (28% / 72% split):**
- Sidebar: 28% width with fixed positioning
- Main Content: 72% width
- Header: Sticky with title and icon
- Chat Area: Scrollable message display
- Controls: Input field + Send button
- Action Buttons: Copy, Clear, Load Sample (fixed at bottom)

**Tablet (45% / 55% split):**
- Sidebar: 45% max height, scrollable
- Main Content: 55% height
- Reduced padding and font sizes

**Mobile (100% stacked):**
- Sidebar: Full width, scrollable section
- Main Content: Full width below sidebar
- Compact button sizes
- Reduced spacing

---

## Features Implemented Throughout Development

### 1. Chat Interface
- Real-time message display with user/bot differentiation
- Empty state message when no conversations
- Auto-scroll to latest message
- Smooth animations and transitions

### 2. Test Case Beautification
- Automatic formatting of AI-generated test cases
- Section headers highlighted in blue
- Numbered items with subtle backgrounds
- Test IDs (TC1, TC2) highlighted in green
- Bullet points with visual hierarchy
- Clean, readable spacing

### 3. Pro Tips Section (Sidebar Enhancement)
- 5 actionable tips for better test case generation:
  1. Be Specific: Add constraints for smarter cases
  2. Include Edge Cases: Mention boundary conditions
  3. API & UI Tests: Specify test layer requirements
  4. Test Scenarios: Ask for multiple path types
  5. Reuse Outputs: Refine iteratively

### 4. User Feedback System
- Toast notifications for all actions
- 3-second auto-dismiss
- Types: Success (Green), Warning (Orange), Error (Red)
- Smooth slide-in animation

### 5. Loading States
- "Sending..." button state during API calls
- Input field disabled during processing
- Prevents duplicate submissions
- Error handling with user-friendly messages

### 6. Keyboard Shortcuts
- Enter key in API input: Start session
- Enter key in chat input: Send message

---

## Example Usage Workflow

1. **User Opens Application**
   - Modal appears requesting API key
   - User enters Langflow API key (minimum 10 characters)
   - Click "Start" button
   - Success message shown

2. **User Generates Test Cases - Option A (Manual Input)**
   - Type user story: "As a customer, I want to..."
   - Press Enter or click Send
   - Chat displays user message in blue
   - AI generates test cases
   - Bot message displayed with beautified formatting
   - Success toast shown

3. **User Generates Test Cases - Option B (Sample Stories)**
   - Click "Load Sample Stories" button
   - Pre-loaded banking user stories displayed
   - User modifies or uses as-is
   - Press Send
   - AI generates test cases for banking scenarios

4. **User Copies Output**
   - Click "Copy Output" button
   - Formatted text copied: [USER] message / [BOT] response
   - "Copied to clipboard" notification shown
   - User can paste into documents/tickets

5. **User Clears Chat**
   - Click "Clear Chat" button
   - Confirmation dialog appears
   - User clicks OK to confirm
   - Chat history cleared
   - Empty state message shown
   - Success notification displayed

---

## Sample Banking Domain User Stories

**Story 1: Fund Transfer**
```
As a customer, I want to transfer funds between my accounts 
so that I can manage my money efficiently.

Expected Test Cases:
- Positive: Successful transfer with valid amounts
- Negative: Transfer with insufficient funds
- Edge Cases: Zero amount, maximum transfer limit
- Acceptance Criteria: Confirmation email sent
```

**Story 2: Transaction History**
```
As a customer, I want to view my transaction history 
for the last 90 days so that I can track my spending.

Expected Test Cases:
- Positive: Display accurate transactions
- Negative: No transactions in period
- Edge Cases: 90 day boundary, timezone handling
- Acceptance Criteria: Searchable and sortable results
```

---

## Technical Architecture

### File Structure
```
testcase-generator-ui.html (Single file, all-in-one)
├── HTML Structure
│   ├── API Key Modal
│   ├── Sidebar (Instructions, Tips, Sample Stories)
│   └── Main Content (Header, Chat, Controls, Buttons)
├── CSS Styling
│   ├── Dark theme variables
│   ├── Responsive media queries
│   └── Component styles
└── JavaScript
    ├── API Configuration
    ├── Message Handling
    ├── Langflow Integration
    └── UI State Management
```

### Key JavaScript Functions

**API & Configuration:**
- `LANGFLOW_CONFIG` - Global API configuration object
- `callLangflowAPI(message)` - POST request to Langflow

**Authentication:**
- `startWithApiKey()` - Validate and store API key
- `toggleApiKeyVisibility()` - Show/hide password field
- `changeApiKey()` - Re-open API key modal

**Chat Management:**
- `addMessage(message, sender)` - Display message with beautification
- `sendMessage()` - Handle user input and API call
- `clearChat()` - Clear history with confirmation
- `copyChat()` - Format and copy to clipboard
- `loadSampleStories()` - Load pre-populated stories

**UI Helpers:**
- `beautifyTestCases(text)` - Format test case output
- `updateSendButtonState(disabled)` - Manage button state
- `showFeedback(message, type)` - Show toast notifications

---

## Deployment Instructions

1. **Save the HTML file**
   - Save as: `testcase-generator-ui.html`
   - Location: Any accessible directory

2. **Ensure Langflow Backend Running**
   - Langflow server running on `http://localhost:7860`
   - Flow ID `23500e26-476d-4508-b840-b6902a1d5e69` configured
   - Valid API key generated

3. **Open in Browser**
   - Double-click the HTML file, or
   - Drag to browser window, or
   - Open via browser File > Open menu

4. **First Use**
   - Enter Langflow API key when prompted
   - Click "Start" button
   - Begin generating test cases

---

## Browser Compatibility

- Chrome/Edge: ✅ Full support
- Firefox: ✅ Full support
- Safari: ✅ Full support
- Mobile Browsers: ✅ Full responsive support

---

## Performance Considerations

- Single HTML file (no round trips)
- No external dependencies (instant load)
- CSS animations use GPU acceleration
- Responsive images and layouts
- Efficient DOM manipulation
- Session-based storage (no persistence overhead)

---

## Future Enhancement Ideas

- Export test cases as PDF/Excel
- Integration with test management tools (Jira, TestRail)
- Multiple test case templates
- Batch generation for multiple stories
- Test case versioning and history
- Customizable test case format
- Collaborative editing with team members

---

## Regeneration Notes

To regenerate this exact UI, follow these steps in order:

1. Create single HTML file with all code
2. Implement dark professional theme first
3. Add sidebar with Quick Start section
4. Add Sample Banking Stories (full format)
5. Integrate direct Langflow API (not widget)
6. Add API Key modal with session storage
7. Implement test case beautification
8. Add Pro Tips section to sidebar
9. Add all feedback/toast notifications
10. Implement keyboard shortcuts
11. Test responsive design across devices
12. Verify all features work end-to-end

---

## Notes

- This specification captures the complete journey from initial requirements to final implementation
- All design decisions made favor user experience and professional appearance
- Security prioritized through session-only API key storage
- Test case beautification improves readability significantly
- Dark theme reduces eye strain during extended use
- Responsive design ensures usability across all devices

---

**Last Updated:** 2026-06-06  
**Version:** 1.0 - Production Ready  
**Status:** ✅ Complete and Functional
