# SSRF — Discovering an Internal Administrator IP with Burp Suite Intruder

I completed another PortSwigger Web Security Academy lab on **Server-Side Request Forgery (SSRF)**. This lab introduced a different twist: using **Burp Suite Intruder** to help identify the last octet of an administrator's internal IP address.

## What I Did

I started by intercepting the stock API request using **Burp Suite**.

The request contained an internal IP address in the `stockApi` parameter. Instead of manually testing each possible IP address, I used **Burp Suite Intruder** to automate the process.

I highlighted the last octet of the administrator's IP address as the payload position and configured the payload type as **Number**.

The range was configured as:

* Start: `1`
* End: `225`
* Step: `1`

Intruder then tested the values across the specified range, allowing me to identify the administrator's internal IP address based on the application's responses.

After identifying the administrator's IP address, I was able to access the admin page through the SSRF vulnerability.

To complete the lab, I copied the delete URL/request patterns for the **Carlos** and **Wiener** accounts from the administrator page and used them to delete both accounts.

## What I Learned

This was my **first practical experience using Burp Suite Intruder to test a range of IP addresses**, and it was an eye-opener.

The main lessons I took away were:

* SSRF can be used to reach internal network resources.
* Internal IP addresses may not be directly accessible from an attacker's machine.
* Burp Suite Intruder can automate repetitive testing.
* Numeric payloads can be useful when testing a range of values.
* SSRF combined with internal network discovery can expose resources that were not intended to be publicly accessible.

Another lab completed and another practical skill added to my cybersecurity journey. 🚀

#Cybersecurity #WebSecurity #PortSwiggerAcademy #SSRF #BurpSuite #Pentesting #WebSecurity
