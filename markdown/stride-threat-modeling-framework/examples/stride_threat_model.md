# STRIDE Threat Model

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **Project Name** | Damn Vulnerable Web Application (DVWA) 2.5 |
| **Created By** | Claude Opus 4.6 (GitHub Copilot) |
| **Created On** | 2026-05-31 |
| **Created With** | stride-threat-modeling-framework v2.4 |

## Threat Details

### STRIDE-1: SQL Injection in `/vulnerabilities/sqli/`

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **ID** | STRIDE-1 |
| **Name** | SQL Injection in `/vulnerabilities/sqli/` |
| **Severity** | Critical |
| **CVSS** | 8.7 CVSS:4.0/AV:N/AC:L/AT:N/PR:L/UI:N/VC:H/VI:H/VA:H/SC:N/SI:N/SA:N |
| **Likelihood** | Very Likely |
| **Summary** | User-controlled `id` parameter in `vulnerabilities/sqli/source/low.php` allows SQL injection due to direct string interpolation in SQL queries without prepared statements, resulting in full database compromise including credential extraction and data manipulation. |
| **Categories** | Tampering / Information Disclosure / Elevation of Privilege |
| **Attack Scenario** | 1. Attacker authenticates to DVWA with any valid user account.<br>2. Attacker navigates to `/vulnerabilities/sqli/` and submits a crafted payload such as `1' UNION SELECT user, password FROM users-- -` in the `id` parameter.<br>3. The value of `$_REQUEST['ip']` is assigned to `$id` in `vulnerabilities/sqli/source/low.php` without any input validation.<br>4. The application interpolates the payload directly into the SQL query `SELECT first_name, last_name FROM users WHERE user_id = '$id'`.<br>5. The database engine executes the injected UNION SELECT statement alongside the original query.<br>6. The application returns all usernames and MD5 password hashes from the `users` table in the HTTP response.<br>7. Attacker cracks the MD5 hashes offline using rainbow tables to obtain plaintext credentials for all accounts. |
| **Existing Controls** | Authentication required to access vulnerability modules.<br>At `medium` level, `mysqli_real_escape_string()` is applied to input.<br>At `impossible` level, PDO prepared statements with bound parameters are used. |
| **Residual Severity** | Critical |
| **Mitigations** | Use parameterized queries (prepared statements) with bound parameters for all database interactions.<br>Implement least-privilege database accounts that cannot access `information_schema` or perform administrative operations.<br>Deploy a Web Application Firewall (WAF) with SQL injection detection rules.<br>Remove verbose database error messages from HTTP responses. |
| **CAPEC** | CAPEC-66 |
| **CWE** | CWE-89 |
| **OWASP** | A03:2021 - Injection |
| **CVE** | N/A |

### STRIDE-2: OS Command Injection in `/vulnerabilities/exec/`

| <!-- Key --> | <!-- Value --> |
| --- | --- |
| **ID** | STRIDE-2 |
| **Name** | OS Command Injection in `/vulnerabilities/exec/` |
| **Severity** | Critical |
| **CVSS** | 8.7 CVSS:4.0/AV:N/AC:L/AT:N/PR:L/UI:N/VC:H/VI:H/VA:H/SC:N/SI:N/SA:N |
| **Likelihood** | Very Likely |
| **Summary** | User-controlled `ip` parameter in `vulnerabilities/exec/source/low.php` allows OS command injection due to direct string concatenation into `shell_exec()` without input validation, resulting in arbitrary command execution on the underlying server. |
| **Categories** | Tampering / Information Disclosure / Elevation of Privilege |
| **Attack Scenario** | 1. Attacker authenticates to DVWA with any valid user account.<br>2. Attacker navigates to `/vulnerabilities/exec/` and submits a crafted payload such as `127.0.0.1; cat /etc/passwd` in the `ip` parameter.<br>3. The value of `$_REQUEST['ip']` is assigned to `$target` in `vulnerabilities/exec/source/low.php` without any input validation.<br>4. The application concatenates the payload directly into the `shell_exec('ping -c 4 ' . $target)` call.<br>5. The operating system interprets the semicolon as a command separator and executes `cat /etc/passwd` after the ping command.<br>6. The output of both commands is returned in the HTTP response.<br>7. Attacker executes reverse shell command to obtain persistent interactive access to the server. |
| **Existing Controls** | Authentication required to access vulnerability modules.<br>At `medium` level, `&&` and `;` characters are removed from input.<br>At `impossible` level, strict IP address validation using numeric checks is enforced. |
| **Residual Severity** | Critical |
| **Mitigations** | Replace `shell_exec()` with language-native libraries for network operations (e.g., PHP `socket` functions).<br>Apply `escapeshellarg()` or `escapeshellcmd()` to all user-supplied values passed to system commands.<br>Implement strict allowlist input validation accepting only valid IPv4/IPv6 addresses.<br>Apply principle of least privilege to the web server process user.<br>Deploy a Web Application Firewall (WAF) with OS command injection detection rules. |
| **CAPEC** | CAPEC-88 |
| **CWE** | CWE-78 |
| **OWASP** | A03:2021 - Injection |
| **CVE** | N/A |

## Threat Summary

| ID | Severity | CVSS | Likelihood | Residual Severity | Name |
| --- | --- | --- | --- | --- | --- |
| STRIDE-1 | Critical | 8.7 | Very Likely | Critical | SQL Injection in `/vulnerabilities/sqli/` |
| STRIDE-2 | Critical | 8.7 | Very Likely | Critical | OS Command Injection in `/vulnerabilities/exec/` |
