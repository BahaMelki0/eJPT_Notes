
---

### Introduction to Web Application Security Testing

#### What Are Web Applications?

- Software programs accessed via web browsers and run on web servers.
    
- Interactive interfaces built with HTML, CSS, and JavaScript.
    
- Operate using a client-server model over HTTP/HTTPS.
    

#### Importance of Web App Security

- Protects sensitive user and business data.
    
- Prevents unauthorized access, data breaches, and financial loss.
    
- Helps meet compliance and regulatory requirements.
    
- Defends against DDoS, defacement, and tampering.
    

#### Security Practices

- Authentication & Authorization
    
- Input Validation & Output Encoding
    
- Secure Communication (TLS/SSL)
    
- Secure Coding Standards
    

---

### Web Application Security Testing

#### Definition

- Identifies vulnerabilities and weaknesses in web apps.
    
- Involves automated tools and manual testing.
    

#### Key Activities

- Vulnerability Scanning
    
- Manual Penetration Testing
    
- Code Review & Static Analysis
    
- Authentication & Authorization Testing
    
- Input Validation & Output Encoding Testing
    
- Session Management & API Security Testing
    

#### Pentesting vs Security Testing

- **Scope**: Pentest simulates real-world attacks; broader security testing includes best practices.
    
- **Objective**: Exploitation vs identification and mitigation.
    
- **Methodology**: Offensive vs defensive.
    

---

### Common Web App Threats & Risks

#### Definitions

- **Threat**: Potential harmful event.
    
- **Risk**: Likelihood a threat will exploit a vulnerability.
    

#### Examples

- Injection (SQL, Command, etc.)
    
- Cross-Site Scripting (XSS)
    
- Broken Authentication
    
- Sensitive Data Exposure
    
- Security Misconfiguration
    
- Insecure Deserialization
    
- Insufficient Logging and Monitoring
    

---

### Web Application Architecture & Components

#### Web App Architecture

- Defines the structure of client and server components.
    
- Supports scalability, maintainability, and security.
    

#### Client-Side Processing

- Runs in the user’s browser.
    
- Built with JavaScript, HTML, CSS.
    
- Handles UI rendering and input validation.
    

#### Server-Side Processing

- Handles data storage, business logic, and security.
    
- Uses languages like PHP, Python, Node.js, Java, etc.
    

#### Communication

- HTTP/HTTPS protocols used to transfer data.
    

---

### Web Application Technologies

#### Part I - Stack Overview

- **Client-Side**: HTML, CSS, JS, Cookies, Local Storage.
    
- **Server-Side**: Web Servers (Apache, Nginx), Application Servers, Databases.
    

#### Part II - Data Interchange & Security

- **Data Interchange**: JSON, XML, REST, SOAP.
    
- **Security**: Authentication, Authorization, SSL/TLS.
    
- **External Tools**: CDNs, Libraries, Frameworks (React, jQuery, etc.)
    

---

### HTTP/S Protocol Fundamentals

#### HTTP Basics

- Stateless application-layer protocol over TCP.
    
- Versions: HTTP/1.0 and HTTP/1.1.
    

#### HTTP Requests

- Components: Method, URL, Headers, and Body.
    
- Common Methods: GET, POST, PUT, DELETE, PATCH, OPTIONS.
    
- Headers: `User-Agent`, `Host`, `Cookie`, `Authorization`, etc.
    

#### HTTP Responses

- Status Codes: 200 (OK), 404 (Not Found), 500 (Server Error), etc.
    
- Headers: `Content-Type`, `Set-Cookie`, `Cache-Control`.
    

#### HTTPS

- Secure HTTP using SSL/TLS.
    
- Encrypts data in transit.
    
- Defends against eavesdropping and MITM attacks.
    

---

### Website Crawling & Spidering

#### Definitions

- **Crawling**: Navigating through all accessible links and forms to build a site map.
    
- **Spidering**: Automated discovery of new resources and links.
    

#### Tools

- **Burp Suite**: Professional version supports spidering.
    
- **OWASP ZAP**: Open-source alternative with crawling capabilities.
    

#### Notes

- Spidering can be noisy; configure with caution.
    
- Passive crawling avoids sending data-modifying requests.
    

---
