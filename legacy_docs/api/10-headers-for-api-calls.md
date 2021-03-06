# Headers for Stock API calls

All Adobe Stock API calls require certain headers and allow the inclusion of optional headers.


## Headers


<table>
  <tr>
   <td><strong>Header</strong>
   </td>
   <td><strong>Detail</strong>
   </td>
  </tr>
  <tr>
   <td>x-api-key
   </td>
   <td><p>Required string. The API key assigned to your API client account when you signed up through adobe.io. See <a href="#">Register your app</a>. 

<p>Example:<br>
<code>x-api-key: a74b00000dcf4075bea68fca6306a1aa</code>
   </td>
  </tr>
  <tr>
   <td>X-Product
   </td>
   <td><p>Required string. The name of your application that is using the API. A common convention is to use the app name followed by a slash and the product version. 

<p>Example:<br>
<code>X-Product: MySampleApp/1.0</code>
   </td>
  </tr>
  <tr>
   <td>Authorization
   </td>
   <td><p>For the Search API, this is optional. For the Licensing API, it is required. An access token issued by Adobe IMS. See<a href="../03-api-authentication.md"> API authentication</a>. The Stock API uses this to access your user's member identifier, licensing status, and default locale for localizing categories and messages that the API returns. In the header, the access token must be preceded by "Bearer ". 

<p>Example:<br>
<code>Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ</code>
   </td>
  </tr>
  <tr>
   <td>X-Request-Id
   </td>
   <td><p>Optional string. A unique request identifier that you define. Used by Adobe Support to trace the request in logs. This header is automatically generated by the server and returned in the response if you do not set it explicitly. See below for example.
   </td>
  </tr>
</table>



## Examples


### Headers and parameters for a search GET


```http
GET /Rest/Media/1/Search/Files?locale=en_US&amp;search_parameters[words]=unicorns HTTP/1.1
Host: stock.adobe.io
X-Product: MySampleApp/1.0
x-api-key: a74b00000dcf4075bea68fca6306a1aa
```



### Headers and parameters for a licensing information GET


```http
GET /Rest/Libraries/1/Member/Profile?content_id=112670342&amp;license=Standard&amp;locale=en_US HTTP/1.1
Host: stock.adobe.io
X-Product: MySampleApp/1.0
x-api-key: a74b00000dcf4075bea68fca6306a1aa
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```



### Request ID returned in search response (for troubleshooting)

This is a response to the search request (like the one above), where the API key is not valid. In this case, the request ID is <code>50eYaxEFurUlb8bOpkxcnzydg6aGiUgc</code>, and could be used for further troubleshooting by Adobe if necessary.


```http
HTTP/1.1 403 Forbidden
Content-Type: application/json
Date: Fri, 10 Nov 2017 20:13:08 GMT
Server: APIP
X-Request-Id: 50eYaxEFurUlb8bOpkxcnzydg6aGiUgc
Content-Length: 55
Connection: Close

{"error_code":"403003","message":"Api Key is invalid"}
```



