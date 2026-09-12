## PortSwigger Lab: User ID Controlled by Request Parameter with Password Disclosure
# 🔐 Vertical Privilege Escalation — IDOR

I completed another hands-on lab from the PortSwigger Web Security Academy, focusing on IDOR and Vertical Privilege Escalation.

The lab demonstrated how manipulating a user-controlled request parameter could allow a normal user to access an administrator's account page and ultimately obtain administrative privileges.

## 🧪 Exploitation Process

I first logged into the application as the normal user Wiener.

The account page made a request similar to:

# GET /my-account?id=wiener HTTP/2

I used Burp Suite to intercept and modify the request.

I changed the id parameter:

# GET /my-account?id=administrator HTTP/2

The server responded with:

200 OK

This indicated that the application was accepting the modified user ID and returning the administrator's account page.

## 🔎 Password Disclosure

After changing the user ID through the browser, I was landed on the administrator's page.

The administrator's password was disclosed in the response. I used Burp Suite to inspect the response and identify the password value in plain text.

I then:

Logged out of the Wiener account.
Logged in using the disclosed administrator credentials.
Successfully gained administrator access.
Opened the Admin Panel.
Deleted the user Carlos.
Successfully completed the lab.
## 🧠 Key Lessons

This lab reinforced several important web security concepts:

IDOR / Insecure Direct Object Reference
Broken Access Control
Vertical Privilege Escalation
Request Parameter Manipulation
Sensitive Information Disclosure
Authentication vs. Authorization

The major takeaway is that being successfully authenticated does not mean a user should automatically be authorized to access another user's or administrator's resources.

An application should properly verify authorization on every sensitive request rather than trusting a user-controlled parameter such as id.

#CyberSecurity #WebSecurity #PortSwigger #IDOR #VerticalPrivilege #BurpSuite #AppSec #Pentesting
