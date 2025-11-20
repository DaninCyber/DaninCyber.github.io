---
layout: post
title: "Understanding SQL Injection Attacks"
date: 2025-11-15
category: Web Security
tags: [sql, web-security, vulnerabilities, owasp]
author: Your Name
---

SQL injection is one of the most common and dangerous web vulnerabilities. In this post, we'll explore how these attacks work and how to prevent them.

## What is SQL Injection?

SQL injection occurs when an attacker can insert malicious SQL code into a query. This happens when user input is not properly sanitized or validated before being used in database queries.

### Example Vulnerable Code

Here's a common example of vulnerable code:
```python
# VULNERABLE CODE - DO NOT USE
username = request.form['username']
password = request.form['password']

query = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "'"
cursor.execute(query)
```

### The Attack

If an attacker enters `admin' OR '1'='1' --` as the username, the query becomes:
```sql
SELECT * FROM users WHERE username = 'admin' OR '1'='1' --' AND password = ''
```

This returns all users since `'1'='1'` is always true, and the `--` comments out the password check!

## Types of SQL Injection

1. **Classic SQLi** - Direct injection into queries
2. **Blind SQLi** - No visible output, requires inference
3. **Time-based Blind SQLi** - Uses database delays to infer data
4. **Union-based SQLi** - Combines results from multiple queries

## Prevention Methods

### 1. Use Parameterized Queries

The most effective defense:
```python
# SECURE CODE
cursor.execute(
    "SELECT * FROM users WHERE username = ? AND password = ?",
    (username, password)
)
```

### 2. Input Validation

- Whitelist acceptable inputs
- Reject special characters when not needed
- Use strict type checking
```python
if not username.isalnum():
    raise ValueError("Invalid username format")
```

### 3. Least Privilege

Database users should have minimal permissions needed for their function.

### 4. Use ORM Frameworks

Modern ORMs like SQLAlchemy, Django ORM, or Hibernate provide built-in protection.

## Testing for SQL Injection

Common test inputs:
- `' OR '1'='1`
- `'; DROP TABLE users; --`
- `1' UNION SELECT NULL, NULL --`

**Always test on systems you own or have permission to test!**

## Conclusion

SQL injection is entirely preventable with proper coding practices. Always use parameterized queries, validate input, and follow the principle of least privilege. Your users' data depends on it!

## Resources

- [OWASP SQL Injection Guide](https://owasp.org/www-community/attacks/SQL_Injection)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security/sql-injection)