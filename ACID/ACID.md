# ACID

### What is ACID stands for ?

* **A**tomicity
* **C**onsistency
* **I**solation
* **D**urability

### What is a transaction ?

A collection of queries that are treated as  **One Unite** of work.

E.g. Account deposit (SELECT, UPDATE, UPDATE), [more details](Transaction.md) 

---
### Atomicity
An atomic transaction is a transaction that will rollback all queries if one or
more queries failed.

* All Queries in a transaction must succeed
* One query fails means all prior successful queries in the transaction should rollback
* If the database went down prior to a commit of a transaction all successful queries in the transaction should rollback

### Consistency

---
### Isolation 

---
* Can Concurrent Transactions see changes that made by other transaction ? it depends on the configuration and the database engine impl 
* Read Phenomena
* Isolation levels

[Isolation more details](Isolation.md)
#### Read Phenomena
### Durability
