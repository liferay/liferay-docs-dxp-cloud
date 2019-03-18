# Environment Variables

Environment variables are a set of dynamic placeholders that can affect the way
a certain service will behave within an environment. For example, if you want to
connect a Liferay instance to a database, you can pass the database URL, user,
and password via environment variables. You can add environment variables to
your application via web console or `wedeploy.json`.

## Adding via Web Console

To add environment variables to your service, all you have to do is go to its
environment variables page and add as many variables as you need.

![Figure 1: You can add environment variables via the web console.](../../images/web-console-env-variables.png)

## Adding via wedeploy.json

You can also add environment variables via your `wedeploy.json` by using the 
`env` property: 

    {
      "id": "db",
      "image": "mysql",
      "env": {
        "MYSQL_ROOT_PASSWORD": "pass",
        "MYSQL_ROOT_USER": "example"
      }
    }
