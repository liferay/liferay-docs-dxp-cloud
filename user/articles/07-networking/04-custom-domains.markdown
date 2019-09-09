---
header-id: custom-domains
---

# Custom Domains

To add a custom domain to a DXP Cloud service, you must first register that 
domain with the dedicated environment IP as an `A` record. Do this using any 
domain name registrar of your choice. Officially DNS propogation takes up to 
24-48 hours to take effect, but in actuality it's much faster nowadays and can 
take a matter of minutes, depending on the registrar. During this propagation 
process, depending on the DNS server that a device reaches out to, one device 
may be able to reach the domain at the updated address while another cannot. 
Eventually the domain will be reachable from a given device and return the 
standard `default backend - 404` error from Kubernetes' ingress controller. Now 
we are ready for the next step. 

| **Note:** The dedicated environment IP can be found on the Custom Domains tab 
| of a service or on the Network page. 

![Figure 1: This example uses Cloudflare as a domain name registrar to create DNS records.](../../images/dns-records.png)

## Adding Your Domain to Your Service

Once the domain is reachable, you can add your domain to your service and 
Liferay DXP Cloud will handle the routing for you. You can do this via the web 
console or `LCP.json`. 

Follow these steps to add custom domains via the web console: 

1.  Go to your environment page. 

2.  Select the service you want to add your custom domains to. 

3.  Click the *Custom Domains* tab and add your custom domains. 

![Figure 2: Use the service's Custom Domains tab to add your domains.](../../images/custom-domains.png)

Alternatively, you can add your custom domains via the `customDomains` property 
in `LCP.json`: 

```json
{
  "id": "liferay",
  "loadBalancer": {
    "customDomains": ["acme.com", "www.acme.com"]
  }
}
```

Please note that Google has a restriction that only 50 custom domains can be 
added to its ingress. 

## Verifying a Custom Domain's Status

Once you have added a custom domain, you will need to wait some time before the 
service endpoint is reachable and stops responding with a 
`default backend - 404` error. 

Behind the scenes, a couple of steps are taking place. First the route needs to 
be added to the ingress controller, which can take around 30 minutes depending 
on the region. After this, Liferay DXP Cloud reaches out to Let's Encrypt for a 
SSL Server Certificate. Then Let's Encrypt responds with a challenge. Once the 
challenge is passed the ingress controller will be updated with the certificate, 
and the service will be reachable (and secure)! If you try to reach the domain 
while this challenge process is happening, you will see security warnings in 
your browser. These can be safely ignored and signify that the process has not 
been completed yet. 

Apart from trying to reach the service endpoint through a browser, you can 
verify its status on the Network page. 

![Figure 3: View all your endpoints and custom domains on the Network page.](../../images/custom-domains-status.png)

To find out more about using SSL certificates in Liferay DXP Cloud, including 
how to setup your own custom SSL certificate, please read 
[this article](/docs/-/knowledge_base/dxp-cloud/load-balancer). 
