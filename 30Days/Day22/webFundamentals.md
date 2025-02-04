#	Day 22

#### 04-02-2022

# TryHackMe Rank  39932 ( 56 Streak )

[TryHachMe DNS in detail](https://tryhackme.com/room/dnsindetail)

## Intro to cURL

By default, cURL will perform GET requests on whatever URL you supply it, such as:


```
	curl https://tryhackme.com

```


This would retrieve the main page for tryhackme with a GET request. Using command line flags for cURL, we can do a lot more than just GET content. The -X flag allows us to specify the request type, eg -X POST. You can specify the data to POST with --data, which will default to plain text data. It's worth mentioning cURL does not store cookies, and you have to manually specify any cookies and values that you would like to send with your request. If you want to send cookies from cURL, you can look up how to do this.

Remember, cookies are not shared between different browsers (I'm counting cURL as a browser here).



### Tasks



There's a web server running on http://MACHINE_IP:8081. Connect to it and get the flags!

    GET request. Make a GET request to the web server with path /ctf/get
    POST request. Make a POST request with the body "flag_please" to /ctf/post
    Get a cookie. Make a GET request to /ctf/getcookie and check the cookie the server gives you
    Set a cookie. Set a cookie with name "flagpls" and value "flagpls" in your devtools (or with curl!) and make a GET request to /ctf/sendcookie




Q1.	What's the GET flag?

```
curl -v http://10.10.9.116:8081/ctf/get
*   Trying 10.10.9.116:8081...
* Connected to 10.10.9.116 (10.10.9.116) port 8081 (#0)
> GET /ctf/get HTTP/1.1
> Host: 10.10.9.116:8081
> User-Agent: curl/7.81.0
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Fri, 04 Feb 2022 03:55:06 GMT
< Content-Length: 37
< Content-Type: text/plain; charset=utf-8
<
* Connection #0 to host 10.10.9.116 left intact
thm{162520bec925bd7979e9ae65a725f99f}

```


Q2.	What's the POST flag?

```
curl -X POST --data "flag_please" -v http://10.10.9.116:8081/ctf/post
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying 10.10.9.116:8081...
* Connected to 10.10.9.116 (10.10.9.116) port 8081 (#0)
> POST /ctf/post HTTP/1.1
> Host: 10.10.9.116:8081
> User-Agent: curl/7.81.0
> Accept: */*
> Content-Length: 11
> Content-Type: application/x-www-form-urlencoded
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Fri, 04 Feb 2022 03:56:43 GMT
< Content-Length: 37
< Content-Type: text/plain; charset=utf-8
<
* Connection #0 to host 10.10.9.116 left intact
thm{3517c902e22def9c6e09b99a9040ba09}

```

Q3.	What's the "Get a cookie" flag?


```
curl -c - -v http://10.10.9.116:8081/ctf/getcookie
*   Trying 10.10.9.116:8081...
* Connected to 10.10.9.116 (10.10.9.116) port 8081 (#0)
> GET /ctf/getcookie HTTP/1.1
> Host: 10.10.9.116:8081
> User-Agent: curl/7.81.0
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
* Added cookie flag="thm{91b1ac2606f36b935f465558213d7ebd}" for domain 10.10.9.116, path /, expire 0
< Set-Cookie: flag=thm{91b1ac2606f36b935f465558213d7ebd}; Path=/
< Date: Fri, 04 Feb 2022 04:00:59 GMT
< Content-Length: 19
< Content-Type: text/plain; charset=utf-8
<
* Connection #0 to host 10.10.9.116 left intact
Check your cookies!# Netscape HTTP Cookie File
# https://curl.se/docs/http-cookies.html
# This file was generated by libcurl! Edit at your own risk.

10.10.9.116     FALSE   /       FALSE   0       flag    thm{91b1ac2606f36b935f465558213d7ebd}


```
Q4.	What's the "Set a cookie" flag?

```

curl --cookie 'flagpls=flagpls' -v http://10.10.9.116:8081/ctf/sendcookie                                                         130 ⨯
*   Trying 10.10.9.116:8081...
* Connected to 10.10.9.116 (10.10.9.116) port 8081 (#0)
> GET /ctf/sendcookie HTTP/1.1
> Host: 10.10.9.116:8081
> User-Agent: curl/7.81.0
> Accept: */*
> Cookie: flagpls=flagpls
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Fri, 04 Feb 2022 04:03:32 GMT
< Content-Length: 37
< Content-Type: text/plain; charset=utf-8
<
* Connection #0 to host 10.10.9.116 left intact
thm{c10b5cb7546f359d19c747db2d0f47b3}

```
