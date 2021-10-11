# Methods

- [Methods](#methods)
  - [OPTIONS](#options)
  - [GET](#get)
  - [HEAD](#head)
  - [POST](#post)
  - [PUT](#put)
  - [PATCH](#patch)
  - [DELETE](#delete)
- [cURL notes](#curl-notes)
- [Server](#server)

## OPTIONS

Shows the method availability for a route through `Access-Control-Allow-Methods` header.

**REQUEST**

```shell
curl -X OPTIONS http://127.0.0.1:3000/posts -i
```

**RESPONSE**

```shell
HTTP/1.1 204 No Content
X-Powered-By: Express
Vary: Origin, Access-Control-Request-Headers
Access-Control-Allow-Credentials: true
Access-Control-Allow-Methods: GET,HEAD,PUT,PATCH,POST,DELETE # Here they are 😎
Content-Length: 0
Date: Mon, 11 Oct 2021 00:30:45 GMT
Keep-Alive: timeout=5
Connection: keep-alive
```

Available methods: `GET`, `HEAD`, `PUT`, `PATCH`, `POST`, `DELETE`

## GET

Gets a resource. It's only used to obtain data from and endpoint. Ex.: *JSON*, *HTML*...

**REQUEST A**

```shell
curl http://127.0.0.1:3000/posts
```

**RESPONSE A**

```json
[
  {
    "id": 1,
    "title": "my-title",
    "author": "typicode"
  }
]
```

**REQUEST B**

```shell
curl https://google.com
```

**RESPONSE B**

```shell
HTTP/2 301
location: https://www.google.com/
content-type: text/html; charset=UTF-8
date: Mon, 11 Oct 2021 00:54:07 GMT
expires: Wed, 10 Nov 2021 00:54:07 GMT
cache-control: public, max-age=2592000
server: gws
content-length: 220
x-xss-protection: 0
x-frame-options: SAMEORIGIN
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000,h3-T051=":443"; ma=2592000,h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"

<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
```

## HEAD

Similar to GET method, but it only obtains the response HEADER. Maybe useful to check content length before getting it.

**REQUEST A**

```shell
curl -I http://127.0.0.1:3000/posts
```

**RESPONSE A**

```json
HTTP/1.1 200 OK
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
X-Content-Type-Options: nosniff
Content-Type: application/json; charset=utf-8
Content-Length: 74
ETag: W/"4a-n84imhvp45krbRWZG+Te+lnMEPU"
Date: Mon, 11 Oct 2021 01:01:13 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

## POST

It creates a new resource.

**REQUEST**

```shell
curl -i -d '{ "id": 2, "title": "nginx-server", "author": "angeloevangelista" }' -H "Content-type: application/json" -X POST http://127.0.0.1:3000/posts
```

**RESPONSE**

```shell
HTTP/1.1 201 Created
X-Powered-By: Express
Vary: Origin, X-HTTP-Method-Override, Accept-Encoding
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
Access-Control-Expose-Headers: Location
Location: http://127.0.0.1:3000/posts/3
X-Content-Type-Options: nosniff
Content-Type: application/json; charset=utf-8
Content-Length: 73
ETag: W/"49-TmBrlTxW31dD9Al6PSjotmk6kuo"
Date: Mon, 11 Oct 2021 01:13:44 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{
  "id": 2,
  "title": "nginx-server",
  "author": "angeloevangelista"
}
```

## PUT

Updates a resource.

**REQUEST**

```shell
curl -i -d '{"name": "angeloevangelista"}' -H "Content-type: application/json" -X PUT http://127.0.0.1:3000/profile
```

**RESPONSE**

```shell
HTTP/1.1 200 OK
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
X-Content-Type-Options: nosniff
Content-Type: application/json; charset=utf-8
Content-Length: 33
ETag: W/"21-Ce58PW4aolC936+1rYyPbgzWQYE"
Date: Mon, 11 Oct 2021 01:18:04 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{
  "name": "angeloevangelista"
}
```

## PATCH

Modify partially a resource. Usually not used, most project uses PUT.

**REQUEST**

```shell
curl -i -d '{"title": "my-title"}' -H "Content-type: application/json" -X PATCH http://127.0.0.1:3000/posts/1
```

**RESPONSE**

```shell
HTTP/1.1 200 OK
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
X-Content-Type-Options: nosniff
Content-Type: application/json; charset=utf-8
Content-Length: 60
ETag: W/"3c-qOyWF5/r1UqULD/LkqKVol5mWZE"
Date: Mon, 11 Oct 2021 01:22:35 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{
  "id": 1,
  "title": "my-title",
  "author": "typicode"
}
```

## DELETE

Deletes a resource.

**REQUEST**

```shell
curl -i -X DELETE http://127.0.0.1:3000/posts/2
```

**RESPONSE**

```shell
HTTP/1.1 200 OK
X-Powered-By: Express
Vary: Origin, Accept-Encoding
Access-Control-Allow-Credentials: true
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
X-Content-Type-Options: nosniff
Content-Type: application/json; charset=utf-8
Content-Length: 2
ETag: W/"2-vyGp6PvFo4RvsFtPoIWeCReyIC8"
Date: Mon, 11 Oct 2021 01:25:14 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{}
```

Even though in response status code is `200`, this method normally return status code `204` (No content), when succeeded, with no body.

# cURL notes

**Basic usage**: `curl <url>`

- `-X`: Sets the method. When not set, `GET` is used.
- `-I`: Sets request method to HEAD.
- `-i`: Include Response headers.
- `-d`: Sets request body data.
- `-H`: Sets a header key.

# Server

To be able to access the local routes You must serve `./db.json` using `json-server` package. You can run it directly from `npx` using the following command:

```shell
npx json-server --watch ./db.json
```
