# Error Codes

> [!TIP]
> Lines in red are no longer in use. There are currently no plans to repurpose unused codes.

<hr>

## Global
> [!NOTE]
> The codes below can be returned by any route.<br>
> The following codes are reserved for general use: 0-10, 1000-1022, 1024-1029

|               Error Code              |              Status Code              |                                           Description                                           |
|:-------------------------------------:|:-------------------------------------:|:-----------------------------------------------------------------------------------------------:|
|                   0                   |                  500                  |                        Internal Error[^1] <a id="global-internal-error"/>                       |
|                   1                   |                  403                  |                         Access Denied[^1] <a id="global-access-denied"/>                        |
|                   2                   |                  503                  |                                Readonly <a id="global-readonly"/>                               |
|                  1000                 |                  429                  |                      Ratelimited (Route) <a id="global-ratelimited-route"/>                     |
|                  1001                 |                  429                  |                     Ratelimited (Global) <a id="global-ratelimited-global"/>                    |
|                  1002                 |                  403                  |                              IP Blocked<a id="global-ip-blocked"/>                              |
| <span style="color: red;">1003</span> | <span style="color: red;">None</span> | <span style="color: red;">Down For Maintenance</span>[^2] <a id="global-down-for-maintenance"/> |
|                  1010                 |                  401                  |                         Invalid API Key <a id="global-invalid-api-key"/>                        |
|                  1011                 |                  401                  |                        Inactive API Key <a id="global-inactive-api-key"/>                       |
|                  1012                 |                  403                  |                        Disabled API Key <a id="global-disabled-api-key"/>                       |
|                  1013                 |                  401                  |                        API Key Required <a id="global-api-key-required"/>                       |
| <span style="color: red;">1014</span> | <span style="color: red;">None</span> |   <span style="color: red;">Anonymous Restricted</span> <a id="global-anonymous-restricted"/>   |
| <span style="color: red;">1020</span> | <span style="color: red;">None</span> |              <span style="color: red;">Disk Full</span> <a id="global-disk-full"/>              |
| <span style="color: red;">1021</span> | <span style="color: red;">None</span> |     <span style="color: red;">Blocked User Agent</span> <a id="global-blocked-user-agent"/>     |
|                  1022                 |                  403                  |                       Service No Access <a id="global-service-no-access"/>                      |
| <span style="color: red;">1024</span> | <span style="color: red;">None</span> |        <span style="color: red;">Unknown Route</span>[^3] <a id="global-unknown-route"/>        |
| <span style="color: red;">1025</span> | <span style="color: red;">None</span> |   <span style="color: red;">Method Not Allowed</span>[^3] <a id="global-method-not-allowed"/>   |
|                  1026                 |                  404                  |                               Not Found <a id="global-not-found"/>                              |

[^1]: Currently not used anywhere, but may be used in the future.
[^2]: Merged into <a href="#global-readonly">Readonly</a>.
[^3]: Handled by framework.

<hr>

> [!NOTE]
> The codes below can only be returned in the [[Images|YiffyAPI/Images]] service.<br>
> The following codes are reserved for this service: 1023, 1030-1059

|               Error Code              |              Status Code              |                                          Description                                          |
|:-------------------------------------:|:-------------------------------------:|:---------------------------------------------------------------------------------------------:|
| <span style="color: red;">1023</span> | <span style="color: red;">None</span> | <span style="color: red;">Invalid Response Type</span> <a id="images-invalid-response-type"/> |
| <span style="color: red;">1030</span> | <span style="color: red;">None</span> |  <span style="color: red;">Category Not Found</span>[^5] <a id="images-category-not-found"/>  |
| <span style="color: red;">1031</span> | <span style="color: red;">None</span> |      <span style="color: red;">Empty Category</span>[^4] <a id="images-empty-category"/>      |
| <span style="color: red;">1040</span> |  <span style="color: red;">404</span> |           <span style="color: red;">Not Found</span>[^5] <a id="images-not-found"/>           |
|                  1041                 |                  400                  |                             No Results <a id="images-no-results"/>                            |
|                  1051                 |                  400                  |                             Amount <1 <a id="images-amount-lt1"/>                             |
|                  1052                 |                  400                  |                             Amount >5 <a id="images-amount-gt5"/>                             |
|                  1053                 |                  404                  |                Image Response Disabled <a id="images-image-response-disabled"/>               |
|                  1054                 |                  400                  |                     [Bulk] Invalid Body <a id="images-bulk-invalid-body"/>                    |
|                  1055                 |                  400                  |                 [Bulk] Invalid Category <a id="images-bulk-invalid-category"/>                |
|                  1056                 |                  400                  |                  [Bulk] Too Many Images <a id="images-bulk-too-many-images"/>                 |
| <span style="color: red;">1057</span> | <span style="color: red;">None</span> |      <span style="color: red;">SFW Only API Key</span> <a id="images-sfw-only-api-key"/>      |

[^4]: Replaced with <a href="#images-no-results">No Results</a>
[^5]: Replaced with <a href="#global-not-found">Global Not Found</a>

<hr>

> [!NOTE]
> The codes below can only be returned in the [[Thumbnails|YiffyAPI/Thumbnails]] service.<br>
> The following codes are reserved for this service: 1060-1069

|               Error Code              |              Status Code              |                                         Description                                         |
|:-------------------------------------:|:-------------------------------------:|:-------------------------------------------------------------------------------------------:|
|                  1060                 |                  500                  |                       Generic Error <a id="thumbnails-generic-error"/>                      |
| <span style="color: red;">1061</span> | <span style="color: red;">None</span> | <span style="color: red;">API Key Required</span>[^6] <a id="thumbnails-api-key-required"/> |
|                  1062                 |                  404                  |                        Invalid Post <a id="thumbnails-invalid-post"/>                       |
| <span style="color: red;">1063</span> | <span style="color: red;">None</span> |      <span style="color: red;">Invalid MD5</span>[^7] <a id="thumbnails-invalid-md5"/>      |
|                  1064                 |                  404                  |                        Invalid Type <a id="thumbnails-invalid-type"/>                       |
|                  1065                 |                  500                  |                             Timeout <a id="thumbnails-timeout"/>                            |
| <span style="color: red;">1066</span> |  <span style="color: red;">404</span> |  <span style="color: red;">Check Not Found</span>[^5] <a id="thumbnails-check-not-found"/>  |
|                  1067                 |                  400                  |                        GIF Disabled <a id="thumbnails-gif-disabled"/>                       |
|                  1068                 |                  400                  |                        Post Deleted <a id="thumbnails-post-deleted"/>                       |

[^6]: Replaced with <a href="#global-api-key-required">Global API Key Required</a>
[^7]: Merged into <a href="#thumbnails-invalid-post">Invalid Post</a>

<hr>

> [!NOTE]
> The codes below can only be returned in the [[Shortener|YiffyAPI/Shortener]] service.<br>
> The following codes are reserved for this service: 1070-1089

|               Error Code              |              Status Code              |                                   Description                                  |
|:-------------------------------------:|:-------------------------------------:|:------------------------------------------------------------------------------:|
|                  1070                 |                  422                  |                 Code Too Long <a id="shortener-code-too-long"/>                |
|                  1071                 |                  422                  |                  Invalid Code <a id="shortener-invalid-code"/>                 |
|                  1072                 |                  409                  |                   Code In Use <a id="shortener-code-in-use"/>                  |
|                  1073                 |                  422                  |                   Invalid URL <a id="shortener-invalid-url"/>                  |
|                  1074                 |                  422                  |               Credit Too Long <a id="shortener-credit-too-long"/>              |
| <span style="color: red;">1075</span> |  <span style="color: red;">404</span> |  <span style="color: red;">Not Found</span>[^5] <a id="shortener-not-found"/>  |
|                  1076                 |                  401                  |      Management Code Required <a id="shortener-management-code-required"/>     |
|                  1077                 |                  403                  |            No Management Code <a id="shortener-no-management-code"/>           |
|                  1078                 |                  401                  |      Management Code Mismatch <a id="shortener-management-code-mismatch"/>     |
| <span style="color: red;">1079</span> | <span style="color: red;">None</span> | <span style="color: red;">URL In Use</span>[^8] <a id="shortener-url-in-use"/> |
|                  1080                 |                  400                  |                    No Changes <a id="shortener-no-changes"/>                   |
|                  1081                 |                  422                  |                  URL Too Long <a id="shortener-url-too-long"/>                 |

[^8]: URLs are no longer unique
