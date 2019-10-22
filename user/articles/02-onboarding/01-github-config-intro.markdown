---
header-id: configuring-your-github-repository
---

# Configuring Your Github Repository

Upon receiving a DXP Cloud onboarding email, you're provisioned a GitHub 
repository hosted in the `dxpcloud` organization. This initial repository only 
exists to help you get started; it expires after 10 days. 

You must

1.  Transfer the initial repository to your own GitHub repository. 

2.  Integrate that repository with the Jenkins (CI) service in DXP Cloud. 

Here, you'll learn how to do this. 

| **Warning:** The initial GitHub repository that DXP Cloud provides for you 
| expires after 10 days. 

## Transferring the Repository

Follow these steps to transfer the initial repository to your own GitHub 
repository: 

1.  Create a new private GitHub repository. 

2.  Clone your initial `dxpcloud` repository locally. 

3.  Push the cloned repository from step two to the remote repository you 
    created in step one. 

If you need help creating, cloning, and pushing GitHub repositories, see 
[GitHub's documentation](https://help.github.com). 

## Integrating with the Jenkins Service

Now you must integrate your new repository with the Jenkins service in DXP 
Cloud. To do this, you must set up a webhook in GitHub that pushes to the 
Jenkins service: 

1.  In GitHub, go to your repository's *Settings* page and select *Webhooks*. 

2.  Click *Add Webhook*. This opens the *Add webhook* form. 

3.  In the *Payload URL* field, add the domain of your DXP Cloud `infra` 
    environment's Jenkins service. For example, the URL of the `infra` 
    environment's `ci` service for a project named `acme` is 
    `https://ci-acme-infra.lfr.cloud/github-webhook/`. Note that the relative 
    path `github-webhook` is required to integrate with the Jenkins GitHub 
    plugin. 

4.  In the *Content type* selector menu, select *application/json*. 

5.  Leave the *Secret* field blank and ensure that *Enable SSL verification* is 
    selected. 

    ![Figure 1: Specify the payload URL and content type, and enable SSL verification.](../../images/webhook-1.png)

6.  Under *Which events would you like to trigger this webhook?*, select 
    *Let me select individual events*. A list of events then appears. 

7.  Select *Pushes* and *Pull Requests* from the list of events. 

    ![Figure 2: You need to select individual events for this webhook.](../../images/webhook-2.png)

    ![Figure 3: Select Pushes, and Pull Requests.](../../images/webhook-3.png)

8.  Make sure *Active* is selected, then click *Add webhook*. 

    ![Figure 4: Set the webhook to Active and finish creating it.](../../images/webhook-4.png)

### Setting Environment Variables

Lastly, you must set two environment variables in the Jenkins service's 
`LCP.json` to point to your new repository: 

-   `GITHUB_REPOSITORY`: Point to your new GitHub repository (remote). 
-   `GITHUB_TOKEN`: Point to a personal access token that you created for your 
    GitHub organization. For instructions on creating and accessing this token, 
    see 
    [GitHub's documentation](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line). 

After updating these environment variables, deploy a new build with the changes. 
Any pushed branches and pull requests in your new repository should now trigger 
a Jenkins build. 
