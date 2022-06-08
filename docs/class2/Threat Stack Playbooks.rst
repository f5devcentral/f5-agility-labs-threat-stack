Threat Stack Playbooks
======================


Self-Protecting Cloud
---------------------

Leveraging the Threat Stack API and simple code enables a host to proactively respond to activity automatically.  

Confirm Python Environment

.. code-block::

   python3 -V 
   Python 3.8.10 


Confirm AWS CLI 

.. code-block::

  aws configure list 
  Name                    Value             Type    Location 
  ----                    -----             ----    -------- 
  profile                <not set>             None    None 
  access_key     ****************M2OT shared-credentials-file 
  secret_key     ****************ZtuZ shared-credentials-file 
  region                us-east-1      config-file    ~/.aws/config 


.. note::

   Note: If not configured, configure the aws cli using the UDF Deployment Cloud Account. 
   
  
Building Network Infrastructure 

Step 1: Create the VPC

.. code-block::

   aws ec2 create-vpc --cidr-block 10.0.0.0/16 

Step 2: Grab the NetworkAclId

.. code-block::

   aws ec2 describe-network-acls | grep NetworkAclId 
   "NetworkAclId": "acl-01d98e20381b55f72", 
 
 
Python Bot Setup 
----------------
The following series of commands are meant to configure and set up the python bot. The python bot can be found in the home directory of the Linux host. 


Step 1: Update Threat Stack Credentials File 

.. code-block::

   sudo vim credentials 
   [default] 
   ts_org=ORG 
   ts_user=USER 
   ts_key=KEY 
   
Step 2: Make the directory


.. code-block::

   mkdir ../.threatstack 
   cp credentials ../.threatstack 
   

Launch Python Bot
-----------------


Using the RuleID to detect the activity and the AWS NACL ID. 


.. code-block::

   python3 .threatstack/integration.py --watchrule RuleID --aws_acl_id ACLID 
   
   python3 integration.py --watchrule 94ec898e-cb04-11ec-9994-c901909a56dc --aws_acl_id acl-01d98e20381b55f72 
   
   python3 integration.py --watchrule 94ec898e-cb04-11ec-9994-c901909a56dc --aws_acl_id acl-01d98e20381b55f72 
   
   Alert poll returned destination set() source [] to block at the firewall 
   Alert poll returned destination set() source [] to block at the firewall 
   Alert poll returned destination set() source [] to block at the firewall 
   Alert poll returned destination set() source [] to block at the firewall 
   Alert poll returned destination set() source [] to block at the firewall 
   Alert poll returned destination set() source [] to block at the firewall 
   

Execute Command 

.. code-block::
   
   wget dadismad.com 
   

 

Terminal Results 

The following is a sample of the resulting terminal activity from the command which executes the malware. 


.. code-block::

   Alert poll returned destination set() source [] to block at the firewall 
   Alert poll returned destination set() source [] to block at the firewall 
   Alert poll returned destination set() source [] to block at the firewall 
   Alert poll returned destination set() source [] to block at the firewall 
   Found address 159.89.83.187/32 in entry {'CidrBlock': '159.89.83.187/32', 'Egress': True, 'Protocol': '-1', 'RuleAction': 'deny', 'RuleNumber': 4} ,    skipping 
   Alert poll returned destination {'164.90.254.173/32', '159.89.83.187/32'} source [{'container': 'Host', 'address': '172.31.20.97'}, {'container':        'Host', 'address': '172.31.20.97/20'}] to block at the firewall 
   Found address 164.90.254.173/32 in entry {'CidrBlock': '164.90.254.173/32', 'Egress': True, 'Protocol': '-1', 'RuleAction': 'deny', 'RuleNumber': 5}    ,skipping 
   Found address 159.89.83.187/32 in entry {'CidrBlock': '159.89.83.187/32', 'Egress': True, 'Protocol': '-1', 'RuleAction': 'deny', 'RuleNumber': 4} ,    skipping
