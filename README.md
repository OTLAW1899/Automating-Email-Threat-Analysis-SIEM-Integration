# Automating Email Threat Analysis & SIEM Integration  

## Overview  
This project demonstrates a **cybersecurity automation workflow** that processes and analyzes email messages from a live Gmail mailbox. Since **email is the most common attack vector**, the project provides a critical defense mechanism by automatically detecting threats and integrating results with a **Security Information and Event Management (SIEM)** platform (Splunk).  

The automation uses **Python** to:  
- Monitor an inbox (Inbox & Spam) via IMAP  
- Parse and analyze suspicious emails  
- Extract and scan URLs & attachments with **VirusTotal**  
- Forward structured results to **Splunk** for centralized monitoring  

---

## Project Components  

### 1. Email Access (Gmail)  
- Uses **IMAP** to retrieve emails  
- Requires enabling IMAP in Gmail settings  
- Authentication via **Google App Passwords** (not primary password)  

### 2. Threat Intelligence (VirusTotal)  
- Email attachments & URLs are hashed/scanned with the **VirusTotal API**  

### 3. SIEM Integration (Splunk)  
- Uses **HTTP Event Collector (HEC)** to send event data securely  
- Configurable endpoint, token, and port (default `8088`)  

---

## Project Structure  

```
├── send_email.py    # Script to send simulated phishing emails
├── main.py         # Script to monitor inbox, analyze threats, forward to Splunk
├── .env.example             # Example environment variables
├── requirements.txt         # Python dependencies
└── README.md                # Project documentation
```

---

## Environment Configuration  

Sensitive credentials are stored in a `.env` file:  

```bash
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_generated_app_password
VT_API_KEY=your_virustotal_api_key
SPLUNK_TOKEN=your_splunk_hec_token
SPLUNK_URL=https://yoursplunkserver:8088
```

---

## Scripts  

### 1. **Phishing Email Simulation (`send_email.py`)**  
- Sends **10 simulated phishing-style emails** (1 per minute)  
- Useful for **training & testing** detection workflows  

**Features:**  
- Fake phishing subject lines & links (safe for training)  
- Secure Gmail SMTP authentication with App Passwords  
- Configurable sender & recipient  

---

### 2. **Email Monitoring & Threat Analysis (`main.py`)**  
- Connects to Gmail via **IMAP**  
- Monitors both **Inbox** and **Spam**  
- Extracts links & attachments → scans with **VirusTotal**  
- Sends structured results to **Splunk HEC**  

**Workflow:**  
1. Load credentials & API keys from `.env`  
2. Retrieve unread emails  
3. Parse headers, body, attachments, links  
4. Scan URLs/attachments with VirusTotal  
5. Forward results to Splunk for analysis  
6. Repeat every **4 minutes**  

---

## Security & Operational Notes  
- Gmail requires IMAP + App Passwords  
- VirusTotal has **API rate limits** → adjust script accordingly  
- Splunk HEC must be enabled and reachable  
- Processed emails are tracked to prevent re-analysis  

---

## Use Case  
By combining both scripts:  
- **Script 1** generates phishing-style test data  
- **Script 2** detects, analyzes, and reports threats to Splunk  

This setup is valuable for:  
- **Security Awareness Training**  
- **SIEM Integration Testing**  
- **Threat Detection Development**  

---

## Installation  

1. Clone the repository:  
   ```bash
   git clone https://github.com/yourusername/email-threat-automation.git
   cd email-threat-automation
   ```

2. Install dependencies:  
   ```bash
   pip install -r requirements.txt
   ```

3. Create a `.env` file from the example and add your credentials.  

4. Run phishing simulator (optional, for test data):  
   ```bash
   python send_email.py
   ```

5. Start email monitoring & Splunk integration:  
   ```bash
   python main.py
   ```

---

## Splunk Dashboard  
- **Incoming Email Logs**: Date, sender, subject, and body preview  
- **Threat Indicators**: URLs flagged by VirusTotal  
- **Attachment Analysis**: Malicious file detection stats  
- **Real-Time Alerts**: Automated correlation with other Splunk data sources  
---
## Future Enhancements
AI/NLP-powered email intent analysis
Sandbox for dynamic attachment execution
YARA-based signature detection
Multi-SIEM support (ELK, QRadar, Sentinel)
Docker deployment for scalability
---
## Conclusion  
This project provides a **hands-on blueprint** for building an email security automation pipeline with **Python, VirusTotal, and Splunk**. It demonstrates how organizations can proactively defend against **email-borne cyber threats** through automation, structured analysis, and centralized SIEM monitoring.  

---
Acknowledgments
VirusTotal API
Splunk HEC
Streamlit

---
## Author  
**Olatunji Lawal**  
*Cybersecurity Analyst*  

📅 *15th August 2025* 
