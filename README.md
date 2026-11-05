# CTF PREPARATION MASTERY GUIDE
Target Date: November 12

## 1. ESSENTIAL TOOLKIT & SETUP
- **Burp Suite Community Edition:** Web traffic interception and repeater.
- **CyberChef:** The Cyber Swiss Army Knife for decoding, hashing, and XOR operations.
- **Ghidra / Cutter:** Open-source reverse engineering and decompilation suites.
- **Python + PwnTools:** Scripting exploits and automating network connections.
- **Wireshark:** PCAP file inspection and network forensics.

---

## 2. CORE DOMAINS & CHEAT SHEETS

### A. WEB EXPLOITATION
- **SQL Injection (SQLi):**
  - Test inputs with `'`, `OR 1=1--`, `UNION SELECT`.
  - Use `sqlmap -u "http://target/page?id=1" --dbs` for automated enumeration.
- **IDOR (Insecure Direct Object References):**
  - Always check if changing user IDs in URLs/JSON payloads (e.g., `/api/user/101` to `/api/user/102`) reveals unauthorized data.
- **Path Traversal:**
  - Look for file inclusion parameters: `../../../../etc/passwd`.

### B. CRYPTOGRAPHY
- **XOR Cipher:**
  - If ciphertext and key length are small, use CyberChef's XOR brute force or write a quick Python script:
    ```python
    ciphertext = b'\x1c\x08\x05...'
    for key in range(256):
        print(bytes([b ^ key for b in ciphertext]))
    ```
- **RSA Common Faults:**
  - Small $e$ ($e=3$): Cube root attack if $m^3 < n$.
  - Common modulus or weak primes: Check with RsaCtfTool.

### C. REVERSE ENGINEERING & PWN
- **Linux Command Quickref:**
  - `file binary` -> Check architecture and stripped status.
  - `checksec --file=binary` -> Check NX, PIE, Canary, RELRO.
  - `strings binary` -> Extract hardcoded flags or secrets.
- **Buffer Overflow Skeleton (Python Pwntools):**
  ```python
  from pwn import *
  p = remote('chal.ctf.net', 1337)
  payload = b'A' * 64 + p64(0x401122) # padding + target address
  p.sendline(payload)
  p.interactive()
  ```

---

## 3. 6-DAY ACTION PLAN
1. **Day 1-2:** Complete OverTheWire Bandit (Levels 0-33) for Linux terminal fluency.
2. **Day 3:** PortSwigger Academy (SQLi & XSS labs).
3. **Day 4:** Cryptohack (Modular Arithmetic & XOR tracks).
4. **Day 5:** picoCTF (Solve 5 past easy binary/pwn challenges).
5. **Day 6:** Mock CTF run using past picoCTF or TryHackMe rooms.
