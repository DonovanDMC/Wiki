# Images

An [[API Key|YiffyAPI/APIKey]] is <span style="color: red;">not</span> required for MOST endpoints of this service. See [[Shared Responses|YiffyAPI/Shared Responses]] for common error responses.

<hr>

## Online Check
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://v2.yiff.rest/online`

::: success
# 200 OK: Success
```json
{
  "success": true,
  "uptime": 0
}
```
:::

<hr>

## List Categories
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://v2.yiff.rest/categories`

::: success
# 200 OK: Success
```json
{
  "success": true,
  "data": [
    {
      "name": "Animals > Birb",
      "db": "animals.birb",
      "sfw": true,
      "count": 0
    }
  ]
}
```
:::

<hr>

## Get Category
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://v2.yiff.rest/categories/{db}`

::: none
# Path Parameters
| Name                                                  | Type   | Description                                                                       |
| ----------------------------------------------------- | ------ | --------------------------------------------------------------------------------- |
| db <span style="color: red" title="required">*</span> | String | The "db" representation of the category (see [List Categories](#list-categories)) |
:::

::: success
# 200 OK: Success
```json
{
  "success": true,
  "data": {
    "name": "Animals > Birb",
    "db": "animals.birb",
    "sfw": true,
    "count": 0
  }
}
```
:::

::: danger
# 404 Not Found: Not Found
```json
{
  "success": false,
  "code": 1030,
  "error": "Category not found."
}
```
:::

## Get Image
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://v2.yiff.rest/images/{id}`

::: none
# Path Parameters
| Name                                                  | Type   | Description              |
| ----------------------------------------------------- | ------ | ------------------------ |
| id <span style="color: red" title="required">*</span> | String | The ID[^1] of the image. |
:::

::: success
# 200 OK: Success
```json
{
  "success": true,
  "data": {
    "artists": ["tazara"],
    "sources": [
      "https://e621.net/posts/4332280",
      "https://www.furaffinity.net/view/35895655/",
      "https://d.furaffinity.net/art/tazara/1586784421/1586784421.tazara_stephen-small__1_.png",
      "https://www.furaffinity.net/user/tazara/"
    ],
    "width": 1275,
    "height": 726,
    "url": "https://static1.e621.net/data/18/ec/18ec7925aed47626e6420dc30e2804ef.png",
    "type": "image/png",
    "name": "18ec7925aed47626e6420dc30e2804ef.png",
    "id": "3552ab3a5ae34c69a58852ef0a1c02f9",
    "md5": "18ec7925aed47626e6420dc30e2804ef",
    "ext": "png",
    "size": 1687084,
    "reportURL": "https://e621.net/posts/4332280", // nullable
    "shortURL": "https://yiff.rocks/3552ab3a5ae34c69a58852ef0a1c02f9",
    "external": true,
    "viewable": true,
    "seen": 0,
    "category": "furry.cuddle"
  }
}
```
:::

::: danger
# 404 Not Found: Not Found
```json
{
  "success": false,
  "code": 1040,
  "error": "Image not found."
}
```
:::

[^1]: In most cases the md5 of the image will also work. For internally hosted images, the id and md5 will always be the same. For externally hosted images, they will be different.

<hr>

## Get Random Image
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://v2.yiff.rest/{category}`

::: none
# Path Parameters
| Name                                                        | Type   | Description                                                                                                                                                                |
| ----------------------------------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| category <span style="color: red" title="required">*</span> | String | The category to get an image from. See [List Categories](#list-categories) for a list of categories. Take the `db` property, and replace any periods with forward slashes.[^2] |
:::

::: none
# Query Parameters
| Name      | Type    | Description                                                                            |
| --------- | ------- | -------------------------------------------------------------------------------------- |
| amount    | Number  | The amount of images to request, between 1-5.                                          |
| notes     | Boolean | If notes should be hidden.                                                             |
| sizeLimit | Number  | The maximum size of images to return, in powers of 2. Units such as KB/MB can be used. |
:::

::: success
# 200 OK: Success
```json
{
  "$schema": "https://schema.yiff.rest/V2.json",
  "images": [
    {
      "artists": ["tazara"],
      "sources": [
        "https://e621.net/posts/4332280",
        "https://www.furaffinity.net/view/35895655/",
        "https://d.furaffinity.net/art/tazara/1586784421/1586784421.tazara_stephen-small__1_.png",
        "https://www.furaffinity.net/user/tazara/"
      ],
      "width": 1275,
      "height": 726,
      "url": "https://static1.e621.net/data/18/ec/18ec7925aed47626e6420dc30e2804ef.png",
      "type": "image/png",
      "name": "18ec7925aed47626e6420dc30e2804ef.png",
      "id": "3552ab3a5ae34c69a58852ef0a1c02f9",
      "md5": "18ec7925aed47626e6420dc30e2804ef",
      "ext": "png",
      "size": 1687084,
      "reportURL": "https://e621.net/posts/4332280", // nullable
      "shortURL": "https://yiff.rocks/3552ab3a5ae34c69a58852ef0a1c02f9",
      "external": true,
      "viewable": true,
      "seen": 0,
      "category": "furry.cuddle"
    }
  ],
  "success": true,
  "notes": [
    {
      "id": 0,
      "content": ""
    }
  ]
}
```
:::

::: info
# Notes

| ID | Content                                                                                                                                                                                                                                              | Active |
| -- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| 1  | `This api host (api.furry.bot) is being removed on June 9th, 2021. Please migrate to https://yiff.rest.`                                                                                                                                             | No     |
| 2  | `We've moved to using subdomains for api versioning! e.g. https://v2.yiff.rest. They have the same functionality, just without the version in the path. The /V2 route will not be removed, but any future api versions will only use the subdomain.` | Yes    |
| 3  | `Hey, we see you aren't using an api key. They're free! To get one, visit https://yiff.rest/apikeys.`                                                                                                                                                | Yes    |
| 4  | `WARNING! This list is STATIC, it can be inaccurate! We recommended parsing the dot notation in https://v2.yiff.rest/categories instead of this!`                                                                                                    | No     |
| 5  | `Since images are getting bigger, we're adding a size limit parameter. Add ?sizeLimit=<size> to limit the size of images we provide you.`                                                                                                            | Yes    |
| 6  | `You can now hide these notes by setting the notes parameter to disabled. (ex: ?notes=disabled)`                                                                                                                                                     | Yes    |
| 7  | `We now have proper documentation: https://docs.yiff.rest`                                                                                                                                                                                           | Yes    |
| 8  | `We have a new service available, a thumbnailer for e621. You can see its documentation at https://docs.yiff.rest/thumbnails.`                                                                                                                       | Yes    |

:::

::: danger
# 400 Bad Request: Amount < 1
```json
{
  "success": false,
  "code": 1051,
  "error": "Amount must be 1 or more."
}
```
:::

::: danger
# 400 Bad Request: Amount > 5
```json
{
  "success": false,
  "code": 1052,
  "error": "Amount must be 5 or less."
}
```
:::

::: danger
# 400 Bad Request: No Results Found
```json
{
  "success": false,
  "code": 1041,
  "error": "No results were found. Try changing your search parameters."
}
```
:::

::: danger
# 404 Not Found: Category Not Found
```json
{
  "success": false,
  "code": 1030,
  "error": "Category not found."
}
```
:::

[^2]: Currently, using the dot notation as is will work, but this is considered legacy behavior and could be broken without notice.

<hr>

## Get Images Bulk
> <code><span style="color: rgb(0, 136, 71);">POST</span></code> `https://v2.yiff.rest/bulk`

<p>Get an arbitrary amount of images across many categories. This endpoint requires an api key, and is restricted to developer approval.</p>
<p>By default, a maximum of 100 images total can be fetched in one request.You can request your limit to be raised by contacting a developer.</p>

::: none
# Query Parameters
| Name      | Type    | Description                                                                            |
| --------- | ------- | -------------------------------------------------------------------------------------- |
| sizeLimit | Number  | The maximum size of images to return, in powers of 2. Units such as KB/MB can be used. |
:::

::: none
# Body Parameters
| Name                                                             | Type   | Description                                                                                                                 |
| ---------------------------------------------------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------- |
| some.category <span style="color: red" title="required">*</span> | Number | A map of category (in db format) to the amount of images. See [List Categories](#list-categories) for a list of categories. |
:::

::: success
# 200 OK: Success
```json
{
  "success": true,
  "data": {
    "furry.cuddle": [
      {
        "artists": ["tazara"],
        "sources": [
          "https://e621.net/posts/4332280",
          "https://www.furaffinity.net/view/35895655/",
          "https://d.furaffinity.net/art/tazara/1586784421/1586784421.tazara_stephen-small__1_.png",
          "https://www.furaffinity.net/user/tazara/"
        ],
        "width": 1275,
        "height": 726,
        "url": "https://static1.e621.net/data/18/ec/18ec7925aed47626e6420dc30e2804ef.png",
        "type": "image/png",
        "name": "18ec7925aed47626e6420dc30e2804ef.png",
        "id": "3552ab3a5ae34c69a58852ef0a1c02f9",
        "md5": "18ec7925aed47626e6420dc30e2804ef",
        "ext": "png",
        "size": 1687084,
        "reportURL": "https://e621.net/posts/4332280", // nullable
        "shortURL": "https://yiff.rocks/3552ab3a5ae34c69a58852ef0a1c02f9",
        "external": true,
        "viewable": true,
        "seen": 0,
        "category": "furry.cuddle"
      }
    ]
  }
}
```
:::

::: danger
# 400 Bad Request: Invalid Body
```json
{
  "success": false,
  "code": 1054,
  "error": "Invalid body, or no categories specified."
}
```
:::

::: danger
# 400 Bad Request: Invalid Category
```json
{
  "success": false,
  "code": 1030,
  "error": "Invalid category specified: invalid.category"
}
```
:::

::: danger
# 400 Bad Request: Too Many Images Requested
```json
{
  "success": false,
  "code": 1056,
  "error": "Total amount of images requested is greater than {limit} ({total})"
}
```
:::
