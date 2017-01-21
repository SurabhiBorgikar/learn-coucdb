# learn-coucdb
Quick Start to learning CouchDB

## What is Apache [CouchDB](https://en.wikipedia.org/wiki/CouchDB)? 
1.  open source database software 
2.  focuses on ease of use 
3.  an architecture that "completely embraces the Web".
4.  has a document-oriented NoSQL database architecture 
5.  implemented in the concurrency-oriented language Erlang; 
6.  it uses JSON to store data, 
7.  JavaScript as its query language using MapReduce, and HTTP for an API.


## Overview about NoSql Dbs:

NoSQL [not only SQL] is a movement towards document stores that do not make use of the relational model.

The primary objective of a NoSQL database is to have the following −
* Simplicity of design,
* Horizontal scaling, and
* Finer control over availability.

#### NoSql DBs:
	Three types:

|Key-val Store | Column Store | Document Store|
|--------------|--------------|---------------|
|Data stores as K,V pairs|Grouped by columns of data|Based on  (K,V) store, where documents contain complex data|
|No Schema|Columns further grouped into column families|Each doc is assigned a unique key used to retrieve any document.|
|Each data - (Index key, corresponding val)|Column families contain any number of columns|designed for storing, retrieving, and managing document-oriented information|
|Cassandra, DynamoDB, BerkleyDB|BigTable,HBase,HyperTable|<u>**CouchDB**</u>, MongoDB|


## Installation

##### On Ubuntu:

######**Steps**:

1: `sudo apt-get update`

2: Install the software to manage the source repos:

       `sudo apt-get install software-properties-common -y`
       
3: Add the PPA that will help fetch the latest CouchDB version:

        `sudo add-apt-repository ppa:couchdb/stable -y`
        
4: Post adding PPA, update the system for latest package:

        `sudo apt-get update`
        
5: Remove the existing version if any previous version exist :

        `sudo apt-get remove couchdb couchdb-bin couchdb-common -yf`
        
6: Install CouchDB:

        `sudo apt-get install couchdb -y`
        

By default, CouchDB runs on **localhost** and uses the port **5984**. You can retrieve this basic information by running curl from the command line:


    `curl localhost:5984`

### Futon
Futon is the built-in, web based, administration interface of CouchDB. 

**Databases:**

1. Creates databases
2. Destroys databases

**Documents:**

1. Creates documents
2. Updates documents
3. Edits documents
4. Deletes documents

**Starting Futon:**
<http://localhost:5984/_utils/>

You can perform various DB operation from your terminal using cURL utility as follows:
-> The below operations can be also performed from the web based interface easily.

`curl localhost:5984`
`{"couchdb":"Welcome","uuid":"74e8f212283cce22b69c98104329d4ea","version":"1.6.1","vendor":{"name":"Ubuntu","version":"14.04"}}`

**List all DBs:**

`curl -X GET http://localhost:5984/_all_dbs`

Output:

`["_replicator","_users"]`

**Creating a DB:**

`curl -X PUT localhost:5984/mydb`

Output:

`{"ok":true}`

**Get Db info:**

`curl -X GET localhost:5984/mydb`

Output:

`{"db_name":"mydb","doc_count":0,"doc_del_count":0,"update_seq":0,"purge_seq":0,"compact_running":false,"disk_size":79,"data_size":0,"instance_start_time":"1484565759558185","disk_format_version":6,"committed_update_seq":0}`

**Deleting a DB:**

List all DBs:

`curl -X GET localhost:5984/_all_dbs`

Output:

`["_replicator","_users","mydb","mydb1"]`

Delete a DB:

`curl -X DELETE localhost:5984/mydb1`

Output:

`{"ok":true}`

Verify if deleted:

`curl -X GET localhost:5984/_all_dbs`

Output:
`["_replicator","_users","mydb"]`



**Creating a Document:**

`curl -X PUT http://localhost:5984/mydb/"111" -d '{"Name":"Surabhi", "Email":"surabhi@gmail.com", "age":"22" }'`

Output:

`{"ok":true,"id":"111","rev":"1-703389496da6dbc37bbb56f16bb6ac4c"}`

**"rev"**, this indicates the revision id. Every time you revise (update or modify) a document a **_rev** value will be generated by CouchDB. If you want to update or delete a document, CouchDB expects you to include the **_rev** field of the revision you wish to change. When CouchDB accepts the change, it will generate a new revision number. This mechanism ensures concurrency control.

Verify if the Document is created:

`curl -X GET localhost:5984/mydb/111`

Output:

`{"_id":"111","_rev":"1-703389496da6dbc37bbb56f16bb6ac4c","Name":"Surabhi","Email":"surabhi@gmail.com","age":"22"}`

**Updating Document**

`curl -X PUT localhost:5984/mydb/111 -d '{"Name":"Surabhi Borgikar", "_rev":"1-703389496da6dbc37bbb56f16bb6ac4c"}'`

Output:

`{"ok":true,"id":"111","rev":"2-33b45809b4a69edb71fc908e1f9956df"}`

Verify:

`curl -X GET localhost:5984/mydb/111`
`{"_id":"111","_rev":"2-33b45809b4a69edb71fc908e1f9956df","Name":"Surabhi Borgikar"}`

Adding a new field to an existing document is not allowed in CouchDB. Instead, a new document using the revision number of previous is created with and a new version number assigned to new(updated) document.
The revision number is passed as part of the Json request from cURL.

### Useful links (referred the following for documenting this):

https://code.tutsplus.com/articles/getting-started-with-couchdb--net-18801

http://guide.couchdb.org/editions/1/en/index.html

https://www.tutorialspoint.com/couchdb/index.htm
