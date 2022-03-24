# tfc_sso_azure

This repository describes a step-by-step on how to configure Single sign-on with Microsoft Azure AD for Terraform Cloud.

At the end of the steps you should be able to login to Terraform Cloud using SAML using Microsoft Azure AD

Based on this documentation:
[Single Sign-on: Microsoft Azure AD](https://www.terraform.io/cloud-docs/users-teams-organizations/single-sign-on/azure-ad)



# Prerequisites

- Access Azure
- Access to Terraform Cloud
 
# How to

## Azure Portal
- login to Azure portal   
https://azure.microsoft.com/en-us/features/azure-portal/
- Go to Azure Active Directory service.
- Go to Enterprise Applications    
![](media/2022-03-23-11-47-21.png)  
- select New application.  
- Select Terraform Cloud    
![](media/2022-03-23-11-48-18.png)
- Give it a name and select create. This can take a minute  
![](media/2022-03-23-11-53-27.png)  
- Go to Single sing-on and click  
![](media/2022-03-23-11-55-19.png)  
- Select the SAML option  
![](media/2022-03-23-11-55-38.png)  
- Copy the `App Federation Metadata Url` which we will need later    
![](media/2022-03-23-11-59-24.png)  
- Leave this page open

## Terraform Cloud

- Login to Terraform Cloud
- Go to settings -> SSO --> Setup your SSO provider    
![](media/2022-03-23-12-00-36.png)  
- Select Azure    
![](media/2022-03-23-12-01-51.png)  
- Paste the `App Federation Metadata Url` from Azure  
![](media/2022-03-23-12-03-13.png)  
- Save settings
- You should see the SSO details in Terraform Cloud
- Copy the Entity ID and Reply URL    
![](media/2022-03-23-12-05-08.png)  

## Azure Portal

- Edit the Basic SAML Configuration    
![](media/2022-03-23-12-06-01.png)  
- Paste the Entity ID and Reply URL from Terraform Cloud
- The Single Sign on URL paste
```
https://app.terraform.io/session
```
- Download the `Certificate (Base64)` which we will need in Terraform Cloud  
![](media/2022-03-23-12-11-16.png)  
- Go to Manage -> Users and groups
- Click on Add user/group  
![](media/2022-03-23-12-12-23.png)  
- select the user you want to add and click assign  
![](media/2022-03-23-12-13-28.png)  


## Terraform Cloud
- Edit your SSO settings  
![](media/2022-03-23-12-14-53.png)  
- Paste the contents of the Public Certificate you downloaded from Azure here  
![](media/2022-03-23-12-16-32.png)
- Save settings
- Click on test  
![](media/2022-03-23-12-17-13.png)  
- Now you can Enable your SSO configuration  
![](media/2022-03-23-12-18-17.png)  

## Test the SSO

- Before enabling SSO you would get this message   
![](media/2022-03-24-16-36-08.png)  
- After you enable SSO you can login 
