Mongo Index Analyser
====================

Mongo Index Analyser is a tool to look though the mongo profile 
collection in order to analyse the use of indexes.

It can report the following information:

 * The number of times each index is used in a query (sub-queries are counted individually)
 * The queries that were executed and did not use an index (either a COLLSCAN or a SORT occured)


Usage
-----

First turn on profiling on your mongod instance from the mongo shell:

```javascript
use somedatabase;
db.setProfilingLevel(2);
```

Then copy and paste the contents of indexStats.js into the shell and run
```javascript
db.indexStats()
```

If you want to increase the size of the profile collection from its default which is small:

```javascript
use yourdatabase;
db.setProfilingLevel(0);
db.system.profile.drop();
db.createCollection("system.profile", {capped: true, size: yourprofilesize})
db.setProfilingLevel(2);
```

On a replicaset you need to do setProfilingLevel on all members seperately, and they all log
to their own profile collection (even though the drop/create commands are mirrored from the primary)

This was tested on mongo 3.0. Your mileage may vary on other versions, and generally :)