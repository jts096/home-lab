## Objective
Review the php source code of all attempted DVWA modules on Low difficulty. Spot vulnerabilities that enabled the exploits to work.

___
## SQL Injection
- The user's input `$id` is directly passed into the SQL query without sanitization.

![[9_1.png]]

## XSS (Reflected)
- The user's input `$_GET['name']` is directly passed into `$html` without sanitization
- The XSS protection filter is disabled

![[9_2.png]]

## Brute Force
- The user's inputs, `$user` and `$pass`, are directly passed into the SQL query, allowing SQL injection to bypass login.
- There is no lockout or waiting period after a certain number of failed login attempts.

![[9_3.png]]

## Command Injection
- The user input `$target` is directly passed into `shell_exec` without sanitization

![[9_4.png]]

## File Upload
- The code accepts any file type
- Uploaded files are stored in a directory that is accessible to anyone and the file's path, `$target_path`, is displayed back to the user. This allowed me to navigate to my .php upload and execute commands in the browser.

![[9_5.png]]
## CSRF
- The code uses GET to change the password, exposing credentials in the URL.
- No CSRF tokens are used to validate that a password change request was made by the logged-in user.

![[9_6.png]]
