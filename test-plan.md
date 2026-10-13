# Web Application Security Assessment — Test Plan

## 1. Project Overview

**Scenario:** A fictional online retailer wants its staging web application assessed before release.

**Target:** OWASP Juice Shop

**Environment:** OWASP Juice Shop running locally in Docker on Kali Linux.

**Assessment type:** Controlled web application security assessment.

## 2. Assessment Objectives

* Understand the application's normal functionality.
* Examine authentication and account management.
* Assess authorisation and access controls.
* Review input handling and validation.
* Examine session behaviour.
* Inspect selected HTTP requests and API endpoints.
* Document evidence, potential impact, and remediation recommendations.

## 3. Scope

### In Scope

* The local OWASP Juice Shop instance.
* The dedicated test account created for this assessment.
* Authentication and account-management functions.
* Authorisation checks using the test account.
* Input validation and error handling.
* Session and cookie behaviour.
* Selected application API requests.
* HTTP traffic observed using browser developer tools and Burp Suite.

### Out of Scope

* Public websites or systems outside the local lab.
* Metasploitable 2, which belongs to a separate project.
* Denial-of-service testing.
* Attacks against real users or accounts.
* Collection of real personal information.
* Testing against external systems without explicit authorisation.

## 4. Tools

* Kali Linux
* Docker Engine
* OWASP Juice Shop
* Firefox
* Burp Suite Community Edition
* Browser developer tools
* Visual Studio Code
* Git and GitHub

## 5. Testing Methodology

1. Map normal application functionality.
2. Configure the proxy and observe ordinary HTTP requests.
3. Select suitable security tests.
4. Perform controlled tests against the local target.
5. Capture sanitised evidence.
6. Assess the impact and likely root cause of each confirmed issue.
7. Recommend practical remediation.
8. Retest fixes where feasible.

## 6. Evidence Handling

* Save screenshots and sanitised request/response examples.
* Remove passwords, session tokens, and other sensitive values.
* Record the test steps and observed results.
* Do not claim a vulnerability unless the evidence supports it.

## 7. Completion Criteria

The project is complete when the lab is reproducible, testing is documented, evidence supports the findings, remediation is explained, retesting is recorded where feasible, and the GitHub repository contains a professional README and final report.
