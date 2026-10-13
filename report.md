# Web Application Security Assessment Report

## 1. Executive Summary

A security assessment was conducted against a locally hosted OWASP Juice Shop application. The purpose was to practise web application security testing, observe application behaviour, collect evidence, and document potential security weaknesses.

During search-input testing, an unusual input caused the application to return a `500 Internal Server Error`. The response included stack-trace information, file paths, and database-related error details.

This behaviour may expose internal application information. SQL injection has not been confirmed, so further validation would be required before making that conclusion.

## 2. Assessment Scope

**Target:** OWASP Juice Shop
**Environment:** Local lab environment
**Target URL:** `http://localhost:3000`

Testing focused on:

* HTTP request and response behaviour
* Response headers
* Search-input handling
* Login and session behaviour
* Basic authorization behaviour

Testing was performed against the intentionally vulnerable lab application, not a public website.

## 3. Methodology

The following activities were performed:

1. Established a baseline HTTP request using Burp Suite Community Edition.
2. Reviewed selected HTTP response headers.
3. Compared normal search input with unusual input.
4. Observed login responses and basic session behaviour.
5. Reviewed access to the user's own account page and behaviour after logout.
6. Recorded observations and saved supporting evidence.

## 4. Finding 001: Search Error Information Disclosure

**Affected area:** Product search
**Observed response:** `500 Internal Server Error`
**Severity:** Preliminary; requires further assessment

### Description

An unusual search input resulted in a server error. The response exposed stack-trace details, application file paths, and database-related error information.

### Potential impact

If similar behaviour occurs in a production application, the disclosed details could help an attacker understand the application's internal structure and identify areas for further investigation.

### Evidence

Refer to:

* `evidence/evidence-003-search-error.png`
* `evidence/evidence-003-search-input-testing.md`, if this notes file is stored in the evidence folder
* `findings/finding-001-search-error-disclosure.md`

Update the paths above if your files are stored elsewhere.

### Recommendation

* Return a generic error message to the user.
* Log detailed errors securely on the server.
* Disable detailed stack traces in production.
* Review input handling and database error handling.
* Investigate the cause of the error and conduct controlled validation before concluding that SQL injection exists.

### Status

Observed and documented. Root cause and exploitability have not been confirmed.

## 5. Limitations

This was a beginner lab assessment of a deliberately vulnerable application. Testing was limited to the areas documented in the project notes. The results do not represent a complete security audit, and untested areas may contain additional weaknesses.

## 6. Conclusion

The assessment provided practical experience with Burp Suite, HTTP requests and responses, input testing, session behaviour, evidence collection, and vulnerability reporting.

The search error demonstrates why applications should avoid exposing detailed internal errors to users. Further testing and validation would be needed to confirm the underlying cause and assess the full risk.

## 7. Tools Used

* OWASP Juice Shop
* Burp Suite Community Edition
* Web browser
* Visual Studio Code
* Markdown documentation
