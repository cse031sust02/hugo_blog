---

date: "2017-04-22T16:13:16+06:00"
title: "So you want to start using Redis?"
---

## What is Redis?

Redis is an in-memory data structure server. Which can be used as database, cache and message broker. 

Redis = REmote DIctionary Server.

>  a key-value store is commonly known today as a dictionary.
>  https://en.wikipedia.org/wiki/Key-value_database

#### # Data Structure Server
Data Structure is a particular way of organizing data. Redis is a data structure server. An important difference between Redis and other structured storage systems is that Redis supports not only strings, but also abstract data types. 

Supported data structures : strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries.

for more details, please visit the links :

- https://redis.io/topics/data-types
- https://redis.io/topics/data-types-intro

#### # Popular noSQL Database
It is a very popular noSQL database. Redis is often ranked the [most popular key-value database](http://db-engines.com/en/ranking/key-value+store).


#### # Message Broker
a messaging broker is an intermediary for messaging. It gives applications a common platform to send and receive messages, and the messages are safe until received. Redis is a widely used use as Message Broker.


### Why use Redis?
Redis is a fantastic choice if you want a highly scalable data store shared by multiple processes, multiple applications, or multiple servers.

You can found more detailed answers on [Stackoverflow](http://stackoverflow.com/a/13645017/7804179) or [Quora](https://www.quora.com/Why-use-Redis)

### Performances & Benchmarks
- https://redis.io/topics/benchmarks
- https://github.com/dwyl/learn-redis#performance--benchmarks

---

## Let's Start

So, How do i start using Redis?

### Install
- http://redis.io/download#installation
 
### Try 
- http://try.redis.io/
- https://github.com/dwyl/learn-redis

### All Commands 
- https://redis.io/commands

### CLI
After we install Redis on our local pc, we can start using the Redis CLI with the `redis-cli` command,

```   
$ redis-cli
127.0.0.1:6379>
```

### GUI
While Redis users heavily use the Command Line Interface (CLI), sometime we may like to use any Graphical User Interface (GUI). Here are some GUIs available for different platform.
  
- [Redis Commander](https://github.com/joeferner/redis-commander)
- [Redismin](https://www.redsmin.com/)
- [Redis Desktop Manager](http://docs.redisdesktop.com/en/latest/)
  