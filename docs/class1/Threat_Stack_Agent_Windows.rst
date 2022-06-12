Threat Stack Windows Agent
==========================

Connecting to the Windows Machine
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First, select **'RDP'** pop up to download the .rdp file to connect to the Windows instance.

.. image:: _static/_rdp_connect.png
   :scale: 50%
   
Then, open the rdp file with your prefferred Microsoft RDP Desktop tool. You will be prompted requesting a password for the **'administrator'** user. The Windows instance password is found under the **'details/credentials'** tab of the UDF environment. Enter the password there into the RDP prompt.

.. image:: _static/admin_creds.png
   :scale: 50%


Deploying the Threat Stack Windows Agent 
----------------------------------------

The Threat Stack windows-based Agent uses the Windows Events & Sysmon to collect file, network, and process data.


Install the Threat Stack Agent
------------------------------
*Prerequisites*

* Access to the Threat Stack Console
* Access to host either via CLI or RDP on a supported Operating System architecture(ARM or x86 architecture)
* Access to a supported browser (Chrome, Edge, Safari, and Firefox)

Threat Stack automatically walks customers through an Agent install on the **Servers** page. Log into **Threat Stack > Click Servers**.

.. image:: _static/_ServerPages_Install.gif

Threat Stack automatically walks customers through an Agent install on the **Servers** page. Log into **Threat Stack > Click Servers**.

*Windows Distributions*

Select **+ Add New Server** and the Command Builder dialog will display. Select **Agent 2.X.X** to proceed to the set of instructions below, specific to your Windows distribution. 

.. attention::
   **Challenge 7** – *Install the Threat Stack Windows Agent*

Let’s begin by deciding the method of instalation, Install Wizard or PowerShell.

Install Wizard
^^^^^^^^^^^^^^^^^^^^^^

Using the local browser, download the msi installer using this link: https://pkg.threatstack.com/v2/Windows/Threat+Stack+Cloud+Security+Agent.latest.msi

Navigate to the Downloads folder, now double click the **Threat+Stack+Cloud+Security+Agent.latest.msi**

.. note::

   **Deployment Key**
   
   979d8df5efe295d73734109b121a33865429ebbd2a8d7ede66147404f993c3bbab4466a0
   
   
   **Ruleset Name**
   
   Windows Rule Set
   

Follow the images below for further details on utilizing the installation wizard.


.. image:: _static/_Install_Windows.png
   :align: center


.. image:: _static/_Install_Windows_Config.png
   :align: center
   

.. image:: _static/_Install_Windows_Deploy.png
   :align: center

.. warning::
   Sysmon installation is completed separately

PowerShell 
^^^^^^^^^^

Open PowerShell and configure environmental variables for a streamlined lab.

.. code-block::

   $Env:MY_DEPLOY_KEY="979d8df5efe295d73734109b121a33865429ebbd2a8d7ede66147404f993c3bbab4466a0"
   $Env:MY_HOSTNAME="StudentN-Windows"


Download and install the Threat Stack Windows Agent.

.. code-block::

   cd 'C:\Users\Administrator\Downloads\'
   wget https://pkg.threatstack.com/v2/Windows/Threat+Stack+Cloud+Security+Agent.latest.msi -OutFile Threat+Stack+Cloud+Security+Agent.latest.msi
   msiexec /qn /i "C:\Users\Administrator\Downloads\Threat+Stack+Cloud+Security+Agent.latest.msi" TSDEPLOYKEY="$Env:MY_DEPLOY_KEY" TSHOSTNAME=$Env:MY_HOSTNAME


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
