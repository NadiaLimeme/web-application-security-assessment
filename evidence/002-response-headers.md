# Evidence 002 — HTTP Response Headers

## Objective

Inspect the HTTP response headers returned by the local OWASP Juice Shop application.

## Request Details

* Method: `GET`
* Path: `/rest/products/search?q=`
* Host: `localhost:3000`
* Response status: `200 OK`
* Content type: `application/json; charset=utf-8`

## Observed Security Headers

* `X-Content-Type-Options: nosniff`
* `X-Frame-Options: SAMEORIGIN`
* `Content-Security-Policy: default-src 'self'; ...`

Note: The complete Content Security Policy was not recorded in this evidence.

## Analysis

The response includes headers that provide browser-side security protections. The `nosniff` value helps prevent MIME-type sniffing, while `SAMEORIGIN` restricts framing to the same origin.

The presence of these headers is useful evidence of existing security controls. Their presence alone does not establish that the application is secure.

## Conclusion

Several security-related response headers were observed. Further testing is required to assess the application's overall security posture.

## Evidence

Screenshot: `evidence-001-http-history.png`
