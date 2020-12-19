---
date: "2017-08-09T11:27:15+06:00"
title: "Introduction to Websocket"
---

---

## Intro

WebSocket is a protocol (like HTTP) which defines how two parties can communicate. It is a technique for two-way communication over one (TCP) socket.

A very good intro is written in this [post](http://blog.teamtreehouse.com/an-introduction-to-websockets)
  
---

### How It Works
  
WebSockets provide a **persistent connection** between a **client** and **server**. 

Once a WebSocket connection is established the connection stays open until the client or server decides to close this connection. With this open connection, the client or server can send messages to each other at any given time.

---

### Why Use Websocket?
  
WebSockets let us talk to the server without using AJAX requests. It provides great solution for real-time, event-driven web applications. We can use WebSocket whenever we need a truly low latency, near realtime connection between the client and the server. Such as Multiplayer online games, Chat applications, Live Updates.

Another use case for WebSocket is developing WebRTC-based applications.

Websockets can replace long-polling (keeping an HTTP connection open until the server has some data to push down to the client).
  
---

## Client & Server
  
WebSocket is designed to be implemented in web browsers and web servers, but it can be used by any client or server application.

### Servers

We can build a WebSocket server using any server-side programming language that is capable of [Berkeley sockets](https://en.wikipedia.org/wiki/Berkeley_sockets), such as PHP, Python or Node.js.

**Popular Libraries :**

* Node.js : [socket.io](http://socket.io/),  [ws](https://github.com/websockets/ws)
* PHP : [Ratchet](http://socketo.me), [PHP WebSockets](https://github.com/ghedipunk/PHP-Websockets)

> Node.js is recommended for implementing websockets, as it will let you use same technology(JavaScript) on both client and server.

### Clients

WebSocket is also a new feature in browsers. It is one of the coolest new features of HTML5 and is currently supported in most modern browsers.