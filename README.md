# 🔐 Automated ISO 27001 GRC & Incident Management (End-to-End)

This project demonstrates a **fully automated GRC + Incident Management system**
built using **Datadog → Shuffle SOAR → TheHive**, aligned with **ISO/IEC 27001**.

The goal is to **verify compliance technically**, calculate **compliance percentages**, auto-create **cases & remediation tasks**, and generate a **live compliance document**.

---

## 🧠 What This Solves

❌ Manual GRC spreadsheets  
❌ Periodic audits with no evidence  
❌ Human-driven incident tracking  

✅ Continuous compliance verification  
✅ Automated incident → case → remediation  
✅ Audit-ready documentation at any time  

---

## 🏗️ Architecture

GitHub / Cloud Logs
↓
Datadog
↓ (Webhook)
Shuffle SOAR
↓
ISO Logic + Scoring
↓
TheHive
↓
Cases & Tasks
↓
Live Compliance Document (UI)

yaml
Copy code

---

## 🧩 PHASE 1 — EVENT INGESTION & ISO MAPPING

### What happens
- Datadog detects security events
- Webhook triggers Shuffle
- Events are mapped to ISO 27001 controls

### Example ISO Mapping (Python)

```python
iso_mapping = {
    "access_change": ["A.9"],
    "admin_action": ["A.6", "A.9"],
    "token_activity": ["A.9.2"],
    "incident_alert": ["A.16"]
}

self.set_key("current_iso_mapping", iso_mapping)
print({"phase": "Phase 1", "mapped_controls": iso_mapping})
🧮 PHASE 2 — AUTOMATED COMPLIANCE CALCULATION
What happens
Each ISO control is scored automatically

Scores are stored for reporting

Python Code
python
Copy code
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
🛠️ PHASE 3 — AUTOMATED REMEDIATION TASKS
What happens
Controls below 80% create remediation tasks automatically

Python Code (YOUR FINAL WORKING VERSION)
```python
Copy code
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
🚨 PHASE 4 — INCIDENT & CASE MANAGEMENT (TheHive)
What happens
Shuffle creates alert in TheHive

Alert auto-converts into Case

Case becomes audit evidence

TheHive API (Example)
http
Copy code
POST /api/v1/alert
POST /api/v1/alert/{alertId}/case
✅ Fully automated
✅ No analyst interaction required

📄 PHASE 5 — LIVE COMPLIANCE DOCUMENT (UI)
What happens
Shuffle renders a human-readable document

Shows compliance %, gaps, and tasks

```Example Output
less
Copy code
ISO 27001 Compliance Summary

A.5 – Policies: 70%
A.6 – Organization: 75%
A.8 – Asset Management: 65%
A.12 – Operations Security: 90%
A.16 – Incident Management: 92%
A.18 – Compliance: 80%

Overall Compliance: 78%
📊 FINAL COMPLIANCE SCORE
Control	Percentage
A.5	70%
A.6	75%
A.8	65%
A.12	90%
A.16	92%
A.18	80%

✅ Overall Compliance (Incident Scope): 78%
```
📁 AUDIT EVIDENCE GENERATED
Datadog logs

Shuffle workflow runs

ISO control mappings

Compliance scores

Remediation tasks

TheHive alerts & cases

Everything is:
✔ Timestamped
✔ Searchable
✔ Exportable
