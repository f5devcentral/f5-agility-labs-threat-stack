Application Infrastructure Protection Agent
=====================================

Deploying the AIP Agent 
---------------------------------
Before you install the AIP host-based Agent, you must prepare your Linux distribution to work with the Agent. 

The AIP host-based Agent uses the Linux Audit Framework to collect file, network, and process data.  


.. image:: _static/serverpages_install_v2.gif



Check for other Agents
----------------------

.. note::

   Conflict can occur between the AIP host-based Agent and other tools leveraging these kernels. Before deploying the Agent, ensure no other      tools that use these kernels. This is the result of a known Linux limitation where only one process can bind to the AuditD socket. 
   
Code Block To Check for Services leveraging audit

.. code-block::

   ps aux | grep audit


Code Block to Check for The AIP Agent on the machine

.. code-block:: 
   
   sudo tsagent status


Install the AIP Agent
------------------------------
*Prerequisites*

* Access to the AIP Console
* Access to host either via CLI or RDP on a supported Operating System architecture(ARM or x86 architecture)
* Access to a supported browser (Chrome, Edge, Safi, and Firefox)



*Linux Distributions*

AIP automatically walks customers through an Agent install on the Servers page. Log into AIP > Click Servers. The Servers page displays.

Select Agent 2.x. The + Add New Server dialog displays. Proceed to the set of instructions below, specific to your Linux distribution. 

*Challenge 6 – Install the AIP Linux Agent*

Let’s begin by configuring some environmental variables for a streamlined lab.


.. code-block:: 
   
   MY_DEPLOY_KEY = 'XXXXXXXXX'
   MY_HOSTNAME= 'StudentN-Linux'
   

.. note::

   **Warning**: Use only the command provided to install the AIP Linux Agent. Using UDF, establish a Terminal session with the host labelled,     “Linux” 
   
   
.. code-block::

  sudo apt-get update && sudo apt-get install threatstack-agent -y && \ 
  sudo tsagent config --set enable_bpf_sensors 1 && \ 
  sudo tsagent config --set enable_inprogress_connects true && \ 
  sudo tsagent setup --deploy-key="$MY_DEPLOY_KEY" --hostname="$MY_HOSTNAME" --ruleset="Base Rule Set" && \ 
  sudo systemctl start threatstack 
  

Windows Distributions 
----------------------

AIP automatically walks customers through an Agent install on the **Servers** page. Log into AIP > Click **Servers**. The **Servers** page displays. 

Select **Agent 2.x.** The + Add New Server dialog displays. Proceed to the set of instructions below, specific to your **Windows Sever 2012 or above**. 

*Challenge 7 – Install the AIP Windows Agent*

Let’s begin by configuring some environmental variables for a streamlined lab. Let’s open **PowerShell**

.. code-block::

   $Env:MY_DEPLOY_KEY="XXXXXXXXX" 
   $Env:MY_HOSTNAME="StudentN-Windows" 

.. note::

   **Warning**: Use only the command provided to install the AIP Windows Agent. Using UDF, establish a Terminal session with the host labelled,      “Windows” 
   
   
   
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
 
   

Container Distributions 
-----------------------
The AIP Container Agent can be orchestrated using Kubernetes, Docker, and others. By default, the following rulesets are applied: 

* Base Rule Set 
* Docker Rule Set 
* Kubernetes Rule Set (Optional)
  
.. note::
 Methodologies for deployment such as container-only is available in our public documentation.


Helm Chart 
----------

Helm is a package manager on top of Kubernetes. It facilitates installation, upgrades, and manages dependencies for the services you install in Kubernetes. 

*Prerequisites*

* Helm installed 
* Configured Values file 



*Challenge 8 – Install the AIP Container Agent*

.. note::

   Warning: Use only the command provided to install the AIP Container Agent. Using UDF, establish a Terminal session with the host labelled,   “k8s” 


.. code-block::

   wget https://raw.githubusercontent.com/threatstack/threatstack-helm/master/values.yaml 
   vim values.yaml 
 
In the values.yaml, lets update a couple things. First, the **hostname on line 51** so Lab leaders can track activity easily in the lab. Then, agentDeployKey on line 67 with your previously used key.  


.. code-block::

   51 additionalSetupConfig: "--hostname=StudentN " 
   
.. code-block::

   67 agentDeployKey: "PROVIDED_DEPLOYKEY" 

Now that we have our values.yaml file updated, lets deploy the AIP Container Agent.  

.. code-block::

   ubuntu@ip-10-1-1-6:~$ helm repo add threatstack https://pkg.threatstack.com/helm 
   "threatstack" has been added to your repositories 

To Reload K8 Config 

.. code-block::

    Error: INSTALLATION FAILED: Kubernetes cluster unreachable: Get "http://localhost:8080/version": dial tcp 127.0.0.1:8080: connect: connection    refused 
   Note: kubectl config view --raw > ~/.kube/config 
   
   

.. code-block::

   helm install threatstack-agent --values values.yaml threatstack/threatstack-agent
   NAME: threatstack-agent
   LAST DEPLOYED: Tue Jun  7 00:12:48 2022
   NAMESPACE: default
   STATUS: deployed
   REVISION: 1
   TEST SUITE: None
   NOTES:
   AIP agents are being deployed. After a few minutes, you should see
   agents showing up on your server tab.

 




