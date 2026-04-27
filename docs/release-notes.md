---
title: EASE ACS release notes
description: Version history and change details for EASE ACS, including new features and improvements.
tags:
  - type/reference
  - role/automation-engineer
  - role/system-administrator
  - feature/ease-acs
sidebar_label: 'Release notes'
---

# EASE ACS release notes

## 25

### 25.0.3

### What's new

:eight_spoked_asterisk: **CON-1173**: Updated SEQ task type to retrieve SEQ value from the Ease Datacenter and store it in a global property on the local OpCon system.

:eight_spoked_asterisk: **CON-1250**: Added log file cleanup logic to the TaskProtocol module.

### 25.0.2

### What's new

:eight_spoked_asterisk: **CON-978**: Added debug mode selector to the agent definition and corrected job status checking.

### 25.0.1

### What's new

:eight_spoked_asterisk: Added support for BUNDLE-RSJEDIT, BUNDLE-SEQ-FTP, and BUNDLE-SEQ-PROMPT tasks.

### Why this matters

Bundles are implemented using sub-schedules that contain the individual Ease tasks in the correct sequences. To implement bundle tasks, additional schedules EASE-LOCAL, EASE-LOCAL-BUNDLE-RSJEDIT, EASE-LOCAL-BUNDLE-SEQ-FTP, and EASE-LOCAL-BUNDLE-SEQ-PROMPT must be installed on the local OpCon system. Machine names in the schedules and sub-schedules should be adjusted to match the local OpCon environment.

### 25.0.0

Initial release. The initial release supports multi-instance capabilities without any bundle tasks.
