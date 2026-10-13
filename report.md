# Web Application Security Assessment Report

## 1. Executive Summary

A web application security assessment was conducted against a locally hosted OWASP Juice Shop application. The objective was to practise web application testing, analyze HTTP traffic, collect evidence, and document potential security weaknesses.

During search-input testing, an unusual input resulted in a `500 Internal Server Error`. The response exposed stack-trace information, application file paths, and database-related error details. This may disclose internal application information. SQL injection was not confirmed.

During an authorization baseline check, a request to `GET /rest/user/whoami` returned a JSON user object when the tested request did not contain the `Cookie`, `Authorization`, `If-None-Match`, or `If-Modified-Since` headers. The object appeared to match the lab test account. The cause and security significance have not been confirmed, so this remains a potential information-disclosure concern requiring further validation.

The assessment was limited to the local training environment and does not represent a complete security audit.

## 2. Assessment Scope

* **Target:** OWASP Juice Shop
* **Environment:** Local lab environment
* **Target URL:** `http://localhost:3000`
* **Testing tool:** Burp Suite Community Edition

Testing focused on:

* HTTP request and response behaviour
* Response headers
* Search-input handling
* Login and session behaviour
* Basic authorization behaviour
* Selected API endpoint behaviour

Testing was performed against the intentionally vulnerable local lab application. No unauthorized systems were targeted.

## 3. Methodology

The following activities were performed:

1. Established a baseline HTTP request using Burp Suite Community Edition.
2. Reviewed selected HTTP response headers.
3. Compared normal search input with unusual input.
4. Observed login responses and basic session behaviour.
5. Reviewed access to the lab test account and behaviour after logout.
6. Inspected selected API requests and responses.
7. Recorded observations and documented supporting evidence.
8. Considered potential impacts and remediation recommendations.

## 4. Finding 001: Search Error Information Disclosure

**Affected area:** Product search

**Observed response:** `500 Internal Server Error`

**Severity:** Preliminary; further risk assessment required

### Description

An unusual search input resulted in a server error. The response exposed stack-trace details, application file paths, and database-related error information.

### Potential impact

In a production application, detailed internal errors could help an attacker understand the application's internal structure and identify areas for further investigation.

### Evidence

Refer to the search-input testing notes, screenshot, and finding document stored in the repository. Confirm the exact file paths before publishing this report.

### Recommendation

* Return a generic error message to the user.
* Log detailed errors securely on the server.
* Disable detailed stack traces in production.
* Review input handling and database error handling.
* Investigate the cause of the error.
* Conduct controlled validation before concluding that SQL injection exists.

### Status

Observed and documented. Root cause and exploitability have not been confirmed.

## 5. Potential Finding 002: Unexpected User Object in Unauthenticated API Test

**Affected endpoint:** `GET /rest/user/whoami`

**Observed response:** `200 OK`

**Severity:** Undetermined; further validation required

### Description

During a repeat test in Burp Suite Repeater, the request was sent without the tested `Cookie`, `Authorization`, `If-None-Match`, and `If-Modified-Since` headers. The response returned a JSON user object that appeared to match the lab test account.

### Potential impact

If a protected endpoint exposes account information to unauthenticated users, it could result in information disclosure. However, the current observation does not establish the root cause, the information exposed to a genuinely anonymous user, or whether the behaviour represents an authorization flaw.

### Evidence

Refer to `evidence/005-authorization-baseline.md` and its sanitized supporting evidence, if present.

### Recommendation

* Compare the response with the application's expected anonymous-user behaviour.
* Repeat the test in a clean, unauthenticated browser session.
* Check whether any other request context could explain the response.
* Record only sanitized request headers, response status, and relevant response field names.
* Avoid recording account identifiers, cookies, or authentication tokens in public evidence.
* Investigate server-side authorization and identity handling if the behaviour is reproducible.

### Status

Potential information disclosure. Further validation required; not a confirmed vulnerability.

## 6. Limitations

This was a beginner lab assessment of an intentionally vulnerable application. Testing was limited to the functionality and endpoints documented in the project notes.

The assessment did not establish the exploitability of SQL injection or confirm an authorization vulnerability. Untested areas may contain additional weaknesses. Results apply only to the tested local lab environment.

## 7. Conclusion

This project provided practical experience with Burp Suite, HTTP request and response analysis, input testing, session behaviour, authorization checks, evidence collection, and vulnerability reporting.

The search error illustrates why applications should avoid exposing detailed internal errors. The API test also highlights the importance of verifying authentication and authorization behaviour before drawing security conclusions.

Further validation would be required to determine the root cause and risk of both observations.

## 8. Tools Used

* OWASP Juice Shop
* Burp Suite Community Edition
* Web browser and developer tools
* Kali Linux
* Visual Studio Code
* Git and GitHub
* Markdown documentation
