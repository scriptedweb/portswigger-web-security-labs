## 🧪 PortSwigger Lab: File Path Traversal

**Status:** ✅ Completed
**Category:** Path Traversal / Improper Input Validation
**Difficulty:** Apprentice

### Summary
This lab demonstrates a classic file path traversal vulnerability where a user-controlled 
parameter is used to construct a file path without adequate sanitization, allowing access 
to files outside the intended directory.

### Technique
By supplying a payload with repeated `../` sequences, it's possible to traverse up the 
directory structure and reach files well outside the application's intended file scope — 
in this case, a sensitive system file.

Example payload:
../../../etc/passwd


### Impact
- Unauthorized access to restricted files
- Potential disclosure of sensitive system or configuration data
- Could serve as a foothold for further post-exploitation activity depending on the 
  exposed content

### Root Cause
Lack of input validation/sanitization on user-supplied file paths, combined with no 
enforcement of a restricted base directory (no allowlisting or path canonicalization check).

### Remediation
- Validate and sanitize all user input used in file operations
- Use an allowlist of permitted file names/paths rather than blocklisting `../`
- Canonicalize paths and verify they remain within the intended base directory
- Run application processes with least-privilege file system access

### Reference
[PortSwigger Web Security Academy – Path Traversal](https://portswigger.net/web-security/file-path-traversal)
