# Configuring via the wedeploy.json File

DXP Cloud uses the `wedeploy.json` file to configure your container. You can use 
this file to configure properties like the service ID, memory, number of CPUs, 
environment variables, volumes, and much more. This table lists the properties 
you can add to `wedeploy.json`:

Field          | Type           | Default          | Description    |
---------------|----------------|------------------|----------------|
id             | String         | random           | The service ID |
image          | String         | wedeploy/hosting | The service image from Docker Hub |
env            | Object         | undefined        | Environment variables |
port           | Number         | 80               | Exposed service port |
cpu            | Number         | 1                | Number of CPUs |
scale          | Number         | 1                | Starting number of instances |
memory         | Number         | 512              | Amount of memory (MB) |
volumes        | Object         | undefined        | Paths to persist data |
customDomains  | Array          | []               | Custom domain names |
healthCheck    | Object         | localhost        | Service health checks |
dependencies   | Array          | []               | Dependency deployment order |
zeroDowntime   | Boolean        | true             | Whether service redeployments occur with no downtime |
public         | Boolean        | true             | Whether the service is reachable via its public URL |
environments   | Object         | {}               | Target environment |
deploy         | Boolean        | true             | Whether to allow deployment to an environment |

## Usage

Here's an example `wedeploy.json` file that uses all the properties: 

    {
      "id": "myservice",
      "image": "wedeploy/example",
      "env": {
        "DB_USER": "root",
        "DB_PASSWORD": "pass123",
      },
      "port": 8080,
      "cpu": 2,
      "scale": 2,
      "memory": 2048,
      "volumes": {
        "storage": "/opt/storage"
      },
      "customDomains": ["myservice.com", "www.myservice.com"],
      "healthCheck": {
        "url": "localhost"
      },
      "environments": {
        "prd": {
          "memory": 4096,
          "cpu": 6,
        },
        "dev": {
          "deploy": false
        }
      }
      "dependencies": ["db", "dbadmin"],
      "zeroDowntime": false,
      "public": false
    }
