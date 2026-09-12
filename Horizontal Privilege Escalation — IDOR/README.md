## PortSwigger Lab: User ID Controlled by Request Parameter
# 🔐 Horizontal Privilege Escalation — IDOR

I just completed the “User ID controlled by request parameter, with unpredictable user IDs” lab on PortSwigger Web Security Academy.

In this lab, I practiced a Horizontal Privilege Escalation / IDOR attack.

# 🧪 What I did

I was logged in as the user Wiener with a valid session.

The challenge was to access another user's account despite the application using unpredictable user IDs (GUIDs).

While exploring the application, I found a blog post created by Carlos. His GUID was exposed within the blog post, giving me the identifier needed to target his account.

I then:

Identified Carlos's exposed GUID.
Copied the GUID.
Modified the relevant request/URL while authenticated as Wiener.
Replaced Wiener's user identifier with Carlos's GUID.
Successfully accessed Carlos's account.
Accessed the associated API endpoint.
Submitted the API endpoint in the PortSwigger solution box and completed the lab.
## 🧠 Key Lesson

This lab demonstrated that unpredictable user IDs do not automatically prevent IDOR.

Even when an application uses GUIDs instead of simple sequential IDs, those identifiers can become exposed elsewhere in the application.

The real security control should be proper authorization checks, ensuring that an authenticated user can only access resources they are actually authorized to access.

## 📚 Concepts Practiced
Horizontal Privilege Escalation
IDOR (Insecure Direct Object Reference)
Broken Access Control
GUID/UUID enumeration through information disclosure
Request parameter manipulation
API access control

#CyberSecurity #WebSecurity #Pentesting #IDOR #HorizontalPrivilege
