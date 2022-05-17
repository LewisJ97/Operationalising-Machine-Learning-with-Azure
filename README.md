# Udacity Project 2: Operationalising Machine Learning


## Project Overview
*The main concepts throughout this project were using the Azure AutoML service to train and deploy a model, then consume the models performance indicators using Swagger UI through utilising the REST API endpoint. The data used was the same bank marketing dataset used in project 1, contains data collected during direct marketing campaigns (phone calls) from a Portuguese banking institution, where the goal is to use this information about individuals to predict their receptiveness to additional marketing materials and products.*

*As a continuation of what was learned throughout project 1, we not only obtain the best model using Azure AutoML, but we configure a cloud-based machine learning production model, deploy it (via an Azure Container Instance), and consume it.*

## Architectural Diagram
![image](https://user-images.githubusercontent.com/56005109/168784266-11fa655e-4e5b-427c-b591-affbcc0c30d0.png)


# Key Steps

## AutoML
*The first stage required developing an AutoML model that we could then deploy. At this point, security is enabled and authentication is completed. In this step, we created a dataset, an experiment using Automated ML, configured a compute cluster, and used that cluster to run the experiment.*

*To being with, the bank marketing dataset had to be created.*
*Data: https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv*

![Data Upload](https://user-images.githubusercontent.com/56005109/168785315-26db74c9-157a-4af6-93c4-08991fefb4cf.PNG)

*Once our dataset was uploaded and available for use, an AutoML run was created with the purpose of classification.*

![Completed-auto-ml1](https://user-images.githubusercontent.com/56005109/168786530-bd3e7ce3-c7e6-4059-93fc-6ca75ce8ac65.PNG)
![Best-model](https://user-images.githubusercontent.com/56005109/168786567-0e063410-c86f-4628-a2a3-da6a6f13318c.PNG)

## Model Deployment
*Once the AutoML run was complete, the best model (Voting Ensemble) was deployed using an Aure Container Instance, with authentication enabled. Then, using the SDK, application insights were enabled for the deployed model, using the logs.py script*

![AutoML-deploy](https://user-images.githubusercontent.com/56005109/168787398-561bba17-50ca-4e29-b6b8-72634ec2b2ba.PNG)
![AutoML-deploy-success](https://user-images.githubusercontent.com/56005109/168787421-dc6ba31b-2010-4aaf-a62e-a5cfdf1e661f.PNG)
![logs](https://user-images.githubusercontent.com/56005109/168787698-37f05d16-4ecf-468d-a87d-1dbecd968982.PNG)
![applicationInsights](https://user-images.githubusercontent.com/56005109/168787463-d484e436-e543-41a5-b5e0-51d8d310b347.PNG)

*After deployment and running the logs.py script (which enables application insights), the output from the script shows GET requests sent to our deployed model. This provides us with a swagger.json file that we can use to initialise and generate Swagger documentation.*

![Logs-output-gitBash](https://user-images.githubusercontent.com/56005109/168788379-ee6dddff-043f-43af-bd02-9fea664ce688.PNG)

*To check the models Swagger documentation, the swagger.sh and serve.py scripts were ran.* 
*The swagger.sh file contains Docker commands that pull the Swagger container image, and runs the Swagger container with port forwarding.*
*The serve.py file creates a HTTP server that we can access the Swagger documentation from.*

![swagger-output](https://user-images.githubusercontent.com/56005109/168789313-81506f9b-5bb3-431e-b1a0-a39729a99dd9.PNG)
![swagger output](https://user-images.githubusercontent.com/56005109/168789437-5610fe9d-8b24-4998-a46d-4ab8f9e88a2c.PNG)
![swagger-output2](https://user-images.githubusercontent.com/56005109/168789487-1563d6bd-c152-41ff-8403-344d460d8880.PNG)

*Now that we had successfully retrieved Swagger documentation, we could consumer the model endpoints (using an endpoint.py script) and interact with the deployed model.*

*The endpoint.py script runs against the API, producing a JSON output from the model.*

![Endpoints Output](https://user-images.githubusercontent.com/56005109/168790414-9a282a58-cb83-4675-8a04-2e256921c8e1.PNG)

## Pipeline Creation & Deployment
*This part of the project required the construction and publishing of a pipeline using the Azure SDK.*

*Using a jupyter notebook, we create an experiment in our existing workspace that was created for our AutoML run, and attach an AmlCompute to the workspace that was utilised in the previous stage of the project.*

![pipeline data1](https://user-images.githubusercontent.com/56005109/168795367-604021d2-0123-4826-8a40-104b3e852389.png)

  *After running the notebook I carried out several checks to ensure that the pipeline was available:*
  
  *1 - The pipeline had been created successfully*
  ![Pipelines](https://user-images.githubusercontent.com/56005109/168795731-6eb81b9f-34cc-4b00-960e-edab74fcdcda.PNG)
  
  *2 - The pipeline had been published successfully and the REST endpoint was available:*
  ![Active Pipeline](https://user-images.githubusercontent.com/56005109/168796100-c595811b-275b-4954-956f-ba6d58c63ddb.PNG)
  
  *3 - Details of the RunDetails Widget from the jupyter notebook:*
  ![run details - jupyter](https://user-images.githubusercontent.com/56005109/168797031-06aa9ee7-80ec-4043-bb3f-7b9edd1e836f.PNG)
  
  *4 - Active published pipeline:*
  ![Pipeline Endpoints](https://user-images.githubusercontent.com/56005109/168797686-2ce3dfc5-cb4f-4b2d-88c5-d2738d040ef2.PNG)

  *5 - Pipeline Endpoints:*
  ![Pipeline and rest endpoint](https://user-images.githubusercontent.com/56005109/168797378-2d1d975b-7d7d-41d1-b25a-6b8d1acd86c7.PNG)
  

## Screen Recording
*The screen recording can be found in the folder - "Project 2 - Screenshots"*
