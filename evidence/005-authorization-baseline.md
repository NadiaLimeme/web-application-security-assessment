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
