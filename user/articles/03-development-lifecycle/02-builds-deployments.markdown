# Builds and Deployments

## Builds

Your application must first go through a build phase before it can be deployed 
to an environment. This initial build phase is when DXP Cloud gets the Docker 
images, creates your container environment, and runs all tasks and build 
configurations specified in your image. 

You can check your environment's build process by clicking the *Builds* tab on 
the top-right side of each environment page. 

![Figure 1: The builds tab lists the builds in your environment.](../../images/builds.png)

## Deployments

If your service builds without errors, then it can be deployed to an 
environment. Once triggered, this deployment process pushes the build to the 
registry and makes it available to your users. During the deployment phase, DXP 
Cloud runs health checks on your services. If these checks succeed, the 
deployment is healthy and ready. 

To access the deployment page, go to your environment page and click the 
*Deployments* tab on the top-right side. 

![Figure 2: The builds tab lists the builds in your environment.](../../images/deployments.png)

## Deploying to Different Environment

When you deploy a build, it deploys by default to the same environment it was 
built in. To deploy it to a different environment, select *Deploy Build to* from 
the build's Actions button. 

![Figure 3: You can also deploy builds to different environments.](../../images/builds-deploy-to.png)
