# Task 2: Phishing Email Analysis Report

This report follows the 8-step guide from the internship task to analyze a sample phishing email.

### 1. Obtain a sample phishing email
* **Action:** The sample `お問合わせありがとうございます (1).eml`  was used.The analysis was performed using the email's raw header and body, as seen in Gmail's "Original message" view  and an online header analyzer.

### 2. Examine sender's email address for spoofing
* **Tool Used:** Gmail "Original message" view.
* **Finding:** The `From:` field is **`ダンスS&E <info@dance-s-and-e.com>`**.
* **Analysis:** The sender's email address is not spoofed.

### 3. Check email headers for discrepancies
* **Tool Used:** Online header analyzer (MXToolbox) and Gmail's "Original message" view.
* **Finding:** The header analysis clearly shows:
    * **`SPF:`** **`PASS`** with IP `163.44.185.107`
    * **`DMARC:`** **`'PASS'`**
* **Analysis:** This is the key discrepancy. The email **passes all authentication checks**, proving it was sent from a legitimate server. The headers also show it was sent "Using PHPMailer 6.9.3", confirming it's a **Content Injection Attack** via the website's contact form.

### 4. Identify suspicious links or attachments
* **Tool Used:** Gmail screenshot of the email body.
* **Finding:** The body contains the link: `http://fintellect.in/index.php?jtolug`.
* **Analysis:** The link is suspicious as it uses insecure `http` and points to an unrelated domain.

### 5. Look for urgent or threatening language in the email body
* **Tool Used:** Gmail screenshot of the email body.
* **Finding:** The translated text shows a financial lure: `*** 💳 You have received a $3,827.00 credit to your account... Please confirm the operation...`.
* **Analysis:** This is a **social engineering** lure using the promise of money to create urgency.

### 6. Note any mismatched URLs
* **Tool Used:** Comparison of Step 2 and Step 4 findings.
* **Finding:** There is a clear **mismatch**:
    * **Sender Domain:** `dance-s-and-e.com`
    * **Link Domain:** `fintellect.in`
* **Analysis:** This is a critical red flag.

### 7. Verify presence of spelling or grammar errors
* **Tool Used:** Gmail screenshot of the email body.
* **Finding:** The email contains a major **contextual error**: it's a mix of a financial scam in English and a standard auto-reply in Japanese.
* **Analysis:** This confirms the attacker's message was "injected" into a legitimate website's contact form.

### 8. Summarize phishing traits found in the email
* **Summary:** This is a **Content Injection Attack**. The attacker exploited a legitimate website's contact form, which is why the email **passed SPF and DMARC**. The attack was identified by the **social engineering lure** (a $3,827.00 credit), the clear **URL mismatch** (`dance-s-and-e.com` vs. `fintellect.in`), and the **contradictory content** (English scam + Japanese auto-reply).
