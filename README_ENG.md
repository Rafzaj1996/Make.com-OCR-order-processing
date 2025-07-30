# 🛠️ Order Processing Automation Workflow – Make.com

This project presents a complete automation workflow in Make.com, which is used to process orders in PDF format, extract customer and order data using Google Cloud Vision OCR and OpenAI API, then generate product codes based on the company’s internal data and add the orders to the CRM system.

---

## 📌 Purpose of the automation

To automate the handling of orders received in PDF format, eliminating the need for manual reading, data extraction, and order entry into the CRM system.

---

## 💡 Technologies and Integrations

| Tool        | Purpose                                 |
|------------------|----------------------------------------------|
| Make.com         | Main workflow platform                   |
| Webhook          | Receiving PDF files with orders                         |
| Google Cloud Vision API (OCR)         | PDF to text conversion                     |
| AirTable         | Order database                     |
| OpenAI API       | Analysis of order content, creation of product codes                       |
| CRM (PlentyMarket) | Adding orders to the system             |

---
## 🗂️ Workflow structure

The workflow consists of **8 main phases**, as outlined below:

---

### 1. 🔗 Webhook – Retrieving orders

- **Description:** The workflow starts with a Make webhook trigger that receives order data along with attached PDF files.
- **Actions:**
  - Receive data on new orders.
  - Iterate through each submitted order batch (if multiple are sent at once).

<img width="1030" height="133" alt="image" src="https://github.com/user-attachments/assets/f85e5c5e-4c08-4851-bf5a-b908c354a084" />


---

### 2. 📄 OCR – Converting PDF to text

- **Description:** Each attached order PDF is sent to the Google Cloud Vision API for text recognition.
- **Actions:**
  - Send PDFs as images to OCR.
  - Receive textual analysis output.

<img width="403" height="171" alt="image" src="https://github.com/user-attachments/assets/d3ab6e51-a081-471b-92eb-6beb79e8c917" />


---

### 3. 🧠 Data extraction – OpenAI API (GPT-4)

- **Description:** Using GPT-4, the order text is analyzed to extract customer data and order details.
- **Actions:**
  - Send processed text to OpenAI GPT-4 with a prompt that outputs a structured JSON.
  - Extracted data includes: customer name, contact info, products, quantities, packaging type, etc.
  - Save the result to Airtable.

<img width="1147" height="275" alt="image" src="https://github.com/user-attachments/assets/e59becd9-8a7f-4fb0-97ad-b2d83ec03591" />


---

### 4. 🧮 Product code generation

- **Description:** Based on the ordered products and data from the Airtable database, a unique code is generated for each product.
- **Actions:**
  - Match product names to internal codes.
  - Handle exceptions for custom or unusual products.

<img width="1251" height="104" alt="image" src="https://github.com/user-attachments/assets/976c8748-bc9e-4dfb-b75e-5c420e6d6426" />


---

### 5. ✅ Code validation

- **Description:** Verifies that each product has been assigned a correct code.
- **Actions:**
  - Check for any missing or mismatched codes.
  - Mark faulty orders for manual review.

<img width="327" height="617" alt="image" src="https://github.com/user-attachments/assets/487609bc-7763-43ea-8f59-125ab346f35a" /> <img width="294" height="624" alt="image" src="https://github.com/user-attachments/assets/4c458ef0-506a-4ae1-9db6-528cc0df2705" />


---

### 6. 📦 Quantity verification (units vs. packs)

- **Description:** Ensure the ordered quantity was correctly interpreted (whether the client provided number of units or packs).
- **Actions:**
  - Analyze unit of measure from the text.

---

### 7. ✍️ Airtable record update

- **Description:** After processing codes and quantities, data is updated in the Airtable database.
- **Actions:**
  - Fill in the record with: product codes, quantities.

<img width="1120" height="213" alt="image" src="https://github.com/user-attachments/assets/da009165-b50f-4ce1-bbf0-6e0ade05bd26" />


---

### 8. 📤 Order submission to CRM

- **Description:** The final step adds the complete order to the company’s CRM system.
- **Actions:**
  - Send the order data to the CRM API.
  - Receive confirmation and update the status in Airtable.

<img width="584" height="93" alt="image" src="https://github.com/user-attachments/assets/9e3168f0-2fdf-426e-ae6f-d836ed1641e0" />



---
## **Author**
Created by Rafał Zajkowski.
