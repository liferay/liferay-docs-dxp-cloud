# Search Service (Elasticsearch)

The Elasticsearch Service is the full-text search engine for your Liferay DXP
application. It is a private service that only communicates with the other
services in your application and does not with the outside internet.

![Figure 1: The Relational Database Service is one of several services available in DXP Cloud.](../../images/services-search.png)

## Configurations

Even though we have fine-tuned the entire stack of services to work well out of
the box, you may need to configure your Elasticsearch further. To do this, you
can include any `.yml` file inside the config folder. When you deploy your
changes, the config file will be automatically injected into your service and
overwrite the default configuration.

    search
    ├── config
    │ └── elasticsearch.yml
    └── wedeploy.json

## Scripts

For full customization, you can use the scripts extension points. This is the
most powerful and customizable functionality so be careful of what you are
running to avoid causing undesired side effects.

Any `.sh` files found in the `script` directory will be run prior to starting
your service. For example, if you wanted to include a script that removed all
log files, you could include something like this:

    search
    ├── script
    │ └── remove-log-files.sh
    └── wedeploy.json

## Environment Variables

`ES_JAVA_OPTS`: Configure the JVM's heap size. 
