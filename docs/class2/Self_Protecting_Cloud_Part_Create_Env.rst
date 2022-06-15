Threat Stack Playbooks
=======================

Self-Protecting Cloud - Part 2
------------------------------

Create Environment
^^^^^^^^^^^^^^^^^^

AWS CLI Setup
^^^^^^^^^^^^^^^
Now that we have confirmed no active AWS CLI accounts. Let's add our **AWS CLI Account** and setup the required **AWS Network**. 


Setup AWS CLI
^^^^^^^^^^^^^^
By typing **aws configure** as illustrated below, you navigate to **Cloud Accounts** in UDF. Here you will find the AWS credentials required, copy/paste both the **API Key** and **API Secret Key**.

.. note::
   In UDF, go to Deployments > Select **Threat Stack Labs** or name of deployment > Cloud Accounts. Here you will find the AWS keys such as; **API Key** and **API Secret Key**.

.. image:: _static/_AWS_AddConfig.gif

Setup AWS Network 
^^^^^^^^^^^^^^^^^^

Step 1: Create the VPC

.. code-block::

   aws ec2 create-vpc --cidr-block 10.0.0.0/16 

Step 2: Grab the NetworkAclId

.. code-block::

   aws ec2 describe-network-acls | grep NetworkAclId 
   "NetworkAclId": "acl-XXXXXXXXXXX" 
   
.. note::
   Save the **NetworkAclId** for later use.

Threat Stack Setup
^^^^^^^^^^^^^^^^^^

Before jumping into the technical configuration on this lab, let us first define our detection rule within the Threat Stack Cloud Security Platform. For this Lab, our rule is intended to highlight network process activity. 


Setup Threat Stack Rule
^^^^^^^^^^^^^^^^^^^^^^^^
The suggested Rule is precreated within Threat Stack's **F5 - Agility Labs** Organization, named **Self Protect: Network: Outbound Connection (Connects) to WAN**. Feel free to create a new rule or clone existing.

.. image:: _static/_RuleCreation_Example.gif


Update the rule using the following criteria: 

* **Rule Name**

 * Self Protect: **StudentN**: Network: Outbound Connection (Connects) to WAN

* **Alert Title**

 * Self Protect: **StudentN**: Network: Outbound Connection (Connects) to WAN: {{exe}} ran by user {{user}} connected to {{dst_ip}}

* **Alert Description**

 * This alerts when a program connects to an external server's service.   An example is a wget/curl to an external HTTP server. This could be used for data exfiltration.  Depending on your environment this could be VERY noisy.   We recommend adding to the rule filter to focus scope of the rule.

* **Aggregate Fields**

 * user, exe, dst_ip 

* **Rule Filter**

 * event_type = "audit" and syscall = "connect" and (connection.dst_addr != "127.0.0.0/8" and connection.dst_addr != "::1/128" and connection.dst_addr != "::" and connection.dst_addr != "0.0.0.0" and connection.dst_addr != "169.254.0.0/16")



Enable Threat Stack Rule
^^^^^^^^^^^^^^^^^^^^^^^^
Using **Rule Quick** actions or by **editing the rule**, update the status of the rule to enable it.

.. image:: _static/_RulesPage_OnOff.gif



Get Rule ID
^^^^^^^^^^^^
.. image:: _static/_Rules_RuleID.gif

.. note::
   Save the **RuleID** for later use.
