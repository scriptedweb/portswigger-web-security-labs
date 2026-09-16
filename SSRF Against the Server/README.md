## SSRF Against the Server — PortSwigger Lab
# 📌 Overview

I completed the SSRF against the server lab on PortSwigger Web Security Academy using Burp Suite.

The lab demonstrated how a vulnerable server-side request mechanism can be abused to access an administrative interface running on the local server.

# 🎯 Objective

Use the SSRF vulnerability to access the internal administrator interface and delete the user wiener.

# 🔎 Reconnaissance

I opened a product and interacted with its Check stock functionality.

I intercepted the request using Burp Suite and identified the stock API URL as a user-controlled value.

I sent the request to Repeater for further testing.

# 🧪 SSRF Testing

The original stock request contained a URL pointing to the stock service.

I modified the destination to:

http://localhost/admin

The application processed the request from the server and returned the internal administrator interface.

This demonstrated that the application could be manipulated into making requests to a service on the local machine.

# 🖥️ Viewing the Internal Interface

I used Burp Suite's Render functionality to view the returned administrator page through the graphical interface.

This allowed me to confirm that the SSRF request had successfully reached the internal admin functionality.

# 💥 Exploitation

After identifying the user deletion functionality, I modified the SSRF destination to:

http://localhost/admin/delete?username=wiener

I sent the request through Burp Repeater.

The server responded with:

HTTP/1.1 302 Found

The user was successfully deleted, completing the lab.

# 🧠 What I Learned

This lab demonstrated an important SSRF concept:

Attacker
   ↓
Vulnerable Web Application
   ↓
Server-side request
   ↓
localhost
   ↓
Internal Admin Interface

The attacker did not need direct access to the administrative interface. Instead, the vulnerable application was used to make the request from the server itself.

# 🔐 Key Takeaway

SSRF can turn the server into a gateway to internal functionality.

A server should not blindly trust or allow user-controlled URLs to access sensitive internal services.

Lab Status: ✅ Solved

Tools: Burp Suite, PortSwigger Web Security Academy

#Cybersecurity #WebSecurity #PortSwigger #Pentesting #BurpSuite #SSRF #AppSec
