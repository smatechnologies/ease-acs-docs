---
sidebar_label: 'Release Notes'
---

# Ease ACS Release Notes

## General

There are no files to create, job subtypes to add or additional software to install.

All information required for the integration is contained in the sma.acs.ACSEase plugin.

The plugin contains the dynamic screen definitions using json schemas that are used to display the connection and task definition requirements. 

It is possible to use this Agent with an on-prem OpCon installation or with a SMA Relay installation. In both instances the agent .dll files are copied into the **plugins** directory associated with the installation.

## Release 25.0.3

:eight_spoked_asterisk: **CON-1173**: Updated SEQ task type to retrieve SEQ value from the Ease Datacenter and store it in a global property on the local OpCon system.    
:eight_spoked_asterisk: **CON-1250**: Add log file cleanup logic to TaskProtocol module..

## Release 25.0.2

:eight_spoked_asterisk: **CON-978**: Add debug mode selector agent definition and correct job status checking.
  
## Release 25.0.1

Added support for BUNDLE-RSJEDIT, BUNDLE-SEQ-FTP and BUNDLE-SEQ-PROMPT tasks.

Bundles are implemented using sub-schedules that contain the individual Ease tasks in the correct sequences. 

To implement bundles tasks, additional schedules EASE-LOCAL, EASE-LOCAL-BUNDLE-RSJEDIT, EASE-LOCAL-BUNDLE-SEQ-FTP and EASE-LOCAL-BUNDLE-SEQ-PROMPT schedules must be installed on the local OpCon system. The machine names in the schedules and sub-schedules should be adjusted to match the local OpCon environment.
 
## Release 25.0.0

Initial Release.

The initial release supports multi-instance capabilities without any bundle tasks. 





