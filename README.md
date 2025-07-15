# Project Title: Github-actions-ec2-infrastructure-terraform
Deployment of Aws ec2 infrastructure with terraform using github-actions to automate the cicd process workflow and on top of the ec2 instance we install jenkins

#### Project overview

1.Docker Setup: Create an accout in Dockerhub to be able to deploy and store docker images activities.

2.Github: Through the imagecreation.yml file script we are able to build and push docker images to dockerhub 

4.Github Configuration: We are oushing the code to gihub so it makes sens if other activities will be halppening on the gihub self hosted runner. We can specify which operating system we are connecting to in aws if its ubuntun, amazon etc

5.Docker - installed docker on the server, to enable you build docker images

#### Prerequisites:

Before starting the project, ensure you have the following prerequisites:

-An AWS account with the necessary permissions to create resources.

-AWS CLI installed on your local machine.

-Basic familiarity with  Docker and DevOps principles.

-Vscode - code editor installed locally on your machine.

- GitHub - a repository for your project code

https://github.com/clement2019/githubactions-aws-ec2-terraform-jenkins.git


### Project Workflow
============
#### STAGE 1
==============
#### step 1: Create the project gihubactions pipeline

#### creating the .github/workflows/gihubactions-infra.yml
#### I have to first create the 
touch .github folder 
cd .github
cd workflows
touch gihubactions-infra.yml


<img width="1800" height="1296" alt="Image" src="https://github.com/user-attachments/assets/49778699-a524-4db7-a4de-89225d855bb9" />

<img width="1620" height="1290" alt="Image" src="https://github.com/user-attachments/assets/dd0ee542-d9d4-4893-9f4d-dd87ef1d5259" />


#### step 2: Set up Aws creadentials  in Github(Github integration with aws)

#### Go to this pject in github and look for settings

<img width="2422" height="1358" alt="Image" src="https://github.com/user-attachments/assets/7251f0f6-0abe-4a02-a2d2-7c6fbdd03131" />

#### go look for secreates and variables

<img width="2540" height="1140" alt="Image" src="https://github.com/user-attachments/assets/2eabd929-5cb8-4583-91c3-48d152960160" />

#### click on actions and enter your aws credentials
access key 
and secret keys

<img width="2434" height="1124" alt="Image" src="https://github.com/user-attachments/assets/f23f806d-94cc-4a44-967c-d5cf058978f4" />


<img width="2370" height="922" alt="Image" src="https://github.com/user-attachments/assets/e0710adc-f5e2-4958-ba47-ae910d60c14c" />

#### Step 3:Running the git push on my local terminal

<img width="1700" height="474" alt="Image" src="https://github.com/user-attachments/assets/72b87a17-67ec-4fc8-9ede-fd5abdb6ba0a" />


#### As shown git push trigeers github to trigger the pipeline actions as shown below 

<img width="2542" height="1330" alt="Image" src="https://github.com/user-attachments/assets/16f0b078-ce85-4d39-a4f1-0a8c56ab2773" />

#### Step 4:jenkins server installed with giyhub actions cicd

<img width="2020" height="1086" alt="Image" src="https://github.com/user-attachments/assets/d8f153e6-8ba0-4936-a847-3d79dcc71f17" />

#### configure jenkins

<img width="1976" height="1274" alt="Image" src="https://github.com/user-attachments/assets/296a9c45-d4cc-45c8-aacf-6fa0d51088c3" />

#### install sugested plugins

<img width="1934" height="1292" alt="Image" src="https://github.com/user-attachments/assets/d078252c-d545-4d5f-8ab8-fb5697365402" />

#### jenkins getting started

<img width="2164" height="1344" alt="Image" src="https://github.com/user-attachments/assets/7cd58c56-a842-49a4-bb68-aa48c9faaad4" />

#### create an account in jenkins

<img width="2142" height="1346" alt="Image" src="https://github.com/user-attachments/assets/de37d0fb-4c58-45f3-8257-65e331bb3f92" />


### jenkins is reeady

<img width="2102" height="1334" alt="Image" src="https://github.com/user-attachments/assets/4349d253-8460-41b5-9d43-e64d32aed240" />


<img width="2556" height="1382" alt="Image" src="https://github.com/user-attachments/assets/79e6c493-ca9a-4688-b6a4-98d99551ff2e" />