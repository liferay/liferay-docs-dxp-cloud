---
header-id: database-service-mysql
---

# Database Service (MySQL)

The database service (MySQL) is a distributed relational database service that 
simplifies the setup, operation, and scaling of your applications. It's a 
private service inside your application environment and can only communicate 
with your other services, not the public Internet. 

![Figure 1: The database service is one of several services available in DXP Cloud.](../../images/services-database.png)

## Environment Variables

You can set these environment variables to configure the database service: 

`LCP_DBNAME`: Your database's name. 

`LCP_MASTER_USER_NAME`: The username for your database's primary user. 

`LCP_MASTER_USER_PASSWORD`: The password for your database's primary user. 

## Managing Your Database

You can use the 
[Adminer](https://hub.docker.com/_/adminer) 
service to manage your database. With Adminer deployed in an environment, you 
can create, delete, modify, or visualize the environment's database. You can 
also export/import a database to/from any of its supported file extensions 
(e.g., `.sql`, `.csv`, `.tsv`). 

Follow these steps to add Adminer to your environment: 

1.  Go to the repository's `lcp` folder and create the `adminer` folder. 

2.  Inside `lcp/adminer`, create the `lcp.json` file with this code: 

    ```json
    {
        "id": "admin",
        "image": "adminer:4.3"
    }
    ```

3.  Commit and push these changes to your repository. 

4.  Go to your environment's services and access the Adminer service. 

5.  Log in with your database service's username and password. 

Note that Adminer's default upload size is 2 MB. To import larger files, you 
must store PHP configurations from your container at 
`/usr/local/etc/php/conf.d`. Here are some example Adminer configurations: 

-   `upload_max_filesize = 500M`
-   `post_max_size = 500M`
-   `memory_limit = -1`
-   `max_execution_time = 0`
