# ImageGen

An [[API Key|YiffyAPI/APIKey]] <span style="color: red;">is</span> required for this service (it must have the "ImageGen" service flag). See [[Shared Responses|YiffyAPI/Shared Responses]] for common error responses.

<p>Meme and image generation - avatar compositing, text overlays, and a handful of video/gif effects. Successful requests return the generated file directly (as <code>image/png</code>, <code>image/jpeg</code>, <code>image/gif</code>, or <code>video/mp4</code> depending on the endpoint) rather than a JSON envelope.</p>

<hr>

## List Endpoints
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://imgen.yiff.rest/endpoints.json`

<p>Returns every currently available endpoint and its parameters. This is the authoritative, always-up-to-date list - the table further down this page is a convenience snapshot and can drift out of date.</p>

::: success
# 200 OK: Success
```json
{
  "endpoints": [
    {
      "name": "dab",
      "parameters": ["avatar0"]
    }
  ]
}
```
:::

<hr>

## Generate
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> <code><span style="color: rgb(0, 136, 71);">POST</span></code> `https://imgen.yiff.rest/api/{endpoint}`

<p>Endpoint-specific parameters (see the table below) are on top of the common ones listed here. GET requests take everything as query string parameters; POST requests take a JSON body instead, and use array keys (<code>avatars</code>/<code>usernames</code>) rather than numbered ones.</p>

::: none
# Path Parameters
| Name                                                        | Type   | Description                                                                                 |
|-------------------------------------------------------------|--------|---------------------------------------------------------------------------------------------|
| endpoint <span style="color: red" title="required">*</span> | String | The name of the endpoint to use. See [List Endpoints](#list-endpoints), or the table below. |
:::

::: none
# Query Parameters (GET)
| Name      | Type   | Description                                                                                              |
|-----------|--------|----------------------------------------------------------------------------------------------------------|
| avatar1   | String | Image URL. Usually a Discord avatar. Supports at least JPG, PNG, GIF, and BMP. Also accepted as `image`. |
| avatar2   | String | Image URL, for endpoints involving two users.                                                            |
| username1 | String | Username for the first user.                                                                             |
| username2 | String | Username for the second user.                                                                            |
| text      | String | Text to render on the generated image.                                                                   |
:::

::: none
# Body Parameters (POST)
| Name      | Type          | Description                                                                       |
|-----------|---------------|-----------------------------------------------------------------------------------|
| avatars   | Array<String> | Image URLs, in order (`avatars[0]` is `avatar1`, etc). Also accepted as `images`. |
| usernames | Array<String> | Usernames, in order.                                                              |
| text      | String        | Text to render on the generated image.                                            |
:::

::: success
# 200 OK: Success
<p>The raw generated file is returned, with an appropriate <code>Content-Type</code>. Standard rate limit headers are also present.</p>
:::

::: danger
# 404 Not Found: Unknown Endpoint
```json
{
  "success": false,
  "code": 1090,
  "error": "Endpoint whatever not found!"
}
```
:::

::: danger
# 400 Bad Request: Bad Request
<p>Returned for both malformed/missing parameters and endpoint-specific validation (e.g. an endpoint that expects `text` to contain a comma-separated pair of strings).</p>
```json
{
  "success": false,
  "code": 1091,
  "error": "index 0 outside of array bounds: 0...0. Are you missing a parameter?"
}
```
:::

::: danger
# 500 Internal Server Error: Generation Error
```json
{
  "success": false,
  "code": 1092,
  "error": "..."
}
```
:::

<hr>

## Endpoints

> [!NOTE]
> This list is a snapshot and can drift out of date - use [List Endpoints](#list-endpoints) for the authoritative list. `avatar1`/`avatar2`/`username1`/`username2`/`text` are the common parameters described above; anything else listed is specific to that endpoint.

| Endpoint               | Parameters                                              |
|------------------------|---------------------------------------------------------|
| `abandon`              | `text`                                                  |
| `aborted`              | `avatar1`                                               |
| `affect`               | `avatar1`                                               |
| `airpods`              | `avatar1`                                               |
| `america`              | `avatar1`                                               |
| `armor`                | `text`                                                  |
| `balloon`              | `text`                                                  |
| `bed`                  | `avatar1`, `avatar2`                                    |
| `bongocat`             | `avatar1`                                               |
| `boo`                  | `text`                                                  |
| `brain`                | `text`                                                  |
| `brazzers`             | `avatar1`                                               |
| `byemom`               | `avatar1`, `username1`, `text`                          |
| `cancer`               | `avatar1`                                               |
| `changemymind`         | `text`                                                  |
| `cheating`             | `text`                                                  |
| `citation`             | `text`                                                  |
| `communism`            | `avatar1`                                               |
| `confusedcat`          | `text`                                                  |
| `corporate`            | `avatar1`, `avatar2`                                    |
| `crab`                 | `text` (two comma-separated strings)                    |
| `cry`                  | `text`                                                  |
| `dab`                  | `avatar1`                                               |
| `dank`                 | `avatar1`                                               |
| `deepfry`              | `avatar1`                                               |
| `delete`               | `avatar1`                                               |
| `disability`           | `avatar1`                                               |
| `doglemon`             | `text`                                                  |
| `door`                 | `avatar1`                                               |
| `egg`                  | `avatar1`                                               |
| `emergencymeeting`     | `text`                                                  |
| `excuseme`             | `text`                                                  |
| `expanddong`           | `text`                                                  |
| `expandingwwe`         | `text`                                                  |
| `facts`                | `text`                                                  |
| `failure`              | `avatar1`                                               |
| `fakenews`             | `avatar1`                                               |
| `farmer`               | `text` (two comma-separated strings)                    |
| `fedora`               | `avatar1`                                               |
| `floor`                | `avatar1`, `text`                                       |
| `fuck`                 | `text`                                                  |
| `garfield`             | `text`, `avatar1`                                       |
| `gay`                  | `avatar1`                                               |
| `godwhy`               | `text`                                                  |
| `goggles`              | `avatar1`                                               |
| `hitler`               | `avatar1`                                               |
| `humansgood`           | `text`                                                  |
| `inator`               | `text`                                                  |
| `invert`               | `avatar1`                                               |
| `ipad`                 | `avatar1`                                               |
| `jail`                 | `avatar1`                                               |
| `justpretending`       | `text`                                                  |
| `keepurdistance`       | `text`                                                  |
| `kimborder`            | `avatar1`                                               |
| `knowyourlocation`     | `text`                                                  |
| `kowalski`             | `text`                                                  |
| `laid`                 | `avatar1`                                               |
| `letmein`              | `text`                                                  |
| `lick`                 | `text`                                                  |
| `madethis`             | `avatar1`, `avatar2`                                    |
| `magik`<sup>[^1]</sup> | `avatar1`                                               |
| `master`               | `text`                                                  |
| `meme`                 | `avatar1`, `top_text`, `bottom_text`, `color`, `font`   |
| `note`                 | `text`                                                  |
| `nothing`              | `text`                                                  |
| `obama`                | `text`                                                  |
| `ohno`                 | `text`                                                  |
| `piccolo`              | `text`                                                  |
| `plan`                 | `text`                                                  |
| `presentation`         | `text`                                                  |
| `quote`                | `avatar1`, `username1`, `text`                          |
| `radialblur`           | `avatar1`                                               |
| `rip`                  | `avatar1`                                               |
| `roblox`               | `avatar1`                                               |
| `salty`                | `avatar1`                                               |
| `satan`                | `avatar1`                                               |
| `savehumanity`         | `text`                                                  |
| `screams`              | `avatar1`, `avatar2`                                    |
| `shit`                 | `text`                                                  |
| `sickban`              | `avatar1`                                               |
| `slap`                 | `avatar1`, `avatar2`                                    |
| `slapsroof`            | `text`                                                  |
| `sneakyfox`            | `text`                                                  |
| `spank`                | `avatar1`, `avatar2`                                    |
| `stroke`               | `text`                                                  |
| `surprised`            | `text`                                                  |
| `sword`                | `text`, `username1`                                     |
| `theoffice`            | `text`                                                  |
| `thesearch`            | `text`                                                  |
| `trash`                | `avatar1`                                               |
| `trigger`              | `avatar1`                                               |
| `tweet`                | `avatar1`, `username1`, `text`, `username2`, `altstyle` |
| `ugly`                 | `avatar1`                                               |
| `unpopular`            | `avatar1`, `text`                                       |
| `violence`             | `text`                                                  |
| `violentsparks`        | `text`                                                  |
| `vr`                   | `text`                                                  |
| `walking`              | `text`                                                  |
| `wanted`               | `avatar1`                                               |
| `warp`                 | `avatar1`                                               |
| `whodidthis`           | `avatar1`                                               |
| `whothisis`            | `avatar1`, `text`                                       |
| `yomomma`              | *(none, returns JSON instead of an image)*              |
| `youtube`              | `avatar1`, `username1`, `text`                          |

[^1]: Currently non-functional - the liquid-rescale effect it depends on needs an ImageMagick build with `liblqr` support, which isn't available in production yet. Returns a 500 Generation Error.
