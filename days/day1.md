# SQL Injection part 1

## Portswigger Labs
### [Lab 1: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data)
 
 **To solve: Have to retrieve all the details of all the product**

-Having SQLi in the category filter

-Enter a payload that gives the condition always true and comments the rest

### [Lab 2: SQL injection vulnerability allowing login bypass](https://portswigger.net/web-security/sql-injection/lab-login-bypass)

**To solve: Login as administrator**

-Having SQLi in the login function
 
-Enter a payload that match the username and ignore the rest of the password part

### [Lab 3 SQL injection UNION attack, determining the number of columns returned by the query](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns)

**To solve: Determine the number of columns**

-Having SQLi in the category filter

-Have to use UNION attack (NULL method) to figure out the number of columns can be also done by ORDER BY
