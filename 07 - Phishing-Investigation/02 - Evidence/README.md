# Lab 07 Evidence Folder

This folder contains all screenshots and artifacts collected during the phishing investigation and detection engineering lab.

## Evidence Index

### 1. Detection Rule Deployment
**File**: `detection-rule-enabled.png`
**Description**: Shows the custom analytics rule "Custom Phishing URL Detection - Lab07" is in Enabled status and actively monitoring Microsoft Defender for Office 365 alerts.
**Proves**: Ability to deploy and configure detection rules in Microsoft Sentinel.

### 2. Detection Logic
**File**: `kql-rule-logic.png`
**Description**: Screenshot of the KQL query used in the custom rule. 
Uses base SecurityAlert schema to ensure compatibility in low-data environments.
**Proves**: KQL proficiency and detection engineering skills.

### 3. Threat Hunt Results
**File**: `threat-hunt-no-results.png`
**Description**: Results of proactive threat hunt for phishing alerts in the last 7 days.
**Finding**: 0 results. Indicates tenant is currently secure with no active phishing campaigns.
**Proves**: Ability to conduct threat hunting and properly document negative findings.

## Methodology
All evidence was collected from Microsoft Sentinel during August 2026 in a home lab environment.

