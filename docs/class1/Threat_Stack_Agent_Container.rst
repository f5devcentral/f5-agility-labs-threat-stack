Threat Stack Containerized Agent
================================

Deploying the Threat Stack Agent 
--------------------------------

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
 
In the values.yaml, lets update a couple things. First, the **hostname on line 51** so Lab leaders can track activity easily in the lab. Then, agentDeployKey on line 67 with your previously used key.

To edit on vim, enter the command 'i' to enter 'insert mode' 

.. code-block::
   
   i


.. code-block::

   51 additionalSetupConfig: "--hostname=StudentN " 
   
.. code-block::

   67 agentDeployKey: "PROVIDED_DEPLOYKEY" 
   

.. image:: _static/config_example_k8s.png


Once you edit the necessary values, then exit by entering the following on vim to write and force quit.


.. code-block::

   :wq!
   
.. image:: _static/vim_force_quit.png
   

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

