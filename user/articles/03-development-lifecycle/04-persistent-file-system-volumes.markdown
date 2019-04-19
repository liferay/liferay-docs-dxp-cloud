# Persistent File System (Volumes) [](id=persistent-file-system-volumes)

## Defining Volumes [](id=defining-volumes)

When establishing your persistent file system (your volume), you must choose the 
folders that contain the data you want to persist. For example, to persist files 
from a Liferay DXP instance located at `/liferay/opt/data`, you must add the 
`volumes` configuration to your `wedeploy.json`. This configuration must contain 
a key for each volume. For example, the following configuration contains a 
`data` key for `/liferay/opt/data`: 

    {
        "id": "lfr",
        "port": 8080,
        "memory": 6144,
        "cpu": 4,
        "volumes": {
            "data": "/liferay/opt/data"
        }
    }

## Sharing Volumes Between Different Services [](id=sharing-volumes-between-different-services)

Because all volumes in an environment are shared, you can share content between 
two or more services. You do this by specifying the service's ID and the 
location of the content to share, in the service's `wedeploy.json`. For example, 
this service (`service1`) shares photos from `/photos`: 

    {
      "id": "service1",
      "volumes": {
        "photos": "/photos"
      }
    }

This service (`service2`) shares photos from `/documents/images`: 

    {
      "id": "service2",
      "volumes": {
        "photos": "/documents/images"
      }
    }

In these examples, note the shared volume key `photos`. Both services can access 
the files within the volume via the key and declared file paths. All volumes 
must use absolute paths. 

**Note**: To delete your service volumes, you can delete the environment that 
your services belong to. 
