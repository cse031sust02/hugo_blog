---
date: "2017-04-11T11:11:22+06:00"
title: "Introduction to Cookie"
---

---

## What is a HTTP Cookie?

Cookies are small files that is sent from a website(server) and stored on users's computer by a browser.

It is also called web cookie, Internet cookie, browser cookie or simply cookie.

### Usage

Cookies are mainly used for these purposes 

  - Session management (user logins, shopping carts)
  - Personalization (user preferences)
  - Tracking (analyzing user behavior)
  
  source : [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)

---

## How server/client sends cookie?

#### Server to Browser

The server tells the client (Browser) to store a cookie using the Set-Cookie HTTP header.

e.g.,

```bash
HTTP/1.0 200 OK
Content-type: text/html
Set-Cookie:"MyCookieName=MyValue; expires=Tue, 11-Apr-2016 09:22:03 GMT; Max-Age=3600"
```

* expires date time is in GMT.
* if expire time is omitted, the cookie will expire at the end of the session (when the browser closes). These type of cookies are called 'session cookies'.

To set cookie using [php](http://php.net/manual/en/function.setcookie.php),

```php
/* expire in 20 second */
setcookie("mycookie", '20seconds', time()+20);  
```


#### Browser to the server

The browser will send back all previously stored cookies to the server using the Cookie header.

e.g.,

```bash
GET /my_page.html HTTP/1.1
Host: www.example.com
Cookie: MyCookieName=MyValue 
```

For more details, please check http://www.cookiecentral.com/faq/#3.2

---

## Secuirity

Confidential or sensitive information should never be stored or transmitted in HTTP Cookies as the entire mechanism is inherently insecure.