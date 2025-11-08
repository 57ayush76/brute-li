# 🔍 Brute-LI Scanner

**Advanced Endpoint Discovery Tool for Security Researchers & Web Penetration Testers**

A powerful **Playwright-based** reconnaissance tool that discovers hidden URLs, API endpoints, and internal resources through dynamic JavaScript analysis and intelligent status code detection.

---

## 🎯 Purpose

Brute-LI Scanner is designed for **authorized security testing**, bug bounty hunting, and penetration testing to:

- 🕵️ **Discover hidden endpoints** that aren't visible in static HTML
- 🔓 **Identify API routes** and internal microservices
- 📄 **Uncover configuration files** (JSON, XML, .env, etc.)
- 🔗 **Map internal architecture** and subdomain variations
- 📊 **Enumerate all reachable resources** within a target domain

---

## ⚡ Key Features

### **Dynamic JavaScript Execution**
- Executes JavaScript in real browser context (Chromium)
- Captures URLs from dynamically loaded content
- Monitors DOM mutations for injected scripts using MutationObserver
- Detects single-page application (SPA) routes

### **Smart Endpoint Discovery**
Finds URLs embedded in:
- HTML source code
- Inline JavaScript
- External JavaScript files (with recursive fetching)
- API responses and JSON data
- Dynamically injected scripts
- Shadow DOM elements

### **Intelligent Status Detection**
- **Accurate HTTP status codes** from real page navigation
- **Content-aware 403 detection** - distinguishes between actual blocks and accessible pages
- **Real response body analysis** - no guessing with headers alone
- **Smart error handling** with proper timeout and retry logic

### **Security-Focused Features**
- 🔐 **Header rotation** - Random User-Agent and Accept-* headers per request
- 🛡️ **WAF-aware scanning** - Polite delays between requests to avoid triggering WAF rules
- 🌐 **Domain filtering** - Automatically filters results to target domain only
- 📊 **Deduplication** - Maintains persistent list to avoid re-testing
- ⏱️ **Configurable timeouts** - Fine-tune scanning behavior

### **Penetration Tester Friendly**
- 🎨 **Color-coded output** - Quick visual scanning of results
  - 🟢 **Green (200-299)**: Accessible resources
  - 🟡 **Yellow (300-399 & 403 with content)**: Redirects & potentially accessible pages
  - 🔴 **Red (403 blocks & errors)**: Blocked resources
  - 🟣 **Magenta (404)**: Not found
  - 🔵 **Cyan (other)**: Other status codes
- 📁 **Persistent output** - Saves results to `urls.txt` with automatic deduplication
- 📈 **Content-length reporting** - Shows actual response size for each URL
- ⏱️ **Configurable Timeouts** - Adjust scanning duration and request delays

---

## 🛠️ How It Works

### Phase 1: JavaScript Scraping
- Launches headless Chromium
- Enables hidden/disabled elements via JavaScript injection
- Extracts URLs from HTML, scripts, and dynamically loaded content
- Monitors for new scripts injected by JavaScript (MutationObserver)
- Resolves relative URLs to absolute URLs
- Filters results to target domain only

### Phase 2: URL Status Checking
- Creates a fresh page for each URL (real browser navigation)
- Captures actual HTTP response status codes
- Retrieves full response body for accurate content length
- Smart 403 detection (content > 5000 bytes = likely accessible)
- Displays results in real-time with color coding

## 📦 Requirements

- Python 3.7+
- Playwright (with Chromium)
- requests
- tldextract
- colorama

## 🚀 Installation

### **Prerequisites**
- Python 3.7 or higher
- pip package manager

### **Setup**
```bash
# Clone the repository
git clone https://github.com/57ayush76/brute-li.git
cd brute-li

# Install dependencies
pip install -r requirements.txt

# Install Playwright browsers
playwright install chromium

# Run the tool
python3 brute-li.py

# Enter target URL when prompted
Enter URL to scan: https://example.com

