# PortSwigger Web Security Academy — Server-Side Parameter Pollution

## Lab: Exploiting Server-Side Parameter Pollution in a Password Reset Mechanism

Completed a PortSwigger Web Security Academy lab demonstrating how **Server-Side Parameter Pollution (SSPP)** can be exploited to compromise a password-reset workflow.

### Objective

The objective was to gain access to the administrator account without accessing the administrator's email inbox.

### Approach

I started by analyzing the normal `POST /forgot-password` request using Burp Suite Repeater.

I then tested how user-controlled input was incorporated into the application's server-side request.

#### 1. Testing parameter injection

I URL-encoded an ampersand:

```text
username=administrator%26x=y
```

The response indicated:

```text
Parameter is not supported
```

This suggested that the injected `&x=y` was being interpreted as a separate parameter by the internal API.

#### 2. Testing query-string truncation

I then tested:

```text
username=administrator%23
```

Since `%23` represents `#`, this was used to truncate the server-side query.

The response changed to:

```text
Field not specified
```

This revealed that the internal API expected another parameter called `field`.

#### 3. Identifying a valid field

I injected:

```text
username=administrator%26field=x%23
```

The application returned:

```text
Invalid field
```

This confirmed that the injected `field` parameter was being recognized.

Using Burp Intruder and the built-in server-side variable names list, I tested possible values and identified `email` as a valid field.

#### 4. Discovering the password-reset token

I inspected the application's JavaScript and identified the password reset endpoint and its `reset_token` parameter.

I then modified the request to:

```text
username=administrator%26field=reset_token%23
```

The application returned the administrator's password-reset token.

#### 5. Account takeover

I used the retrieved reset token through the password-reset endpoint, set a new password, and successfully authenticated as the administrator.

Finally, I accessed the Admin Panel and deleted the `carlos` user, completing the lab.

### Attack Chain

```text
Forgot Password
      ↓
Analyze POST /forgot-password
      ↓
Test parameter injection
      ↓
%26 → &
      ↓
Discover hidden "field" parameter
      ↓
Use %23 → # to truncate query
      ↓
Identify valid field values
      ↓
Discover reset_token
      ↓
Retrieve administrator reset token
      ↓
Reset administrator password
      ↓
Authenticate as administrator
      ↓
Complete objective
```

### Key Lessons

* Server-side parameter pollution can manipulate requests made by backend applications.
* URL encoding can be important when testing how input is parsed by different components.
* Error messages can reveal hidden backend parameters and functionality.
* JavaScript files can expose useful application logic and undocumented endpoints.
* Password-reset tokens must be protected as carefully as passwords.
* Burp Suite Repeater and Intruder are valuable for systematically testing web application behavior.

**Tools:** Burp Suite, PortSwigger Web Security Academy, Burp Repeater, Burp Intruder

**Vulnerability:** Server-Side Parameter Pollution (SSPP)

**Impact:** Password-reset token disclosure → Administrator account takeover
