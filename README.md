
# SQL Injection Detection and Prevention Using ModSecurity

A controlled web application security lab using ModSecurity and OWASP Core Rule Set (CRS) to detect and block SQL injection attempts.

## Overview

This repository documents my cybersecurity internship task completed as part of the Cyber Security Analyst Internship at ICT Academy of Kerala (ICTAK).

The task demonstrates the implementation and configuration of ModSecurity as a Web Application Firewall (WAF), integrated with the OWASP Core Rule Set (CRS).

A locally hosted PHP and MariaDB web application was used to perform controlled SQL injection testing. Normal and suspicious HTTP requests were compared, and ModSecurity audit logs were analyzed to investigate the triggered security rules.

## Objectives

- Set up a local web application testing environment.
- Install and configure ModSecurity.
- Integrate OWASP Core Rule Set (CRS).
- Test SQL injection-style HTTP requests.
- Analyze HTTP response codes.
- Investigate ModSecurity audit logs.
- Identify detection and blocking rules.

## Lab Environment

| Component | Configuration |
|---|---|
| Operating System | Kali Linux |
| Web Server | Apache HTTP Server 2.4.66 |
| PHP | 8.4.23 |
| Database | MariaDB 11.8.8 |
| Web Application Firewall | ModSecurity 2.9.13 |
| Rule Set | OWASP CRS 3.3.9 |
| Target Application | Local SQL Injection Lab |
| Target URL | http://127.0.0.1/sqli-lab/ |

## Tools and Technologies

- Kali Linux
- Apache HTTP Server
- PHP
- MariaDB
- ModSecurity
- OWASP Core Rule Set (CRS)
- Linux Terminal
- cURL

## Implementation

### 1. Web Application Setup

Prepared a local PHP and MariaDB demonstration application and deployed it under:

`/var/www/html/sqli-lab/`

The application included a login page, homepage, and a separate SQL injection demonstration endpoint.

### 2. ModSecurity Installation and Configuration

Installed and enabled ModSecurity in Apache.

Verified the following:

- ModSecurity Apache module was loaded.
- Security rule engine was enabled using `SecRuleEngine On`.
- Apache configuration test returned `Syntax OK`.
- OWASP CRS rules were loaded.

### 3. OWASP CRS Integration

Integrated OWASP Core Rule Set (CRS) version 3.3.9 with ModSecurity to inspect incoming HTTP requests and identify suspicious patterns.

### 4. SQL Injection Testing

Performed two controlled tests against the local demonstration endpoint.

**Normal Request**

Username parameter:

`testuser`

Observed response:

`HTTP 200 OK`

**SQL Injection Test**

Test payload:

`test' OR '1'='1`

Observed response:

`HTTP 403 Forbidden`

The suspicious request was intercepted by ModSecurity.

## Test Results

| Test | Expected Security Behaviour | Observed Result |
|---|---|---|
| Normal username request | Allow request | HTTP 200 |
| SQL injection test | Block suspicious request | HTTP 403 |

## ModSecurity Audit Log Analysis

The audit log was reviewed at:

`/var/log/apache2/modsec_audit.log`

The following OWASP CRS rules were identified:

| Rule ID | Description | Observation |
|---|---|---|
| 942100 | SQL Injection Attack Detected via libinjection | Detected SQL injection indicators |
| 949110 | Inbound Anomaly Score Exceeded | Evaluated blocking threshold |
| 980130 | Inbound Anomaly Score Exceeded (Correlated) | Recorded correlated anomaly details |

### Security Findings

- SQL injection detection was triggered by rule 942100.
- The inbound anomaly score reached 8.
- The SQL injection component score was 5.
- Rule 949110 evaluated the inbound anomaly threshold and denied the request.
- Rule 980130 recorded correlated anomaly information.
- The audit log recorded `Action: Intercepted (phase 2)`.

These findings confirmed that ModSecurity was operating in blocking mode for the tested request.

## Key Learning Outcomes

Through this internship task, I gained practical experience in:

- Understanding Web Application Firewalls (WAF).
- Installing and configuring ModSecurity.
- Integrating OWASP Core Rule Set.
- Understanding SQL injection attack patterns.
- Analyzing HTTP status codes.
- Investigating security alerts and audit logs.
- Understanding anomaly-based request blocking.
- Learning the importance of secure database queries.

## Security Recommendations

A Web Application Firewall provides an additional layer of protection but does not replace secure application development.

Recommended security practices include:

- Use parameterized queries and prepared statements.
- Validate user input appropriately.
- Apply least-privilege database permissions.
- Monitor security logs regularly.
- Keep the WAF and security rules updated.
- Perform authorized security testing.

## Scope and Limitations

- Testing was performed only in a controlled local Kali Linux environment.
- The vulnerable demonstration endpoint was not intended for public exposure.
- Testing was limited to specific SQL injection test requests.
- Successful blocking of one test payload does not guarantee protection against every SQL injection technique.
- Additional security testing and source-code review are required for broader assessment.

## Internship Details

**Organization:** ICT Academy of Kerala (ICTAK)

**Program:** Cyber Security Analyst Internship

**Task:** SQL Injection Detection and Prevention Using ModSecurity

**Prepared By:** Athulya Binu

**Platform:** Kali Linux – Local Lab Environment

**Report Date:** 03 November 2026

## Disclaimer

This repository is intended for educational and cybersecurity learning purposes only.

All testing was conducted against a locally hosted demonstration application. The intentionally vulnerable endpoint must not be exposed to a public network.

---

**Author:** Athulya Binu

**GitHub:** [athulyabinuu](https://github.com/athulyabinuu)

**LinkedIn:** [athulyabinu](https://www.linkedin.com/in/athulyabinu/)
