# Thumbnails

An [[API Key|YiffyAPI/APIKey]] <span style="color: red;">is</span> required for this service. See [[Shared Responses|YiffyAPI/Shared Responses]] for common error responses.

## Get Thumbnail Information
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://thumbs.yiff.rest/{id}`

::: none
# Path Parameters
| Name                                                  | Type   | Description                    |
| ----------------------------------------------------- | ------ | ------------------------------ |
| id <span style="color: red" title="required">*</span> | String | The MD5 or ID of an e621 post. |
:::

::: success
# 200 OK: Success
```json
{
  "success": true,
  "post_id": 5220880,
  "gif": null, // will usually be null, gifs can no longer be generated
  "png": "https://thumbs.yiff.media/922a7bfc2a0a19cb789cbb62c80ccba9.png" // also nullable
}
```
:::

::: danger
# 400 Bad Request: Deleted Post
```json
{
  "success": false,
  "code": 1068,
  "error": "Post is deleted"
}
```
:::

::: danger
# 404 Not Found: Invalid ID
```json
{
  "success": false,
  "code": 1062,
  "error": "Invalid Post: Not found (ID)"
}
```
:::

::: danger
# 404 Not Found: Invalid MD5
```json
{
  "success": false,
  "code": 1062,
  "error": "Invalid Post: Not found (MD5)"
}
```
:::

<hr>

## Create Thumbnail
> <code><span style="color: rgb(254, 85, 27);">PUT</span></code> `https://thumbs.yiff.rest/{id}/{type}`
<p>A 202 Accepted will be returned in most circumstances. This is a non committal answer. You must fetch `checkURL` at the specified `checkAt` time. (you will be given a new check time if it's still processing)</p>
<p>If generation has already been started by someone else, a 202 Accepted will still be returned.</p>
<p>If a thumbnail has already been created, a 200 OK will be returned.</p>

::: none
# Path Parameters
| Name                                                    | Type   | Description                    |
| ------------------------------------------------------- | ------ | ------------------------------ |
| id <span style="color: red" title="required">*</span>   | String | The MD5 or ID of an e621 post. |
| type <span style="color: red" title="required">*</span> | String | `png`                          |
:::

::: success
# 200 OK: Generation Complete
```json
{
  "success": true,
  "status": "done",
  "post_id": 5220880,
  "url": "https://thumbs.yiff.media/922a7bfc2a0a19cb789cbb62c80ccba9.png"
}
```
:::

::: success
# 202 Accepted: Generation In Progress
```json
{
  "success": true,
  "status": "processing",
  "post_id": 5220880,
  "checkURL": "https://thumbs.yiff.rest/check/922a7bfc2a0a19cb789cbb62c80ccba9/png",
  "checkAt": 0, // (unix millis) the time at which you should fetch the above url
  "time": 0, // the milliseconds after which you should check the above url (see checkAt)
  "startedAt": 0 // (unix millis) the time at which processing started
}
```
:::

::: danger
# 400 Bad Request: Deleted Post
```json
{
  "success": false,
  "code": 1068,
  "error": "Post is deleted"
}
```
:::

::: danger
# 400 Bad Request: GIF Disabled
```json
{
  "success": false,
  "code": 1067,
  "error": "The gif type has been disabled."
}
```
:::

::: danger
# 404 Not Found: Invalid Type
```json
{
  "success": false,
  "code": 1062,
  "error": "Invalid Type: invalid"
}
```
:::

::: danger
# 404 Not Found: Invalid ID
```json
{
  "success": false,
  "code": 1062,
  "error": "Invalid Post: Not found (ID)"
}
```
:::

::: danger
# 404 Not Found: Invalid MD5
```json
{
  "success": false,
  "code": 1062,
  "error": "Invalid Post: Not found (MD5)"
}
```
:::

::: danger
# 500 Internal Server Error: Generation Timeout
```json
{
  "success": false,
  "code": 1065,
  "error": "Generation timed out.",
  "expiresAt": 0 // (unix millis) when the failed generation expires (retrying is possible after expiry), also nullable
}
```
:::

::: danger
# 500 Internal Server Error: Generation Error
```json
{
  "success": false,
  "code": 1060,
  "error": "Generation encountered an error.",
  "expiresAt": 0 // (unix millis) when the failed generation expires (retrying is possible after expiry), also nullable
}
```
:::

<hr>

## Check Generation Progress
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://thumbs.yiff.rest/check/{id}/{type}`

::: none
# Path Parameters
| Name                                                    | Type   | Description                    |
| ------------------------------------------------------- | ------ | ------------------------------ |
| id <span style="color: red" title="required">*</span>   | String | The MD5 or ID of an e621 post. |
| type <span style="color: red" title="required">*</span> | String | `png`                          |
:::

::: success
# 200 OK: Generation In Progress
```json
{
  "success": true,
  "status": "processing",
  "post_id": 5220880,
  "checkURL": "https://thumbs.yiff.rest/check/922a7bfc2a0a19cb789cbb62c80ccba9/png",
  "checkAt": 0, // (unix millis) the time at which you should fetch the above url
  "time": 0, // the milliseconds after which you should check the above url (see checkAt)
  "startedAt": 0 // (unix millis) the time at which processing started
}
```
:::

::: success
# 201 Created: Generation Complete
```json
{
  "success": true,
  "status": "done",
  "post_id": 5220880,
  "url": "https://thumbs.yiff.media/922a7bfc2a0a19cb789cbb62c80ccba9.png"
}
```
:::

::: danger
# 400 Bad Request: Deleted Post
```json
{
  "success": false,
  "code": 1068,
  "error": "Post is deleted"
}
```
:::

::: danger
# 400 Bad Request: GIF Disabled
```json
{
  "success": false,
  "code": 1067,
  "error": "The gif type has been disabled."
}
```
:::

::: danger
# 404 Not Found: Invalid Type
```json
{
  "success": false,
  "code": 1062,
  "error": "Invalid Type: invalid"
}
```
:::

::: danger
# 404 Not Found: Invalid ID
```json
{
  "success": false,
  "code": 1062,
  "error": "Invalid Post: Not found (ID)"
}
```
:::

::: danger
# 404 Not Found: Invalid MD5
```json
{
  "success": false,
  "code": 1062,
  "error": "Invalid Post: Not found (MD5)"
}
```
:::

::: danger
# 404 Not Found: Check Not Found
```json
{
  "success": false,
  "code": 1066,
  "error": "Not Found"
}
```
:::

::: danger
# 500 Internal Server Error: Generation Timeout
```json
{
  "success": false,
  "code": 1065,
  "error": "Generation timed out.",
  "expiresAt": 0 // (unix millis) when the failed generation expires (retrying is possible after expiry), also nullable
}
```
:::

::: danger
# 500 Internal Server Error: Generation Error
```json
{
  "success": false,
  "code": 1060,
  "error": "Generation encountered an error.",
  "expiresAt": 0 // (unix millis) when the failed generation expires (retrying is possible after expiry), also nullable
}
```
:::
