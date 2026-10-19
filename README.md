# SOC Lab 001: Suspicious Login Investigation

## Overview
A beginner SOC analyst portfolio project using Splunk Enterprise to investigate simulated authentication logs, identify repeated failed logins, and examine a successful login following multiple failures.

## Objectives
- Ingest CSV authentication logs into Splunk.
- Use Splunk Search Processing Language (SPL) to filter and analyze events.
- Identify repeated failed login attempts by source IP.
- Reconstruct a login timeline.
- Document findings in a preliminary incident report.

## Tools
- Splunk Enterprise
- Splunk Search Processing Language (SPL)
- Windows 10
- GitHub

## Dataset
This project uses eight simulated authentication events. The IP addresses are reserved for documentation and examples; they do not identify real attackers.

## Key Findings
- Eight authentication events were ingested successfully.
- Five failed login events were identified.
- `203.0.113.45` generated three failed attempts followed by a successful login for `jbrown`.
- `198.51.100.22` generated two failed attempts for `admin`.
- The suspicious login sequence warrants further investigation but does not independently prove account compromise.

## Example SPL Queries

### Failed login analysis
```spl
source="auth_logs.csv" status="failed"
```

### Failed logins by source IP
```spl
source="auth_logs.csv" status="failed"
| stats count by src_ip
| sort - count
```

### Authentication timeline
```spl
source="auth_logs.csv" username="jbrown"
| sort 0 _time
| table _time username src_ip status
```

## Investigation Documentation
- Investigation notes: `SOC-Lab-001-Investigation-Notes.txt`
- Incident report: `SOC-Lab-001-Incident-Report.txt`
- Sample data: `auth_logs.csv`

- Failed login analysis evidence: [View screenshot](evidence-failed-logins.png)
- 
## Skills Demonstrated
- Log ingestion and analysis
- SPL filtering and aggregation
- Authentication event triage
- Source IP analysis
- Timeline reconstruction
- Evidence-based incident reporting

## Limitations
This is a simulated learning exercise, not a production security investigation. No real compromise was detected or confirmed.

## Author
Tyresse Bracy — Aspiring SOC Analyst
