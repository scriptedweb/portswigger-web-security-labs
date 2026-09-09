# Unprotected Functionality with Unpredictable URL
📌 Overview

I completed the Unprotected Functionality with Unpredictable URL lab on PortSwigger Web Security Academy using Burp Suite.

The lab demonstrated how an application can attempt to hide sensitive functionality behind an unpredictable URL while still failing to enforce proper access control.

🎯 Objective

Access the hidden administrator panel and delete the user Carlos.

🔎 Reconnaissance

I inspected the application's page source looking for information about hidden functionality.

During this process, I discovered that the administrator functionality was referenced within the application's JavaScript.

The administrator URL contained an unpredictable path similar to:

/administrator-panel-xxxxxx

Although the path was difficult to guess, it was exposed through the application's client-side code.

🔓 Exploitation

After identifying the administrator URL, I copied the path and requested it directly through the browser.

The application returned the administrator panel without properly verifying whether my account had administrator privileges.

I then located the user:

Carlos

and deleted the account.

The lab was successfully completed.

🧠 Key Takeaway

Making an administrative URL difficult to guess does not provide effective access control.

An attacker may discover supposedly hidden URLs through:

Page source
JavaScript
Application responses
Other client-side resources
Reconnaissance

The application must therefore perform server-side authorization checks whenever sensitive functionality is requested.

🔐 Security Principle

Unpredictable ≠ Protected

A hidden or difficult-to-guess URL should never be treated as a replacement for proper authorization.

🛠️ Tools
Burp Suite
Browser Developer Tools / Page Source
PortSwigger Web Security Academy

Lab status: ✅ Solved

#CyberSecurity #PortSwigger #WebSecurity #Pentesting #BurpSuite #AccessControl #AppSec
