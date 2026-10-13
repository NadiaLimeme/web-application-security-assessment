# Search Input Test — Normal Input

## 1. Objective

Observe how the local OWASP Juice Shop application handles a normal product search request.

## 2. Environment

* Target: OWASP Juice Shop
* Target URL: `http://localhost:3000`
* Tool: Burp Suite Community Edition
* Feature tested: Product search
* Test input: `apple`

## 3. Test Procedure

1. Opened Burp Suite and navigated to Proxy → HTTP history.
2. Located the product search request.
3. Sent the request to Repeater.
4. Changed the search parameter to `apple`.
5. Clicked Send and reviewed the response.

## 4. Results

* HTTP status code: `200 OK`
* Response content: Product information was returned in the response body.
* Error message: None reported during this test.

## 5. Analysis

The application accepted the normal search input and returned product information with a successful HTTP response.

This result establishes a baseline for normal search behaviour. It does not prove that the search feature is free from security vulnerabilities.

## 6. Conclusion

The normal product search test completed successfully. Further controlled testing is required to assess how the application handles unusual or potentially unsafe input.

## 7. Evidence

Tool: Burp Suite Community Edition — Repeater.

Screenshot: To be added if a screenshot of the Repeater request and response is captured.

## 8. Additional Test — Special-Character Input

### Objective

Observe how the product search endpoint responds to an input containing an apostrophe.

### Test Details

* Endpoint: `/rest/products/search`
* Parameter: `q`
* Test input: `test'123`
* HTTP status: `200 OK`

### Observed Result

The application returned a successful HTTP response. The response body contained product data or an empty result.

The test did not produce a reported HTTP error.

### Analysis

The response indicates that the application processed the request at the HTTP level. However, the status code alone does not establish whether the input was safely processed by the application's backend.

The available observation does not confirm SQL injection, cross-site scripting, or another vulnerability. Additional evidence would be needed to determine whether the input affected application behaviour in an unexpected or unsafe way.

### Conclusion

The special-character test completed. No vulnerability was confirmed by this test.

### Evidence

Tool: Burp Suite Community Edition — Repeater.

Screenshot: Add a screenshot of the request and response if captured. Remove session tokens and other sensitive information before saving.
