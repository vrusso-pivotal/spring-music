# Pipeline setup and execution

How to setup this sample pipeline on your Concourse server:

1. Setup the pipeline credentials file
  * Make a copy of the sample credentials file  
  __cp ci/credentials.yml.sample ci/credentials.yml__  

  * Edit _ci/credentials.yml_ and fill out all the required credentials:  
_deploy-username:_ the CF CLI userID to deploy apps on the Cloud Foundry deployment  
_deploy-password:_ the corresponding password to deploy apps on the Cloud Foundry deployment  
_pws-organization:_ the ID of your targeted organization in Cloud Foundry   
_pws-space:_ the name of your targeted space in Cloud Foundry (e.g. development)  
_pws-api:_ the url of the CF API. (e.g. https://api.run.pivotal.io)  
_pws-app-suffix:_ the domain suffix to append to the application hostname (e.g. my-test-app)  
_pws-app-domain:_ the domain name used for your CF apps (e.g. cfapps.io)   

2. Configure the sample pipeline in Concourse with the following commands:  
   __fly -t local login <concourse-url>__  
   Example:  
   __fly -t local login http://192.168.100.4:8080__  
   __fly -t local set-pipeline -c ci/pipeline.yml -p blue-green-pipeline -l ci/credentials.yml__

3. Access to the Concourse web interface (e.g. http://192.168.100.4:8080 ), click on the list of pipelines, un-pause the _blue-green-pipeline_ and then click on its link to visualize its pipeline diagram.

You will then notice the pipeline's jobs getting executed within a few seconds, one at a time, if the previous job in the pipeline is executed successfully.
