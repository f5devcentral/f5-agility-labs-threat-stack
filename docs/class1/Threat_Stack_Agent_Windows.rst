Threat Stack Windows Agent
==========================

Deploying the Threat Stack Windows Agent 
----------------------------------------

Threat Stack automatically walks customers through an Agent install on the **Servers** page. Log into Threat Stack > Click **Servers**. The **Servers** page displays. 

Select **Agent 2.x.** The + Add New Server dialog displays. Proceed to the set of instructions below, specific to your **Windows Sever 2012 or above**. 

*Challenge 7 – Install the Threat Stack Windows Agent*

Let’s begin by configuring some environmental variables for a streamlined lab. Let’s open **PowerShell**

.. code-block::

   $Env:MY_DEPLOY_KEY="979d8df5efe295d73734109b121a33865429ebbd2a8d7ede66147404f993c3bbab4466a0" 
   $Env:MY_HOSTNAME="StudentN-Windows" 

.. note::

   **Warning**: Use only the command provided to install the Threat Stack Linux Agent. Using UDF, establish a Terminal session with the host labelled,      “Windows” 
   
   
Sysmon Install
--------------

Run the following commands from powershell/terminal:

.. code-block::

   wget https://download.sysinternals.com/files/Sysmon.zip -OutFile Sysmon.zip 
   Expand-Archive -Path 'C:\Users\Administrator\Downloads\Sysmon.zip' -DestinationPath 'C:\Users\Administrator\Downloads\Sysmon\' 
   cd 'C:\Users\Administrator\Downloads\Sysmon\' 
   wget https://raw.githubusercontent.com/SwiftOnSecurity/sysmon-config/master/sysmonconfig-export.xml -OutFile sysmonconfig-export.xml 
   sysmon -i sysmonconfig-export.xml 

 
.. code-block::

   tsagent config --set EventLogs "Security,Microsoft-Windows-Sysmon/Operational" 
   tsagent restart 
