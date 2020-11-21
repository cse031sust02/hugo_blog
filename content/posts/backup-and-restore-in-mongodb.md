---
date: "2019-09-05T01:29:14+06:00"
title: "Backup and Restore MongoDB Databases"
---

MongoDB comes with two commands that allow us to quickly backupand restore to our running MongoDB instances. In order to take backups, we can use the `mongodump` command which creates BSON dump files. And to restore those dump, we can use the `mongorestore` command.

##  Taking Backups

#### - all databases
```
$ mongodump
```

#### - single database
```
$ mongodump --db <DATABASE>
```

#### - single collection
```
$ mongodump --db <DATABASE> --collection <COLLECTION>
```

#### - from remote host
```
$ mongodump --host <HOST>:<PORT> --username <USERNAME> --password <USERNAME> --db <DATABASE>
```

#### - using uri
```
$ mongodump --uri="<CONNECTION STRING>"
```

*if your local mongodump is having lower version than remote mongodb and the above command does not work, try adding the  `--forceTableScan` option.


> we can also use `-d` instead of `--db`, and `-c` instead of `--collection`

src : https://docs.mongodb.com/manual/reference/program/mongodump

---

## Restore from dump

#### - all databases
```
$ mongorestore <DUMP_FOLDER>
```
> it will create all the database and collection in local mongodb from the dump folder

#### - single database
```
$ mongorestore -d <NEW_DATABASE> <DUMP_DIRECTORY>
```

#### - single collection
```
$ mongorestore -d <NEW_DATABASE> -c <NEW_COLLECTION> <COLLECTION.bson>
```
To remote host,

```
$ mongorestore --uri="<DB_URI>" -d <NEW_DATABASE> -c <NEW_COLLECTION> <COLLECTION.bson>
```

### Note :
There is a new option called `--nsInclude` from mongo 3.4. Using this option, we can use namespaces instead of older options where db_name and collection_name are given.

#### Example : 

- **Old Way** : `mongorestore --db db_name --collection collection_name`
- **Using `--nsInclude`** : `mongorestore --nsInclude db_name.collection_name`

src : https://docs.mongodb.com/manual/reference/program/mongorestore