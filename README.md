**ULPF - Universal Log Pre-processing Framework**

A framework for parsing, normalizing, and standardizing heterogeneous security and network logs into a unified, analytics-ready representation.

**Overview**

Modern enterprise environments generate logs from a large variety of sources including firewalls, intrusion detection systems, network monitoring tools, web servers, proxy servers, and operating systems.

These sources produce logs in different formats and with different field names, making centralized analysis difficult.

**ULPF (Universal Log Pre-processing Framework)** addresses this problem by providing a modular preprocessing layer that:

- Accepts heterogeneous security and network events
- Parses source-specific log formats
- Extracts meaningful fields
- Normalizes events into a common schema
- Preserves the original raw event
- Maintains parser and processing metadata
- Provides an extensible architecture for onboarding new log sources
The framework is designed to act as a universal translation layer between raw enterprise logs and downstream systems such as SIEM platforms, data lakes, analytics engines, and AI/ML pipelines.

**Problem Statement**

Enterprise environments produce logs in many different formats:

- Syslog
- JSON
- Firewall-specific formats
- IDS/IPS alerts
- Web access logs
- Proxy access logs
- Vendor-specific formats
- Application-specific formats

Without normalization, every downstream system needs to understand each individual format.

This results in:

- High parser development effort
- Difficult log source onboarding
- Inconsistent field names
- Poor cross-source correlation
- Increased maintenance effort
- Difficulty building unified analytics

ULPF provides a common preprocessing layer to solve these problems.

**How the Code Runs**

ULPF is a command-line Python framework. It reads raw log lines from a file or standard input, identifies the log source type, routes the event to the correct parser module, and outputs a standardized JSON result.

Execution Flow:

1. Input log line is received
2. Source type is provided* using --source-type
3. Dispatcher resolves the parser
4. Parser extracts source-specific fields
5. Normalized ECS-like output is generated
6. Raw log is preserved
7. Final JSON result is printed

How to Run:

1) List supported parsers
bash
python -m ulpf --list-sources

This prints all supported canonical log types and aliases.


2) Parse a log file
bash
python -m ulpf --source-type conn.json --input-file conn.json --pretty

Example for Cisco ASA:
bash
python -m ulpf --source-type cisco_asa --input-file cisco_asa.log --pretty

Example for syslog:
bash
python -m ulpf --source-type syslog --input-file syslog.log --pretty

3) Read from standard input
If no file is provided, ULPF can read from stdin.

bash
cat conn.json | python -m ulpf --source-type conn.json

How Outputs Are Generated

For every raw log line, ULPF returns one JSON document containing:

- raw_event — the original log line
- parsed — source-specific extracted fields
- normalized — ECS-like standardized fields
- parse_status — success, partial, or error
- errors — any parse issues
- parser metadata such as:
- source_type
- parser_name
- parser_version

**Output Characteristics**

**Lossless design**
ULPF always preserves:
- the original raw log
- the parsed source event
- the normalized event

**ECS-like normalization**
The normalized section uses common fields like:
- event.*
- source.*
- destination.*
- network.*
- http.*
- dns.*
- user.*
- host.*
- observer.*
- rule.*

This makes logs easier to correlate across different sources.


**ULPF Pipeline:**

<img width="393" height="468" alt="image" src="https://github.com/user-attachments/assets/d3594314-9bc4-4a40-870b-702b170e4e77" />


