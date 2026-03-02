### SQL 문장들
데이터 조작어(DML): Select, Insert, Update, Delete
데이터 정의어(DDL): Create, Alter, Drop, Rename, Truncate
데이터 제어어(DCL): Grant, Revoke
트랜잭션 제어어(TCL): Commit, Rollback

### Null Function
| Function            | DB         | Meaning                     |
| ------------------- | ---------- | --------------------------- |
| `NVL(x,y)`          | Oracle     | If x is NULL → return y     |
| `ISNULL(x,y)`       | SQL Server | If x is NULL → return y     |
| `IFNULL(x,y)`       | MySQL      | If x is NULL → return y     |
| `COALESCE(x,y,...)` | All DBs    | Return first NON-NULL value |

| Function      | Meaning                                        |
| ------------- |------------------------------------------------|
| `NULLIF(x,y)` | If x = y → return NULL, else return x          |

### ORACLE Commit
DDL 문장 수행하면, 실행이전, 이후에 자동으로 커밋함.
DDL은 AUTO COMMIT FALSE해도 자동 커밋함
DML은 AUTO COMMIT FALSE하면 커밋 안함.


### SAVEPOINT
```ORACLE
SAVEPOINT sp1;
ROLLBACK TO sp1;
```
```SQLSERVER
SAVE TRANSACTION sp1;
ROLLBACK TRANSACTION sp1;
```

### TOP, WITH TIES, ORDER BY (SQL Server)
TOP can be used alone, but results may be unpredictable.
WITH TIES must be used with ORDER BY.