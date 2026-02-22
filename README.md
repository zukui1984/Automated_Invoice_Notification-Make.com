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

7. The result looks like this

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/b42853be-fa1c-4106-9494-8a0c212a95af" />


### Step 2: Fetch Regional Data via HTTP
1. Add a new module: **HTTP -> Make a request**.
2. Configure the module to fetch data from the German public holiday API:
3. Authentication Type: No authentication
4. URL: `https://feiertage-api.de/api/`
5. Method: **GET**
6. Query String:
   - Name: `nur_land`
   - Value: Map the state variable (e.g., BY) from the Webhook module using drag-and-drop.
7. Run the module to ensure it executes successfully (turns green).

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/2748bdc8-bb53-46d6-ad15-217d9a302e25" />

<img width="500" height="700" alt="image" src="https://github.com/user-attachments/assets/5bbf24ec-b9b2-4099-863f-38b38073f01a" />

### Step 3: Calculate VAT (Tools Module)
1. Add a new module: **Tools -> Set variable** (or Get variable depending on your flow).
2. Configure the calculation:
   - Variable name: `vat_amount`
   - Variable value: Drag the price variable from the Webhook module and multiply it by 19% VAT.
   - Formula: `{{price}} * 0.19`
3. Execute the module to verify the calculation outputs correctly.

## Tools 
<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/c51e197c-950f-46dd-bf1a-907d5b857b39" />

<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/971fc51b-2fdb-4a97-bac7-76b356be0451" />

### Step 4: Generate the Google Docs Invoice
1. Create a new Google Doc to serve as your template and insert the following text with placeholders:
```text
RECHNUNG

Kunde: {{customer_name}}
Datum: {{now}}
Leistung: {{service_name}}
Preis (Netto): {{price}} EUR
MwSt (19%): {{vat_amount}} EUR
Gesamtbetrag: {{total}} EUR

Vielen Dank für Ihren Auftrag!
```

### Google Docs screenshot
<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/99030e20-3838-44bb-97a3-6bf7b5f7893e" />

2. Back in Make.com, add the **Google Docs -> Create a document** from a template module.
3. Connect your Google account, select the template file you just created, and map the variables from the previous modules (Webhook and Tools) to the corresponding placeholders in the document.

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/139b5220-1f9c-4576-afbc-a4329be3e92a" />

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/5b16884f-3c47-449a-9cfa-3e02e52b0a22" />

4. Execute the module to generate a test document.

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/47b03e99-02d9-4c8e-a9b1-a12f617cf473" />


