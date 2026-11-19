# Password Cracking Lab — JTR & Networkwalks Tools

**Program:** Cybersecurity at Networkwalks — Week 3 Project Work
**Author:** Vipin P P ([@croissant911](https://github.com/croissant911))
**Status:** ✅ Completed

## Overview

This repo documents Week 3 of the Networkwalks Cybersecurity & Ethical Hacking program, covering two password-cracking project modules against password-protected PDF files:

- **PM1 — Password Cracking with JTR:** using John the Ripper (CLI) and Johnny (GUI) to recover a PDF's open password.
- **PM2 — Password Cracking with Networkwalks Tools:** using Networkwalks' free browser-based Hash Calculator and Password Cracker to do the same thing without installing anything.

The goal was to understand, hands-on, how password-protected files store their password as a hash, how that hash is extracted, and how a dictionary/wordlist attack recovers the original password — and why weak passwords make that trivial.

## Tools & Technologies

| Tool | Purpose |
|---|---|
| Kali Linux | Attack platform |
| `pdf2john` | Extracts a crackable hash from an encrypted PDF |
| John the Ripper (JTR) | CLI password cracking tool |
| Johnny | GUI front-end for JTR |
| `rockyou.txt` + `--rules=Best64` | Wordlist and mangling rules used for the attack |
| Networkwalks Hash Calculator | Browser-based PDF hash extractor |
| Networkwalks Password Cracker | Browser-based dictionary attack tool |

## Module 1 — Password Cracking with JTR

**Task:** Recover the password of a locked PDF using JTR (John + Johnny), on both Kali Linux (CLI) and Windows (Johnny GUI).

**Steps performed:**
1. Extracted the PDF's password hash with `pdf2john "My Locked PDF.pdf" > pdf.hash`
2. Ran John the Ripper against the hash:
   ```bash
   john --format=PDF --wordlist=/usr/share/wordlists/rockyou.txt --rules=Best64 pdf.hash
   ```
3. John matched the hash to a password from the wordlist in a few seconds.
4. Repeated the same recovery using the Johnny GUI on Windows for comparison — loaded the hash file, ran "Start new attack," and Johnny surfaced the cracked password in its results table.
5. Opened the originally locked PDF using the recovered password to confirm the crack.

*(Screenshots of the terminal session, Johnny GUI, and the unlocked PDF are in [`/screenshots`](./screenshots).)*

## Module 2 — Password Cracking with Networkwalks Tools

**Task:** Recover the password of the same locked PDF using Networkwalks' own browser-based tools instead of JTR.

**Steps performed:**
1. Uploaded the locked PDF to the [Networkwalks Hash Calculator](https://networkwalks.com/hash-calculator/), which parses the PDF locally in-browser and extracts a `$pdf$...` hash (pdf2john/hashcat-compatible format) — no file upload to a server required.
2. Copied the full hash value.
3. Pasted the hash into the [Networkwalks Password Cracker](https://networkwalks.com/password-cracker/) and ran the dictionary attack against its built-in wordlist.
4. The tool worked through the wordlist and returned the cracked password on a match.
5. Used the recovered password to unlock the PDF, confirming the result matched Module 1.

*(Screenshots of the Hash Calculator output, the Password Cracker running, and the match are in [`/screenshots`](./screenshots).)*

## Key Takeaways

- A password-protected PDF's "security" is really only as strong as the password itself — the hash extraction step is identical regardless of password strength.
- Dictionary + rule-based attacks (`rockyou.txt` + `Best64`) make short, common, or lightly-modified passwords crackable in seconds.
- Both the full CLI workflow (JTR) and a simplified browser-based workflow (Networkwalks tools) land on the same result — useful for understanding the underlying mechanics vs. having a fast practical tool.
- Reinforces why strong, unique, sufficiently long passwords matter for any password-protected document, not just logins.

## Ethical Note

This exercise was carried out on files intentionally provided for a training lab exercise, for educational purposes only, as part of a structured cybersecurity course. The techniques shown here should only be used on files/systems you own or have explicit authorization to test.

## Screenshots

```
/screenshots
  ├── jtr-cli-crack.png
  ├── johnny-gui-crack.png
  ├── networkwalks-hash-calculator.png
  ├── networkwalks-password-cracker.png
  └── unlocked-pdf.png
```

---
*Part of the [Cybersecurity at Networkwalks](https://networkwalks.com) training program.*
