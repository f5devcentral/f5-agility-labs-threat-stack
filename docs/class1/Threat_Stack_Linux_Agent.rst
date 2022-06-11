Threat Stack Linux Agent
========================

Deploying the Threat Stack Host Linux Agent 
-------------------------------------------

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
  sudo tsagent config --set enable_inprogress_connects true
  
  
Then enter:

  
.. code-block::
  
  sudo tsagent setup --deploy-key="$MY_DEPLOY_KEY" --hostname="$MY_HOSTNAME" --ruleset="Base Rule Set" && \ 
  sudo systemctl start threatstack 
 
 
.. note::

   You can access your 'deployment-key' from the server UI. Deployment keys are unique per Threat Stack Organization.
