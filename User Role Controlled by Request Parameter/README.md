User Role Controlled by Request Parameter
📌 Overview

I completed the User Role Controlled by Request Parameter lab on PortSwigger Web Security Academy using Burp Suite.

The lab demonstrated how relying on a user-controllable parameter to determine privileges can result in vertical privilege escalation.

🔎 Reconnaissance

I inspected the browser's stored cookies and identified an administrative control parameter:

admin=false

This indicated that the application was storing role-related information on the client side.

🧪 Testing

I modified the cookie value:

admin=false

to:

admin=true

I then refreshed the page.

The application accepted the modified value and treated my account as an administrator.

💥 Impact

By modifying a client-controlled parameter, I was able to gain access to administrative functionality that should have been restricted.

This demonstrates vertical privilege escalation caused by broken access control.

🧠 Key Takeaway

My main lesson from this lab is:

Client-controlled values should never be trusted for authorization decisions.

A user can modify cookies, URL parameters, and hidden form fields. The server should independently determine the user's role and enforce authorization for every privileged action.

🔐 Security Principle
Client says: admin=true
        ↓
Server should NOT simply trust it ❌
        ↓
Server verifies user's actual role
        ↓
Allow / Deny access

Lab Status: ✅ Solved

#Cybersecurity #WebSecurity #Pentesting #PortSwigger #BurpSuite #AccessControl #AppSec
