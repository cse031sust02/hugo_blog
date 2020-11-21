---
date: "2017-04-10T11:31:28+06:00"
title: "HTTP প্রোটোকল  এর বেসিক কাহিনী!"
---

## TCP/IP

TCP = Transmission Control Protocol 

IP = Internet Protocol

TCP/IP হলো একটা Protocol Suite.

TCP/IP = TCP + IP + more protocols .. 

WWW ( World Wide Web ) এ Browser গুলা Server এর সাথে connect করার জন্য TCP use করে। 
HTTP, HTTPS, SMTP, FTP ইত্যাদি protocol গুলা তাদের কাজের জন্য  TCP কে use করে। 

---

## HTTP (HyperText Transfer Protocol)
 
HTTP হলো একটা request-response stateless protocol যার মাধ্যমে Client এবং Server পরস্পর Communicate করতে পারে। 

Client টা Server এর কাছে Request পাঠায় , Server সেইটার Response পাঠায়। 
 
#### Request Message এর Format

```bash
Request Line 
Request Header fields
Empty Line 
An Optional Message Body
```

**e.g.,**

```bash
GET /index.html HTTP/1.1
Host : www.example.com 
```

* GET হলো Method
* index.html হলো Requested File
* Http/1.1 হলো HTTP Version
 
#### Response Message এর Format

```bash
Status  Line 
Response Header Fields 
Empty Line 
An Optional Message Body
```

**e.g.,**

```bash
HTTP/1.1 200 OK
```

* HTTP/1.1 = HTTP Version, 200 = Status Code, OK = reason message 

> *Header fields এর সম্পর্কে জানতে [Wikipedia](http://en.wikipedia.org/wiki/List_of_HTTP_header_fields) তে দেখুন*
 
সুতরাং , আমরা যখন ব্রাউজার এ `www.example.com/blog.php` লিখে এন্টার করি,  ব্রাউজার (Client) টা Server কে আসলে এরকম একটা request করে, 

```bash
GET  /blog.php HTTP/1.1 
Host : www.example.com 
```

আর Server এর response টা এরকম, 

```bash
HTTP/1.0 200 OK
Date: Tue, 26 May 2015 23:59:59 GMT
Content-Type: text/html
Content-Length: 1202 

<html>
<body>
  <h1>Blog</h1>
  content goes here 
</body>
</html>
```

---

### HTTP Methods/Verbs
Resource এ কি টাইপের action করতে চাই সেটা indicate করার জন্য কিছু method আছে । 
common method গুলা হলো  GET, POST, PUT, DELETE .

---

### Status Codes 

Informational : 1XX -- request recieve হইসে, process চলসে । 

Successfull : 2XX -- client এর request succssfully receive করা হইসে। 

Redirectional : 3XX -- Client এর extra কিছু করতে হবে, mostly redirected । 

Client Error : 4XX -- Client কোন error করছে । 

Server Error : 5XX -- Server এ কোন সমস্যা আছে। 

---

### HTTPS ( HyperText Transfer Protocol Secure )
 
HTTPS = HTTP + SSL (Secure Socket Layer)
 
এটা HTTP এর উপরে একটা Layer (SSL/TLS Protocol) দিয়ে বানানো যেটা HTTP Communication এ কিছু secuirity যোগ করে। 
এটার মেইন উদ্দেশ্য হলো Wiretapping আর Man-in-the-middle-attack থেকে protect করা। 
 
HTTPS এ Server ও Client গুলা  HTTP এর মতই communicate করে কিন্তু communication টা একটা Secure SSL connection এর উপরে হয় যেটা request এবং response টাকে encrypt/decrypt করে। 
 
SSL টার mainly ২ টা কাজ 

- এইটা verify করা যে Client টা Directly Server এর সাথেই communicate করতেছে </li>
- এইটা ensure করা যে client ও  server এর মধ্যকার কথাবার্তা শুধু client ও server ই পরতে পারতেছে 

HTTPS এ header, message সবই encrypted থাকে।
 
কোন site কে যদি আমরা HTTPS use করে secure করতে চাই তাহলে পুরা site টাকেই HTTPS এ host করতে হবে। এমন না যে কিছু page এ শুধু  করব। 
