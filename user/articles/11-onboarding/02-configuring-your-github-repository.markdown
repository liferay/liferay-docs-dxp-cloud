---
header-id: configuring-your-github-repository
---

# Configuring Your Github Repository

## Transferring the Code to Your Own Organization

Once you have received an onboarding email for DXP Cloud, you'll be provisioned 
a repository on Github hosted in the organization `dxpcloud`. This repository is 
only for trial purposes, and the codebase should be transferred to your own 
Github repository. Follow these steps to transfer the codebase: 

1. Create a private repository in your organization for the codebase. 
2. Clone the `dxpcloud` repository locally. 
3. Push the local code from step 2 to the remote repository created in step 1. 

## Integrating with the Jenkins Service

The next step is to setup a webhook that pushes to the Jenkins service. Go to 
your remote repository's Settings page and set the payload URL to point to the 
domain of the Jenkins service on your `infra` environment. For the `ci` service 
in the `acme` project in the `infra` environment, the url would be 
`https://ci-acme-infra.lfr.cloud/github-webhook/`. The `github-webhook` relative 
path needs to be added to integrate with Jenkins' Github plugin. 

In addition, change the content-type to `application/json`. 

![Figure 1: Specifying the payload URL.](../../images/webhook-1.png)

After setting the payload URL you can select individual events to trigger a 
request to Jenkins, including push events and pull request events. 

![Figure 2: Selecting specific events.](../../images/webhook-2.png)

Finally, two environment variables need to be added/edited in the `LCP.json` of 
the `ci` service to point to the new repository. 

`GITHUB_REPOSITORY` should point to the new remote repository. `GITHUB_TOKEN` 
should point to a personal access token you created for your Github 
organization. Update these two environment variables and deploy a new build with 
the changes. 

After making these changes, you should see pushed branches and pull requests to 
the new remote repository trigger a build in Jenkins. 
