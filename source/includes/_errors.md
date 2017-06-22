# Errors

The Direct Swap API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request was not understood
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The Deal or Term requested is hidden for administrators only
404 | Not Found -- The specified Deal, Term, or other entity could not be found
405 | Method Not Allowed -- You tried to access an object with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The object you requested has been removed from our servers
418 | I'm a teapot
429 | Too Many Requests -- You're requesting too many resources at once. Slow down.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
