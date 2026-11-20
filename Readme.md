# Module 09: Enterprise Exchange Online & Defender for Office 365 Mail Security Lab

**Tenant:** `ApexModernWork.onmicrosoft.com`  
**Architect:** Varun Mahajan (`varun25293`)  
**Focus Areas:** Microsoft Defender for Office 365 (Plan 1), Anti-Phishing Impersonation Protection, Safe Links Time-of-Click URL Detonation, Safe Attachments Dynamic Delivery, and Exchange Online Message Trace Forensics.

---

## Architecture & Defense-in-Depth Flow

```text
Inbound / Internal Email & Teams Messages
        │
        ▼
┌───────────────────────────────────────────────────────────────────┐
│ Layer 1: Anti-Phishing & Executive Impersonation Policy           │
│ • Policy: Apex Executive AntiPhishing Policy (Priority 0)         │
│ • Threshold: 2 - Aggressive | User & Owned Domain Protection: On  │
│ • Spoof & Mailbox Intelligence: On → Action: Quarantine           │
└───────────────────────────────────────────────────────────────────┘
        │
        ▼
┌───────────────────────────────────────────────────────────────────┐
│ Layer 2: Safe Links (Time-of-Click URL Rewriting & Detonation)    │
│ • Policy: Apex Corporate SafeLinks Policy                         │
│ • Coverage: Exchange Email (Internal/External), Teams & O365 Apps │
│ • Enforcement: Real-Time Scanning + Wait Before Delivery +        │
│   Click-Through to Original URL Blocked                           │
└───────────────────────────────────────────────────────────────────┘
        │
        ▼
┌───────────────────────────────────────────────────────────────────┐
│ Layer 3: Safe Attachments (Hypervisor Sandbox Detonation)         │
│ • Policy: Apex Corporate SafeAttachments Policy                   │
│ • Mode: Dynamic Delivery (Immediate Body + Sandboxed Attachment)  │
│ • Redirect: admin@ApexModernWork.onmicrosoft.com (AdminOnlyAccess)│
└───────────────────────────────────────────────────────────────────┘
        │
        ▼
┌───────────────────────────────────────────────────────────────────┐
│ Layer 4: SOC Operations, Quarantine & Exchange Message Trace      │
│ • Audit & Forensics: Exchange Admin Center Message Trace          │
│ • Tracks Delivered, Failed, and Undeliverable Mail Flow Events    │
└───────────────────────────────────────────────────────────────────┘
