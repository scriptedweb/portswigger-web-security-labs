## SQL Injection UNION Attack — Determining the Number of Columns
# Overview

This PortSwigger Web Security Academy lab focused on determining the number of columns returned by a vulnerable SQL query before performing a UNION-based SQL injection.

I used the UNION SELECT NULL technique required by the lab and also tested ORDER BY as an additional method to reinforce my understanding.

# Objective

Determine the number of columns returned by the original SQL query.

Method 1: UNION SELECT NULL

I progressively increased the number of NULL values in the injected UNION query:

'+UNION+SELECT+NULL--
'+UNION+SELECT+NULL,NULL--
'+UNION+SELECT+NULL,NULL,NULL--

The first two attempts produced an invalid response, while the third produced a valid response.

This indicated that the original query returned 3 columns.

Why NULL?

NULL is useful when determining the column count because it is generally compatible with different SQL data types.

The basic idea is:

1 NULL       → ❌
2 NULLs      → ❌
3 NULLs      → ✅

Therefore:

Number of columns = 3

Method 2: ORDER BY

I also tested the same lab using ORDER BY.

I progressively increased the column index:

' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
' ORDER BY 4--

The responses indicated that column 3 was valid, while the next column produced an invalid response.

This independently confirmed that the query returns 3 columns.

# Key Learning

I initially thought ORDER BY and UNION SELECT NULL were two different types of UNION SQL injection.

I now understand that they are two different techniques for determining the number of columns returned by the original query.

Once the number of columns is known, a UNION query can be constructed with the same number of columns.

## Memory Trick 🧠

# COUNT → MATCH → UNION

COUNT the columns.
MATCH the number of columns.
Then use UNION to continue testing.
Tools
PortSwigger Web Security Academy
Burp Suite
SQL Injection
UNION-based SQL Injection
Conclusion

This lab helped me understand an important prerequisite of UNION-based SQL injection: the injected SELECT must return the same number of columns as the original query.

I also reinforced my understanding by using both UNION SELECT NULL and ORDER BY to independently determine the column count.
