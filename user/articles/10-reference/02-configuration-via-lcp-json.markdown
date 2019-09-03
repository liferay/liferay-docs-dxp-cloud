---
header-id: configuration-via-lcp-json
---

# Configuration via LCP.json

Each service in your DXP Cloud environments has an `LCP.json` file that you can 
use to configure the service. You can configure properties like the service ID, 
memory, number of CPUs, environment variables, volumes, and much more. 

This table lists the properties you can add to `LCP.json`: 

Field | Type | Default Value | Description |
----- | ---- | ------------- | ----------- |
`id` | String | random | The service ID |
`image` | String | `""` | The service image from Docker Hub |
`env` | Object | undefined | Environment variables |
`loadBalancer` | Object | `{}` | Declaration of exposed ports and domains |
`cpu` | Number | `1` | Number of CPUs |
`scale` | Number | `1` | Starting number of instances |
`memory` | Number | `512` | Amount of memory (MB) |
`volumes` | Object | undefined | Paths to persist data |
`readinessProbe` | Object | `{}` | Service readiness check |
`livenessProbe` | Object | `{}` | Service liveness check |
`dependencies` | Array | `[]` | Dependency deployment order |
`kind` | String | Deployment | Deployment type (e.g, Deployment or StatefulSet) |
`ports` | Array | `[]` | Declaration of ports and protocols |
`environments` | Object | `{}` | Environment-specific configurations |
`deploy` | Boolean | `true` | Whether the service will be deployed for the specified environment. Only use this property inside the `environments` property; not at the root level. See the sample `LCP.json` file. |
`autoscale` | Object | `{ "cpu": 80, "memory": 80 }` | The target average utilization for CPU and memory in auto-scaling. For more information about how this works with auto-scaling, see [Auto-scaling](/docs/-/knowledge_base/dxp-cloud/auto-scaling). |

## Usage

Here's an example `LCP.json` file that uses all the properties: 

```json
{
  "id": "myservice",
  "image": "liferaycloud/example",
  "env": {
    "DB_USER": "root",
    "DB_PASSWORD": "pass123"
  },
  "loadBalancer": {
    "cdn": true,
    "targetPort": 3000,
    "customDomains": ["example.com"],
    "ssl": {
      "key": "...",
      "crt": "..."
    }
  },
  "cpu": 2,
  "scale": 2,
  "memory": 2048,
  "volumes": {
    "storage": "/opt/storage"
  },
  "livenessProbe": {
    "httpGet": {
      "path": "/status",
      "port": 3000
    },
    "initialDelaySeconds": 40,
    "periodSeconds": 5,
    "successThreshold": 5
  },
  "readinessProbe": {
    "exec": {
      "command": ["cat", "/tmp/healthy"]
    },
    "initialDelaySeconds": 40,
    "periodSeconds": 5
  },
  "dependencies": ["service1", "service2"],
  "kind": "statefulSet",
  "ports": [
    {
      "port": 3400,
      "targetPort": 7000,
      "protocol": "TCP"
    },
    {
      "port": 9000,
      "targetPort": 8000,
      "protocol": "TCP",
      "external": true
    }
  ],
  "environments": {
    "prd": {
      "memory": 4096,
      "cpu": 6
    },
    "dev": {
      "deploy": false
    }
  },
  "autoscale": {
    "cpu": 90,
    "memory": 90
  }
}
```
