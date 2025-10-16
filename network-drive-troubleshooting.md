## 🧾 Ticket Summary

**Ticket ID:** 014  
**User:** CORP\Ife  
**Date:** October 16, 2025  
**Reported Issue:**  
> "I can't access the shared folder on our Accounting server. It says the network path was not found."

---

## 🛠️ Environment

- **Company Name:** CORP Inc.  
- **Domain Name:** CORP.local  
- **File Server:** ACCT-SERVER  
- **Server IP Address:** 192.168.10.10  
- **DNS Server:** 192.168.1.1  
- **User Account:** CORP\Ife  
- **Share Path:** `\\ACCT-SERVER\SharedDocs`

---

## 🔍 Troubleshooting Steps

### Step 1: Confirm Scope of the Issue

- Asked CORP\Ife if other users were experiencing the same problem.
- Confirmed: **Only CORP\Ife** is affected. Others can access the shared folder.

### Step 2: Test Network Connectivity

- Remotely accessed CORP\Ife’s system.
- Verified internet access: working.
- Ran:

  ```bash
  ping ACCT-SERVER
````

* **Result:** "Ping request could not find host ACCT-SERVER."

* Tried pinging the server by IP:

  ```bash
  ping 192.168.10.10
  ```

  * **Result:** Success

📌 **Conclusion:** The computer can reach the server by IP, but name resolution is failing (likely DNS issue).

---

### Step 3: Check Local DNS Resolution

* Ran:

  ```bash
  nslookup ACCT-SERVER
  ```

  * **Result:** DNS request timed out

* Suspected hardcoded name resolution issue.

* Opened the `hosts` file:

  ```
  C:\Windows\System32\drivers\etc\hosts
  ```

* Found incorrect entry:

  ```
  192.168.10.99 ACCT-SERVER
  ```

* Removed the line and saved the file.

---

### Step 4: Flush DNS Cache

* Ran:

  ```bash
  ipconfig /flushdns
  ```

* Retested:

  ```bash
  ping ACCT-SERVER
  ```

  * **Result:** Success

---

### Step 5: Remap the Shared Drive

* Removed old mapping:

  ```bash
  net use * /delete
  ```

* Reconnected using:

  ```bash
  net use \\ACCT-SERVER\SharedDocs /user:CORP\Ife
  ```

✅ Network drive was accessible again.

---

## ✅ Resolution

* The issue was caused by a hardcoded, incorrect entry in the local `hosts` file.
* After removing it, flushing DNS, and reconnecting the drive, the issue was resolved.

---

## 🔁 Follow-Up Actions

* Verified DNS settings were set to internal DNS: `192.168.1.1`
* Reminded user not to modify system files like `hosts` without IT guidance
* Logged the fix and closed the ticket

---

## 📘 Lessons Learned

* If server access by IP works but name does not, suspect DNS
* The `hosts` file overrides DNS — always check it for hardcoded values
* Use tools like `ping`, `nslookup`, and `ipconfig` for efficient diagnostics

---

## 🧰 Tools/Commands Used

```bash
ping ACCT-SERVER
ping 192.168.10.10
nslookup ACCT-SERVER
ipconfig /flushdns
net use * /delete
net use \\ACCT-SERVER\SharedDocs /user:CORP\Ife
```

---

## 🧠 Reflection

> This lab reflects a realistic issue that IT Support professionals face often. It demonstrates my understanding of DNS, user account management, basic networking tools, and troubleshooting process. I documented it here to show my ability to resolve endpoint issues independently.

````

---

## ✅ 2. Update your `README.md`

Add this section to your `README.md` so it links to your lab:

```markdown
## 🔬 Labs

- [Network Drive Not Accessible – DNS Issue Lab](./labs/network-drive-troubleshooting.md)
````

You can also keep or add your section like this:

```markdown
## 🛠️ Contents

- Troubleshooting exercises covering Windows and network issues
- Ticket triage and incident handling simulations
- Security basics and best practices labs
- Study notes, tips, and summaries
```

---

## ✅ 3. Organize Your Repo Like This:

Here’s how to organize your GitHub folders:

```
Google-it-labs/
│
├── README.md
├── labs/
│   └── network-drive-troubleshooting.md
│   └── printer-issues.md        # (optional: create later)
│
├── study-notes/
│   └── dns-basics.md            # (optional: create later)
│   └── ports-and-protocols.md   # (optional)
│
├── images/
│   └── network-drive-lab/
│       └── ping-failure.png
│       └── hosts-file-before.png
│       └── fixed-drive.png
```
