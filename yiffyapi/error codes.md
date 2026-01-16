# Error Codes

> [!TIP]
> Any lines in red are no longer in use. Currently there are no plans to reuse codes.

<hr>

## Global
> [!NOTE]
> The codes below can be returned by any route.<br>
> The following codes are reserved for general use: 0-10, 1000-1022, 1024-1029

|               Error Code              |              Status Code              |                        Description                        |
|:-------------------------------------:|:-------------------------------------:|:---------------------------------------------------------:|
|                   0                   |                  500                  |                     Internal Error[^1]                    |
|                   1                   |                  403                  |                     Access Denied[^1]                     |
|                   2                   |                  503                  |                          Readonly                         |
|                  1000                 |                  429                  |                    Ratelimited (Route)                    |
|                  1001                 |                  429                  |                    Ratelimited (Global)                   |
|                  1002                 |                  403                  |                         IP Blocked                        |
| <span style="color: red;">1003</span> | <span style="color: red;">None</span> | <span style="color: red;">Down For Maintenance</span>[^2] |
|                  1010                 |                  401                  |                      Invalid API Key                      |
|                  1011                 |                  401                  |                      Inactive API Key                     |
|                  1012                 |                  403                  |                      Disabled API Key                     |
|                  1013                 |                  401                  |                      API Key Required                     |
| <span style="color: red;">1014</span> | <span style="color: red;">None</span> |   <span style="color: red;">Anonymous Restricted</span>   |
| <span style="color: red;">1020</span> | <span style="color: red;">None</span> |         <span style="color: red;">Disk Full</span>        |
| <span style="color: red;">1021</span> | <span style="color: red;">None</span> |    <span style="color: red;">Blocked User Agent</span>    |
|                  1022                 |                  403                  |                     Service No Access                     |
| <span style="color: red;">1024</span> | <span style="color: red;">None</span> |     <span style="color: red;">Unknown Route</span>[^3]    |
| <span style="color: red;">1025</span> | <span style="color: red;">None</span> |  <span style="color: red;">Method Not Allowed</span>[^3]  |
|                  1026                 |                  404                  |                         Not Found                         |

[^1]: Currently not used anywhere, but may be used in the future
[^2]: Merged into "Readonly"
[^3]: Handled by framework

<hr>

> [!NOTE]
> The codes below can only be returned in the [[Images|YiffyAPI/Images]] service.<br>
> The following codes are reserved for this service: 1023, 1030-1059

|               Error Code              |              Status Code              |                       Description                       |
|:-------------------------------------:|:-------------------------------------:|:-------------------------------------------------------:|
| <span style="color: red;">1023</span> | <span style="color: red;">None</span> |  <span style="color: red;">Invalid Response Type</span> |
| <span style="color: red;">1030</span> | <span style="color: red;">None</span> | <span style="color: red;">Category Not Found</span>[^5] |
| <span style="color: red;">1031</span> | <span style="color: red;">None</span> |   <span style="color: red;">Empty Category</span>[^4]   |
| <span style="color: red;">1040</span> |  <span style="color: red;">404</span> |      <span style="color: red;">Not Found</span>[^5]     |
|                  1041                 |                  400                  |                        No Results                       |
|                  1051                 |                  400                  |                        Amount <1                        |
|                  1052                 |                  400                  |                        Amount >5                        |
|                  1053                 |                  404                  |                 Image Response Disabled                 |
|                  1054                 |                  400                  |                   [Bulk] Invalid Body                   |
|                  1055                 |                  400                  |                 [Bulk] Invalid Category                 |
|                  1056                 |                  400                  |                  [Bulk] Too Many Images                 |
| <span style="color: red;">1057</span> | <span style="color: red;">None</span> |    <span style="color: red;">SFW Only API Key</span>    |

[^4]: Replaced with "No Results"
[^5]: Replaced with global "Not Found"

<hr>

> [!NOTE]
> The codes below can only be returned in the [[Thumbnails|YiffyAPI/Thumbnails]] service.<br>
> The following codes are reserved for this service: 1060-1069

|               Error Code              |              Status Code              |                      Description                      |
|:-------------------------------------:|:-------------------------------------:|:-----------------------------------------------------:|
|                  1060                 |                  500                  |                     Generic Error                     |
| <span style="color: red;">1061</span> | <span style="color: red;">None</span> | <span style="color: red;">API Key Required</span>[^6] |
|                  1062                 |                  404                  |                      Invalid Post                     |
| <span style="color: red;">1063</span> | <span style="color: red;">None</span> |    <span style="color: red;">Invalid MD5</span>[^7]   |
|                  1064                 |                  404                  |                      Invalid Type                     |
|                  1065                 |                  500                  |                        Timeout                        |
| <span style="color: red;">1066</span> |  <span style="color: red;">404</span> |  <span style="color: red;">Check Not Found</span>[^5] |
|                  1067                 |                  400                  |                      GIF Disabled                     |
|                  1068                 |                  400                  |                      Post Deleted                     |

[^6]: Replaced with global "API Key Required"
[^7]: Merged into "Invalid Post"

<hr>

> [!NOTE]
> The codes below can only be returned in the [[Shortener|YiffyAPI/Shortener]] service.<br>
> The following codes are reserved for this service: 1070-1089

|               Error Code              |              Status Code              |                   Description                   |
|:-------------------------------------:|:-------------------------------------:|:-----------------------------------------------:|
|                  1070                 |                  422                  |                  Code Too Long                  |
|                  1071                 |                  422                  |                   Invalid Code                  |
|                  1072                 |                  409                  |                   Code In Use                   |
|                  1073                 |                  422                  |                   Invalid URL                   |
|                  1074                 |                  422                  |                 Credit Too Long                 |
| <span style="color: red;">1075</span> |  <span style="color: red;">404</span> |  <span style="color: red;">Not Found</span>[^5] |
|                  1076                 |                  401                  |             Management Code Required            |
|                  1077                 |                  403                  |                No Management Code               |
|                  1078                 |                  401                  |             Management Code Mismatch            |
| <span style="color: red;">1079</span> | <span style="color: red;">None</span> | <span style="color: red;">URL In Use</span>[^8] |
|                  1080                 |                  400                  |                    No Changes                   |
|                  1081                 |                  422                  |                   URL Too Long                  |

[^8]: URLs are no longer unique
