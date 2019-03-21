# Search Service (Elasticsearch)

The Elasticsearch Service is the full-text search engine for your Liferay DXP 
application. It's a private service that only communicates with the other 
services in your application, not with the outside Internet. 

![Figure 1: The Relational Database Service is one of several services available in DXP Cloud.](../../images/services-search.png)

## Configurations

Although the stack of DXP Cloud services are fine-tuned to work well by default, 
you may need to configure Elasticsearch further. To do this, you can include any 
YML file inside the `config` folder. When you deploy your changes, the config 
file is automatically injected into your service and overwrites the default 
configuration. Here's an example folder structure of such a file inside the 
`config` folder: 

    search
    ├── config
    │ └── elasticsearch.yml
    └── wedeploy.json

## Scripts

You can use scripts for more extensive customizations. However, use caution when 
doing so. This is the most powerful way to customize the search service and can 
cause undesired side effects. 

Any `.sh` files found in the `script` folder are run prior to starting your 
service. For example, to include a script that removes all log files, you could 
place it in the following directory structure: 

    search
    ├── script
    │ └── remove-log-files.sh
    └── wedeploy.json

## Environment Variables

`ES_JAVA_OPTS`: Configure the JVM's heap size. 
