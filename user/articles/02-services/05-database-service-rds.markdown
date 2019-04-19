# Database Service (RDS) [](id=database-service-rds)

The Relational Database Service (RDS) is a distributed relational database 
service designed to simplify the setup, operation, and scaling of your 
applications. It's a private service inside your application environment and can 
only communicate with your other services, not the public internet. 

![Figure 1: The Relational Database Service is one of several services available in DXP Cloud.](../../images/services-database.png)

## Environment Variables [](id=environment-variables)

`WEDEPLOY_DBNAME`: Your database's name. 

`WEDEPLOY_MASTER_USER_NAME`: The primary user username for your database. 

`WEDEPLOY_MASTER_USER_PASSWORD`: The password for your primary user.

## Managing Your Database [](id=managing-your-database)

You can use the 
[Adminer](https://hub.docker.com/_/adminer) 
service to manage your database. With Adminer deployed in an environment, you 
can create, delete, modify, or visualize the environment's database. You can 
also export or import a database from any of its supported file extensions 
(e.g., `.sql`, `.csv`, `.tsv`). 

Follow these steps to add Adminer to your environment: 

1.  Go to the repository's `wedeploy` folder and create the `adminer` folder. 

2.  Inside `wedeploy/adminer`, create a file called `wedeploy.json` that 
    contains this code: 

        {
            "id": "admin",
            "image": "adminer:4.3"
        }

3.  Commit and push these changes to your repository. 

4.  Go to your environment's services and access the Adminer service. 

5.  Log in with the username and password configured with your database service. 

Note that Adminer's default upload size is 2 MB. If you want to import larger 
files, you must store PHP configurations from your container at 
`/usr/local/etc/php/conf.d`. Here are some Adminer configurations: 

-   `upload_max_filesize = 500M`
-   `post_max_size = 500M`
-   `memory_limit = -1`
-   `max_execution_time = 0`
