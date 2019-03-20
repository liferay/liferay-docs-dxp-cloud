# Continuous Integration

With DXP Cloud, you get a powerful Jenkins Continuous Integration out of the
box. When you send a pull request or make a commit to one of your pre-configured
GitHub branches, it will trigger an automatic test cycle on your code to check
for any errors. If the tests pass, we will build your services and show their
status on the *Builds* page of your environment. 

If your tests fail, you can check the Jenkins dashboard and logs at 
`ci-companyname-infra.us-east-1.lfr.cloud`. 

**Note:** Continuous integration only works if you are deploying from GitHub, 
not from the CLI. 
