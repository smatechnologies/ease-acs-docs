---
sidebar_label: 'ACSEase Operation'
---

# ACS Ease Operation

Once the sma.acs.ACSEase plugin has been registered with the OpCon system, it will be possible to perform agent and task definitions.
All definitions can only be performed using Solution Manager.

The implementation of the bundle task types requires the installation of the EASE-LOCAL, EASE-LOCAL-BUNDLE-RSJEDIT, EASE-BUNDLE-SEQ-FTP and EASE-BUNDLE-SEQ-PROMPT schedules in the local OpCon System.

The EASE-LOCAL schedule contains container jobs that are used to inject the EASE-LOCAL-BUNDLE-RSJEDIT, EASE-BUNDLE-SEQ-FTP and EASE-BUNDLE-SEQ-PROMPT sub-schedules. The sub-schedules contain ACS Ease tasks to execute the sequence of tasks within the selected bundled request. Each task in the subschedule is submitted to the Ease Datacenter for execution. It is possible to view the individual joblogs of these tasks as well as restart the individual tasks should this be required.

After inserting the schedules in the local OpCon system, the tasks in the sub-schedules should be updated to match the Ease Agent and an all days frequency definition available on the local OpCon system.  

The Ease Agent definition contains a **Debug** option which should be selected when doing trouble shooting. Selecting this field will log
all information (request and response) to the executing tasks job log. 

## Defining ACS Ease connection

The Agent definition defines the OpCon Rest-API connections to your local OpCon system and the target Ease DataCenter OpCon system.
 
This is done by adding a new ACS Ease Agent definition using Solution Manager. 

Items defined in red are required values (note : global properties are supported). 

![Defining a Connection](../static/img/agent.png)

![Defining a Connection](../static/img/agent1.png)

1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Agents**.
4.  Select **+Add** to add a new agent definition.
5.  Fill in the agent details
    - Insert a unique name for the connection.
    - Select **ACS Ease** from the **Type** drop-down list.
    - Select **General Settings**
    - Check that the NetCom Name is set to **\<Default\>** or the SMA Relay name if Relay is being used. 
    - Select **ACS Ease Settings**
    - In the **Customer Id** field enter customer number provided by the Ease DataCenter.
    - In the **Retain Log Files** field enter a value defining the number of days to retain log files (default is 30 days).
    - In the **Ease DataCenter** section
        - In the **Ease URL** field enter the host and port number provided by the Ease DataCenter (host:port).
        - In the **Ease User** field enter the user name provided by the Ease DataCenter.
        - In the **Ease User Password** filed enter the password associated with the provided Ease User.  
        - In the **Local DataCenter** section
        - In the **OpCon URL** filed enter the host and port number of the local OpCon system (host:port).
        - In the **User** field enter the user name for the local OpCon system.
        - In the **User Password** filed enter the password associated with the local OpCon User.  

6.  Save the definition changes. 
7.  Select **Communication Settings**
    Ensure that the **Requires XML Escape Sequences: User-Defined** field is set to **True**. 
    I not change the field and save the definition changes.
8.  Start the connection by selecting the **Change Communication Status** button and selecting **Enable Full Comm.**. 

## Defining tasks

The ACS Ease Connection supports the following task types:

Task Type                | Description
-------------------------|-------------------------------------
BUNDLE-RSJEDIT           | MONITOR and RSJEDIT tasks
BUNDLE-SEQ-FTP           | SEQ, COPY-RPT-OUT and RUN-FTP-OUT tasks
BUNDLE-SEQ-PROMPT        | SEQ and PROMPT tasks
COPY-DATA-TO-LTRFILE     | Copy outgoing Data File to Letter Files for FTP
COPY-RENAME-LTRFILE-OUT  | Copy or Rename Letter File for FTP
COPY-RPT-OUT             | Copy Report to Letter Files for FTP
FILEPERMS                | Update Letter File Privileges to 774
MONITOR                  | File Monitor for Incoming File       
MOVE-LTRFILE-TO-DATA     | Move incoming Letter File to Data Files
PROMPT                   | Answer a Single Prompt               
PROMPTSEQ                | Answer a Single Prompt with a SEQ    
RUN-FTP-OUT              | FTP Letter File off Symitar      
RENAME-LTRFILE-IN        | Rename Letter File Removing Prefix   
RESET                    | Reset a Single Prompt                
RSJ                      | Run Symitar Job (single-threaded)    
RSJEDIT                  | Runs Symitar Job with Edit File      
RSJMULTI                 | Run Symitar Job (multi-threaded)     
SEQ                      | Collect the SEQ of a Report and store it in a global property on the local OpCon system 
SEQ-SEND                 | Copy Specified SEQ to Reports for FTP
TRANSLATE2COMMAS         | Answer a Single Prompt containing commas

Defining tasks only requires providing the values associated with the specific task. It is possible to use global properties when defining
tasks.

### BUNDLE-RSJEDIT Task

![Defining a BUNDLE-RSJEDIT Master Job](../static/img/bundle-rsjedit.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **BUNDLE-RSJEDIT : MONITOR and RSJEDIT tasks** from the **Task Type** drop-down list.

Enter details for Task Type **BUNDLE-RSJEDIT**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the the name of the RSJ job associated with the RSJ task.
    - In the **Monitor File** field enter the monitor file name associated with the MONITOR task.
    - In the **Edit File** field enter the edit file name associated with the RSJ task.
4.  Save the definition changes. 

### BUNDLE-SEQ-FTP Task

![Defining a BUNDLE-SEQ-FTP Master Job](../static/img/bundle-seq-ftp.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **BUNDLE-SEQ-FTP : SEQ, COPY-RPT-OUT and RUN-FTP-OUT tasks** from the **Task Type** drop-down list.

Enter details for Task Type **BUNDLE-SEQ-FTP**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the the name of the RSJ job associated with the SEQ task.
    - In the **Output File** field enter the output file name associated with the COPY-RPT-OUT and RUN-FTP-OUT tasks.
    - In the **Email** field enter an email address that will receive notification when the transfer is complete.
4.  Save the definition changes. 

### BUNDLE-SEQ-PROMPT Task

![Defining a BUNDLE-SEQ-PROMPT Master Job](../static/img/bundle-seq-prompt.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **BUNDLE-SEQ-PROMPT : SEQ, and PROMPT tasks** from the **Task Type** drop-down list.

Enter details for Task Type **BUNDLE-SEQ-PROMPT**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the the name of the RSJ job associated with the SEQ task.
    - In the **Prompt Job Name** field enter the name of the RSJ job associated with this PROMPTSEQ task.
    - In the **Prompt** field enter prompt to submit.
4.  Save the definition changes. 

### COPY-DATA-TO-LTRFILE Task

![Defining a COPY-DATA-TO-LTRFILE Master Job](../static/img/copy-data-to-ltrfile.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **COPY-DATA-TO-LTRFILE : Copy outgoing Data File to Letter Files for FTP** from the **Task Type** drop-down list.
    
Enter details for Task Type **COPY-DATA-TO-LTRFILE**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Source File** field enter the source file name associated with the task.
    - In the **Output File** field enter the output file name associated with the task.
4.  Save the definition changes. 

### COPY-RENAME-LTRFILE-OUT Task

![Defining a COPY-RENAME-LTRFILE-OUT Master Job](../static/img/copy-rename-ltrfile-out.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **COPY-RENAME-LTRFILE-OUT : Copy or Rename Letter File for FTP** from the **Task Type** drop-down list.
    
Enter details for Task Type **COPY-RENAME-LTRFILE-OUT**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - select an Action from the **Action** drop-down list.
    - In the **Source File** field enter the source file name associated with the task.
    - In the **Output File** field enter the output file name associated with the task.
4.  Save the definition changes. 

### COPY-RPT-OUT Task

![Defining a COPY-RPT-OUT Master Job](../static/img/copy-rpt-out.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **COPY-RPT-OUT : Copy Report to Letter Files for FTP** from the **Task Type** drop-down list.
    
Enter details for Task Type **COPY-RPT-OUT**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Output File** field enter the output file name associated with the task.
4.  Save the definition changes. 

### FILEPERMS Task

![Defining a FILEPERMS Master Job](../static/img/fileperms.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **FILEPERMS : Update Letter File Privileges to 774** from the **Task Type** drop-down list.
    
Enter details for Task Type **FILEPERMS**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **File** field enter the letter file name whose privileges will be updated.
4.  Save the definition changes. 

### MONITOR Task

![Defining a MONITOR Master Job](../static/img/monitor.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **MONITOR : File Monitor for Incoming File** from the **Task Type** drop-down list.
    
Enter details for Task Type **MONITOR**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **File** field enter the monitor file name associated with the task.
4.  Save the definition changes. 

### MOVE-LTRFILE-TO-DATA Task

![Defining a MOVE-LTRFILE-TO-DATA Master Job](../static/img/move-ltrfile-to-data.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **MOVE-LTRFILE-TO-DATA : Move incoming Letter File to Data Files** from the **Task Type** drop-down list.
    
Enter details for Task Type **MOVE-LTRFILE-TO-DATA**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Source File** field enter the source file name associated with the task.
    - In the **Output File** field enter the output file name associated with the task.
4.  Save the definition changes. 

### PROMPT Task

![Defining a PROMPT Master Job](../static/img/prompt.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **PROMPT : Answer a Single Prompt** from the **Task Type** drop-down list.
    
Enter details for Task Type **PROMPT**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the the name of the RSJ job associated with this request.
    - In the **Prompt** field enter prompt.
    - In the **Response** field enter the response to the associated prompt.
4.  Save the definition changes. 

### PROMPTSEQ Task

![Defining a PROMPTSEQ Master Job](../static/img/prompt-seq.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **PROMPTSEQ : Answer a Single Prompt with a SEQ** from the **Task Type** drop-down list.
    
Enter details for Task Type **PROMPTSEQ**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the name of the RSJ job associated with this request.
    - In the **Prompt** field enter prompt to submit.
4.  Save the definition changes. 

### RUN-FTP-OUT Task

![Defining a RUN-FTP-OUT Master Job](../static/img/run-ftp-out.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **RUN-FTP-OUT : FTP Letter File off Symitar** from the **Task Type** drop-down list.
    
Enter details for Task Type **RUN-FTP-OUT**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Output File** field enter the output file name associated with the task.
    - In the **Email** field enter an email address that will receive notification when the transfer is complete.
4.  Save the definition changes. 

### RENAME-LTRFILE-IN Task

![Defining a RENAME-LTRFILE-IN Master Job](../static/img/rename-ltrfile-in.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACSEase** from the **Job Type** drop-down list.
    - Select **RENAME-LTRFILE-IN : Rename Letter File Removing Prefix** from the **Task Type** drop-down list.
    
Enter details for Task Type **RENAME-LTRFILE-IN**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - select an Action from the **Action** drop-down list.
    - In the **Source File** field enter the source file name associated with the task.
    - In the **Output File** field enter the output file name associated with the task.
4.  Save the definition changes. 

### RSJ Task

![Defining a RSJ Master Job](../static/img/rsj.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **RSJ : Run Symitar Job (single-threaded)** from the **Task Type** drop-down list.
    
Enter details for Task Type **RSJ**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Job Name** field enter the the name of the RSJ job associated with this request.
4.  Save the definition changes. 

### RSJEDIT Task

![Defining a RSJEDIT Master Job](../static/img/rsj-edit.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **RSJEDIT :Runs Symitar Job with Edit File** from the **Task Type** drop-down list.
    
Enter details for Task Type **RSJEDIT**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the name of the RSJ job associated with this request.
    - In the **Edit File** field enter the edit file name associated with the task.
4.  Save the definition changes. 

### RSJMULTI Task

![Defining a RSJMULTI Master Job](../static/img/rsj-multi.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **RSJMULTI : Run Symitar Job (multi-threaded)** from the **Task Type** drop-down list.
    
Enter details for Task Type **RSJMULTI**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Job Name** field enter the name of the RSJ job associated with this request.
4.  Save the definition changes. 

### SEQ Task

![Defining a SEQ Master Job](../static/img/seq.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **SEQ : Collect the SEQ of a Report** from the **Task Type** drop-down list.
    
Enter details for Task Type **SEQ**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier that will be used to create a schedule instance property containing the sequence number on the Ease Datacenter OpCOn environment. Any (.) period or (_) underscore characters are removed and the adjust identier is prefixed with SEQ-. The sequence number value is retrieved from the Ease Datacenter and stored in a global property on the local system. If the Identifier is ABC.DEF then the sequence number will be stored on the local system in a property SEQ-ABCDEF.
    - In the **Job Name** field enter the name of the RSJ job associated with this request.
    - In the **Report Name** field enter the report name associated with the task.
4.  Save the definition changes. 

### SEQ-SEND Task

![Defining a SEQ-SEND Master Job](../static/img/seq-send.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **SEQ-SEND : Copy Specified SEQ to Reports for FTP** from the **Task Type** drop-down list.
    
Enter details for Task Type **SEQ-SEND**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Seq** field enter the six digit number of the desired report.
4.  Save the definition changes. 

### STRANSLATE2COMMAS Task

![Defining a TRANSLATE2COMMAS Master Job](../static/img/translate2commas.png)
1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Master Jobs**.
4.  Select **+Add** to add a new master job definition.
5.  Fill in the task details.
    - Select the **Schedule** name from the drop-down list.
    - In the **Name** field enter a unique name for the task within the schedule.
    - Select **ACS Ease** from the **Job Type** drop-down list.
    - Select **TRANSLATE2COMMAS : Answer a Single Prompt containing commas** from the **Task Type** drop-down list.
    
Enter details for Task Type **STRANSLATE2COMMAS**. 

1.  Select the **Task Details** button.
2.  In the **Integration Selection** section, select the primary integration which is an ACSEase connection previously defined.
3.  In the **TaskConfiguration** section
    - In the **Identifier** field enter a unique identifier for the task.
    - In the **Prompt** field enter the prompt value for the job.
    - In the **Response** field enter the response with (^) that will be converted to commas (,).
4.  Save the definition changes. 
      
   
