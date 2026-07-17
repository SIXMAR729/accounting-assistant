# 🚀 Release Notes: New Features & UI Improvements

## 🆕 New Features

### 1. Smart Categorization
The system automatically categorizes your expenses by scanning transaction keywords:
* **Food:** `coffee`, `pizza`, `restaurant`, `lunch`, `dinner`, `cafe`, `burger`
* **Transport:** `taxi`, `grab`, `uber`, `bus`, `train`, `fuel`, `parking`
* **Entertainment:** `movie`, `cinema`, `netflix`, `spotify`, `gaming`
* **Shopping:** `clothes`, `shoes`, `electronics`, `amazon`
* **Bills:** `electricity`, `water`, `internet`, `rent`, `insurance`
* **Health:** `pharmacy`, `medicine`, `doctor`, `hospital`

### 2. Visual Category Breakdown Bar
* **Color-Coded Bar:** Visual horizontal bar showing real-time spending distribution.
* **Detailed Legend:** Displays category names, exact amounts, and percentages.
* **Dynamic Updates:** Automatically updates based on your active filters.

### 3. Dark/Light Theme Toggle
* **Header Icon:** Quickly toggle themes by clicking the 🌙 / ☀️ icon.
* **Persistence:** Saves your preference across sessions using `localStorage`.
* **Smooth UI:** Features fluid visual transitions between modes.

### 4. CSV Export
* **One-Click Download:** Instant export of your entire receipt database.
* **Full Data Scope:** Includes date, vendor, category, total, and itemized lists.
* **Broad Compatibility:** Fully compatible with Microsoft Excel and Google Sheets.

### 5. Month Filter
* **Smart Dropdown:** Displays available months alongside active receipt counts.
* **Combined Search:** Works natively with the search bar for granular filtering.

### 6. Enhanced Stats
* **Monthly Tracking:** New "This Month" dedicated spending card.
* **Averages:** Displays the average spend calculated per receipt.
* **AI Integration:** Includes category breakdowns inside the AI summary response.

---

## 📊 UI Improvements

* **Category Badges:** Visual color-coding for quick scanning (e.g., `cat-food`, `cat-transport`).
* **Empty States:** Redesigned blank screens featuring helpful action icons.
* **Skeleton Loading:** Smoother perceived performance during data fetching.
* **Header Subtitle:** Dynamically displays the total receipt count.
* **Period Labels:** Automatically updates to reflect your active filters.
* **Keyboard Shortcut:** Press `Ctrl+K` or `Cmd+K` to instantly focus the search bar.
* **Mobile Grid:** Enhanced responsive layouts tailored for smaller screens.


# 📊 Edge AI Accounting Assistant

An intelligent, privacy-first accounting assistant skill designed for the Google Edge AI Gallery. 

This skill leverages on-device AI to process images of receipts and invoices, smoothly extracting critical financial data like vendors, line items, and totals. All extracted information is instantly stored in a high-speed, local SQLite database on your device, ensuring maximum privacy and offline availability.

## 🚀 Key Features

*   **🔒 100% Privacy by Design**: All document processing and storage happens directly on your device. Your sensitive financial data never leaves your phone or laptop.
*   **⚡ Local Edge AI**: Uses **Gemma-4-E4B-it** to reliably parse raw receipt images and unstructured user prompts into clean, structured JSON payloads.
*   **🗄️ Offline WASM Database**: Uses `sql-wasm.js` to run a lightning-fast embedded SQLite database directly within the application sandbox. No backend servers required!
*   **💬 Conversational Summaries**: Need to see your expenses? Just ask! Ask the assistant to "Summarize my expenses" or "Show my database" to get an instant view of all your tracked records.

## 🤔 How it Works

1.  **Input:** The user provides an image (receipt/invoice) or a text description of an expense to the assistant.
2.  **Extraction:** The Edge AI model analyzes the request, structuring the data into a strict JSON payload consisting of `vendor`, `total`, `date`, and line `items`.
3.  **Action Trigger:** The assistant parses the parsed JSON into `index.html` via the tool execution environment.
4.  **Local Storage:** The frontend scripts process the incoming JSON payload and commit the expense accurately to the underlying SQLite database inside `sql-wasm.js`.

## 🛠️ Tech Stack

*   **AI Model**: Gemma-4-E4B-it (Recommended)
*   **Agent Logic**: `SKILL.md` Instruction System
*   **Database**: `sql-wasm.js` (WebAssembly SQLite)
*   **Frontend**: HTML / Vanilla JS (for handling UI summaries & insertion logic)

## 📦 Usage

To run this skill, it should be natively imported into your compatible Google Edge AI environment. Ensure your runtime has access to the tool functions defined in `SKILL.md` (specifically the `run_js` tool handler).

### Sample AI Output format
When processing a receipt, the assistant will interface with the app using this structure:

```json
{
  "vendor": "Coffee Shop",
  "total": 5.50,
  "date": "2026-04-20",
  "items": [
    {
      "name": "Latte",
      "price": 4.50,
      "quantity": 1
    }
  ]
}
```

## 🔐 Notes on Data Security
Because this skill does not transmit your SQL database over any networks, the database is hidden inside the application sandbox of your operating system. It is physically hidden from user file explorers and external USB inputs to maximize security. Use the conversational summarization feature to display your saved database natively inside the App!
