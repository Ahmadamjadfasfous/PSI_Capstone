🕵️‍♂️ DFIR End-to-End Triage
Digital Forensics & Incident Response Project

📌 Overview
This project is a Python-based Digital Forensics & Incident Response (DFIR) tool designed to perform a complete triage on a target system or evidence folder.
It analyzes processes, files, network activity, and forensic artifacts (CSV logs), then generates a final report with visual charts to highlight suspicious activity.

⚙️ Features
🔍 Process Analysis: List running processes with PID and name.

📂 File Evidence: Extract file size, modification time, SHA-256 hash, and status (recent/normal).

🧩 Duplicate Detection: Identify duplicate files by comparing hashes.

📊 Artifact Analysis: Parse CSV logs to calculate events by type and hour.

🎨 Visualization: Generate Stacked Bar Charts showing event distribution by type and time.

🌐 Network Checks: Test if specific ports (e.g., 80) are open.

💻 System Commands: Run commands like whoami for context.

🌍 HTTP Requests: Validate responses from URLs (200, 403, 404).

📝 Final Report: Save results in JSON format inside the reports folder.

📂 Project Structure
Code
project/
│
├── src/
│   ├── main.py              # Main entry point
│   ├── data_handler.py      # CSV reading & analysis
│   ├── logic.py             # Core logic (processes, files, ports, HTTP)
│   └── utils.py             # Helper functions
│
├── data/
│   ├── sample_evidence/     # Evidence files (notes.txt, payload.bin, report.docx)
│   └── artifacts.csv        # Raw logs for analysis
│
├── reports/
│   ├── artifact_stacked.png # Generated chart
│   └── triage_report.json   # Final report
│
└── README.md                # Documentation
🚀 How to Run
Install Python 3.9+.

Install dependencies:

bash
pip install -r requirements.txt
(Required: matplotlib, psutil, hashlib, requests)

Run the tool:

bash
python src/main.py data/sample_evidence data/artifacts.csv
Outputs:

JSON report → reports/triage_report.json

Chart → reports/artifact_stacked.png

📊 Example Chart
The chart shows events grouped by hour and stacked by type:

Hour 08 → High activity (process + file_created + file_deleted).

Hour 09 → Moderate activity.

Hour 10 → Mixed events including critical ones.

Hour 11 → Low activity.

📝 Example Report (triage_report.json)
json
{
  "target_folder": "data/sample_evidence",
  "generated_at": "Sat Sep 12 05:50:00 2026",
  "process_count": 5,
  "file_count": 12,
  "recent_files": ["payload.bin"],
  "duplicate_files": {
    "abc123...": ["file1.txt", "file2.txt"]
  },
  "artifact_analysis": {
    "total_events": 24,
    "by_type": {
      "process_started": 9,
      "file_created": 8,
      "file_deleted": 7
    },
    "by_hour": {
      "08": 9,
      "09": 4,
      "10": 7,
      "11": 3
    }
  },
  "port_80_open": true,
  "whoami": "student",
  "http_checks": {
    "https://httpbin.org/status/200": "200 OK",
    "https://httpbin.org/status/403": "403 Forbidden",
    "https://httpbin.org/status/404": "404 Not Found"
  }
}
🎯 Notes
Evidence files have different roles:

notes.txt → Investigator notes.

payload.bin → Binary/malware sample.

report.docx → Formal incident report.

artifacts.csv is the main structured log file used for analysis.

All outputs are saved automatically in the reports folder.

