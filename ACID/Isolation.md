# Isolation

* Can Concurrent Transactions see changes that made by other transaction ? it depends on the configuration and the database engine impl
* Read Phenomena
* Isolation levels

## Read Phenomena
* Dirty reads
  * Reading data that another transaction wrote but not committing it yet
  * There is a chance that other transactions rollback the changes, So our transaction read a **dirty read**
  * Dirty read is causing inconsistency
* Non-repeatable reads
  * Reading something and when you try to read it again this value had changed
* Phantom reads
    * Something you can't read because it does not exist yet
    * Read without scope or bounds may cause this problem eg read data and another transaction inserts new data with a successful commit when our transaction tries to read the data again the result has changed
* Lost Updates
  * When A transaction wrote something and before committing the changes I try to read it again, We found the result is different from what we expected because another transaction had changed the same data within the same row

### Dirty reads example

| PID | QNT | Price|
|-----|-----|------|
| 1   | 900 | 5    |
| 2   | 600 | 4    |

| Transaction 1                                                                                                                      | Transaction 2     |
|------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| ` BEGIN TX1;`                                                                                                                      | `BEGIN TX2;`      | 
| `SELECT PID, QNT*PRICE FROM SALES` <br/> the result will be <br/>Product 1, 50<br/>Product 2, 80                                   |in the same time <br/>`UPDATE SALES SET QNT = QNT+5 WHERE PID =1` |
| `SELECT SUM(QNT*PRICE) FROM SALES`<br/>We get $155 when it should be $130 <br/>We read a “dirty” value that has not been committed ||
| `COMMIT TX1` |`ROLLBACK TX2`|
