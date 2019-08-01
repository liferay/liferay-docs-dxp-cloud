---
header-id: private-network
---

# Private Network

Every environment has its own private network. This lets services from the 
same environment communicate through multiple secure communication protocols 
without having to interact with the public Internet. 

For example, your project by default only exposes your web server service to 
public connections. Connections between other services (e.g., Liferay DXP, 
database, etc.) are routed through the private network. 

For every connection configured in this private network, you must specify these 
variables: 

`targetPort`: The internal port of the service to expose. 

`port`: The external port of the service to connect to. 

`protocol`: The type of connection to create (TCP and UDP are supported). 

`external`: Whether your connection is available to external connections. The 
default value `false` restricts the connection to internal DXP Cloud 
connections. 

Here's an example configuration: 

```json
{
  "id": "db",
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
  ]
}
```
