# Pools

Search pools with tags.

<hr>

## Search Pools
> <code><span style="color: rgb(52, 141, 248);">GET</span></code> `https://pools.e621.church/json`

::: none
# Query Parameters
| Name                | Type    | Description                                                                        |
| ------------------- | ------- | ---------------------------------------------------------------------------------- |
| limit               | Number  | The maximum number of results to return. Between `0` and `320`, defaults to `100`. |
| page                | Number  | The page of results to get.                                                        |
| cover               | Boolean | If cover data should be included. Defaults to false.                               |
| id                  | Number  | ID of the pool.                                                                    |
| name_matches        | String  | Name of the pool.                                                                  |
| description_matches | String  | Description of the pool.                                                           |
| creator_id          | Number  | ID of the pool's creator.                                                          |
| creator_name        | String  | Name of the pool's creator.                                                        |
| is_active           | Boolean | If the pool is active.                                                             |
| category            | String  | `collection`, `series`                                                             |
| order               | String  | `name`, `created_at`, `post_count`, `id_asc`, `id_desc`                            |
| tags                | String  | A space separated set of strings.[^1]                                              |
:::

::: success
# 200 OK: Success
```json
{
  "pools": [
    {
      "id": 0,
      "name": "NAME",
      "created_at": "0000-00-00T00:00:00.000",
      "updated_at": "0000-00-00T00:00:00.000",
      "creator_id": 0,
      "description": "",
      "is_active": true,
      "category": "series",
      "post_ids": [
        13
      ],
      "tag_string": "tagme"
    }
  ],
  "total": 0
}
```
:::

::: success
# 200 OK: Success (With Cover)
```json
{
  "pools": [
    {
      "id": 0,
      "name": "NAME",
      "created_at": "0000-00-00T00:00:00.000",
      "updated_at": "0000-00-00T00:00:00.000",
      "creator_id": 0,
      "description": "",
      "is_active": true,
      "category": "series",
      "post_ids": [
        13
      ],
      "tag_string": "tagme"
      "cover": {
        // raw post data from e621
        "post": {
          "id": 0,
          "created_at": "0000-00-00T00:00:00.000",
          "updated_at": "0000-00-00T00:00:00.000",
          "file": {
            "width": 0,
            "height": 0,
            "ext": "png",
            "size": 0,
            "md5": "00000000000000000000000000000000",
            "url": "https://static1.e621.net/data/00/00/00000000000000000000000000000000.jpg"
          },
          "preview": {
            "width": 0,
            "height": 0,
            "url": "https://static1.e621.net/data/preview/00/00/00000000000000000000000000000000.jpg"
          },
          "sample": {
            "has": true,
            "height": 0,
            "width": 0,
            "url": "https://static1.e621.net/data/sample/00/00/00000000000000000000000000000000.jpg",
            "alternates": {}
          },
          "score": {
            "up": 0,
            "down": 0,
            "total": 0
          },
          "tags": {
            "general": [],
            "artist": [],
            "contributor": [],
            "copyright": [],
            "character": [],
            "species": [],
            "invalid": [],
            "meta": [],
            "lore": []
          },
          "locked_tags": [],
          "change_seq": 0,
          "flags": {
            "pending": false,
            "flagged": false,
            "note_locked": false,
            "status_locked": false,
            "rating_locked": false,
            "deleted": false
          },
          "rating": "s",
          "fav_count": 0,
          "sources": [],
          "pools": [
            0
          ],
          "relationships": {
            "parent_id": null,
            "has_children": false,
            "has_active_children": false,
            "children": []
          },
          "approver_id": null,
          "uploader_id": 0,
          "description": "",
          "comment_count": 0,
          "is_favorited": false,
          "has_notes": false,
          "duration": null
        },
        // intended to be used to construct ui elements
        "data": {
          "html_id": "post_0",
          "html_class": [
            "thumbnail",
            "pending",
            "rating-safe",
            "blacklistable"
          ],
          "html_data": {
            "id": 0,
            "flags": "",
            "tags": "tagme",
            "rating": "s",
            "file_ext": "png",
            "width": 0,
            "height": 0,
            "size": 0,
            "created_at": "0000-00-00T00:00:00.000",
            "uploader": null,
            "uploader_id": 0,
            "score": 0,
            "fav_count": 0,
            "is_favorited": false,
            "pools": [
              0
            ],
            "md5": "00000000000000000000000000000000",
            "preview_url": "https://static1.e621.net/data/preview/00/00/00000000000000000000000000000000.jpg",
            "large_url": "https://static1.e621.net/data/sample/00/00/00000000000000000000000000000000.jpg",
            "file_url": "https://static1.e621.net/data/00/00/00000000000000000000000000000000.png",
            "preview_width": 0,
            "preview_height": 0
          },
          "html_tooltip": "Rating: s\nID: 0\nDate: 0000-00-00 00:00:00\nStatus: active\nScore: 0\n\ntagme",
          "file_url": "https://static1.e621.net/data/sample/00/00/00000000000000000000000000000000.png"
        }
      }
    }
  ],
  "total": 0
}
```
:::

[^1]: Metatags and groups are not supported. `-` and `~` are supported. Aliases are resolved.
