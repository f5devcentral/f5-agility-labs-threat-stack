Threat Stack Agent
==================

Deploying the Threat Stack Agent 
---------------------------------

The Threat Stack host-based Agent uses the Linux Audit Framework to collect file, network, and process data.  


.. image:: _static/_ServerPages_Install.gif

   
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
  


 
   

Container Distributions 
-----------------------
The Threat Stack Container Agent can be orchestrated using Kubernetes, Docker, and others. By default, the following rulesets are applied: 

* Base Rule Set 
* Docker Rule Set 
* Kubernetes Rule Set (Optional)



Helm Chart 
----------

Helm is a package manager on top of Kubernetes. It facilitates installation, upgrades, and manages dependencies for the services you install in Kubernetes. 

*Prerequisites*

* Helm installed 
* Configured Values file 



*Challenge 8 – Install the Threat Stack Container Agent*

.. note::

   Warning: Use only the command provided to install the Threat Stack Container Agent. Using UDF, establish a Terminal session with the host labelled,   “k8s” 


.. code-block::

   wget https://raw.githubusercontent.com/threatstack/threatstack-helm/master/values.yaml 
   vim values.yaml 
 
In the values.yaml, lets update a couple things. First, the **hostname on line 51** so Lab leaders can track activity easily in the lab. Then, agentDeployKey on line 67 with your previously used key and  


.. code-block::

   51 additionalSetupConfig: "--hostname=StudentN " 
   
.. code-block::

   67 agentDeployKey: "PROVIDED_DEPLOYKEY" 

Now that we have our values.yaml file updated, lets deploy the Threat Stack Container Agent.  

.. code-block::

   ubuntu@ip-10-1-1-6:~$ helm repo add threatstack https://pkg.threatstack.com/helm 
   "threatstack" has been added to your repositories 

To Reload K8 Config 

.. code-block::

    Error: INSTALLATION FAILED: Kubernetes cluster unreachable: Get "http://localhost:8080/version": dial tcp 127.0.0.1:8080: connect: connection    refused 
   Note: kubectl config view --raw > ~/.kube/config 
   

.. code-block::

   helm install threatstack-agent --values values.yaml threatstack/threatstack-agent 

