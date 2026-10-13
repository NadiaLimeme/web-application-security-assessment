# Evidence 004: Authentication and Session Behaviour

## Objective

Observe how the application responds to login requests.

## Test Environment

* Application: OWASP Juice Shop
* Proxy: Burp Suite Community Edition
* Target: Local test application at `http://localhost:3000`

## Test Performed

* Action: Submitted login requests using the lab test account.
* HTTP method: POST
* Endpoint: `/rest/user/login`

## Observed Results

* Initial attempt: `401 Unauthorized`
* Another attempt: `413` response observed
* Subsequent attempt: `200 OK`

## Result

The latest login request returned `200 OK`, indicating that the request was accepted. The earlier unsuccessful responses were also observed during testing.

## Security Assessment

The different responses show that the application handled the requests differently. The earlier responses do not, by themselves, establish a security vulnerability.

## Evidence

* Burp Suite HTTP history showing the login request and response status codes.
* Screenshot to be added if captured, with passwords, tokens, and session cookies excluded.

## Status

Login test completed. Further session testing may be performed.

## Session Persistence Test

### Test Performed

After logging in successfully, navigated to another page within OWASP Juice Shop.

### Observed Result

The user remained logged in after navigating to another page.

### Assessment

The application maintained the authenticated state during normal navigation. This is expected behaviour, but it does not by itself confirm that session security controls are effective.

### Status

Normal session persistence observed.

## Logout Behaviour Test

### Test Performed

Selected Logout from the account menu after a successful login.

### Observed Result

The application returned to a logged-out state.

### Assessment

The logout action appeared to end the authenticated state in the browser. This is expected behaviour. Further testing would be needed to verify whether the server-side session or authentication token is invalidated correctly.

### Status

Normal logout behaviour observed.
