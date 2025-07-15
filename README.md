# Project Title: Github Actions Ec2 Infrastructure Provsioning with Terraform
Deployment of Aws ec2 infrastructure with terraform using github-actions to automate the cicd process workflow and on top of the ec2 instance we install jenkins

#### Project overview

1.IAM user Setup: create an IAM user with administrative access and generate secret key and access key for that user.

2.Github: Creet the prpject in gihuband clone to your root directory in your local terminal 

4.Github Configuration: We are pushing our codes to github so it makes sense if other activities will be happening on the github hosted runner itself. We can specify which operating system we are connecting to in aws if its ubutun, amazon etc

5.Create terraform files - icrete terraform files neccessacry for the provisioning
6. Create backend.tf files to store terraform statefiles

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
#### step 1: Create the project in github and Clone it into yourproject root folder
cd githubactions-aws-ec2-terraform-jenkins
 
 #### Create the project gihubactions pipeline

#### creating the .github/workflows/gihubactions-infra.yml

touch .github folder 
cd .github
cd workflows
touch gihubactions-infra.yml


<img width="1800" height="1296" alt="Image" src="https://github.com/user-attachments/assets/49778699-a524-4db7-a4de-89225d855bb9" />

<img width="1620" height="1290" alt="Image" src="https://github.com/user-attachments/assets/dd0ee542-d9d4-4893-9f4d-dd87ef1d5259" />

name: Infrastructure Provisioning with Gihubactions

on:
  push:
    branches:
      - master
permissions:
      id-token: write # for aws oidc connection
      contents: read   # for actions/checkout
      pull-requests: write # for GitHub bot to comment PR
env:
  TF_LOG: INFO
  AWS_REGION: ${{ secrets.AWS_REGION }}
  AWS_ACCESS_KEY: ${{ secrets.AWSACCESSKEY }}
  AWS_SECRET_ACCESS_KEY: ${{ secrets.AWSSECRETACCESSKEY }}
  role-session-name: GitHub-OIDC-TERRAFORM      

jobs:
  deploy:
    name: Terraform
    runs-on: ubuntu-latest
    defaults:
      run:
        shell: bash
        working-directory: ./infra
    steps:

    - name: Checkout Repo
      uses: actions/checkout@v1


    - name: Setup Terraform
      uses: hashicorp/setup-terraform@v2
      with:
        
        terraform_version: 1.5.5

    - name: Terraform fmt
      id: fmt
      run: terraform fmt

    - name: Terraform Init
      id: init
      env:
        AWS_BUCKET_NAME: ${{ secrets.AWS_BUCKET_NAME }}
        AWS_BUCKET_KEY_NAME: ${{ secrets.AWS_BUCKET_KEY_NAME }}
      run: |
        rm -rf .terraform
        terraform init 
        
    - name: Terraform Validate
      id: validate
      run: terraform validate -no-color 

    - name: Terraform Plan
      id: plan
      run: terraform plan -no-color

    - name: Terraform destroy
      id: apply 
      run: terraform destroy -auto-approve
      
    
#### step 2: Set up Aws credentials in Github(Github integration with aws)

#### Go to this pject in github and look for settings

<img width="2422" height="1358" alt="Image" src="https://github.com/user-attachments/assets/7251f0f6-0abe-4a02-a2d2-7c6fbdd03131" />

#### go look for secreates and variables

<img width="2540" height="1140" alt="Image" src="https://github.com/user-attachments/assets/2eabd929-5cb8-4583-91c3-48d152960160" />

#### click on actions and enter your aws credentials
access key 
and secret keys

<img width="2434" height="1124" alt="Image" src="https://github.com/user-attachments/assets/f23f806d-94cc-4a44-967c-d5cf058978f4" />

#### Step 3:Running the git push on my local terminal

<img width="1700" height="474" alt="Image" src="https://github.com/user-attachments/assets/72b87a17-67ec-4fc8-9ede-fd5abdb6ba0a" />


#### As shown git push trigers github to kick start the github actions pipeline actions as shown below 

<img width="2542" height="1330" alt="Image" src="https://github.com/user-attachments/assets/16f0b078-ce85-4d39-a4f1-0a8c56ab2773" />


<img width="2526" height="1272" alt="Image" src="https://github.com/user-attachments/assets/6e45fa42-d6bf-4783-a7d6-61e9e8b98642" />


#### If git push is ruan again miatekingly youn get bthe response below

<img width="2544" height="1268" alt="Image" src="https://github.com/user-attachments/assets/5bed1a46-85d6-439a-ab9e-5f40a1b2bc3f" />

#### Step 4:jenkins server installed with github actions cicd

<img width="2370" height="922" alt="Image" src="https://github.com/user-attachments/assets/e0710adc-f5e2-4958-ba47-ae910d60c14c" />

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



============
#### STAGE 2: CLEAN UP
==============
#### step1 : Destroy the resources created

#### run terraform destroy 

<img width="1250" height="718" alt="Image" src="https://github.com/user-attachments/assets/3a8a66f6-40e7-4aa8-ad9f-57b41e5fde4f" />


<img width="2288" height="1364" alt="Image" src="https://github.com/user-attachments/assets/070499cd-54c4-4d6b-a49e-2a6b2c64798e" />


<img width="2510" height="1132" alt="Image" src="https://github.com/user-attachments/assets/74874182-249d-42f9-b00a-f541bbdac9fd" />


<img width="2058" height="606" alt="Image" src="https://github.com/user-attachments/assets/18d16dca-6eba-4ac0-a600-351d896d9e91" />