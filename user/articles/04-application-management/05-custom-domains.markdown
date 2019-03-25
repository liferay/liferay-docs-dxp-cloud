# Custom Domains

## Pointing Your Domain to a DXP Cloud Service

To add a custom domain to a DXP Cloud service, you must point that domain to the
service's URL. To do this, you must use a Domain Management Tool (DMT) and 
create CNAME records to map the domain to the DXP Cloud service. First, go to 
your domain provider configuration and add the servers' addresses to the master
and slave entries. These addresses are provided by the DMT you're using. 

**Note:** Some domain providers let you add CNAME entries. In this case, you 
don't need to use a DMT. 

Once you point your domain to a DMT, you can add a CNAME entry to each domain or 
subdomain you want to add. The value for the full domain can be either 
`dns.us-west-1.liferay.cloud` or the service URL. 

![Figure 1: This example uses Cloudflare as a DMT to point a domain to the DXP Cloud DNS servers.](../../images/cloudflare-ss2.png)

## Adding Your Domain to Your Service

Once you have pointed your domain to a DXP Cloud service, you can add your 
domain to your service. You can do this via the web console or `wedeploy.json`. 

### Adding Your Domain via the Web Console

Go to your environment page, select the service you want to add your custom
domain to, click the *Custom Domains* tab, and add your domains. You can check 
if your certificate was properly created by going to the Activities page. 

![Figure 2: Select the Custom Domains tab and add your domains.](../../images/custom-domain-web-console.png)

### Adding Your Domain via wedeploy.json

You can also add your custom domain via the `customDomains` property in 
`wedeploy.json`: 

    {
      "id": "liferay",
      "customDomains": ["example.com", "www.example.com"]
    }
