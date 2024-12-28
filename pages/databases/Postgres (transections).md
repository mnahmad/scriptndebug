



```sql

begin;


statements; 

commit;

or 
rollback;
```

- only uncommited transection can be rollbacked. OOPs


## Savepoints 
- rollback till the save point, 
- good if there are multiple batches of related transections, thus, if a batch have issues, one can roll back to the post batch save point. 
- saves a lot of time otherwise everything has to be rollbacked, aka complete rollback. 
```sql 
savepoint name;
```


read committed isolation level where select can only see commited changes. 

