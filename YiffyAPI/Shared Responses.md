# Shared Responses

<p>These may show up on any given route in any service.</p>
<p>The contents of <code>error</code> &amp; <code>message</code> are unreliable, use <code>code</code> instead. See <a href="/YiffyAPI/Error Codes">Error Codes</a> for a full list.</p>


::: danger
# 401 Unauthorized: Invalid API Key
```json
{
   "success": false,
   "code": 1010,
   "error": "Invalid API key."
 }
 ```
:::

::: danger
# 401 Unauthorized: API Key Inactive
```json
{
   "success": false,
   "code": 1011,
   "error": "API key is inactive."
 }
 ```
:::

::: danger
# 401 Unauthorized: API Key Required
```json
{
   "success": false,
   "code": 1013,
   "error": "An API key is required to access this service."
 }
 ```
:::

::: danger
# 403 Forbidden: API Key Disabled
```json
{
   "success": false,
   "code": 1012,
   "error": "Your API key has been disabled by an administrator. See \"extra.reason\" for the reasoning.",
   "extra": {
     "reason": "",
     "support": "https://yiff.rest/support"
   }
 }
 ```
:::

::: danger
# 403 Forbidden: No Access To Service
```json
{
   "success": false,
   "code": 1022,
   "error": "You do not have access to this service."
 }
 ```
:::

::: danger
# 403 Forbidden: IP Blocked
```json
{
   "success": false,
   "code": 1002,
   "error": "You have been blocked from accessing this service.",
   "extra": {
     "reason": "",
     "support": "https://yiff.rest/support"
   }
 }
 ```
:::

::: danger
# 429 Too Many Requests: Rate Limited
```json
// global headers will also be present
{
  "success": false,
  "error": "Request Limit Exceeded",
  "code": 1000,
  "info": {
    "limit": 0, // X-RateLimit-Limit
    "remaining": 0, // X-RateLimit-Remaining
    "reset": 0, // X-RateLimit-Reset
    "resetAfter": 0, // X-RateLimit-Reset-After
    "retryAfter": 0, // Retry-After
    "bucket": "", // X-RateLimit-Bucket
    "precision": "millisecond", // X-RateLimit-Precision
    "global": false
  }
}
 ```
:::
:::

::: danger
# 429 Too Many Requests: Globally Rate Limited
```json
// route specific headers will also be present
{
  "success": false,
  "error": "Request Limit Exceeded",
  "code": 1001,
  "info": {
    "limit": 0, // X-RateLimit-Global-Limit
    "remaining": 0, // X-RateLimit-Global-Remaining
    "reset": 0, // X-RateLimit-Global-Reset
    "resetAfter": 0, // X-RateLimit-Global-Reset-After
    "retryAfter": 0, // Retry-After
    "precision": "millisecond", // X-RateLimit-Global-Precision
    "global": true
  }
}
 ```
:::

::: danger
# 503 Service Unavailable: Read Only
```json
{
   "success": false,
   "code": 2,
   "error": "This service is currently in read only mode. Try again later."
 }
 ```
:::
