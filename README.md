# 💸 Kharcha - Personal Expense Tracker

Kharcha is a lightweight, fast, and secure browser-based expense tracking application. Built entirely on the client side, it leverages a serverless architecture—utilizing GitHub Gists and Google Sheets—for seamless and secure data synchronization.

## ✨ Features
* **100% Client-Side:** No dedicated backend server or database is required. Simply open the HTML file in any browser to start tracking.
* **Dual Cloud Synchronization:** * *Primary Storage:* GitHub Gists (maintains application state in JSON format).
  * *Backup Storage:* Google Sheets (provides a structured, tabular view of your expense records).
* **Secure Authentication:** Protected by a custom 4-digit PIN.
* **Smart Credential Management:** API tokens and PIN hashes are securely stored in the browser's `localStorage`. No sensitive credentials are hardcoded in the repository.
* **Visual Insights:** Interactive charts powered by Chart.js provide category-wise and payment mode (Cash vs. Online) financial breakdowns.
* **Data Export:** One-click export functionality to download records as a CSV file.

## 🛠️ Tech Stack
* HTML5, CSS3, Vanilla JavaScript
* [Chart.js](https://www.chartjs.org/) (Data Visualization)
* GitHub REST API (Gists)
* Google Apps Script (Web App Backend)

## 🚀 Setup & Installation

To set up this application on a new device or browser, follow these steps:

### 1. Launch the Application
* Clone the repository and open `index.html` in your preferred web browser, or access it via your hosted GitHub Pages link.

### 2. Configure Your GitHub Token
* On the login screen, click the **"Set Token"** button.
* Paste your GitHub Personal Access Token (ensure it has `gist` permissions). This token will be securely saved in your browser's local storage.

### 3. Google Sheets Integration
* The `GS_WEBAPP_URL` and `GS_SYNC_KEY` are pre-configured in the source code. 
* Once your token is set, adding or syncing expenses will automatically back up your data to the designated Google Sheet.

## 🔒 Security Disclaimer
For security purposes, personal access tokens and PINs are strictly excluded from the source code. To reset your credentials, simply clear your browser's local storage data and reconfigure the token via the application interface.
