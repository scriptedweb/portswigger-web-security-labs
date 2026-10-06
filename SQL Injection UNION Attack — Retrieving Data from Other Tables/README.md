# SQL Injection UNION Attack — Retrieving Data from Other Tables

## Overview

I completed the **SQL Injection UNION Attack — Retrieving Data from Other Tables** lab on PortSwigger Web Security Academy using Burp Suite.

The objective was to use a UNION-based SQL injection to retrieve interesting data from another database table.

## Determining the Number of Columns

I first used the following payload:

```sql
' UNION SELECT NULL,NULL--
```

The response confirmed that the original query returned **two columns**.

Using `NULL` as a placeholder is useful because it is generally compatible with different SQL data types.

## Retrieving Data from Another Table

After determining the column count, I used:

```sql
' UNION SELECT username,password FROM users--
```

This instructed the database to return the `username` and `password` values from the `users` table.

The response exposed the credentials contained in the lab's `users` table.

## Completing the Lab

I used the retrieved administrator credentials to authenticate to the administrator account and successfully complete the lab.

## Key Learning

This lab helped me understand the practical progression of a UNION-based SQL injection:

```text
Determine column count
        ↓
Identify compatible data types
        ↓
Identify interesting table/columns
        ↓
Use UNION SELECT
        ↓
Retrieve data
```

The important lesson is that a UNION attack requires the injected query to return the same number of columns as the original query, with compatible data types in the corresponding positions.

## Tools

* PortSwigger Web Security Academy
* Burp Suite
* SQL Injection
* UNION-based SQL Injection

## Security Impact

If an application is vulnerable to UNION-based SQL injection, an attacker may potentially retrieve data from database tables that they were never intended to access.

Depending on the application's database privileges and the information exposed, this can lead to disclosure of sensitive information such as usernames, credentials, personal information, or other application data.

## Conclusion

This lab strengthened my understanding of how UNION-based SQL injection can progress from determining the structure of the original query to retrieving data from other database tables.

**COUNT → MATCH → RETRIEVE.**
