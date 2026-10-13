# Evidence 003: Search Input Testing

## Objective

Observe how OWASP Juice Shop handles normal and unusual search inputs.

## Test Environment

* Application: OWASP Juice Shop
* Proxy: Burp Suite Community Edition
* Target: Local test application at `http://localhost:3000`

## Test Performed

Tested the product search functionality using the following inputs:

* Normal input: `apple`
* Special-character input: `test'123`

## Observed Results

* The normal search returned `200 OK` and product information.
* The special-character search returned `200 OK`, with product information or an empty result.

## Result

The application processed both search inputs and returned an HTTP success response.

## Security Assessment

No vulnerability was confirmed by these tests. Additional testing would be required to determine whether the search function handles input safely.

## Evidence

* Refer to `search-test-notes.md` in the project root.
* Add a Burp Suite HTTP history screenshot if available.

## Status

Initial search-input testing completed. No confirmed vulnerability identified.

## Additional Test: Search Request in Burp Repeater

### Test Performed

Sent a search request through Burp Suite Repeater using the query parameter `q=apple`.

### Observed Result

* HTTP method: GET
* Endpoint: `/rest/products/search?q=apple`
* HTTP response: `200 OK`

### Assessment

The application processed the search request and returned a successful HTTP response. This confirms that the endpoint responds to the tested input. It does not, by itself, prove that input validation is secure or that a vulnerability exists.

### Evidence

* Burp Suite Repeater request and response showing the search query and `200 OK` status.
* Screenshot to be captured and saved in the project's `evidence` folder.

### Status

Basic search request test completed.

## Additional Test: Special-Character Search Input

### Test Performed

Sent a search request through Burp Suite Repeater using the query parameter `q=test%27123`.

### Observed Result

* HTTP method: GET
* Endpoint: `/rest/products/search`
* Test input: `test%27123`
* HTTP response: `500 Internal Server Error`

### Assessment

The application returned a server error when processing the tested input. This may indicate an unhandled input or application error. Further investigation is required to determine the cause and whether there is a security impact.

### Evidence

* Burp Suite Repeater request and response showing the test input and `500 Internal Server Error`.
* Screenshot to be saved in the project's evidence folder.

### Status

Potential input-handling issue identified; investigation required.

## Error Response Inspection

### Observed Result

The response to the special-character search request returned `500 Internal Server Error` and included detailed technical information.

### Potential Security Concern

Detailed error messages may disclose internal application information that could help an attacker understand the application's implementation or identify weaknesses.

### Evidence

* Burp Suite Repeater response showing the HTTP 500 status and technical error details.
* Screenshot: `evidence-003-search-error.png`

### Severity

Not yet assessed. The impact depends on the specific technical information disclosed.

### Recommended Remediation

* Handle unexpected input safely.
* Return generic error messages to users.
* Keep detailed diagnostic information in protected server-side logs.
* Investigate and fix the underlying application error.

### Status

Potential information-disclosure issue identified; confirmation required.

## Technical Error Details

### Observed Result

The special-character search request returned `500 Internal Server Error`. Inspection of the response showed:

* A stack trace or source-code file paths.
* A database or SQL-related error.

### Potential Security Impact

Detailed errors may disclose internal application paths, implementation details, or database information. This information could assist further attacks if exposed in a production application.

### Security Classification

Potential information disclosure and input-handling failure.

SQL injection has not been confirmed.

### Recommended Remediation

* Validate and safely handle search input.
* Use parameterized database queries.
* Return generic error messages to users.
* Store detailed diagnostic information in protected server-side logs.
* Add automated tests for unusual and malformed search inputs.

### Status

Potential finding documented; root cause and security impact require further investigation.
