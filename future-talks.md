# Future talks I might give

Feedback welcome! Please open an issue or make a pull request.

## Blueprint Driven Development

At vuzz we're using API Blueprint, a markup language for designing RESTful HTTP APIs. Instead of keeping API documentation and implementation separate, we use the API Blueprint file as a master file that changes how the API behaves on the surface. Since the Blueprint must be updated for the API to be updated, we call this workflow Blueprint Driven Development (BDD). BDD automates the process of keeping documentation and implementation synchronized.

## Finding Food Pictures with Food Pictures
We've crated a system for finding similar food pictures given an input food picture. For instance, if you send it a picture of a hamburger it'll find other pictures with various types of hamburgers. The work we did falls into three rough categories: 
- Building and training the model
- Encapsulating the model in a responsive service
- Deploying the service as a microservice in the cloud

## Microservices with Terraform
In this talk I'll share how I've built up the DevOps systems that we use by vuzz. We have a lot of services, and each are run through CICD pipelines.

## Taking Control with Terraform
In this short talk I'll talk about how I put an entire system running on AWS under terraform management. I automated the import process and was able to put the whole system under terraform management in less than two hours. 

## Less fleshed out ideas

- Training Wavenet as a denoising auto encoder to create a time strething DSP plugin
