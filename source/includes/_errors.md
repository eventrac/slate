# Errors

<aside class="notice">
In the case of a 422 validation error, a reason message will also be included in the response body
</aside>

The eventrac API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthenticated -- Your API key is wrong.
403 | Forbidden -- You are not allowed to access tis location.
404 | Not Found -- The specified kitten could not be found.
405 | Method Not Allowed -- You tried to access a service with an invalid method.
422 | Validation Errors -- Your request contains validation errors
500 | Service Exception -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
