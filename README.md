# Avotangi WhatsApp AI Stylist 🤖👞

An AI-powered WhatsApp consultation workflow built with **n8n** that helps luxury footwear brands like Avotangi deliver personalized product recommendations through chat.

Instead of browsing endlessly, customers can simply message on WhatsApp and receive curated footwear suggestions that match their needs and style.



## ✨ Project Overview

Modern D2C brands are moving toward conversational commerce. This project demonstrates how a simple WhatsApp conversation can be transformed into a guided, personalized shopping journey.

With this workflow, the system can:

* 📲 Understand customer intent from chat
* 🧠 Extract structured preferences using AI
* 💾 Remember returning users
* 🎯 Recommend the most relevant products
* 💬 Maintain a premium conversational tone

---

## 🔄 How the System Works

### High-Level Flow

1. User sends a WhatsApp message
2. n8n receives and normalizes the input
3. AI extracts preferences from the message
4. Preferences are stored in memory
5. Products are fetched from Shopify
6. Products are scored against user needs
7. Top recommendations are sent back
8. A follow-up message encourages engagement

---

## 🧩 Workflow Stages in Detail

### 1. WhatsApp Trigger

The workflow begins when a user sends a message on WhatsApp. The trigger captures the message and converts it into a consistent structure.

**Purpose:** ensure reliable downstream processing.

---

### 2. AI Intent Extraction

Google Gemini analyzes the user message and extracts structured preferences.

**Fields extracted:**

* occasion (daily, office, travel, festive, casual, formal)
* style (minimal, premium, bold, classic)
* comfort needs (comfortable, cushioned, soft, lightweight)
* colors mentioned
* budget hint (low, mid, premium)

**Example**

User message:

> I want comfortable shoes for daily office use

AI output:

```json
{
  "occasion": "daily",
  "style": "",
  "comfort_needs": "comfortable",
  "colors": [],
  "budget_hint": "mid"
}
```

---

### 3. Conversation State Update

The workflow cleans and normalizes extracted values and records the last interaction time.

**Purpose:** maintain consistent user context.

---

### 4. Persistent Memory (Google Sheets)

User preferences are stored so the system can recognize returning customers.

**Stored fields:**

* phone (identifier)
* occasion
* style
* colors
* comfort_needs
* budget_hint
* last_updated

✅ Enables basic personalization across sessions
⚠️ Production recommendation: hash phone numbers before storage

---

### 5. Product Retrieval

The workflow fetches live product data from the Avotangi Shopify store.

**Purpose:** ensure recommendations use the latest catalog.

---

### 6. Intelligent Product Scoring

Each product is evaluated against the user’s preferences.

**Scoring logic:**

* Occasion match → +3
* Style match → +2
* Comfort match → +2
* Vendor bonus → +1

Products are sorted by score and the top three are selected.

---

### 7. Luxury Recommendation Messaging

The system sends:

1. ✨ Curated intro message
2. 👞 Product images with captions
3. 🤍 Follow-up call to action

The tone is designed to feel premium and consultative rather than robotic.

---

## 🚀 Key Features

### Core capabilities

* WhatsApp conversational flow
* AI-powered preference extraction
* Memory-based personalization
* Automated product ranking
* Multi-message recommendation sequence
* Error-tolerant JSON parsing

### Advanced behavior

* Fallback when user intent is weak
* Conditional recommendation flow
* Batch product delivery
* Delay handling to avoid rate limits

---

## 🛠️ Technology Stack

**Automation**

* n8n

**AI**

* Google Gemini

**Messaging**

* WhatsApp Business API

**Commerce**

* Shopify product feed

**Memory**

* Google Sheets

---

## 📁 Repository Structure

```
.
├── whatsapp_input_processor_safe.json
└── README.md
```

---

## ⚙️ Setup Instructions

### Step 1: Import the Workflow

1. Open n8n
2. Import the JSON file from this repository
3. Save the workflow

---

### Step 2: Configure Credentials

You must provide your own credentials for:

* WhatsApp Business API
* Google Sheets
* Google Gemini

🔐 This repository intentionally does not include any secrets.

---

### Step 3: Replace Placeholders

Search and replace the following values in the workflow:

* YOUR_GOOGLE_SHEET_ID
* YOUR_WHATSAPP_PHONE_ID

---

### Step 4: Activate and Test

* Enable the workflow
* Configure the webhook in Meta
* Send a test WhatsApp message

---

## 🔐 Security and Privacy

**Current protections**

* Credentials removed before publishing
* No API keys in the repository
* Basic safe parsing implemented

**Recommended for production**

* Hash phone numbers before storage
* Restrict Google Sheet permissions
* Add monitoring and error alerts
* Implement stronger rate limiting

---

## 💼 Business Use Cases

**Luxury D2C brands**

* personalized product discovery
* WhatsApp concierge shopping
* clienteling automation

**E-commerce stores**

* guided selling
* preference capture
* repeat customer personalization

**Fashion and footwear brands**

* style-based recommendations
* occasion-based selling
* premium conversational experience

---

## 🧪 Example Conversation

**User**

> I need comfortable shoes for office use

**System behavior**

1. Extracts intent
2. Stores preferences
3. Scores products
4. Sends curated recommendations
5. Prompts for further refinement

---

## 🚧 Known Limitations

* Optimized mainly for text input
* Product scoring is rule-based
* Google Sheets is not ideal for very large scale
* Requires WhatsApp Business approval

---

## 🔮 Future Improvements

* vector-based product search
* RAG with product embeddings
* cart recovery automation
* multilingual support
* customer lifetime value tracking
* real-time inventory filtering

---

## 👨‍💻 Author

**Dinesh**

If this project helped you, consider giving the repository a star.

---

## 📜 License

This project is intended for educational and demonstration purposes. Replace credentials and implement proper data protection before using in production.
