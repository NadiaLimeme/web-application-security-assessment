# Finding 001: Search Error Information Disclosure

## Summary

A special-character search input caused OWASP Juice Shop to return an HTTP 500 Internal Server Error. The response included a stack trace or source-code file paths and a database-related error.

## Affected Component

Product search endpoint: `/rest/products/search`

## Test Input

`test%27123`

## Evidence

* HTTP response status: `500 Internal Server Error`
* Technical stack trace or file paths observed.
* Database-related error observed.
* Supporting evidence: `evidence/evidence-003-search-error.png`

## Potential Impact

If detailed internal errors are exposed to unauthenticated or ordinary users in a production application, they may reveal implementation details that assist further attacks.

## Severity

Tentatively Low to Medium; final severity depends on the details exposed, reproducibility, and security impact.

## Root Cause

Not confirmed. The application may have an unhandled input or database-processing error.

## Recommended Remediation

* Use parameterized database queries.
* Validate and safely handle search input.
* Return generic error messages to users.
* Keep detailed diagnostics in protected server-side logs.
* Add regression tests for malformed search input.

## Retest Criteria

Repeat the same search test after remediation. The application should handle the input without exposing stack traces, file paths, or database error details.

## Status

Potential finding documented; root cause and exploitability not confirmed.
