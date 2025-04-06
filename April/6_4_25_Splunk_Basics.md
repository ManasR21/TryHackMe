# Splunk Components Summary

Splunk has three main components:

1. **Forwarder**
2. **Indexer**
3. **Search Head**

---

## 1. Splunk Forwarder

- Lightweight agent installed on the monitored system.
- Collects and forwards data to Splunk.
- Consumes minimal system resources.
- Common data sources:
  - **Web servers**: Web traffic logs.
  - **Windows machines**: Event Logs, PowerShell, Sysmon data.
  - **Linux hosts**: System and service logs.
  - **Databases**: Connection requests, responses, errors.

---

## 2. Splunk Indexer

- Core component for processing incoming data.
- Parses and normalizes data into **field-value pairs**.
- Determines data types and stores them as **events**.
- Enables fast and efficient searching and analysis.

---

## 3. Splunk Search Head

- Interface used for searching indexed data.
- Uses **Search Processing Language (SPL)**.
- Sends queries to the indexer and displays results.
- Supports data visualization:
  - Tables
  - Pie charts
  - Bar charts
  - Column charts

---

# Splunk Interface Overview

When accessing Splunk, the home screen includes several panels that help navigate and use the tool efficiently.

---

## 1. Splunk Bar

- Located at the top of the interface.
- Provides:
  - **Messages**: System-level messages.
  - **Settings**: Configure Splunk instance.
  - **Activity**: Job progress review.
  - **Help**: Tutorials and documentation.
  - **Find**: Search feature.
- Allows switching between installed Splunk apps.

---

## 2. Apps Panel

- Displays all installed Splunk apps.
- **Search & Reporting** is the default app in every installation.

---

## 3. Explore Splunk Panel

- Provides quick links to:
  - Add data to Splunk.
  - Install new apps.
  - Access documentation.

---

## 4. Home Dashboard

- Displays dashboards (none by default).
- Options to:
  - Select from available dashboards.
  - Create and manage custom dashboards.
  - View personal dashboards under the **Yours** tab.
