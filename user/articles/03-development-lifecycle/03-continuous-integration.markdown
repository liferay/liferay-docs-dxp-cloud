# Continuous Integration [](id=continuous-integration)

DXP Cloud contains Jenkins Continuous Integration by default. When you send a 
pull request or make a commit to one of your pre-configured GitHub branches, it 
triggers an automatic test cycle to check your code for any errors. If the tests 
pass, DXP Cloud builds your services and shows their status on your 
environment's *Builds* page. If the tests fail, you can check the Jenkins 
dashboard and logs at `ci-companyname-infra.us-east-1.lfr.cloud`. 

**Note:** Continuous integration only works if you are deploying from GitHub, 
not from the CLI. 
