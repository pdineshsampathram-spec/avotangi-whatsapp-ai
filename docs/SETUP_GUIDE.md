# Setup Guide

This guide explains how to run the Avotangi WhatsApp AI Stylist workflow locally using n8n.

---

## ✅ Prerequisites

Before starting, make sure you have:

* n8n installed and running
* WhatsApp Business API access
* Google account for Sheets
* Google Gemini API key
* Internet access from your n8n instance

---

## 📥 Step 1 — Import the Workflow

1. Open your n8n dashboard
2. Click **Import from File**
3. Select `whatsapp_input_processor_safe.json`
4. Save the workflow

At this stage the workflow will load but will not run until credentials are configured.

---

## 🔐 Step 2 — Configure Credentials

You must create and attach the following credentials inside n8n:

### WhatsApp Business API

Used by:

* WhatsApp Trigger
* WhatsApp Send nodes

Make sure your webhook is properly configured in Meta.

---

### Google Sheets OAuth

Used for persistent memory storage.

Steps:

1. Create Google Sheets OAuth credential in n8n
2. Connect your Google account
3. Ensure the target sheet is accessible

---

### Google Gemini API

Used by the Intent Extractor node.

Steps:

1. Create Gemini credential in n8n
2. Paste your API key
3. Test the connection

---

## 🔁 Step 3 — Replace Placeholders

Open the workflow and replace the following values:

* `YOUR_GOOGLE_SHEET_ID`
* `YOUR_WHATSAPP_PHONE_ID`

These must match your actual environment.

---

## 📊 Step 4 — Prepare Google Sheet

Create a sheet with the following headers (exact spelling recommended):

* phone
* occasion
* style
* colors
* comfort_needs
* budget_hint
* last_updated

Ensure the sheet permissions allow your n8n credential to write.

---

## ▶️ Step 5 — Activate the Workflow

1. Turn the workflow **Active**
2. Send a test WhatsApp message
3. Monitor execution in n8n

You should see:

* intent extraction
* memory update
* product recommendations sent

---

## 🧪 Testing Tips

Try messages like:

* "I want comfortable daily shoes"
* "Looking for premium formal footwear"
* "Need lightweight travel shoes"

---

## ⚠️ Production Recommendations

Before real deployment, consider:

* hashing phone numbers
* adding error monitoring workflow
* implementing stronger rate limits
* moving memory from Sheets to a database

---

## 🆘 Troubleshooting

**Workflow not triggering**

* verify WhatsApp webhook
* check n8n is publicly reachable

**No recommendations sent**

* verify product API response
* check Gemini credential

**Google Sheets errors**

* verify OAuth connection
* check sheet permissions

---

**Maintained by Dinesh**
