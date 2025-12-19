# n8n AI Finance
Workflow on n8n for AI personal finance tracker
AI WhatsApp Finance Tracker
A self-hosted, automated personal finance assistant that runs entirely on n8n.

This bot allows you to track expenses by sending photos of receipts or text messages to a WhatsApp number. It uses AI to parse receipt data, categorizes expenses, and logs everything into a Google Sheet that is automatically created and formatted for you.

✨ Features
📸 Receipt Scanning: Send a photo of a receipt. The bot uses OCR and AI (Google Gemma via OpenRouter) to extract the date, merchant, line items, and total cost.

🧠 Intelligent Categorization: Automatically categorizes items (e.g., Food, Transport, Household) without manual input.

📊 Automatic Google Sheets Dashboard:

Logs every transaction in real-time.

Auto-generates a "Dashboard" with formulas, a Pie Chart (Breakdown), and a Column Chart (Trends).

Creates a "Budget_Limits" sheet to track spending caps.

💰 Budget Management: Set limits via chat commands (e.g., "Budget Food 500").

📈 Instant Reporting: Type "Report" to get a visual graph and text summary of your current month's spending vs. your budget.

🔐 Secure & Private: Self-hosted on n8n. Your data lives in your own Google Drive.

🛠️ Tech Stack
Workflow Engine: n8n

Messaging: WhatsApp Business API (Meta)

Database/Storage: Google Sheets (Data) & Local JSON file (User Auth)

AI/LLM: Google Gemma 2 (via OpenRouter)

OCR: OCR.Space

Visualization: QuickChart.io

🚀 Prerequisites
To run this workflow, you need the following API keys and accounts:

Google Cloud Console: Enable Sheets API & Drive API. Create OAuth Credentails.

Meta for Developers: Create a System User and get a WhatsApp Access Token.

OCR.Space: Free API key for text extraction.

OpenRouter: API key for LLM processing.

n8n: A self-hosted instance (Docker recommended) or n8n Cloud.

⚙️ Installation & Setup
1. Environment Variables
This project relies on environment variables for security. Add the following to your n8n .env file or environment configuration:

Bash

# --- Google OAuth ---
GOOGLE_CLIENT_ID="your_google_client_id"
GOOGLE_CLIENT_SECRET_MAIN="your_google_client_secret"
GOOGLE_REDIRECT_URI="https://your-n8n-instance.com/webhook/google-callback"

# --- Services ---
OCR_SPACE_API_KEY="your_ocr_key"

# --- WhatsApp ---
WHATSAPP_PHONE_ID="your_whatsapp_phone_id"
2. Import Workflows
Import the two JSON files into your n8n instance:

Main WhatsApp Workflow.json: Handles incoming messages, AI logic, and reporting.

System_Google_Callback.json: Handles the OAuth authentication flow and creates the initial Spreadsheet.

3. Google OAuth Setup
In Google Cloud Console, add your GOOGLE_REDIRECT_URI to the "Authorized Redirect URIs".

Ensure the URI ends with /webhook/google-callback.

📱 Usage Guide
Once running, send a message to your WhatsApp bot number:

1. Initialization
Start: Send any message (e.g., "Hi").

Auth: The bot will detect you are a new user and send a Google Authentication link. Click it to authorize the bot to create your "YOUR AI TRACKER" spreadsheet.

2. Commands
Scan Receipt: Simply upload a photo.

The bot will reply with a breakdown and update the sheet.

Set Budget: Send a text like:

Budget Food 500

Budget Transport 200

Check Status: Send text:

Report (Generates a chart and summary)

Help: Send text:

Menu

📂 File Structure
Transactions Sheet: Raw log of all items extracted from receipts.

Budget_Limits Sheet: Stores the limits you set via chat.

Dashboard Sheet: Auto-generated pivot tables and charts for visualization.

🛡️ Security Note
This project uses Environment Variables to store sensitive keys. Never hardcode your API keys inside the workflow nodes if you plan to share or commit your JSON files.

Created with ❤️ using n8n.
