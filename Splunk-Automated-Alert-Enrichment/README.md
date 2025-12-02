# **Splunk Automated Alert Enrichment Pipeline**

This project automates Tier-1 SOC alert triage using **Splunk**, **n8n**, **AbuseIPDB**, **Gemini AI**, and **Slack**.
You can use this workflow to enrich alerts, add threat-intel context, and send structured triage summaries directly to your Slack channel.

---

## **📌 Overview**

The goal of this lab project is to streamline the alert-handling process by automating enrichment steps that a Tier-1 analyst normally performs manually.

Using Splunk as the log source, n8n as the automation engine, Gemini as the enrichment assistant, and AbuseIPDB for IOC reputation lookups, this pipeline produces fast, consistent, and structured triage outputs.

---

## **🔧 Components**

### **1. Windows Event Logs**

* Forwarded to Splunk via Universal Forwarder
* Event types: Security logs, Sysmon logs (optional), Authentication events

### **2. Splunk**

* Ingests Windows logs
* Detects suspicious activity using custom correlation searches
* Sends each alert to n8n through a webhook step

### **3. n8n Workflow**

Handles the full automation pipeline:

1. **Webhook Trigger** – Pulls alert data from Splunk
2. **Data Processing** – Extracts IOCs (IP, hash, domain, username, etc.)
3. **Gemini AI Prompting** – Sends alert + IOCs for triage analysis
4. **AbuseIPDB Lookups** – Enriches IP addresses with reputation, score, categories
5. **Structured Output Formatting** – Summary, IOC enrichment, triage notes
6. **Slack Notification** – Sends the final triage package to a Slack channel

### **4. Gemini AI**

* Generates a structured triage report
* Provides severity context, reasoning, and breakdown
* Parses and organizes the enrichment data

### **5. Slack**

* Delivers final alert output to your chosen SOC/monitoring channel
* Ready for analyst review or escalation

---

## **🚀 Workflow Diagram**

```
                   +-------------------------+
                   |      Windows Host       |
                   |  (Event Logs / Sysmon)  |
                   +------------+------------+
                                |
                                | Logs (WinEvent, Sysmon)
                                v
                       +--------+--------+
                       |     Splunk      |
                       |  Index + Search |
                       +--------+--------+
                                |
                                | Alert Payload (via Webhook)
                                v
                         +------+------+
                         |    n8n      |
                         |  Workflow   |
                         +------+------+
                                |
      +-------------------------+--------------------------+
      |                         |                          |
      |                         |                          |
      v                         v                          v
+-------------+        +----------------+        +------------------+
| AbuseIPDB   |        | Gemini AI      |        | Slack Channel    |
| IP Lookup   |        | Triage Output  |        | SOC Notifications |
+------+------+        +--------+-------+        +---------+--------+
       |                         |                          |
       +----------- Enriched + AI Structured Triage -------+
                               (Sent to Slack)



```

---

## **📄 Deliverables**

* Full project documentation (PDF)
* n8n workflow export
* Splunk correlation search examples
* Gemini prompt template for consistent triage output
* IOC enrichment structure (AbuseIPDB fields + triage fields)

---

## **🎯 Learning Objectives**

By completing this project, you gain practical experience with:

* Alert triage automation
* Threat intelligence enrichment
* Splunk → n8n integration
* Webhook-based data pipelines
* Using LLMs for SOC analysis assistance
* Sending incident summaries to collaboration tools
* Engineering repeatable SOC workflows in a homelab

---

## **🧪 Environment**

This project was built entirely in a **homelab environment** for educational purposes.

---

## **💬 Feedback**

Suggestions, feedback, and improvement ideas are welcome!
This workflow can be extended into full SOAR automation, enrichment chaining, or escalation handling.