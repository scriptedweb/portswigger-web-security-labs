Unprotected Functionality — PortSwigger Lab
📌 Overview

I completed the Unprotected Functionality lab from the PortSwigger Web Security Academy using Burp Suite.

The lab demonstrated how sensitive administrative functionality can become accessible when an application fails to enforce proper server-side access controls.

🎯 Objective

Access the administrator functionality and delete the user Carlos.

🔎 Reconnaissance

I intercepted the application's requests using Burp Suite and investigated potentially interesting URL paths.

I first tested:

/robots.txt

The server responded with:

404 Not Found

Since this did not reveal anything useful, I continued testing for predictable administrative functionality.

🔓 Discovering the Administrator Panel

I tested:

/administrator-panel

The application returned the administrator panel even though I was not authenticated as an administrator.

This demonstrated that the functionality was unprotected.

💥 Exploitation

From the exposed administrator panel, I located the user:

Carlos

I selected the option to delete the user.

The lab was then successfully completed.

🧠 Key Takeaway

This lab demonstrated an important access-control principle:

A functionality being hidden from the user interface does not make it secure.

If an application fails to perform proper authorization checks on sensitive endpoints, an attacker may discover the endpoint and directly access privileged functionality.

Security Impact

Depending on the exposed functionality, this type of vulnerability could allow an unauthorized user to:

Access administrative functions
Delete users
Modify accounts
Change application settings
Perform other privileged actions
🛠️ Tool Used
Burp Suite
PortSwigger Web Security Academy
🔐 Recommended Mitigation

Applications should enforce server-side authorization checks for every sensitive administrative endpoint and verify that the authenticated user has the required privileges before performing the requested action.

Key lesson:

🔒 A hidden door is not the same as a locked door.

#Cybersecurity #WebSecurity #Pentesting #PortSwigger #BurpSuite #AccessControl
