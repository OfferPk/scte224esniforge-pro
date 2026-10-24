# SCTE224ESNIForge Pro (v1.0.0)

### SCTE 224 (ESNI) Event Scheduling, Program Rights, Blackout & Alternate Content Studio

---

## Overview

**SCTE224ESNIForge Pro** is an engineering utility and command-line tool built for broadcast playout engineers, live sports OTT streaming architects, Regional Sports Networks (RSNs), and FAST channel operators. It provides automated XML generation, audience entitlement simulation, and SCTE-35 in-band bridge synchronization for:

- **ANSI/SCTE 224 (2018 / 2021\)**: Event Scheduling and Notification Interface (ESNI)  
- **ANSI/SCTE 35 (2024)**: Digital Program Insertion (Tag 0x02 Blackout Override)  
- **ANSI/SCTE 236**: Content Identification & Metadata (EIDR / Ad-ID)  
- **Apple HLS (RFC 8216bis)**: Dynamic `#EXT-X-DATERANGE` Alternate Content Ingest

---

## Core Capabilities

1. **Normative SCTE 224 XML Generator**:  
   - Synthesizes `Media`, `MediaPoint`, `ViewingPolicy`, and `Audience` XML documents conforming strictly to `urn:scte:224:2018`.  
   - Formats temporal durations as ISO 8601 `xs:duration` strings (`PT7200S`).  
2. **Edge Audience Entitlement Simulator**:  
   - Evaluates incoming viewer session profiles (Country, Nielsen DMA, Postal Code, Device Type) against multi-tier exclusion boundaries.  
   - Issues deterministic playout decisions: `BLACKOUT` (Slate / 403), `ALTERNATE_CONTENT` (Regional stream splice), or `PASS_THROUGH` (Primary stream).  
3. **SCTE-35 In-Band Blackout Bridge**:  
   - Maps ESNI schedule triggers into SCTE-35 `time_signal` and `segmentation_descriptor` (Tag 0x02, type 0x18 Blackout Override) metadata.  
   - Generates production-ready Apple HLS `#EXT-X-DATERANGE` tags.  
4. **10-Point Normative Compliance Auditor**:  
   - Validates XML namespaces, `matchSignal` tags, ISO 8601 duration syntax, ViewingPolicy actions, geographic demarcation, and playout lead times.  
5. **Standalone Python CLI (`esni-cli.py`)**:  
   - Headless schedule XML generation and viewer entitlement evaluation for automated CI/CD and edge playout microservices.

---

## Getting Started

### Web Studio

Open `source-code/index.html` in any modern web browser. Operates 100% locally with zero external network dependencies.

### Command-Line Interface

\# Generate SCTE 224 MediaPoint XML

python3 build/esni-cli.py schedule \--media-point-id "urn:sports:mp-1" \--duration 7200 \--action "Blackout"

\# Evaluate viewer entitlement

python3 build/esni-cli.py evaluate \--country "GB" \--dma "803" \--postal "SW1A 1AA" \--device "SmartTV"

### Automated Testing

python3 test\_esni.py