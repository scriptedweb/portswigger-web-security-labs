# PortSwigger Lab: Username Enumeration via Different Responses

## 🔐 Username & Password Enumeration

I just completed the **“Username enumeration via different responses”** lab on PortSwigger Web Security Academy.

This lab gave me practical experience with how differences in application responses can help an attacker identify valid usernames and subsequently discover valid passwords.

### 🧪 What I Practiced

I used **Burp Suite Intruder** to automate requests against the login functionality.

First, I tested a list of potential usernames and analyzed the responses from the application. A difference in the responses allowed me to identify a **valid username**.

After obtaining a valid username, I then used Intruder to test multiple password candidates against that known username until I identified the **correct password**.

### 🧠 Key Lessons

This lab demonstrated how seemingly small differences in authentication responses can provide valuable information to an attacker.

The attack flow was essentially:

```text
Potential usernames
        ↓
Username enumeration
        ↓
Valid username identified
        ↓
Password enumeration
        ↓
Valid credentials
        ↓
Successful login
```

It also reinforced the importance of defensive controls such as:

* Rate limiting
* Account lockout or temporary lockout
* Monitoring repeated failed authentication attempts
* Consistent authentication error messages
* Strong, unique passwords
* Multi-factor authentication (MFA)

Account lockout and rate limiting can significantly reduce the effectiveness of automated brute-force attempts, although they should be implemented carefully to avoid creating denial-of-service opportunities against legitimate users.

Another practical lesson added to my web security journey. 🚀

#Cybersecurity #WebSecurity #PortSwigger #Pentesting #BurpSuite #Authentication #BruteForce
