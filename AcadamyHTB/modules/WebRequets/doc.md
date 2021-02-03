# HyperText Transfert Protocol

## Introduction

### Basics

HTTP protocol used to access ressources over the www.
HTTP communication : client <-> server
Client request server for a ressource
Port default HTTP : `80`
Structure of a URL
![structureURL](img/url_structure.png)
`GET` is request method but the type of request can vary.
Reponse can also contains information susch as the status code `200 OK`, to mean the request processed successfully.

### HTTPS

Network analyzer [Wireshark](https://www.wireshark.org/)
In the case of a website that is not secured it is easy to intercept the login and password for a person who is on the same network.
HTTPSecure is a protocol to encrypt communication between host and client.
Default port for HTTPS is `443`
`301 Moved Permanently` response code is to redirect the client to secure HTTPS.
[Flow HTTPS](img/HTTPS_Flow.jpeg)

### Request and Reponse

[Burp tool](https://portswigger.net/burp)
Burp is a tool that acts as a `proxy server` and can be used to examine and modify HTTP requests.
Tab proxy > Intercept.
`Forward` to analyse the request.
`CTRL + R` to copy request in tab `Repeater`.
Go on and click on `send` to get answer of server.

### Headers

1. General Headers
2. Entity Headers
3. Request Headers
4. Response Headers
5. Security Headers

#### 1. General Headers

Can be common to both the request and response.
Contextual and use to describe the message.
| Header | Description |
| ------ | ----------- |
| Date   | date & time message origin |
| Connection | close or keep-alive |

`curl -I -X GET https://www.example.com` 

#### 2. Entity Headers

Same to general headers to request and response.
Use to describe the content being transferred.
Found in responses and POST or PUT requests.

More information [W3](https://www.w3.org/Protocols/rfc2616/rfc2616-sec7.html)

In this header can find :
* Content-type
* Media-Type
* Boundary
* Content-lenght
* Content-Encoding

#### 3. Request Headers

Content :
* Host : name or IP address
* User-Agent : client request ressource
* Accept : media understand by client
* Cookie : name=value, [cookie](https://en.wikipedia.org/wiki/HTTP_cookie)
* Referer
* Autorization : Server identify client and after successful, server returns a token unique.

Request Header and usage [here](https://tools.ietf.org/html/rfc7231#section-5)

#### 4. Responsable Headers

Use to provide more context about the reponse.
Content :
* Server
* Set-cookie
* WWW-Authenticate

[More](https://tools.ietf.org/html/rfc7231#section-6)

#### 5. Security Hearders 

Content :
* Content-Security-Policy
* Strict-Transport-Security
* Referrer-Policy

[More](https://owasp.org/www-project-secure-headers/)

## Breaking it Down

### HTTP methods 

* GET : request a specific ressource
* POST : send data to server
* HEAD : request the headers
* PUT : same POST but create new ressource on the server
* DELETE : delete an existing ressource
* OPTIONS : depend server

### Response codes 

* 1xx : provides information and continue processing the request
* 2xx : Positive response codes returned when a request succeeds
* 3xx : server redirect the client
* 4xx : improper request from client.
* 5xx : some problem with the HTTP server itself

[HTTP Status Codes](https://support.cloudflare.com/hc/en-us/articles/115003014432-HTTP-Status-Codes)

## A Dive into Methods

### GET Method

[Basic Authentification](https://en.wikipedia.org/wiki/Basic_access_authentication)

Send request GET in url by :
```
url.com/nomdossier/fichier.php?name1=value1&name2=value2
```

### POST Method

Server can impose lenght restrictions on URL. 
So better to use POST instead.
POST method is used to send data to the server.
Cookies -> base64 encoding

### PUT and DELETE Methods

By defaults, PUT and DELETE methods are disallowed, cause damage or result in unintended access.
Usually these methods are allowed on WebDAV (extension of HTTP)
Can be found by sending an `OPTIONS` request on server.
`PUT` to be used to owerwrite any existing file or create a new one.
`DELETE` to be used to delete an existing file.

## CURL

### GET

default http requests made by cURL are GET.

`-v` option to request verbose

Basic AUTH Login:
```
curl http://admin:password@site.com/ -vvv
```
or
```
curl -u admin:password  http://site.com/ -vvv
```

to Follow Redirections :
```
curl -u admin:password -L http://inlanefreight.com/
```



## Ressources:
[Academy HTB](https://academy.hackthebox.eu/)
[Wireshark](https://www.wireshark.org/)
[Burp tool](https://portswigger.net/burp)
[HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
[HTTP Status Codes](https://support.cloudflare.com/hc/en-us/articles/115003014432-HTTP-Status-Codes)
[Basic Authentification](https://en.wikipedia.org/wiki/Basic_access_authentication)
[WebDAV](https://en.wikipedia.org/wiki/WebDAV)