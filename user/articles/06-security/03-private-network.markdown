# Private Networks [](id=private-networks)

Every environment has its own private network. This allows services from the
same environment to communicate through multiple secure communication protocols. 
For example, to connect a Liferay DXP instance hosted on your local machine to a 
database hosted on DXP Cloud, the database must provide an HTTP interface. 
However, if the Liferay DXP instance is also hosted on the same DXP Cloud 
environment, you can refer to the database via its service ID and therefore 
bypass the need for an HTTP interface. 

Every service in an environment is reachable through its ID. You can therefore 
communicate between services by passing the service ID as the address. For 
example, imagine you have a MySQL service hosted on DXP Cloud with the following 
configuration:

    {
        "id": "db",
        "image": "mysql:5.7",
        "memory": 4096,
        "env":{
            "MYSQL_ROOT_PASSWORD": "passw0rd",
            "MYSQL_DATABASE": "lportal"
        },
        "volumes": {
            "data": "/var/lib/mysql"
        },
        "zeroDowntime": false
    }

To connect your Liferay DXP instance to this MySQL service, you could configure 
your `portal-ext.properties` file like this: 

    jdbc.default.driverClassName=com.mysql.jdbc.Driver
    jdbc.default.password=passw0rd
    jdbc.default.username=root
    jdbc.default.url=jdbc:mysql://db/lportal?characterEncoding=UTF-8&amp;dontTrackOpenResources=true&amp;holdResultsOpenOverStatementClose=true&amp;useFastDateParsing=false&amp;useUnicode=true

Note that the ID (`mysql`) functions as the URL to call the MySQL service. 

## Configure a Service as Private [](id=configure-a-service-as-private)

By default, all services are available for public access via their DXP Cloud
URLs. To make a service private, set the `public` key to false: 

    {
        "id": "app",
        "public": false
    }

This makes your service reachable only by other services in your environment 
(the load balancer doesn't expose the service). 
