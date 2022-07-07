## roll back my last delete command in MySQL

https://stackoverflow.com/questions/2356566/how-can-i-roll-back-my-last-delete-command-in-mysql

```sql
start transaction;

savepoint sp1;

delete from customer where ID=1;

savepoint sp2;

delete from customer where ID=2;

rollback to sp2;

rollback to sp1;
```

## use begin transaction and rollback

https://www.navicat.com/en/company/aboutus/blog/1712-using-transactions-in-stored-procedures-to-guard-against-data-inconsistencies

## deleting large amounts of data in sql, however do not use this directly without making sure you can roll back / backup first!!!!

https://stackoverflow.com/questions/1318972/deleting-millions-of-rows-in-mysql

do more research before doing next delete

