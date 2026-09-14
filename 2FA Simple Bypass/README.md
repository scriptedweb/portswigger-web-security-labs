## 🔐 Another PortSwigger Lab Completed — 2FA Simple Bypass

Today, I completed another PortSwigger Web Security Academy lab focused on 2FA Simple Bypass.

In the lab, I first authenticated using the provided user credentials and successfully completed the OTP verification sent to my email.

I then signed out and logged in using Carlos' credentials. When the application requested the 2FA code, I tested whether the application had properly enforced the second authentication step.

Instead of entering the OTP, I changed the URL directly to:

# /my-account

The application granted access to the protected account page without requiring the 2FA verification to be completed.

## 🎯 Lab successfully solved.

# 🧠 Key Takeaway

This lab taught me that implementing an OTP page is not enough.

The application must ensure that 2FA verification is successfully completed before allowing access to protected resources.

If a user can simply bypass the verification page and directly access /my-account, the second authentication factor has effectively been bypassed.

Another hands-on lesson in Authentication, Access Control, Web Security, and Burp Suite. 🚀

#Cybersecurity #WebSecurity #PortSwigger #Pentesting #BurpSuite #AppSec #EthicalHacking
