# Burp Suite - Summary

## Burp Suite - Web Application Penetration Testing

**Burp Suite** is a Java-based framework for web application penetration testing. It's the industry standard tool for testing web apps, mobile apps, and APIs.

## Core Functionality

Burp Suite acts as a proxy that captures and manipulates HTTP/HTTPS traffic between your browser and web servers. This allows you to intercept, view, and modify requests/responses in real-time for security testing.

## Burp Suite Editions

### Community Edition (Free)

- **Burp Proxy:** Intercept and inspect traffic
- **Burp Repeater:** Manually modify and resend requests
- **Burp Intruder:** Automated attacks (rate-limited)
- **Burp Decoder:** Encode/decode data
- **Burp Comparer:** Compare data
- **Burp Sequencer:** Analyze token randomness

### Professional Edition (Licensed)

Additional features over Community:

- **Automated vulnerability scanner**
- **Unlimited fuzzer/brute-forcer** (no rate limits)
- **Save projects** and generate reports
- **Built-in API** for tool integration
- **Unrestricted extensions** from BApp Store
- **Burp Collaborator:** Request catcher service

### Enterprise Edition (Licensed)

Server-based continuous scanning solution:

- **Automated periodic scanning** (runs on server, not local machine)
- **CI/CD integration** for DevSecOps workflows
- **Multiple concurrent scans** with scalability
- **Role-based access control** for teams

## Quick Setup

Default proxy: **127.0.0.1:8080**

Configure your browser to use this proxy, then intercept and test traffic.

## Burp Suite Key Features

**Proxy**

Intercepts and modifies HTTP/HTTPS traffic in real-time.

**Repeater**

Captures and resends requests multiple times. Useful for testing payloads and vulnerabilities (SQLi, XSS).

**Intruder**

Automates requests for brute-forcing and fuzzing. Rate-limited in Community Edition.

**Decoder**

Encodes/decodes data (Base64, URL, hex, etc.).

**Comparer**

Compares two pieces of data to spot differences in responses.

**Sequencer**

Tests randomness of tokens (session cookies, CSRF tokens) to identify weak generation.

## Extensions

**BApp Store:** Marketplace for third-party extensions (Java, Python, Ruby).

**Example:** Logger++ for enhanced logging.

Load extensions via the **Extender** module.

## Burp Suite - Getting Started

**Launch & Setup**

1. Accept terms and conditions
2. Select project type (click **Next** in Community Edition)
3. Keep default configuration
4. Click **Start Burp**

## Burp Dashboard

The dashboard has four quadrants:

**Tasks (Top Left)**

Background tasks Burp Suite performs. Default "Live Passive Crawl" automatically logs visited pages.

**Event Log (Top Right)**

Shows actions performed by Burp (proxy start, connections made, etc.).

**Issue Activity (Bottom Left)**

Professional only. Displays vulnerabilities found by automated scanner, ranked by severity.

**Advisory (Bottom Right)**

Professional only. Detailed vulnerability information with references and remediations. Can export to reports.

## Help Icons

**Question mark icons (?)** throughout Burp Suite open context-specific help windows. Use them for clarification on features.

## Training

First launch may show training options - highly recommended to complete when available.

## Burp Proxy

**Core Function**

Intercepts HTTP/HTTPS requests and responses between your browser and the target server. Allows you to view, modify, drop, or forward traffic before it reaches its destination.

**Key Features**

**Intercept Control**

Click **"Intercept is on"** button to toggle interception on/off. When off, traffic passes through but is still logged.

**HTTP History**

All requests/responses are automatically logged in the **HTTP history** tab, even with interception disabled. Useful for reviewing past traffic.

**WebSocket Support**

Captures and logs WebSocket communication in the **WebSockets history** tab.

**Proxy Settings**

Access via **Proxy settings** button:

- **Response Interception:** Enable rules to intercept server responses (off by default)
- **Match and Replace:** Use regex to automatically modify requests/responses (e.g., change User-Agent, manipulate cookies)

**Quick Actions**

From intercepted requests you can:
- **Forward:** Send to destination
- **Drop:** Discard the request
- **Send to Repeater/Intruder:** Further testing
- **Edit:** Modify before forwarding

## Burp Target Tab

The Target tab helps map and scope your testing targets. Contains three sub-tabs:

**Site Map**

Automatically maps visited pages in a tree structure while proxy is active. Shows:
- All browsed pages and endpoints
- API endpoints accessed by the web app
- Hierarchical structure of the application

**Professional:** Includes automated crawling functionality.

**Issue Definitions**

Complete list of web vulnerabilities that Burp Scanner looks for, including:
- Detailed descriptions of each vulnerability
- References and documentation
- Useful for reports and vulnerability research

**Note:** Scanning feature requires Professional edition, but definitions are available in Community.

**Scope Settings**

Controls which targets Burp intercepts and logs:
- **Include in scope:** Add specific domains/IPs to test
- **Exclude from scope:** Remove domains/IPs from testing
- Prevents capturing unnecessary traffic
- Focuses testing on intended targets

**Best Practice:** Define scope early to avoid cluttered logs and focus on relevant traffic.

## Burp Suite - Scoping

**Why Use Scoping?**

Prevents overwhelming traffic logs by focusing only on specific target applications.

**How to Set Scope**

1. Go to **Target** tab
2. Right-click target from the site map
3. Select **"Add To Scope"**
4. Click **"Yes"** when prompted to stop logging out-of-scope traffic

**Verify Scope**

Check the **Scope settings** sub-tab in Target to view included/excluded domains and IPs.

**Stop Intercepting Out-of-Scope Traffic**

By default, the proxy still intercepts everything even with scope set.

**To fix:**
1. Go to **Proxy settings** sub-tab
2. Find **"Intercept Client Requests"** section
3. Enable **"And URL Is in target scope"**

This ensures Burp completely ignores out-of-scope traffic for cleaner logs and focused testing.

**Best Practice**

Set scope early in your testing to avoid cluttered logs and maintain focus on intended targets.
