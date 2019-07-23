---
header-id: persistent-file-system-volumes
---

# Persistent File System (Volumes)

When establishing your persistent file system (your volume), you must choose the 
folders that contain the data you want to persist. For example, to persist files 
from a Liferay DXP instance located at `/liferay/opt/data`, you must add the 
`volumes` configuration to your `LCP.json`. This configuration must contain a 
key for each volume. For example, the following configuration contains a `data` 
key for `/liferay/opt/data`: 

```json
{
    "id": "lfr",
    "memory": 6144,
    "cpu": 4,
    "volumes": {
        "data": "/liferay/opt/data"
    }
}
```

## Sharing Volumes Between Different Services

Because all volumes in an environment are shared, you can share content between 
services. You do this by setting the service's ID and location (absolute path) 
of the content to share, in in the service's `LCP.json`. For example, this 
service (`service1`) shares photos from `/photos`: 

```json
{
  "id": "service1",
  "volumes": {
    "photos": "/photos"
  }
}
```

This service (`service2`) shares photos from `/documents/images`: 

```json
{
  "id": "service2",
  "volumes": {
    "photos": "/documents/images"
  }
}
```

In these examples, note the shared volume key `photos`. Both services can access
the files within the volume via the key and declared file paths. 

| **Note:** To delete your service volumes, you can delete the environment that 
| your services belong to. 
