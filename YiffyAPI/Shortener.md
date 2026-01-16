# Shortener

An [[API Key|YiffyAPI/APIKey]] <span style="color: red;">is</span> required for this service. See [[Shared Responses|YiffyAPI/Shared Responses]] for common error responses.

## Shorten A URL
> <code><span style="color: rgb(0, 136, 71);">POST</span></code> `https://yiff.rocks/create`

::: none
# Query Parameters
| Name     | Type    | Description                                                                |
| -------- | ------- | -------------------------------------------------------------------------- |
| editable | Boolean | If the shortened url should be editable (you will get a code to edit with) |
:::

::: none
# Body Parameters
| Name                                                   | Type   | Description                                                                               |
| ------------------------------------------------------ | ------ | ----------------------------------------------------------------------------------------- |
| code                                                   | String | The code to use, random if not specified.                                                 |
| credit                                                 | String | The name to credit, defaults to the discord name of the user associated with the api key. |
| url <span style="color: red" title="required">*</span> | String | The URL to shorten                                                                        |
:::

::: success
# 200 OK: Success
```json
{
  "success": true,
  "data": {
    "code": "ac611fcb338457fc4b3b83ad7072d632",
    "createdAt": "2026-01-16T13:45:04.851-06:00",
    "modifiedAt": "2026-01-16T13:45:04.851-06:00",
    "url": "https://static.femboy.fan/posts/ac/61/ac611fcb338457fc4b3b83ad7072d632.png",
    "pos": 37509,
    "credit": "YiffyAPI",
    "fullURL": "https://yiff.rocks/ac611fcb338457fc4b3b83ad7072d632"
  }
}
```
:::

::: danger
# 409 Conflict: Code In Use
```json
{
  "success": false,
  "code": 1072,
  "message": "Code has already been taken",
  "errors": {}
}
```
:::

::: danger
# 422 Unprocessable Entity: Code Too Long
```json
{
  "success": false,
  "code": 1070,
  "message": "Code is too long",
  "errors": {}
}
```
:::

::: danger
# 422 Unprocessable Entity: Invalid Code
```json
{
  "success": false,
  "code": 1071,
  "message": "Code is invalid",
  "errors": {}
}
```
:::

::: danger
# 422 Unprocessable Entity: Invalid URL
```json
{
  "success": false,
  "code": 1073,
  "message": "Url is invalid",
  "errors": {}
}
```
:::

::: danger
# 422 Unprocessable Entity: URL Too Long
```json
{
  "success": false,
  "code": 1081,
  "message": "Url is too long",
  "errors": {}
}
```
:::

::: danger
# 422 Unprocessable Entity: Credit Too Long
```json
{
  "success": false,
  "code": 1074,
  "message": "Creator name is too long",
  "errors": {}
}
```
:::

<hr>

## Get A Short URL (Redirect)
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://yiff.rocks/{code}`

::: none
# Path Parameters
| Name                                                    | Type   | Description                       |
| ------------------------------------------------------- | ------ | --------------------------------- |
| code <span style="color: red" title="required">*</span> | String | The code of the short url to get. |
:::

::: success
# 302 Found: Redirect
```
// Redirected to url
```
:::

::: danger
# 404 Not Found: Not Found
```
Unknown short url code.
```
:::

<hr>

## Get A Short URL (Preview)
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://yiff.rocks/{code}+`

::: none
# Path Parameters
| Name                                                    | Type   | Description                       |
| ------------------------------------------------------- | ------ | --------------------------------- |
| code <span style="color: red" title="required">*</span> | String | The code of the short url to get. |
:::

::: success
# 200 OK: Success
```
// HTML page
```
:::

::: danger
# 404 Not Found: Not Found
```
Unknown short url code.
```
:::

<hr>

## Get A Short URL (JSON)
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://yiff.rocks/{code}.json`

::: none
# Path Parameters
| Name                                                    | Type   | Description                       |
| ------------------------------------------------------- | ------ | --------------------------------- |
| code <span style="color: red" title="required">*</span> | String | The code of the short url to get. |
:::

::: success
# 200 OK: Success
```json
{
  "success": true,
  "data": {
    "code": "ac611fcb338457fc4b3b83ad7072d632",
    "createdAt": "2026-01-16T13:45:04.851-06:00",
    "modifiedAt": "2026-01-16T13:45:04.851-06:00",
    "url": "https://static.femboy.fan/posts/ac/61/ac611fcb338457fc4b3b83ad7072d632.png",
    "pos": 37509,
    "credit": "YiffyAPI",
    "fullURL": "https://yiff.rocks/ac611fcb338457fc4b3b83ad7072d632"
  }
}
```
:::

::: danger
# 404 Not Found: Not Found
```json
{
  "success": false,
  "code": 1075,
  "error": "A short url with that code was not found."
}
```
:::

<hr>

## Delete A Short URL
> <code><span style="color: rgb(211, 61, 61);">DELETE</span></code> `https://yiff.rocks/{code}.json`

::: none
# Request Body
| Name                                                              | Type   | Description                                                  |
| ----------------------------------------------------------------- | ------ | ------------------------------------------------------------ |
| managementCode <span style="color: red" title="required">*</span> | String | The management code you received when creating the shorturl. |
:::

::: success
# 204 No Content: Success
```
// No Content
```
:::

::: danger
# 401 Unauthorized: Management Code Required
```json
{
  "success": false,
  "code": 1076,
  "message": "A management code is required."
}
```
:::

::: danger
# 401 Unauthorized: Management Code Mismatch
```json
{
  "success": false,
  "code": 1078,
  "message": "That management code does not match this short url."
}
```
:::

::: danger
# 403 Forbidden: No Management Code
```json
{
  "success": false,
  "code": 1077,
  "message": "That short url cannot be edited by you."
}
```
:::

::: danger
# 404 Not Found: Not Found
```json
{
  "success": false,
  "code": 1075,
  "message": "A short url with that code was not found."
}
```
:::

<hr>

## Modify A Short URL
> <code><span style="color: rgb(115, 92, 255);">PATCH</span></code> `https://yiff.rocks/{code}.json`

::: none
# Request Body
| Name                                                              | Type   | Description                                                                               |
| ----------------------------------------------------------------- | ------ | ----------------------------------------------------------------------------------------- |
| managementCode <span style="color: red" title="required">*</span> | String | The management code you received when creating the shorturl.                              |
| credit                                                            | String | The name to credit, defaults to the discord name of the user associated with the api key. |
| url                                                               | String | The URL to shorten                                                                        |
:::

::: success
# 204 No Content: Success
```
// No Content
```
:::

::: danger
# 400 Bad Request: No Changes
```json
{
  "success": false,
  "code": 1080,
  "message": "No changes were detected."
}
```
:::

::: danger
# 401 Unauthorized: Management Code Required
```json
{
  "success": false,
  "code": 1076,
  "message": "A management code is required."
}
```
:::

::: danger
# 401 Unauthorized: Management Code Mismatch
```json
{
  "success": false,
  "code": 1078,
  "message": "That management code does not match this short url."
}
```
:::

::: danger
# 403 Forbidden: No Management Code
```json
{
  "success": false,
  "code": 1077,
  "message": "That short url cannot be edited by you."
}
```
:::

::: danger
# 404 Not Found: Not Found
```json
{
  "success": false,
  "code": 1075,
  "message": "A short url with that code was not found."
}
```
:::

::: danger
# 422 Unprocessable Entity: Invalid URL
```json
{
  "success": false,
  "code": 1073,
  "message": "Url is invalid",
  "errors": {}
}
```
:::

::: danger
# 422 Unprocessable Entity: URL Too Long
```json
{
  "success": false,
  "code": 1081,
  "message": "Url is too long",
  "errors": {}
}
```
:::

::: danger
# 422 Unprocessable Entity: Credit Too Long
```json
{
  "success": false,
  "code": 1074,
  "message": "Creator name is too long",
  "errors": {}
}
```
:::
