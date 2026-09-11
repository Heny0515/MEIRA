# MEIRA

### Metrology Enforcement & Intelligence Risk Analytics

> A digital Legal Metrology enforcement and verification ecosystem designed to improve instrument verification, risk-based inspection, certificate management, and anomaly detection.

---

## 📌 Overview

**MEIRA (Metrology Enforcement & Intelligence Risk Analytics)** is a prototype digital platform for streamlining the Legal Metrology verification and enforcement process.

The system provides role-based workflows for **business owners, Legal Metrology Officers (LMOs), GATC users, and administrators**. It combines risk-based verification, physical inspection, accuracy testing, serial-number verification, certificate generation, and officer activity anomaly detection into a single platform.

The prototype is designed around the idea of moving from a conventional inspection workflow toward a more **risk-aware, transparent, and digitally traceable enforcement system**.

---

## 🎯 Problem Statement

Traditional metrology verification processes can involve multiple manual steps, making it difficult to:

* Prioritize inspections based on risk.
* Maintain a consistent verification workflow.
* Track instrument verification requests.
* Validate instrument accuracy and tolerance.
* Maintain digital verification certificates.
* Detect unusual officer activity.
* Provide a simple mechanism for certificate verification and grievance reporting.

MEIRA addresses these challenges through a centralized digital workflow.

---

## 💡 Proposed Solution

MEIRA provides an integrated workflow where:

1. An owner submits an instrument verification request.
2. The system calculates an initial risk score.
3. Administrators review and assign verification work.
4. Officers perform physical and accuracy inspections.
5. Instrument serial numbers are verified.
6. The declared risk is audited by the verifying officer.
7. Valid instruments receive a digital certificate.
8. Certificate information can be publicly verified.
9. Officer activity can be analyzed for unusual patterns.

---

## 🚀 Key Features

### 1. Role-Based Access

The prototype provides different interfaces and workflows for:

* **ADMIN**
* **LMO (Legal Metrology Officer)**
* **GATC**
* **OWNER**
* **PUBLIC**

Each role has access to functionality relevant to its responsibilities.

---

### 2. Verification Request Management

Owners can submit verification requests containing instrument and business information.

The system maintains request status throughout the verification lifecycle.

Example workflow:

```text
Request Submitted
       ↓
Risk Assessment
       ↓
Admin Review
       ↓
Officer Assignment
       ↓
Physical Inspection
       ↓
Accuracy Testing
       ↓
Serial Verification
       ↓
Risk Audit
       ↓
Certificate / Rejection
```

---

### 3. Risk-Based Verification

MEIRA calculates an inspection risk score using four parameters:

* **Workload (W)**
* **Expertise (E)**
* **Location (L)**
* **Duration (D)**

Each parameter has an associated multiplier.

The prototype uses the following calculation:

```text
Actual Risk =
min(100, round((W × Mw) + (E × Me) + (L × Ml) + (D × Md)))
```

### Risk Categories

| Risk Score | Risk Level |
| ---------- | ---------- |
| 0–24       | LOW        |
| 25–44      | MEDIUM     |
| 45–64      | HIGH       |
| 65–100     | CRITICAL   |

This allows verification requests to be prioritized according to their calculated risk.

---

## 🔍 Instrument Verification

The verification workflow contains multiple checks.

### Physical Inspection

The officer checks:

* Seal integrity
* Physical condition
* Display / zero indication

The system can reject the verification if mandatory physical requirements are not satisfied.

---

### ⚖️ Accuracy & Tolerance Testing

The officer enters:

* Declared value
* Measured value
* Permitted tolerance

The system calculates the measurement error and determines whether the instrument satisfies the specified tolerance.

If the measured error exceeds the permitted tolerance, certificate approval is blocked.

```text
Declared Value
       ↓
Measured Value
       ↓
Calculate Error
       ↓
Compare with Tolerance
       ↓
 ┌───────────────┐
 │ Within Limit? │
 └───────┬───────┘
     YES │ NO
      ↓     ↓
  Continue  Reject
```

---

## 🔢 Serial Number Verification

MEIRA includes serial-number verification using string matching.

The captured/entered serial number is compared with the registered serial number.

The prototype uses **Levenshtein distance** to identify differences.

| Result   | Condition    |
| -------- | ------------ |
| MATCH    | Exact match  |
| REVIEW   | Distance = 1 |
| MISMATCH | Distance > 1 |

This helps identify possible serial-number inconsistencies during verification.

---

## 🧾 Digital Certificate Generation

After successful verification, MEIRA generates a digital certificate containing relevant verification information such as:

* Certificate ID
* Request ID
* Instrument details
* Owner information
* Verifying officer
* Verification dates
* GPS/context information
* Evidence hash
* Declared value
* Measured value
* Tolerance
* Error
* Serial verification result
* Risk audit information

The certificate can subsequently be searched and verified through the public verification interface.

---

## 🔐 Risk Audit

Before certificate approval, the verifying officer performs a mandatory risk audit.

The officer confirms whether the calculated risk score is legitimate.

If the officer identifies a possible misdeclaration, the request can be flagged for further action.

The prototype also demonstrates a fine workflow with a **₹5,000 fine under Section 53** for the relevant prototype scenario.

---

## 🚨 Rejection Workflow

MEIRA supports rejection of verification requests when required conditions are not satisfied.

Possible rejection reasons include:

* Tolerance failure
* Broken seal
* Damaged physical structure
* Display / zero-indication issue
* Serial-number mismatch
* Misdeclared risk

This creates a traceable verification decision rather than simply approving or rejecting a request without structured reasoning.

---

## 📊 Officer Activity & Anomaly Detection

MEIRA includes a prototype anomaly-detection mechanism for officer activity.

The system groups certificate activity by:

```text
Officer + Day
```

Historical activity is used to establish a baseline.

When sufficient historical data is available, the system identifies unusually high activity using a threshold based on historical averages.

The prototype also includes synthetic activity generation to demonstrate anomaly detection during a project demo.

Example:

```text
Historical Officer Activity
          ↓
Calculate Baseline
          ↓
Compare Current Activity
          ↓
Unusual Spike?
       ↙     ↘
     YES      NO
      ↓        ↓
   Flag       Normal
```

---

## 🌐 Public Certificate Verification

MEIRA provides a public verification interface where users can search for certificate information.

The system also provides a mechanism for users to report grievances related to verification records.

---

## 📷 Camera Support

The prototype uses browser camera access for capturing instrument-related information.

It uses:

```javascript
navigator.mediaDevices.getUserMedia()
```

for camera preview.

The current prototype does **not** contain a full OCR engine such as Tesseract. Serial verification is performed using captured/entered serial information and JavaScript-based matching logic.

---

## 💾 Data Persistence

The prototype maintains application state using browser storage.

It attempts to use:

```text
window.storage
```

when available and falls back to:

```text
localStorage
```

The primary shared state contains:

* Verification requests
* Certificates
* Anomaly reviews

The state is stored using:

```text
meira-shared-state
```

---

## 🌍 Multi-Language Support

MEIRA supports three interface languages:

* 🇬🇧 English
* 🇮🇳 Hindi
* ગુજરાતી Gujarati

The selected language is stored in browser storage.

---

## 🏭 Supported Instrument Categories

### Weighing Instruments

* Electronic Platform Scale
* Price Computing Weighing Instrument
* Electronic Weighbridge
* Digital Counter Scale

### Volume Instruments

* Petrol Dispenser
* Gas Meter
* CNG Dispenser

---

## 📍 Supported Demonstration Regions

The prototype includes demonstration regions in Ahmedabad:

* Kalupur
* Vatva GIDC
* Naroda GIDC
* Sarkhej
* Maninagar
* Navrangpura
* SG Highway
* Chandkheda

---

## 👥 User Roles

| Role   | Main Responsibility                                       |
| ------ | --------------------------------------------------------- |
| ADMIN  | Manage requests, review risk and assign verification work |
| LMO    | Perform field verification and approve/reject instruments |
| GATC   | Participate in the verification workflow                  |
| OWNER  | Submit verification requests and view relevant records    |
| PUBLIC | Verify certificates and report grievances                 |

---

## 🔄 Complete System Workflow

```text
                 ┌──────────────┐
                 │    OWNER     │
                 └──────┬───────┘
                        │
                        ▼
              Submit Verification
                   Request
                        │
                        ▼
                Risk Calculation
                        │
                        ▼
                 ┌──────────────┐
                 │    ADMIN     │
                 └──────┬───────┘
                        │
                        ▼
                Officer Assignment
                        │
                        ▼
                 ┌──────────────┐
                 │     LMO      │
                 └──────┬───────┘
                        │
                        ▼
                Physical Inspection
                        │
                        ▼
                 Accuracy Testing
                        │
                        ▼
                Serial Verification
                        │
                        ▼
                   Risk Audit
                        │
                 ┌──────┴───────┐
                 │              │
                 ▼              ▼
             APPROVED        REJECTED
                 │
                 ▼
          Digital Certificate
                 │
                 ▼
          Public Verification
```

---

## 🛠️ Technology Stack

The current prototype is intentionally lightweight.

### Frontend

* HTML5
* CSS3
* JavaScript
* SVG

### Browser APIs / Storage

* Browser Camera API
* `localStorage`
* Browser-based storage interface when available

### Architecture

```text
Single-Page Web Application
          │
          ├── HTML
          ├── CSS
          └── Vanilla JavaScript
```

No external backend, framework, package manager, or database is required to run the current prototype.

---

## 📁 Project Structure

```text
MEIRA/
│
├── index.html
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── .gitignore
│
└── docs/
    ├── ARCHITECTURE.md
    ├── DEMO.md
    ├── FUTURE-SCOPE.md
    └── PROJECT-INFO.md
```

---

## ▶️ How to Run

### Option 1: Directly in Browser

1. Download or clone the repository.
2. Open the project folder.
3. Open `index.html` in a modern web browser.

### Option 2: VS Code

Open the project in VS Code and run `index.html` using a local development server such as Live Server.

No installation of Node.js, npm, React, or other frameworks is required for the current prototype.

---

## 🔑 Demo Credentials

The prototype contains predefined demonstration accounts.

| Role  | Email               | Password   |
| ----- | ------------------- | ---------- |
| ADMIN | `admin@meira.demo`  | `admin123` |
| LMO   | `lmo018@meira.demo` | `lmo123`   |
| LMO   | `lmo027@meira.demo` | `lmo123`   |
| GATC  | `gatc@meira.demo`   | `gatc123`  |
| OWNER | `owner@meira.demo`  | `owner123` |
| OWNER | `owner2@meira.demo` | `owner123` |

> **Note:** These credentials are for demonstration purposes only and must not be used in a production system.

---

## 🧪 Suggested Demo Flow

For demonstrating the complete MEIRA workflow:

```text
1. Login as OWNER
        ↓
2. Create verification request
        ↓
3. View calculated risk
        ↓
4. Login as ADMIN
        ↓
5. Review and assign request
        ↓
6. Login as LMO / GATC
        ↓
7. Perform physical inspection
        ↓
8. Perform accuracy/tolerance test
        ↓
9. Verify serial number
        ↓
10. Complete risk audit
        ↓
11. Approve verification
        ↓
12. Generate certificate
        ↓
13. Verify certificate publicly
```

---

## ❌ Failure Scenarios for Demonstration

The system can also demonstrate rejection scenarios.

### Example 1: Tolerance Failure

```text
Measured Error > Permitted Tolerance
              ↓
        Verification Failed
              ↓
           Rejection
```

### Example 2: Serial Mismatch

```text
Registered Serial ≠ Captured Serial
              ↓
        MISMATCH / REVIEW
              ↓
      Verification Decision
```

### Example 3: Physical Inspection Failure

```text
Broken Seal / Damaged Structure /
Display Issue
              ↓
        Verification Failed
```

---

## 🔮 Future Scope

The current project is a functional prototype. A
