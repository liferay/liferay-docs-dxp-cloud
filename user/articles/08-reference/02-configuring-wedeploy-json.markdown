# Configuring via the wedeploy.json

The `wedeploy.json` file is used to configure your container requirements.
There, you can configure properties like id, memory, number of CPUs, environment
variables, volumes, and much more. Here is a table which contains all the
properties that you can add to your `wedeploy.json`.

Field          | Type           | Default        | Description    |
---------------|----------------|----------------|----------------|
id             | String         | random         | The ID representing your service name |
image          | String         | wedeploy/hosting | Service image from Docker Hub |
env            | Object         | undefined      | Environment variables |
port           | Number         | 80             | Exposed service port |
cpu            | Number         | 1              | Number of processing units |
scale          | Number         | 1              | Starting number of instances  |
memory         | Number         | 512            | Amount of computing memory (in MB) |
volumes        | Object         | undefined      | Paths to persist data |
customDomains  | Array          | []             | Set custom domain names |
healthCheck    | Object         | localhost      | How the services' health is checked |
dependencies   | Array          | []             | Deployment dependency order |
zeroDowntime   | Boolean        | true           | Interruption during deployment |
public         | Boolean        | true           | Make the service reachable through its public URL |
environments   | Object         | {}             | Target environment to have its configurations modified |
deploy         | Boolean        | true           | Allow deployment to a environment |

## Usage

Here is an example of all the properties being used in the `wedeploy.json`: 

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
