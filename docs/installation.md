---
sidebar_label: 'Installation'
---

# Ease ACS Installation

Download the ACS Ease software from the SMA FTP Site.
Location will be in
**/OpCon Releases/Integrations/Ease/** 
Select the required version.

- Unzip the ACSEase.zip file.
- On-prem customers 
  Copy the ACSEase directory to the \\SAM\\plugins directory
- Cloud customers
  Copy the ACSEase directory to the \\Relay\\plugins directory

Version 25.0.3
- Unzip the InsertEaseWorkflows.zip file into a temporary directory.
- Execute the EaseInsertApi.exe program which contains the workflows definitions and uses the OpCon Rest-API to insert the
  workflows. Please note that before using this program, the EASE-LOCAL schedules should not exist in the target system.

  It is possible to change the schedule names by entering a value other than EASE-LOCAL for the --sched-name argument. 
  Remember that this value must match the local schedule name in the agent definition.  

  The program has five arguments :

    --host-address `<host address>`           the address of the OpCon system (i.e. PROD - no https, just the name)
    --host-port `<host port>`                the port number of the OpCon Rest-API (i.e. 443)
    --api-token `<token>`                     an authentication token for the OpCon API
    --sched-name EASE-LOCAL                 the name of the main Ease local schedule to create
    --ease-agent `<ease agent>`               the Ease agent to be used


Version 25.0.1
- Use Deploy to insert the workflow \\workflows\\EASE-LOCAL.json into the local OpCon system.
  
  - Edit the EASE-LOCAL.json file 
    - changing the primary machine name to match the target OpCon system.
    - changing the userid used to execute the tasks.
  - Import the changed EASE-LOCAl.json file into Deploy using the **File Import** function.
  - Deploy the EASE-LOCAL schedule to the target OpCon system (the schedule includes the required sub-schedules).  

