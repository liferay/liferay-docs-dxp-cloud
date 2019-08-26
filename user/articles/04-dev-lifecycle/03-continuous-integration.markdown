---
header-id: continuous-integration
---

# Continuous Integration

DXP Cloud contains 
[Jenkins](https://jenkins.io/) 
continuous integration by default. When you send a pull request or make a commit 
to one of your pre-configured GitHub branches, an automatic test cycle checks 
your code for errors. If the tests pass, DXP Cloud builds your services and 
shows their status on your environment's Builds page. If the tests fail, you can 
check the Jenkins dashboard and logs at `ci-companyname-infra.lfr.cloud`. 

| **Note:** Continuous integration only works if you deploy from GitHub, not the 
| CLI. 
