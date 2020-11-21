---
date: "2020-05-21T01:29:14+06:00"
title: "Backup and Restore in PostgreSQL"
---

PostgreSQL is a object-relational database management system. It is most advanced open soruce relational database.


### Taking backups using pg_dump : 

[pg_dump](https://www.postgresql.org/docs/9.3/app-pgdump.html) is a utility for backing up a PostgreSQL database.

We can extract the database in script file or archive file formats :

- Script Files : These are plain-text files containing the SQL commands. We can restore data from these script files using *psql*. 
- Archive Files : The archive files allow *pg_restore* to rebuild the database. It also allow to be selective about what is restored.

#### Examples :

- output in script file :

```
$ pg_dump {DATABASENAME} > {FILENAME}.sql
```

- output in archive file formats :

```
$ pg_dump -Fc {DATABASENAME} > {FILENAME}.dump
$ pg_dump -Fc {DATABASENAME} > {FILENAME}.zip
```

- using host and username :

```
$ pg_dump -h {HOSTNAME} -U {USERNAME} {DATABASENAME} > {FILENAME}.sql

```

- extract a single table :

```
$ pg_dump -t {TABLENAME} {DATABASENAME} > {FILENAME}.sql
```

### Restore database using pg_restore : 

[pg_restore](https://www.postgresql.org/docs/9.3/app-pgrestore.html) is a utility for restoring a PostgreSQL database from an archive created by pg_dump (in one of the non-plain-text formats).

#### Examples :

- restore from archives :

```
$ pg_restore -d {NEWDATABASE} {FILENAME}.dump
$ pg_restore -d {NEWDATABASE} {FILENAME}.zip
```

- using host and username :

```
$ pg_restore -h {HOSTNAME} -U {USERNAME} -d {NEWDATABASE} {FILENAME}.dump
```

### Restore database using psql : 

[Psql](https://www.postgresql.org/docs/9.3/app-psql.html) is the interactive terminal for working with Postgres.

#### Examples :

- restore data from script files :

```
$  psql -d {NEWDATABASE} -f {FILENAME}.zip
```

- using host and username :

```
$  psql -h {HOSTNAME} -U {USERNAME} -d {NEWDATABASE} -f {FILENAME}.zip
```