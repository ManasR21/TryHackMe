
# DFIR Summary

## What is DFIR?
- DFIR stands for Digital Forensics and Incident Response.
- Involves collecting forensic artifacts from digital devices to investigate incidents.
- Helps identify attacker footprints, assess compromise extent, and restore systems.

## Need for DFIR
- Detects real attacker activity vs false alarms.
- Removes attacker presence from networks.
- Identifies breach scope and timeline.
- Discovers security loopholes.
- Understands attacker behavior.
- Facilitates sharing threat intelligence.

## Who Performs DFIR?
- Requires skills in both Digital Forensics and Incident Response.
- Forensics experts identify digital artifacts.
- IR professionals analyze security incidents.
- DFIR professionals combine both fields for holistic investigations.

## Key Concepts

### Artifacts
- Digital evidence of activities (e.g., registry keys).
- Collected from file systems, memory, and networks.

### Evidence Preservation
- Evidence must be write-protected and copied before analysis.
- Ensures original data integrity.

### Chain of Custody
- Evidence must be securely handled and transferred.
- Any mishandling weakens its credibility.

### Order of Volatility
- Capture most volatile data first (e.g., RAM before disk).
- Ensures no critical data is lost.

### Timeline Creation
- Organize artifacts chronologically to reconstruct events.

## DFIR Tools

### Eric Zimmerman's Tools
- Suite for Windows registry, file system, and timeline analysis.

### KAPE (Kroll Artifact Parser and Extractor)
- Automates artifact collection and timeline creation.

### Autopsy
- Open-source platform for analyzing data from digital media.

### Volatility
- Memory analysis for Windows and Linux systems.

### Redline
- FireEye’s tool for forensic data collection and analysis.

### Velociraptor
- Open-source platform for endpoint monitoring and response.

## Incident Response (IR) Process

### Standard Models
- **NIST (SP-800-61)**: Preparation → Detection & Analysis → Containment, Eradication & Recovery → Post-incident Activity
- **SANS (PICERL)**: Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned

### PICERL Breakdown
- **Preparation**: Setup teams, tools, and plans.
- **Identification**: Detect and confirm incidents.
- **Containment**: Limit impact with short/long-term actions.
- **Eradication**: Fully remove threats and entry points.
- **Recovery**: Restore affected services.
- **Lessons Learned**: Review and improve defenses.
