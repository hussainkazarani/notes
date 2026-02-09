## HTTP (HyperText Transfer Protocol)
HTTP is a protocol which is used by `Web Browsers` and `Web Servers` to communicate to each other

> **Working of HTTP Protocol** <br>
> 1\. client sends request to server <br>
> 2\. server processes the request <br>
> 3\. server sends back response <br>
> 4\. client receives the response

### Methods
> `GET` &rarr; can only read the data <br>
> `POST` &rarr; can read and also send data to server <br>
> `PUT` &rarr; update data completely <br>
> `PATCH` &rarr; update data partially <br>
> `DELETE` &rarr; delete some data on server

### Status Codes
<u>**200's &rarr; Sucess**</u> <br>
200 &rarr; request successful <br>
201 &rarr; resource created

<u>**300's &rarr; Redirection**</u> <br>
301 &rarr; moved permanently

<u>**400's &rarr; Client Error**</u> <br>
400 &rarr; bad request <br>
401 &rarr; unauthorized <br>
403 &rarr; forbidden <br>
404 &rarr; not found

<u>**500's &rarr; Server Error**</u> <br>
500 &rarr; internal server error <br>
503 &rarr; service unavailable

## HTTP Headers
information about the request and responses being sent to server from client or vice versa <br>
HTTP headers are **key–value pairs** sent with requests and responses that have metadata about how to handle the data

### Response Headers (server &rarr; client)
`Content-Type` &rarr; tells the client what kind of data is in the response body <br>
`Content-Length` &rarr; size of the response body in bytes. used to know when response is done <br>
`Set-Cookie` &rarr; server tells the browser to store a cookie. used for sessions <br>
`Cache-Control` &rarr; controls how caching should behave

### Request Headers (client &rarr; server)
`User-Agent` &rarr; identifies the client software making the request <br>
`Accept` &rarr; tells the server what content types the client can handle <br>
`Authorization` &rarr; carries authentication credentials <br>
`Content-Type` &rarr; describes the format of the request body being sent

### Common Content-Types (MIME types)
<u>**Text**</u> <br>
`text/plain` &rarr; raw text <br>
`text/html` &rarr; HTML page <br>
`text/css ` &rarr; CSS styles <br>

<u>**Application**</u> <br>
`application/json ` &rarr; JSON data <br>
`application/javascript` &rarr; JS <br>
`application/xml ` &rarr; XML <br>

<u>**Image**</u> <br>
`image/jpeg` <br>
`image/png` <br>
`image/gif`

```js
// example
// client request
POST /api/users HTTP/1.1
Host: example.com
User-Agent: MyApp/1.0
Accept: application/json
Authorization: Bearer abc.def.ghi
Content-Type: application/json
Content-Length: 52

{
  "name": "Hussain",
  "email": "hussain@example.com"
}

// server response
HTTP/1.1 201 Created
Content-Type: application/json
Content-Length: 73
Cache-Control: no-store
Set-Cookie: session_id=xyz789; HttpOnly; Secure

{
  "id": 42,
  "name": "Hussain",
  "status": "created"
}
```