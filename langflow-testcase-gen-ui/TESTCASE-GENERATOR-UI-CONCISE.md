Context

You are an AI Assistant helping to develop an AI-Powered Test Case Generator UI with professional dark theme and direct Langflow API integration.

INSTRUCTIONS:

STEPS

1) [MANDATORY] Create a fully functional single-page HTML UI for an AI-powered Test Case Generator
2) [MANDATORY] Implement professional dark theme with semantic button colors (Blue for actions, Red for destructive, Green for success)
3) [MANDATORY] Create left sidebar with Quick Start instructions, Sample Banking Stories, and Pro Tips
4) [MANDATORY] Add API Key modal on page load for secure session-based authentication
5) [MANDATORY] Integrate direct Langflow REST API (POST to /api/v1/run/{flowId}) with proper error handling
6) [MANDATORY] Implement test case beautification with formatting for headers, numbered items, test IDs, and bullet points
7) [MANDATORY] Add chat interface with message display, input field, and Send button with loading states
8) [MANDATORY] Implement Copy Chat, Clear Chat, and Load Sample Stories buttons with user feedback
9) [MANDATORY] Add proper scrolling with visible scrollbars and auto-scroll to latest message
10) [MANDATORY] Implement responsive design for desktop (28%/72% split), tablet (45%/55%), and mobile (stacked)
11) [MANDATORY] Add Pro Tips section with 5 actionable tips for better test case generation
12) [MANDATORY] Use keyboard shortcuts: Enter in API field to start, Enter in chat to send message

Example:

Sample Banking Domain User Stories:

1. As a customer, I want to transfer funds between my accounts so that I can manage my money efficiently.
2. As a customer, I want to view my transaction history for the last 90 days so that I can track my spending.

Color Scheme:
- Use dark professional colors
- Use meaning colors for buttons
- Text: Light on dark backgrounds

Pro Tips Content:
- Be Specific: Add constraints like budgets or user roles for smarter test cases
- Include Edge Cases: Mention boundary conditions (zero amounts, max transfers)
- API & UI Tests: Specify if you need backend, frontend, or integration tests
- Test Scenarios: Ask for happy path, sad path, and error scenarios at once
- Reuse Outputs: Copy generated test cases and refine them iteratively

Output:

1) Single self-contained HTML file (testcase-generator-ui.html)
2) Direct Langflow API integration with X-API-Key authentication
3) Session-based API key storage (not persisted)
4) Beautifully formatted test case output with professional styling
5) Responsive design working across all devices
6) No external dependencies except Langflow backend API
7) Complete chat management with history and copy functionality

Configuration:

host_url: "http://localhost:7860"
flow_id: "23500e26-476d-4508-b840-b6902a1d5e69"
api_key: User-entered at runtime (minimum 10 characters)
api_endpoint: POST /api/v1/run/{flowId}

Payload Format:
{
  "input_value": "user message",
  "output_type": "chat",
  "input_type": "chat"
}

Key Functions:

- startWithApiKey() - Validate and store API key in session
- sendMessage() - Handle user input, call Langflow API, display response
- addMessage(message, sender) - Display message with beautification for bot responses
- beautifyTestCases(text) - Format test case output with HTML styling
- clearChat() - Clear history with confirmation dialog
- copyChat() - Format and copy chat history to clipboard
- loadSampleStories() - Load pre-populated banking user stories
- showFeedback(message, type) - Display toast notifications (success/error/warning)

Layout Structure:

Sidebar (28% width):
- Quick Start (4-step instructions)
- Sample Banking Stories (full user story format)
- Pro Tips (5 actionable tips)

Main Content (72% width):
- Header: Title with icon
- Chat Display: Scrollable message area with auto-scroll
- Chat Controls: Input field + Send button
- Action Buttons: Copy Output, Clear Chat, Load Sample Stories

Features Implemented:

✅ Professional dark theme with semantic colors
✅ API Key modal with show/hide toggle
✅ Beautifully formatted test case output
✅ Test case beautification with section headers, numbered items, test IDs
✅ Real-time message display with user/bot differentiation
✅ Copy to clipboard with feedback
✅ Clear chat with confirmation
✅ Load sample stories without confirmation
✅ Loading states and error handling
✅ Keyboard shortcuts (Enter to send/start)
✅ Toast notifications for all actions
✅ Responsive design (desktop/tablet/mobile)
✅ Session-only API key storage
✅ Auto-scroll to latest message
✅ Visible scrollbars

Deployment:

1. Save HTML file as testcase-generator-ui.html
2. Ensure Langflow running on http://localhost:7860
3. Flow ID 23500e26-476d-4508-b840-b6902a1d5e69 configured
4. Open HTML file in any modern browser
5. Enter Langflow API key when prompted
6. Start generating test cases

Browser Support: Chrome, Firefox, Safari, Edge (all versions)

Status: ✅ Production Ready - All features implemented and tested
