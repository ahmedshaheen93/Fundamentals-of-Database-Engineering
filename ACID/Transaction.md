# What is a transaction ?

A collection of queries that are treated as  **One Unite** of work.

E.g. Account deposit (SELECT, UPDATE, UPDATE)

### Transaction lifespan

* Transaction BEGIN
* Transaction COMMIT
* Transaction ROLLBACK
* Transaction unexpected ending = ROLLBACK (e.g. crash)

### Nature of Transactions

* Transactions are used ti change and modify data
* It's normal to have a read only transaction (e.g. generate a report to ger consistent snapshot bast at the time of transaction)
---
## Transaction Example

Send 100$ from Account 1 to Account 2

### Database state before the transaction for ACCOUNT TABLE

| ACCOUNT_ID | BALANCE |
|------------|---------|
| 1          | 1000    |
| 2          | 500     |

#### 1- Transaction BEGIN

```SQL
BEGIN TX1;
```

#### 2- Select Account Balance

```SQL
SELECT BALANCE
FROM ACCOUNT
WHERE ACCOUNT_ID = 1;
```

#### 3- Check that the Balance Should not be negative at the end

* This kind of check could be on the code base of application as it's a business constrain
* Or at database level

```SQL
BALANCE > 100
```

#### 4- Debit the Account 1 with 100$

```SQL
UPDATE ACCOUNT
SET BALANCE = BALANCE - 100
WHERE ACCOUNT_ID = 1;
```

#### 5- credit the Account 2 with 100$

```SQL
UPDATE ACCOUNT
SET BALANCE = BALANCE + 100
WHERE ACCOUNT_ID = 2;
```

#### 6 - Transaction COMMIT
```SQL
COMMIT TX1
```
#### Database state after the transaction for ACCOUNT TABLE

| ACCOUNT_ID | BALANCE |
|------------|---------|
| 1          | 900     |
| 2          | 600     |
