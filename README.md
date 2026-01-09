# 🔐 Automated GRC & Incident Management Platform (ISO/IEC 27001)

**Automated Security Compliance, Incident Response & Continuous Assurance**

This project demonstrates an **end-to-end Governance, Risk & Compliance (GRC) automation platform** that ingests live security telemetry, maps events to **ISO/IEC 27001 controls**, calculates compliance coverage, auto-creates incidents and remediation tasks, and generates an **audit-ready compliance document** — fully orchestrated using **Shuffle SOAR**.

The solution proves how **manual GRC work can be eliminated** and replaced with **continuous, technically verifiable compliance**.

---

## ⭐ Key Highlights

- ✅ Live security event ingestion  
- ✅ Automated ISO/IEC 27001 control mapping  
- ✅ Continuous compliance percentage calculation  
- ✅ Automatic incident & case creation  
- ✅ Remediation task planning  
- ✅ Audit-ready compliance document generation  
- ✅ UI-based visibility (no spreadsheets, no manual work)

---

## 🧠 Why This Project Matters

Traditional GRC implementations suffer from:

- Manual evidence collection  
- Spreadsheet-based tracking  
- No technical verification  
- Audit fatigue year after year  

This project directly answers two critical GRC questions:

> **How do we technically verify compliance?**  
> **How do we reduce manual, repetitive GRC work year after year?**

---

## 🏗️ Architecture Overview

### Tools Used

- **Datadog** – Live log & security event detection  
- **Shuffle SOAR** – Orchestration & automation  
- **TheHive** – Incident & case management  
- **Python** – Compliance logic & scoring  
- **ISO/IEC 27001** – Control framework  

### Data Flow

Security Events
↓
Datadog (Detection)
↓
Shuffle Webhook
↓
ISO Control Mapping
↓
Compliance Scoring Engine
↓
TheHive (Alerts → Cases)
↓
Audit-Ready Compliance Document (UI)


---

## 🧪 Two Complementary Prototypes

### 🔴 1. Online (Live) Prototype

- Live log ingestion using Datadog  
- Events routed into Shuffle workflows  
- Automated ISO/IEC 27001 control mapping  
- Auto-created incidents and cases (TheHive)  
- Real-time compliance percentage calculation  
- Human-readable compliance document rendered in Shuffle UI  

**Use Case:**  
Continuous monitoring, SOC automation, real-time compliance

---

### 🟢 2. Offline / Audit-Ready Prototype

- Simulated audit inputs  
- Deterministic compliance scoring  
- Gap identification & remediation planning  
- Repeatable outputs (ideal for audits)  

**Use Case:**  
Audits, assessments, demos, certifications

---

## 🧩 Automation Phases (End-to-End)

---

## 🧩 Phase 1 — Event Ingestion & ISO Control Mapping

### What Happens
- Datadog detects security-relevant activity
- Webhook triggers Shuffle workflow
- Events are mapped to ISO/IEC 27001 controls

### Example Python Mapping Logic

```python
iso_mapping = {
    "access_change": ["A.9"],
    "admin_action": ["A.6", "A.9"],
    "token_activity": ["A.9.2"],
    "incident_alert": ["A.16"]
}

self.set_key("current_iso_mapping", iso_mapping)

print({
    "phase": "Phase 1",
    "mapped_controls": iso_mapping
})
```
🧮 Phase 2 — Automated Compliance Calculation
What Happens

Each ISO control is scored automatically

Compliance snapshot is stored for reporting

Python Logic
```
iso_scores = {
    "A.5": 70,
    "A.6": 75,
    "A.8": 65,
    "A.12": 90,
    "A.16": 92,
    "A.18": 80
}

self.set_key("compliance_snapshot", iso_scores)

overall = sum(iso_scores.values()) / len(iso_scores)

print({
    "phase": "Phase 2",
    "overall_compliance": round(overall, 2),
    "scores": iso_scores
})
```

🛠️ Phase 3 — Automated Remediation Planning
What Happens

Controls below threshold automatically generate remediation tasks

Tasks are tracked as compliance gaps

Final Working Python Logic
```
tasks = []

snapshot = self.get_key("compliance_snapshot", {})

for ctrl, score in snapshot.items():
    try:
        score = float(score)
    except:
        continue

    if score < 80:
        tasks.append({
            "control": ctrl,
            "task": f"Remediate ISO 27001 control {ctrl}",
            "priority": "High",
            "status": "Open"
        })

self.set_key("iso_remediation_tasks", tasks)

print({
    "phase": "Phase 3",
    "tasks_created": len(tasks),
    "tasks": tasks
})
```
🚨 Phase 4 — Incident & Case Management (TheHive)
What Happens

Shuffle creates alerts in TheHive

Alerts are automatically promoted to cases

Each case becomes formal audit evidence

TheHive API Endpoints Used
```
POST /api/v1/alert
POST /api/v1/alert/{alertId}/case
```
✅ Fully automated
✅ No analyst intervention required

📄 Phase 5 — Live Compliance Document (UI)
What Happens

Shuffle generates a human-readable compliance document

Shows compliance %, gaps, and remediation tasks

Rendered directly in the Shuffle UI

Example Output
```
ISO 27001 Compliance Summary

A.5 – Policies: 70%
A.6 – Organization: 75%
A.8 – Asset Management: 65%
A.12 – Operations Security: 90%
A.16 – Incident Management: 92%
A.18 – Compliance: 80%

Overall Compliance: 78%
```
## 📊 ISO/IEC 27001 Compliance Coverage (Incident Scope)

| ISO Control | Description | Compliance |
|------------|-------------|------------|
| A.5 | Information Security Policies | 70% |
| A.6 | Organization of Information Security | 75% |
| A.8 | Asset Management | 65% |
| A.12 | Operations Security | 90% |
| A.16 | Incident Management | 92% |
| A.18 | Compliance | 80% |

> **Overall Compliance Score (Incident Scope): 78%**

## 📁 Audit Evidence Generated

The platform automatically generates and maintains **complete, verifiable audit evidence** across the entire incident lifecycle.

### 🔍 Evidence Sources

- 🟢 **Datadog Logs**  
  Security events and telemetry captured in real time

- 🔁 **Shuffle Workflow Executions**  
  Full orchestration trails with inputs, outputs, and timestamps

- 🧩 **ISO 27001 Control Mappings**  
  Technical linkage between events and compliance controls

- 📊 **Compliance Score Snapshots**  
  Control-wise and overall compliance percentages

- 🛠️ **Remediation Task Plans**  
  Auto-generated actions for controls below threshold

- 🚨 **TheHive Alerts & Cases**  
  Incidents tracked, classified, and promoted to cases

---

### ✅ Evidence Characteristics

All generated evidence is:

✔ **Timestamped** – Verifiable chronology  
✔ **Searchable** – Fast audits & investigations  
✔ **Exportable** – Ready for auditors & certifications  
✔ **Audit-Ready** – No manual preparation required  

> This eliminates spreadsheets, screenshots, and last-minute audit panic.

---

## 🧭 Future Enhancements

Planned improvements to extend compliance coverage and operational maturity:

- 📈 **SLA & KPI Tracking** (MTTD, MTTR, response compliance)
- 🧠 **Risk Register Integration** (incident → risk linkage)
- ⚡ **Auto-closure of Low-Risk Cases**
- 🌐 **Multi-Framework Support**  
  (SOC 2, NIST, GDPR, CIS Controls)
- 📤 **One-Click ISO Audit Export**  
  (PDF / ZIP evidence bundle)

---

## 🧑‍💻 Author

**Tagur Krishna Nethipudi**  
🔐 Security | 📋 GRC | ⚙️ SOAR Automation  

- GitHub: [https://github.com/Tagurkrishna](https://github.com/Tagurkrishna)

> Built to demonstrate how **compliance can be continuous, technical, and automated** — not manual and reactive.
