# Custom Domains

To add a custom domain to a DXP Cloud service, you must point that domain to the
dedicated environment IP as a record. 

| **Note:** The dedicated environment IP can be found on the Custom Domains or 
| Network tabs of any service in that environment. 

![Figure 1: This example uses Cloudflare as a DMT to create DNS records.](../../images/dns-records.png)

## Adding Your Domain to Your Service

Once you have pointed your domain to a DXP Cloud environment IP, you can add 
your domain to your service and DXP Cloud handles the routing for you. You can 
do this via the web console or `LCP.json`. 

Follow these steps to add your domain via the web console: 

1.  Go to your environment page. 

2.  Select the service you want to add your custom domain to. 

3.  Click the *Custom Domains* tab, and add your domains. 

You can check if your certificate was properly created by going to the 
Activities page. 

![Figure 2: Select the Custom Domains tab and add your domains.](../../images/custom-domains.png)

Alternatively, you can add your custom domain via the `customDomains` property 
in `LCP.json`: 

```json
{
  "id": "liferay",
  "loadBalancer": {
    "customDomains":["acme.com","www.acme.com"]
  }
}
```

## Verifying Domain Status

Once your domain is set up, you can verify its status and configuration on the
Network tab. 

![Figure 3: View all your endpoints and custom domains on the Network tab.](../../images/custom-domain-status.png)
