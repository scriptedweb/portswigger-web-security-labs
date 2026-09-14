## 2FA Simple Bypass — PortSwigger Lab
# 📌 Overview

I completed the 2FA Simple Bypass lab on PortSwigger Web Security Academy using Burp Suite.

The lab demonstrated an authentication flaw where the application failed to properly enforce the second factor before granting access to a protected account page.

# 🎯 Objective

Access Carlos' account without completing the required 2FA verification.

# 🔐 Authentication Flow

The normal login process was:

Username + Password
        ↓
OTP Verification
        ↓
/my-account

I first logged in using the provided user's credentials and successfully completed the OTP verification.

# 🧪 Testing the 2FA Enforcement

I then logged out and authenticated using Carlos' credentials.

The application requested an OTP:

Username + Password
        ↓
OTP requested

Instead of entering the OTP, I directly changed the URL to:

/my-account

The application allowed me to access the protected account page.

# 💥 Impact

The application was treating the user as sufficiently authenticated before the 2FA process had been completed.

This meant that an attacker who obtained a user's username and password could potentially bypass the second authentication step by directly requesting a protected resource.

## 🧠 Key Takeaway

Showing a 2FA verification page is not enough — the server must enforce successful 2FA verification before granting access to protected resources.

A secure authentication flow should look like:

Username + Password
        ↓
Correct credentials?
        ↓
      YES
        ↓
2FA verification
        ↓
Correct OTP?
        ↓
      YES
        ↓
Create fully authenticated session
        ↓
Access protected resources

The key lesson from this lab was understanding that authentication is about what the server actually enforces, not just what the user interface appears to require.

Lab Status: ✅ Solved

#Cybersecurity #WebSecurity #PortSwigger #Pentesting #BurpSuite #Authentication #AppSec
