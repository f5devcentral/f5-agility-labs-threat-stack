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

