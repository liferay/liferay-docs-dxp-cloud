# Builds and Deployments

## Builds

When publishing your application to an environment, it must first go through a
build phase before being deployed. This initial build phase is when we pull the
Docker images, create your container environment, and run all tasks and build
configurations specified in your image.

You can check the build process of your environment by clicking on the *Builds*
tab located on the top-right side of each environment page.

![Figure 1: The builds tab lists the builds in your environment.](../../images/builds.png)

## Deployments

If your service was built without errors, then it will be ready to be deployed
to an environment. Once triggered, this deployment process will push the build
to the registry and making it available to your users. During the deployment
phase, we run Health Checks on your services to make sure they are healthy. When
the checks are successful, the deployment is healthy and ready.

To access the deployment page, go to your environment page and click on the
*Deployments* tab located on the top-right side of the environment page.

![Figure 2: The builds tab lists the builds in your environment.](../../images/deployments.png)

## Deploying to Different Environment

By default, when you deploy a build, it will deploy to the same environment that
it was built to. If you would like to deploy a build to a different environment,
you can just select the menu dropdown on the building activity and select the 
*Deploy Build to* option. 

![Figure 3: You can also deploy builds to different environments.](../../images/builds-deploy-to.png)
