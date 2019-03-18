# Persistent File System (Volumes)

## Defining Volumes

When establishing your persistent file system, or as we call it *Volume*, you
are choosing which are the folders that you want to persist its data. Let's say
that you want to persist files from a Liferay Portal instance that is located on
`/liferay/opt/data`, all you have to do is add the `volumes` configuration to
your `wedeploy.json.` It would look like the example below.

    {
        "id": "lfr",
        "port": 8080,
        "memory": 6144,
        "cpu": 4,
        "volumes": {
            "data": "/liferay/opt/data"
        }
    }

As you can see, you can add a key for each volume. In this example, the key
`data` was added and its value is `/liferay/opt/data`.

## Sharing Volumes Between Different Services

Now, let's say that you have two or more different services and you want to
share content between them. We can do this because all volumes are shared within
an environment. You can specify specific ID's to choose which volume you want to
access. For example, imagine you have two services whose service IDs are
`service1` and `service2` and you want to share content located in `/photos`
from the `service1` and content located in `/documents/images` from the
`service2`.

In this scenario, this is how the services would connect to the volumes via
their `wedeploy.json`:

`service1`

    {
      "id": "service1",
      "volumes": {
        "photos": "/photos"
      }
    }

`service2`

    {
      "id": "service2",
      "volumes": {
        "photos": "/documents/images"
      }
    }

In this example, we are sharing the volume ID `photos` between two different
services and both can access the files within that volume by the declared paths.
All volumes must use absolute paths, not relative ones.

**Note**: To delete your service volumes, you can delete the environment that 
your services belong to or deleting it via shell. 
