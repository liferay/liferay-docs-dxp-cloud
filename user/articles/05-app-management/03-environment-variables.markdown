---
header-id: environment-variables
---

# Environment Variables

Environment variables are a set of dynamic placeholders that can affect the way 
a service behaves within an environment. For example, if you want to connect a 
Liferay DXP instance to a database, you can pass the database's URL, user, and 
password via environment variables. You can add environment variables to your 
application via the web console or `LCP.json`. 

## Adding Environment Variables via the Web Console

To add environment variables to your service, follow these steps: 

1.  Go to the service's *Environment Variables* tab. 

2.  Add as many variables as you need. Enter each environment variable as a 
    key-value pair, with the variable name (key) in a field on the left, and the 
    value in the field to its right. 

3.  Click *Save*. The service now restarts with the updated environment 
    variables. 

![Figure 1: You can add environment variables via the web console.](../../images/env-vars-add-web-console.png)

## Adding Environment Variables via LCP.json

You can also add environment variables via your `LCP.json` by using the `env` 
property. This example adds the environment variables `MYSQL_ROOT_PASSWORD` and 
`MYSQL_ROOT_USER` with the values `pass` and `example`, respectively: 

```json
{
  "id": "db",
  "image": "mysql",
  "env": {
    "MYSQL_ROOT_PASSWORD": "pass",
    "MYSQL_ROOT_USER": "example"
  }
}
```
