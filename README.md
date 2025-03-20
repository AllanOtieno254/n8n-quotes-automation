# n8n Quotes Automation - Fetch & Process Motivational Quotes
![main workflow](https://github.com/user-attachments/assets/4e37ac04-1a3e-464c-be71-57fa42013d79)
[![n8n](https://img.shields.io/badge/n8n-Workflow-blue)](https://n8n.io/)
[![License](https://img.shields.io/github/license/AllanOtieno254/n8n-quotes-automation)](LICENSE)

🚀 **n8n Quotes Automation** is an automated workflow built with **n8n**, a low-code workflow automation tool. This project fetches motivational quotes from an API, processes them through different logic nodes, and extracts meaningful insights.

---

## 📌 Features

✅ Fetches 30 random motivational quotes from an API
✅ Splits the response into individual quote entries
✅ Filters quotes that contain the keyword **"life"**
✅ Picks a **random quote** from the filtered list
✅ Adds an **index number** to each quote for better structuring
✅ Supports testing & debugging through **n8n's execution logs**
✅ Works with **API credentials** to ensure secure data retrieval

---

## 📷 Workflow Overview

🔹 **Workflow Architecture**
![main workflow](https://github.com/user-attachments/assets/4e37ac04-1a3e-464c-be71-57fa42013d79)

## 🛠️ Required Tools

Before getting started, ensure you have the following installed:

- **n8n**: Automation platform → [Download n8n](https://n8n.io/)
- **Node.js**: Required for running n8n workflows → [Install Node.js](https://nodejs.org/)
- **Git**: For version control → [Install Git](https://git-scm.com/)

---

## 🚀 Setup & Installation

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/AllanOtieno254/n8n-quotes-automation.git
cd n8n-quotes-automation
```

### 2️⃣ Install n8n
```bash
npm install -g n8n
```

### 3️⃣ Import the Workflow
1. Open **n8n** by running:
   ```bash
   n8n start
   ```
2. Navigate to the `workflow` tab.
3. Click **Import** and upload `n8n-workflow.json`.

### 4️⃣ Run the Workflow
- Click **Test Workflow** to fetch quotes and process them.

---

## 🔄 Workflow Breakdown: Triggers & Nodes

### **1️⃣ HTTP Request Node** - Fetch Quotes from API
🔹 **Purpose**: This node sends an HTTP request to an external quotes API to retrieve random motivational quotes.

🔹 **API Used**: [qapi.vercel.app](https://qapi.vercel.app/api/quotes)

🔹 **Configuration**:
- **Method**: `GET`
- **URL**: `https://qapi.vercel.app/api/quotes`
- **Headers**: `{ "Content-Type": "application/json" }`
- **Expected Response**: JSON object containing 30 quotes

🔹 **Example API Response**:
```json
[
    { "quote": "Life is what happens when you're busy making other plans.", "author": "John Lennon" },
    { "quote": "The only way to do great work is to love what you do.", "author": "Steve Jobs" }
]
```

### **2️⃣ Split Out Node** - Split Quotes into Individual Items
🔹 **Purpose**: The **Split Out** node takes the JSON array of quotes and creates separate outputs for each quote.

🔹 **Configuration**:
- **Input Data**: JSON array from HTTP Request
- **Output Data**: Single quote per execution loop

🔹 **Example Transformation**:
| Input JSON  | Output JSON  |
|-------------|-------------|
| `[ { "quote": "Life is what happens...", "author": "John Lennon" }, { "quote": "Do what you love...", "author": "Steve Jobs" } ]` | `{ "quote": "Life is what happens...", "author": "John Lennon" }` (1st run), `{ "quote": "Do what you love...", "author": "Steve Jobs" }` (2nd run) |


### **3️⃣ Code Node** - Filter Quotes Containing the Word "Life"
🔹 **Purpose**: Filters out quotes that do not contain the word "life"

🔹 **JavaScript Code Used:**
```javascript
const keyword = "life";
const filteredQuotes = items.filter(item => item.json.quote.toLowerCase().includes(keyword));
return filteredQuotes;
```

🔹 **Expected Output**: Only quotes that include "life"

### **4️⃣ Code Node** - Pick a Random Quote
🔹 **Purpose**: Selects a random quote from the filtered list

🔹 **JavaScript Code Used:**
```javascript
const randomIndex = Math.floor(Math.random() * items.length);
return [items[randomIndex]];
```

🔹 **Expected Output**: A single randomly selected quote

### **5️⃣ Code Node** - Add Index Number to Quotes
🔹 **Purpose**: Assigns an index to each quote for better structuring

🔹 **JavaScript Code Used:**
```javascript
return items.map((item, index) => ({ json: { index: index + 1, ...item.json }}));
```

🔹 **Expected Output**:
```json
{
  "index": 1,
  "quote": "Life is what happens when you're busy making other plans.",
  "author": "John Lennon"
}
```

---

## 🔐 Setting Up API Credentials (If Required)
1. Go to **n8n Credentials** tab
2. Click **New Credential** → Select `HTTP Request`
3. **Authentication Type**: `None` (if public API) or `Bearer Token` (if required)
4. If authentication is needed:
   - **Token Type**: `Bearer`
   - **API Key**: `Your API Key Here`

---

## 🛠️ Troubleshooting

🔴 **Issue:** HTTP Request Fails ❌
✅ **Solution:** Check API URL, headers, and ensure the API is available.

🔴 **Issue:** No Quotes Appear ❌
✅ **Solution:** Ensure the API response is structured correctly and check filtering logic.

🔴 **Issue:** Workflow Crashes ❌
✅ **Solution:** Check logs in **n8n Execution History**.

---

## 🎯 Future Improvements
✅ Add support for multiple API sources  
✅ Integrate with Telegram bot for daily quote delivery  
✅ Store quotes in a database for long-term storage  

---

## 📜 License
This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing
Feel free to fork, modify, and contribute to this project. PRs are welcome! 🎉

---

## 📬 Contact

🔹 **GitHub:** [AllanOtieno254](https://github.com/AllanOtieno254)  
🔹 **LinkedIn:** [Allan Otieno Akumu](https://www.linkedin.com/in/allan-otieno-akumu/)  
🔹 **Twitter:** [@allan_codes](https://twitter.com/allan_codes)  

---

🔹 _Happy Automating! 🚀_

