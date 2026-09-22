# OS Command Injection — Simple Case

I completed another PortSwigger Web Security Academy lab on **OS Command Injection**.

## What I Did

The application had a stock-checking feature that used a `stockId` parameter.

I intercepted the request and sent it to **Burp Suite Repeater** for testing.

I modified the `stockId` parameter and used:

```text id="7k2qwm"
1|whoami
```

The `|` character was used to separate the original value from the injected operating system command.

The `whoami` command asks the operating system to identify the user under which the command is running.

The successful response confirmed that the application was vulnerable to **OS command injection**, allowing me to complete the lab.

## Key Lesson

OS command injection occurs when an application passes user-controlled input into an operating system command without properly preventing command injection.

The basic flow was:

```text id="6h4q1p"
User input
    ↓
stockId parameter
    ↓
Application processes the input
    ↓
OS command
    ↓
Injected command executes
```

### Tools Used

* Burp Suite Repeater
* PortSwigger Web Security Academy

Another lab completed and another vulnerability understood through hands-on practice. 🔐

#Cybersecurity #WebSecurity #PortSwigger #Pentesting #BurpSuite #OSCommandInjection
