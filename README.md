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

**ULPF Pipeline:**

<img width="393" height="468" alt="image" src="https://github.com/user-attachments/assets/d3594314-9bc4-4a40-870b-702b170e4e77" />


