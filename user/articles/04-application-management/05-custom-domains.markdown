# Custom Domains

## Pointing Your Domain to DXP Cloud Service

To add a custom domain to a DXP Cloud service you must point your domain to your
service URL. To do this, you have to use a Domain Management Tool (DMT) and
create CNAME records to map your domain to a DXP Cloud service. First, go to
your domain provider configuration and add the servers addresses to the Master
and Slave entries. These addresses are provided by the DMT you've chosen.

**Note:** Some domain providers allow you to add CNAME entries. This way, you do
not need to use a DMT.

Once you are pointing your domain to a DMT, you can add a CNAME entry to each
domain or subdomain you want to add. The value for the full domain can be either
`dns.us-west-1.liferay.cloud` or the service URL. 

![Figure 1: This example uses Cloudfare as a DMT to point your domain to the DXP Cloud DNS servers.](../../images/cloudflare-ss2.png)

## Adding Your Domain to Your Service

Once you have pointed your domain to a DXP Cloud service, you are able to add
your domain to your service. There are two ways to add your domain to a service; 
via the Web Console or the `wedeploy.json`. 

### Adding Your Domain via the Web Console

Go to your environment page, select the service you want to add your custom
domain to, click the *Custom Domains* tab, and add your domains there. You can 
check if your certificate was properly created by going to the Activities page.

![Figure 2: Select the Custom Domains tab.](../../images/custom-domain-web-console.png)

### Adding Your Domain via wedeploy.json

You can also add your custom domain via `wedeploy.json` through the 
`customDomains` property: 

    {
      "id": "liferay",
      "customDomains": ["example.com", "www.example.com"]
    }
