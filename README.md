# 💸 Kharcha - Personal Expense Tracker

Ek simple, fast, aur secure browser-based expense tracker. Ye app purely frontend par chalta hai aur data ko securely save karne ke liye serverless architecture (GitHub Gists + Google Sheets) ka use karta hai.

## ✨ Features
* **100% Client-Side:** Koi dedicated database ya heavy backend server nahi. Bas HTML file open karo aur chalao.
* **Dual Cloud Sync:** * **Primary:** GitHub Gist (JSON format mein state maintain karne ke liye).
  * **Backup:** Google Sheets (Data ko table format mein neatly dekhne ke liye).
* **Secure Auth:** 4-digit PIN protection.
* **Smart Storage:** API tokens aur PIN safely browser ki `localStorage` mein store hote hain (code mein hardcoded nahi).
* **Visual Insights:** Chart.js ke through category-wise aur payment mode (Cash vs Online) ka breakdown.
* **Export:** One-click CSV download option.

## 🛠️ Tech Stack
* HTML, CSS, Vanilla JavaScript
* [Chart.js](https://www.chartjs.org/) (Data visualization ke liye)
* GitHub REST API (Gists)
* Google Apps Script (Web App backend)

## 🚀 Setup Instructions (New Device/Browser)

Kyunki ye ek personal tool hai, kisi naye phone ya laptop par ise setup karne ke liye bas ye steps follow karein:

### 1. App Open Karein
* Repository ko clone karein aur `index.html` ko kisi bhi browser mein open karein. (Ya isey GitHub Pages par host kar lein).

### 2. GitHub Token Set Karein
* App ki login screen par **"Set Token"** button par click karein.
* Apna GitHub Personal Access Token (`ghp_...`) paste karein. *(Dhyan rahe ki token ke paas 'gist' ki permission ho).*
* Token securely browser mein save ho jayega.

### 3. Google Sheets Backup
* Code mein `GS_WEBAPP_URL` aur `GS_SYNC_KEY` set hai. 
* Jaise hi aap token set karke koi naya kharcha add karenge ya "Sync" dabayenge, data automatically aapki connected Google Sheet mein chala jayega.

## 🔒 Security Note
Security reasons ki wajah se GitHub token ya PIN kabhi bhi source code mein hardcode nahi kiye gaye hain. Agar aap kabhi token reset karna chahein, toh browser ka local data clear karke dobara "Set Token" use kar sakte hain.
