### Introduction to Security Auditing

**Overview:**  
Security auditing is a systematic process for evaluating and verifying an organization’s security measures and controls to ensure they are effective, appropriate, and compliant with relevant policies and regulations. This process involves reviewing the organization’s information systems, networks, applications, and operational procedures to identify vulnerabilities, weaknesses, and improvement opportunities.

**Key Benefits:**  
Security audits help in identifying vulnerabilities, ensuring regulatory compliance, enhancing risk management, refining security policies and procedures, supporting business objectives, and promoting continuous improvement.

**Auditing Lifecycle:**

1. **Planning and Preparation:** Define audit goals, scope, and the systems/processes to be reviewed; gather documentation; establish the audit team and schedule.
2. **Information Gathering:** Review policies, conduct interviews, and collect technical details.
3. **Risk Assessment:** Identify assets and threats, evaluate vulnerabilities, and determine risk levels.
4. **Audit Execution:** Perform technical tests, verify compliance, and evaluate controls.
5. **Analysis and Evaluation:** Analyze findings, compare them against standards, and prioritize issues.
6. **Reporting:** Document findings, offer recommendations, and present the results.
7. **Remediation:** Develop and implement remediation plans, conduct follow-up audits, and continuously monitor improvements.


**Types of Security Audits:**  
Security audits can be categorized by scope, methodology, and organizational focus.  

**Security Auditing & Penetration Testing:**  
While security audits assess controls and overall security posture, penetration testing focuses on actively exploiting vulnerabilities. Common practice is to perform a security audit first and then conduct a penetration test, though both can be integrated into a combined approach.  

---

### Governance, Risk, and Compliance (GRC)

**GRC Overview:**

- **Governance:** Involves the framework of policies, procedures, and practices ensuring that an organization meets its objectives, manages risks, and complies with laws—emphasizing policy development, defined roles, and accountability.
- **Risk Management:** Focuses on identifying, assessing, and mitigating risks that could impact assets and operations.
- **Compliance:** Ensures adherence to applicable laws, regulations, and industry standards through internal policies, audits, and assessments.

**Standards, Frameworks & Guidelines:**

- **Frameworks** (e.g., [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework), COBIT) provide a high-level roadmap for risk management.
- **Standards** (e.g., [ISO/IEC 27001](https://www.iso.org/isoiec-27001-information-security.html), [PCI DSS](https://www.pcisecuritystandards.org/), HIPAA, GDPR) set formal, measurable security requirements.
- **Guidelines** (e.g., [OWASP Top 10](https://owasp.org/www-project-top-ten), CIS Controls, NIST SP 800-53) offer actionable, non-mandatory recommendations.  
    Combining these approaches helps organizations build a robust cybersecurity posture that aligns strategic risk management with compliance needs.

---

### From Auditing to Penetration Testing

1. **Develop a Security Policy:**  
    Establish a security policy by gathering requirements (e.g., purpose, access control, audit and accountability, configuration management, identification, and authentication). An example of a comprehensive policy can be found in [NIST SP 800-53](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final).
    
2. **Conduct Security Auditing with Lynis:**  
    https://cisofy.com/lynis/ Lynis has it's own control IDs we can use in the scans. It gives an audit report based on what lynis found on the machine.
    
3. **Perform Penetration Testing:**  
    After the audit the goal of the pentest pahse is to validate the effectiveness of remediation actions  ensuring the server / service is secure and compliant with the security policy. Then compare initial audit findings with the pentest to verify that vulns have been addressed and check for new vulnerabilities. And then we do the reporting : Executive summary - Methodology - Findings and Recommendations.
