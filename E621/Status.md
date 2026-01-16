# Status

## Get Combined Status
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://status.e621.church/json`

A JSON schema for this response can be found [here](https://status.e621.church/schema/combined.json)

::: none
# Path Parameters
| Name  | Type   | Description                                                                                                    |
| ----- | ------ | -------------------------------------------------------------------------------------------------------------- |
| limit | Number | The number of history entries to return. Defaults to `100`, any number between `1` and `1000` can be provided. |
:::


::: success
# 200 OK: Success
```json
{
  "current": {
    "available": true,
    "state": "up", // down, partially-down, maintenance, error
    "status": 200,
    "statusMessage": "OK",
    "since": "0000-00-00T00:00:00.000Z",
    "note": "" // nullable
  },
  "history": [
    {
      "available": false,
      "state": "maintenance",
      "status": 1,
      "statusMessage": "Maintenance",
      "since": "0000-00-00T00:00:00.000Z",
      "note": "E621 is currently in maintenance mode."
    }
  ]
}
```
:::

<hr>

## Get Current Status
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://status.e621.church/json/current`

A JSON schema for this response can be found [here](https://status.e621.church/schema/current.json)

::: success
# 200 OK: Success
```json
{
  "available": true,
  "state": "up", // down, partially-down, maintenance, error
  "status": 200,
  "statusMessage": "OK",
  "since": "0000-00-00T00:00:00.000Z",
  "note": "" // nullable
}
```
:::

<hr>

## Get Historical Status
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://status.e621.church/json/history`

A JSON schema for this response can be found [here](https://status.e621.church/schema/history.json)

::: none
# Path Parameters
| Name  | Type   | Description                                                                                                    |
| ----- | ------ | -------------------------------------------------------------------------------------------------------------- |
| limit | Number | The number of history entries to return. Defaults to `100`, any number between `1` and `1000` can be provided. |
| date  | String | The date to get the history of as an ISO-8601 timestamp. Only the day, month, and year are considered.         |
:::


::: success
# 200 OK: Success
```json
[
  {
    "available": false,
    "state": "maintenance",
    "status": 1,
    "statusMessage": "Maintenance",
    "since": "0000-00-00T00:00:00.000Z",
    "note": "E621 is currently in maintenance mode."
  }
]
```
:::
