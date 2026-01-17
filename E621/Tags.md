# Tags

Tag resolver. 

> [!NOTE]
> If we're being real I'm not 100% sure if this thing actually works right, it's intended to be supplied with a list of tags and return all of the top level tags. It does not resolve implication chains, all tags in the chain must be present for it to remove the implied tags.

> [!WARNING]
> This tool is not designed to see public use. Its api is weird and unpredictable, and I do not plan on fixing it.

<hr>

## Get
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://tags.e621.church/get`

::: none
# Query Parameters
| Name                                                    | Type    | Description                                             |
| ------------------------------------------------------- | ------- | ------------------------------------------------------- |
| tags <span style="color: red" title="required">*</span> | String  | Space separated set of tags                             |
| basic                                                   | Boolean | If only `tags` should be returned. Defaults to `false`. |
:::

::: success
# 200 OK: Success
```json
// supplied "pikachu generation_1_pokemon pokemon_(species) m"
{
  "tags": [
    "pikachu",
    "male"
  ],
  "aliases": {
    "list": [
      "m"
    ],
    "results": {
      "m": "male"
    }
  },
  "implied": {
    "list": [
      "pokemon_(species)",
      "generation_1_pokemon"
    ],
    "results": {
      "pokemon_(species)": [
        // (...)
        "generation_1_pokemon",
        // (...)
      ],
      "generation_1_pokemon": [
        // (...)
        "pikachu",
        // (...)
      ]
    }
  }
}
```
:::

::: success
# 200 OK: Success (Basic)
```json
// supplied "pikachu generation_1_pokemon pokemon_(species) m"
{
  "tags": [
    "pikachu",
    "male"
  ]
}
```
:::

::: danger
# 422 Unprocessable Entity: Missing Tags
```json
{
  "success": false,
  "message": "Missing tags",
  "code": null
}
```
:::
