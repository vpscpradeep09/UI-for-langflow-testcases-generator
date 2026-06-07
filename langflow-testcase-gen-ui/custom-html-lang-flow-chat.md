Context
You are an AI Assistant HELPING IN DEVELOPING A HTML UI
INSTRUCTIONS:
STEPS
1) [MANDATORY] 1) Create a fully functional single-page HTML UI for an AI-powered Testcase Generator
2) [MANDTORY]  Give the user friendly instructions on how to use the Testcase Generator but make it short and concise
3) [MANDATORY] Give an option to copy paste the sample user stories for banking domain
4) [MANDATORY] Implement clear option to clear the chat
5) [MANDATORY] Implement copy option to copy the chat output
6) [CRITICAL] Embed the Langflow chat interface for Testcase generation at top right with proper css styling and also proper alignment 
  <script src="https://cdn.jsdelivr.net/gh/langflow-ai/langflow-embedded-chat@main/dist/build/static/js/bundle.min.js"></script>
  with host_url,flow_id and API Key
    host_url="http://localhost:7860"
    flow_id="23500e26-476d-4508-b840-b6902a1d5e69"
7) [CRITICAL] Implement only Langflow chat without any settings showing the icon to open the chat
8) [MANDATORY] Add Proper scrolling options with scroll bars
9) [MANDATORY] Use blue and white as background theme



Example:
Sample Banking Domain User Stories to include:
1. As a customer, I want to transfer funds between my accounts so that I can manage my money efficiently.
2. As a customer, I want to view my transaction history for the last 90 days so that I can track my spending.

Output:
1)All HTML structure in one file
2)The Langflow chat widget script and embed configuration
3)No external dependencies except the Langflow CDN script

Additional information:
Below is the html file i used to connect for a simple chat conversation , you can take only details of CDN, Host and api key from below

<html>
  <head>
    <script src="https://cdn.jsdelivr.net/gh/langflow-ai/langflow-embedded-chat@main/dist/build/static/js/bundle.min.js"></script>
  </head>
  <body>
    <langflow-chat
      host_url="http://localhost:7860"
      flow_id="23500e26-476d-4508-b840-b6902a1d5e69"
      api_key="Enter Your API Key"
	window_title="Testcase Generator"
	placeholder='Give your input for generating testcases'
	start_open="true"
	chat_position='bottom-right'
	bot_message_style='{ "color": "#333", "backgroundColor": "#cc6699" }'
	placeholder_sending="Generating testcases"
	height=700
	width=450
	online_message='TC Bot is here to help you'
    ></langflow-chat>
  </body>
</html>