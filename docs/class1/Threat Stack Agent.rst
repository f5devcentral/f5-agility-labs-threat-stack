Threat Stack Agent
=====================================

Deploying the Threat Stack Agent 
---------------------------------
Before you install the Threat Stack host-based Agent, you must prepare your Linux distribution to work with the Agent. 

The Threat Stack host-based Agent uses the Linux Audit Framework to collect file, network, and process data.  


Check for other Agents
----------------------

.. note::

   Conflict can occur between the Threat Stack host-based Agent and other tools leveraging these kernels. Before deploying the Agent, ensure no other      tools that use these kernels. This is the result of a known Linux limitation where only one process can bind to the AuditD socket. 
   
Code Block To Check for Services leveraging audit

.. code-block::

   ps aux | grep audit


Code Block to Check for The Threat Stack Agent on the machine

.. code-block:: 
   
   sudo tsagent status


Install the Threat Stack Agent
------------------------------
*Prerequisites*

* Access to the Threat Stack Console
* Access to host either via CLI or RDP on a supported Operating System architecture(ARM or x86 architecture)
* Access to a supported browser (Chrome, Edge, Safi, and Firefox)

*Linux Distributions*

Threat Stack automatically walks customers through an Agent install on the Servers page. Log into Threat Stack > Click Servers. The Servers page displays.

Select Agent 2.x. The + Add New Server dialog displays. Proceed to the set of instructions below, specific to your Linux distribution. 

*Challenge 6 – Install the Threat Stack Linux Agent*

Let’s begin by configuring some environmental variables for a streamlined lab.


.. code-block:: 
   
   MY_DEPLOY_KEY = 'XXXXXXXXX'
   MY_HOSTNAME= 'StudentN-Linux'
   

.. note::

   **Warning**: Use only the command provided to install the Threat Stack Linux Agent. Using UDF, establish a Terminal session with the host labelled,     “Linux” 
   
   
.. code-block::

  sudo apt-get update && sudo apt-get install threatstack-agent -y && \ 
  sudo tsagent config --set enable_bpf_sensors 1 && \ 
  sudo tsagent config --set enable_inprogress_connects true && \ 
  sudo tsagent setup --deploy-key="$MY_DEPLOY_KEY" --hostname="$MY_HOSTNAME" --ruleset="Base Rule Set" && \ 
  sudo systemctl start threatstack 
  

Windows Distributions 
----------------------

Threat Stack automatically walks customers through an Agent install on the **Servers** page. Log into Threat Stack > Click **Servers**. The **Servers** page displays. 

Select **Agent 2.x.** The + Add New Server dialog displays. Proceed to the set of instructions below, specific to your **Windows Sever 2012 or above**. 

*Challenge 7 – Install the Threat Stack Windows Agent*

Let’s begin by configuring some environmental variables for a streamlined lab. Let’s open **PowerShell**

.. code-block::

   $Env:MY_DEPLOY_KEY="979d8df5efe295d73734109b121a33865429ebbd2a8d7ede66147404f993c3bbab4466a0" 
   $Env:MY_HOSTNAME="StudentN-Windows" 

.. note::

   **Warning**: Use only the command provided to install the Threat Stack Linux Agent. Using UDF, establish a Terminal session with the host labelled,      “Windows” 
   
.. code-block::

   wget https://pkg.threatstack.com/v2/Windows/Threat+Stack+Cloud+Security+Agent.latest.msi -OutFile Threat+Stack+Cloud+Security+Agent.latest.msi
   
   msiexec /qn /i "C:\Users\Administrator\Downloads\Threat+Stack+Cloud+Security+Agent.latest.msi" TSDEPLOYKEY="$Env:MY_DEPLOY_KEY" TSHOSTNAME=$Env:MY_HOSTNAME 
 
   

Container Distributions 
-----------------------
The Threat Stack Container Agent can be orchestrated using Kubernetes, Docker, and others. By default, the following rulesets are applied: 

* Base Rule Set 
* Docker Rule Set 
* Kubernetes Rule Set

Helm Chart 
----------

Helm is a package manager on top of Kubernetes. It facilitates installation, upgrades, and manages dependencies for the services you install in Kubernetes. 

*Prerequisites*

* Helm installed 
* Configured Values file 


Install the Threat Stack Helm Chart 
-----------------------------------

These instructions assume you already have Helm installed in your environment. It also assumes any Role-Based Access Control (RBAC) configuration has been completed for proper operation of Helm. Please see Installing Helm for instructions on installing Helm in your environment. 

.. code-block:: 
   
   hello world!
   

Uninstall the Helm Chart 
-------------------------
To uninstall the Helm chart, run the following command: 
.. code-block:: 
   
   hello world!
   

Remove an Agent 
---------------

To remove the Threat Stack Agent, follow your OS's normal software package removal option. The package was installed via Apt or Yum (even for the curl installer). 


For example: 

.. code-block:: 
   
   sudo systemctl stop threatstack
   
or

.. code-block:: 
   
   sudo dpkg -r threatstack-agent




