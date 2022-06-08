Threat Stack API
================

Threat Stack offers two types of APIs – Webhooks and REST API. The Webhooks API pushes trigger-based alerts to a specific URL and allows Threat Stack users to operationalize the alerts in near-real time. Meanwhile, the REST API allows the user to write queries to access Threat Stack information about organization-specific security concerns. 

 

* Alert Webhooks 

* RESTful API 


Webhook API 
-----------

.. image:: _static/_Integrations_Webhook_LiveEx.gif


 

Webhooks allow Threat Stack users to send trigger-based alerts to a specific URL and operationalize the alert data in near-real time. Threat Stack sends alert details in JSON format through HTTPS Post. 


* Using the Alert Webhooks API requires: 

* webhook network access (whitelisting) 

a third-party service – such as Slack, Zapier, webhooks.io, or IFTTT – to integrate Threat Stack Alert Webhooks into your existing applications and workflows 

.. note:: 

   *Important Note*: Webhook sends alerts through HTTPS POST, the Webhook URL must be HTTPS. 
   
   


*Challenge 2 – Review Webhook*

1. Navigate to the Threat Stack Cloud Security Platform: https://app.threatstack.com/login 
2. Select Settings > Integrations in the navigation bar 
3. Scroll to the Webhook API section 
4. Click this link to review the events sent to Request Bin: https://requestbin.com/r/enga46ei5gint/ 
