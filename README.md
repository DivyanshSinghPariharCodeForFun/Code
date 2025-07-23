
## 🔐 Generate Key + CSR for `*.religare.in`

Run this in your server/terminal:

### 📄 Step 1: Generate Private Key

```bash
openssl genrsa -out religare.in.key 2048
```

This creates the private key file:
`religare.in.key` (keep this safe, NEVER share it)

---

### 📄 Step 2: Generate CSR for Wildcard Cert

```bash
openssl req -new -key religare.in.key -out religare.in.csr
```

It will now ask for details. Fill like this:

| Prompt                 | Your Input                    |
| ---------------------- | ----------------------------- |
| **Country Name**       | IN                            |
| **State**              | Delhi (or your state)         |
| **Locality**           | New Delhi (or city)           |
| **Organization Name**  | Religare Ltd. (or legal name) |
| **Org Unit**           | IT or WebOps                  |
| **Common Name**        | `*.religare.in`               |
| **Email**              | your official email           |
| **Challenge Password** | Leave blank                   |

After this, you'll get:

* `religare.in.csr` → send this to CA
* `religare.in.key` → keep secure

---

## 📂 Final File Structure

```bash
/etc/ssl/religare/
├── religare.in.key     # ← private key (used in NGINX)
├── religare.in.csr     # ← send this to CA
└── religare.in.crt     # ← will come back from CA
```

(Optional: CA may also send `ca-bundle.crt` or intermediate cert)

---

## 🔁 After You Get `.crt` from CA

Your NGINX config stays the same:

```nginx
ssl_certificate     /etc/ssl/religare/religare.in.crt;
ssl_certificate_key /etc/ssl/religare/religare.in.key;
```

✅ You're now enterprise-grade with wildcard SSL.

Want me to auto-create these with no prompts (via config file)? Or help you validate `.crt` when CA gives it? Let me know.
