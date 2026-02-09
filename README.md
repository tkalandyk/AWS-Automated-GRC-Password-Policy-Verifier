<img width="1280" height="720" alt="Yellow and Black Modern R BSoul Playlist YouTube Thumbnail" src="https://github.com/user-attachments/assets/b2298eaf-cf01-4458-99e6-57c27cbd5d84" />

# AWS Automated GRC: Password Policy Verifier



## What this project covers
This project demonstrates **Automated GRC (GRC Engineering)** by verifying an AWS account’s **password policy configuration** directly via AWS APIs, then generating **audit-ready evidence** in **CSV + JSON**.

It’s built to replace the traditional “audit season scramble” approach (manual console clicking + screenshots + spreadsheets) with a repeatable, fast, evidence-producing workflow.

> **Environment note:** This was executed against a **live AWS account** with **real IAM users** and **AWS Identity Center (SSO) enabled** in a **test environment**. This is not a toy mock-up.

---

## 🎥 Click the Picture Below to Watch Demo Video ⬇️
[![Automated GRC: AWS Password Policy Verifier (Walkthrough Video)](https://github.com/user-attachments/assets/56ad64fd-793a-4a56-b5de-756f5fcaa127)](https://youtu.be/GPZalUoe-y8)

---
## Why traditional GRC breaks at scale
The old workflow usually looks like this:
- Log into AWS Console
- Navigate IAM settings
- Take screenshots
- Paste into Excel / GRC tool
- Repeat for every account

Problems:
- **Slow + expensive** (hours of human effort per audit cycle)
- **Error-prone** (missed settings, wrong account, wrong role)
- **Stale evidence** (configuration can change minutes after screenshots)

---

## The new way: Compliance as Code (Automated GRC)
This tool treats compliance checks like engineering:
- Pulls **live configuration** directly from AWS
- Evaluates it against defined standards
- Produces **timestamped artifacts** you can hand to auditors or internal teams

### Quantifiable business impact (realistic + defensible)
- **Evidence collection time:** reduces “manual screenshot collection” from **~30–90 minutes per account** to **seconds per run**
- **Audit readiness:** enables “run-on-demand” evidence instead of **weeks of audit prep**
- **Operational efficiency:** frees GRC + engineering from repetitive evidence tasks so they can focus on real risk reduction

(These ranges depend on number of AWS accounts, teams, and audit scope—this tool is designed to scale with those realities.)

---

## Who benefits (and how)

### GRC / Compliance
- Gets **repeatable evidence** without living in “screenshot hell”
- Can run checks anytime to stay audit-ready (not just once a year)
- Clear pass/fail outputs for rapid reporting

### DevOps / Cloud Engineers
- Receives **technical JSON output** that is easy to interpret and automate against
- Faster remediation cycles (run → fix → rerun immediately)
- Eliminates ambiguity around “what exactly is configured right now”

### Auditors
- Receives **timestamped, consistent artifacts**
- Less back-and-forth, fewer “can you re-send that screenshot” requests
- Easier sampling and verification because evidence is structured

### Executives (CISO/CTO/CEO)
- Faster audit posture visibility (quick understanding of where risk stands)
- Reduced audit disruption and labor cost
- Stronger assurance that controls are continuously verifiable

---

## What it checks (current scope)
The script retrieves and evaluates the AWS account’s IAM password policy configuration, including:
- Minimum password length
- Require symbols / numbers / uppercase / lowercase
- Password reuse prevention
- Password maximum age (if configured)
- Allow users to change their own password
- Hard expiry behavior
- **Identity Center (SSO) detection** + IAM console user count (to identify hybrid auth scenarios)

<img width="700" height="630" alt="image" src="https://github.com/user-attachments/assets/3aa8141e-0207-40f7-a667-cdc461c3e414" />


> This project is intentionally built so the compliance standards and checks can be **custom-tailored** to a company’s specific requirements (different baselines, stricter/looser thresholds, additional controls).

---

## Mapped controls (as implemented)
This implementation maps results to:
- **SOC 2 CC6.2** (Logical access security measures)
- **NIST 800-53 IA-5** (Authenticator management)

> The control mappings and thresholds can be customized per organization, audit scope, or internal risk policy.

---

## How it works (high level)
1. **Authenticate to AWS** (AWS CLI credentials / profile)
2. **Detect authentication model**
   - Checks if AWS Identity Center (SSO) is present
   - Counts IAM users and identifies IAM console users (hybrid scenario detection)
3. **Pull live policy configuration** via AWS IAM API
4. **Normalize + evaluate** settings against defined compliance standards
5. **Generate evidence artifacts**
   - CSV summary (clean + auditor friendly)

<img width="842" height="433" alt="image" src="https://github.com/user-attachments/assets/92022075-8627-4e09-838f-206f2d5daa21" />

     
   - JSON report (engineering + automation friendly)

 <img width="669" height="909" alt="image" src="https://github.com/user-attachments/assets/ef78367f-83dc-41f1-b277-3afe8295b53c" />

  ---
  
<img width="820" height="548" alt="image" src="https://github.com/user-attachments/assets/419d05e4-0201-49ba-8493-1547e49744b2" />
  

---

## Tech stack
- **Python 3**
- **boto3** (AWS SDK for Python)
- **AWS IAM + STS APIs**
- **AWS Identity Center detection** via `sso-admin`

---

## How to run
From the project directory:

```bash
python password_policy_checker.py

