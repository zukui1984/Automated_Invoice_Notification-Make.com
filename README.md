# Automated Invoice Generation & Notification Workflow (Make.com)

## Overview
The scenario listens for incoming webhook data, enriches it via an external API, calculates tax variables, generates a formatted Google Docs invoice from a template, and automatically emails the final document to the client.

**Live Scenario Blueprint:** [Link Scenario](https://eu1.make.com/public/shared-scenario/uCKnuQXfAUe/b2-c-invoice-holiday-welcome-automation)

## Scenario Architecture
1. **Webhooks:** Triggers the scenario and receives payload data.
2. **HTTP:** Fetches regional data from a public API.
3. **Tools:** Calculates the VAT (Value Added Tax).
4. **Google Docs:** Populates an invoice template with the processed data.
5. **Gmail:** Emails the generated invoice to the customer.

---

## 🚀 Step-by-Step Implementation Guide

### Step 1: Configure the Webhook Trigger
1. Create a new scenario in Make.com.
2. Add the **Webhooks** module and select **Custom Webhook**.
3. Name the webhook: `Invoice Trigger`.
4. Copy the generated webhook URL.
5. To determine the data structure, send a test request to the webhook URL by appending the following query parameters in your browser - in this case https://hook.eu1.make.com/x5srk7lbgq2kvf8ysifr39et3bd2h6cq?**name=Test&price=100&state=BY&service=Consulting**: 
<img width="745" height="437" alt="image" src="https://github.com/user-attachments/assets/7e425bdd-5f87-4e0a-bee5-56fb664dab8a" />

6. The Make.com interface should display a green "Accepted" message, indicating the data structure was successfully determined.

<img width="745" height="172" alt="image" src="https://github.com/user-attachments/assets/39030875-5494-4d89-91b6-7a9eb8d14d03" />



