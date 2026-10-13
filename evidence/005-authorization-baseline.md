# Evidence 005: Authorization Baseline

## Objective

Establish normal access to the authenticated user's own account information.

## Test Environment

* Application: OWASP Juice Shop
* Proxy: Burp Suite Community Edition
* Target: Local test application at http://localhost:3000

## Test Performed

Logged in with the lab test account and accessed the account page. Inspected the related request in Burp Suite HTTP history.

## Observed Result

* The account page was accessible to the logged-in user.
* Request inspected: GET /rest/user/whoami?fields=email
* Observed HTTP status: 304 Not Modified

## Assessment

The 304 response indicates that a cached representation may be reused. It does not, by itself, confirm whether authorization controls are secure. A fresh response and its authentication context would be needed for a stronger conclusion.

## Status

Baseline observation recorded. Authorization testing remains in progress.

## Post-Logout Access Test

### Test Performed

Logged out of the lab account and used the website's normal navigation to check account access.

### Observed Result

The application returned to the logged-out state and asked the user to log in to access account features.

### Assessment

The application restricted access to account features through normal navigation after logout. This is expected behaviour. This test alone does not prove that every protected endpoint or server-side session is invalidated.

### Status

Normal post-logout behaviour observed.

### Unauthenticated Access Check — Pending Verification

* **Endpoint:** `GET /rest/user/whoami`
* **Observed status:** `200 OK`
* **Test condition:** The user believed they were logged out.
* **Observation:** The response contained a `user` object in JSON format. Whether it contained actual account information has not yet been confirmed.
* **Verification status:** Pending.
* **Next action:** Check whether the request included a session cookie or authorization credentials. Verify the response content without exposing sensitive information.
* **Conclusion:** No confirmed vulnerability at this stage.

### Fresh Private-Window Check

* **Endpoint:** `GET /rest/user/whoami`
* **Test condition:** Fresh private browser window; no login performed during this test.
* **Authorization header:** Not present.
* **Observed HTTP status:** `304 Not Modified`.
* **Assessment:** The response may involve cache validation. This status does not confirm whether the endpoint returns account information to an unauthenticated client.
* **Conclusion:** Authorization behaviour remains unverified. Further testing is required using a fresh response and checking whether session cookies are present.

### Repeater Cache-Validation Check

**Test ID:** AUTH-006

**Endpoint:** `GET /rest/user/whoami`

**Test objective:** Investigate the repeated `304 Not Modified` response.

**Procedure:**

1. Selected the request from Burp Suite HTTP history.
2. Sent the request to Burp Repeater.
3. Removed the identified conditional cache headers.
4. Left the other request headers unchanged.

**Observed result:**

* HTTP status: `304 Not Modified`
* Response body: Empty or absent
* Cookies: Present
* Conditional cache headers: Removed for this test

**Assessment:**

The endpoint continued to return `304 Not Modified` after the identified conditional cache headers were removed. The cause of this response remains undetermined. Because cookies were retained, this test does not establish unauthenticated access behaviour.

**Conclusion:** No confirmed vulnerability. Further verification is required.

**Next action:** Investigate the request and response headers, then perform a separate request without session cookies or authorization credentials to establish the endpoint's unauthenticated behaviour.

### Repeater Cache-Validation Follow-up

**Test ID:** AUTH-007

**Endpoint:** `GET /rest/user/whoami`

**Test objective:** Determine whether removing the `If-None-Match` header changes the response status.

**Procedure:**

1. Selected the request in Burp Suite Repeater.
2. Removed the `If-None-Match` request header.
3. Left the remaining request headers unchanged.
4. Sent the request again.

**Observed result:**

* HTTP status: `304 Not Modified`
* Response body: No visible body
* Cookies: Present
* `If-None-Match`: Removed for this test
* Response included an `ETag` header.

**Assessment:**

The response remained `304 Not Modified` after the `If-None-Match` header was removed. The reason for the response remains undetermined. Cookies were retained, so this test does not establish whether the endpoint exposes account information without authentication.

**Conclusion:** No confirmed vulnerability. Authorization testing remains in progress.

**Next action:** Verify the response using a fresh request without cookies or authorization credentials, and record the resulting status and response structure.

### Unauthenticated Endpoint Test

**Test ID:** AUTH-008

**Endpoint:** `GET /rest/user/whoami`

**Test objective:** Observe the endpoint's response when session cookies and authorization credentials are not sent.

**Procedure:**

1. Selected the request in Burp Suite Repeater.
2. Removed the `Cookie` header.
3. Confirmed that no `Authorization` header was present.
4. Sent the request to the local OWASP Juice Shop application.
5. Inspected the HTTP status and response structure.

**Observed result:**

* HTTP status: `200 OK`
* Cookie header: Removed
* Authorization header: Absent
* Response body: A JSON response containing a `user` object.
* Returned field meanings: Not yet verified.

**Assessment:**

The endpoint returned a successful HTTP status and a user object without the tested authentication headers. This observation requires further analysis to determine whether the object represents an authenticated account, an anonymous/default user, or another application response.

A `200 OK` response and the presence of a `user` object alone do not establish unauthorized access to another user's information.

**Conclusion:** Potential issue under investigation; vulnerability not yet confirmed.

**Next action:** Inspect the response structure without recording personal values. Determine whether the fields represent a real account or an anonymous/default object, and compare the result with the expected behaviour of the application.

**Scope:** Local OWASP Juice Shop lab only.

### Validation of Unauthenticated User Response

**Test ID:** AUTH-009

**Endpoint:** `GET /rest/user/whoami`

**Test condition:** Request sent from Burp Repeater without a `Cookie` or `Authorization` header.

**Observed result:**

* HTTP status: `200 OK`
* Response body: JSON containing a user object with fields that appear to be account-identifying.
* Field values: Not recorded in this report.
* Account identity: Not yet verified.

**Assessment:**

The endpoint returned a user object when the tested authentication headers were absent. Further comparison is needed to determine whether the object represents a real account or an anonymous/default user.

**Status:** Potential security issue under investigation; not confirmed.

**Next action:** Compare the response structure with the expected anonymous response and the profile structure of the lab test account. Preserve sanitized evidence showing the request headers, response status, and relevant field names.

**Scope:** Local OWASP Juice Shop lab only.

### Follow-up: Unauthenticated Account Information Check

**Test ID:** AUTH-010

**Endpoint:** `GET /rest/user/whoami`

**Test condition:** Burp Repeater request with `Cookie` and `Authorization` headers removed.

**Initial observation:**

* HTTP status: `200 OK`
* Response: A JSON user object containing account-identifying fields.
* Comparison: The object appeared to match the lab test account.
* Cache behaviour: Earlier requests returned `304 Not Modified`; cache-related behaviour requires careful separation from authentication testing.

**Assessment:**

The initial result raises a potential concern that account information may be returned without the tested authentication headers. The finding is not yet confirmed because the request and response need to be reproduced under clean conditions and alternative explanations ruled out.

**Status:** Potential information disclosure — pending verification.

**Next action:** Repeat the request without authentication headers or conditional cache validators, verify the response, and retain sanitized evidence without account values or tokens.

