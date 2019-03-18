# Private Networks

Every environment has its own private network, this allows services from the
same environment to communicate with each other through multiple secure
communication protocols. Imagine you want to connect a Liferay Portal instance
hosted on your local machine to a database hosted on DXP Cloud, this will work
only if your database provides an HTTP interface. On the other hand, if your
Liferay Portal instance is hosted on DXP Cloud, you can simply refer your
database by using its service ID.

Every service inside an environment is reachable through its ID. This means that
you can communicate from one service to another by passing the service ID as the
address.

For example, imagine you have a MySQL service hosted on DXP Cloud with the
following configurations:

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

Now, if you want to connect your Liferay Portal instance to this MySQL service,
this would be the configuration of your `portal-ext.properties`:

    jdbc.default.driverClassName=com.mysql.jdbc.Driver
    jdbc.default.password=passw0rd
    jdbc.default.username=root
    jdbc.default.url=jdbc:mysql://db/lportal?characterEncoding=UTF-8&amp;dontTrackOpenResources=true&amp;holdResultsOpenOverStatementClose=true&amp;useFastDateParsing=false&amp;useUnicode=true

Notice that we just declared the ID (`mysql`) as the URL to call the MySQL 
service.

## Configure a Service as Private

By default, all services are available for public access via their DXP Cloud
URLs. If you want to make a service private, you can configure the `public` key
to false. This way, your service will only be reachable by other services inside
your environment but will not be exposed by the load balancer.

    {
        "id": "app",
        "public": false
    }
