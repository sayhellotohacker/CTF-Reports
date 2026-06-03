
# SSRF with Filter Bypass – URL Parser Confusion via Encoded Credentials

## Summary

A **Server-Side Request Forgery (SSRF)** vulnerability was identified in the stock check feature. The application fetches data from an internal system based on a user-supplied URL. A whitelist-based anti-SSRF defense was bypassed using **URL parser confusion** combined with **double URL encoding** to access the internal admin interface and delete a user.

**Severity:** Critical  
**CWE:** CWE-918 – Server-Side Request Forgery  
**Technique:** SSRF → Filter Bypass → Internal Admin Access

---

## Technical Details

- **Vulnerable Parameter:** `stockApi`
- **Functionality:** Fetches stock data from a user-supplied URL
- **Defense:** URL hostname validated against a whitelist (only `stock.weliketoshop.net` allowed)
- **Parser Flaw:** The URL parser accepts embedded credentials and misinterprets encoded fragments

---

## Step-by-Step Exploitation

### Step 1: Identify Whitelist Behavior

Changed the `stockApi` parameter to `http://127.0.0.1/` — rejected. The application parses the URL, extracts the hostname, and validates it against a whitelist.

### Step 2: Test Credential Embedding

Supplied `http://username@stock.weliketoshop.net/` — **accepted.** The URL parser supports the `username@host` format, interpreting `stock.weliketoshop.net` as the target host.

### Step 3: Attempt Fragment Injection

Appended `#` to the username: `http://username#@stock.weliketoshop.net/` — **rejected.** The parser now treats everything before `@` differently.

### Step 4: Bypass with Double URL Encoding

Double-encoded the `#` to `%2523`:

```
http://username%2523@stock.weliketoshop.net/
```

Result: **Internal Server Error** — the server attempted to connect to `username`, confirming the parser was confused about where the hostname ends.


### Step 5: Final Payload — Access Admin & Delete User

Crafted the final payload using `localhost` with port 80 and the bypass technique:

```
http://localhost:80%2523@stock.weliketoshop.net/admin/delete?username=carlos
```

**Why this works:**
- The parser sees `stock.weliketoshop.net` as the host (passes whitelist)
- After decoding, the actual request goes to `localhost:80`
- The path `/admin/delete?username=carlos` is appended, triggering the delete action

> **[Screenshot 2: Response confirming successful deletion of user carlos]**
![](./images/picture.png)  
---

## Payload Breakdown

| Component | Purpose |
|-----------|---------|
| `localhost:80` | Internal target to access |
| `%2523` | Double-encoded `#` — confuses parser, splits host from credentials |
| `@stock.weliketoshop.net` | Whitelisted host — passes validation |
| `/admin/delete?username=carlos` | Admin action path |

---

## Impact

- **Internal Service Access:** Admin interfaces, databases, cloud metadata endpoints
- **Privileged Actions:** User deletion, configuration changes, data exfiltration
- **Bypass Anti-SSRF Controls:** Parser confusion defeats whitelist-based defenses

---

## Remediation

1. **Parse then Validate:** Fully decode and parse the URL first, then validate the resolved hostname — not the pre-parsed string.
2. **Block Credential Embedding:** Reject URLs containing `@` in the authority section.
3. **Use Allowlist with IP Resolution:** Resolve the hostname to an IP and validate the IP against the allowlist.
4. **Network Segmentation:** Restrict outbound requests from the application server at the network layer.
5. **Least Privilege:** Run internal services on non-default ports with authentication required.

---

*PortSwigger Web Security Academy lab. Demonstrates bypassing SSRF protections using URL parser inconsistencies and double encoding.*
