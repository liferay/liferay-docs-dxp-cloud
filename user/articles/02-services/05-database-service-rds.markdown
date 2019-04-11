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

## Managing Your Database

As a simple way for you to manage your database, we present the [Adminer](https://hub.docker.com/_/adminer) service. With Adminer deployed into an environment, you can create, delete, modify or just visualize the database for such enviroment. You can also export or import a database from any of its supported file extencion (e.g. `.SQL`, `.CSV`, `.TSV`).

To add the `Adminer` service to your environment do the following: 

1. Go to repository's `wedeploy/` and create a folder called `adminer`. 
2. Inside `wedeploy/adminer` create a file called `wedeploy.json` containing:
   ```json
     {
       "id": "admin",
       "image": "adminer:4.3"
     }
3. Commit and push these changes to your repository.
4. Go to your environment's services and access the `Adminer`.
5. Log in using the username and password configured your database service.

**Note**: Adminer's default upload size is 2MB. If you want to import files larger than that, you have to store PHP configurations at `/usr/local/etc/php/conf.d` from your container. Here goes some of the Adminer's configurations:
  * `upload_max_filesize = 500M`
  * `post_max_size = 500M`
  * `memory_limit = -1`
  * `max_execution_time = 0`