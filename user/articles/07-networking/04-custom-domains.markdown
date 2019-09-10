---
header-id: custom-domains
---

# Custom Domains

To add a custom domain to a DXP Cloud service, you must first register that 
domain with the dedicated environment IP as an `A` record. Do this using the 
domain name registrar of your choice. DNS propagation can take up to 24-48 hours 
to take effect, but in some cases takes only a few minutes. During this 
propagation process, depending on the DNS server that a device reaches out to, 
one device may be able to reach the domain at the updated address while another 
cannot. Eventually, the domain will be reachable from any device and return the 
standard `default backend - 404` error from the Ingress Load Balancer. Now 
you're ready for the next step. 

| **Note:** You can find the dedicated environment IP on a service's Custom 
| Domains or the Network page. 

![Figure 1: This example uses Cloudflare as a domain name registrar to create DNS records.](../../images/dns-records.png)

## Adding Your Domain to Your Service

Once the domain is reachable, you can add it to your service and Liferay DXP 
Cloud will handle the routing for you. You can do this via the web console or 
`LCP.json`. 

Follow these steps to add custom domains via the web console: 

1.  Go to your environment page. 

2.  Select the service to which you want to add the custom domains. 

3.  Click the *Custom Domains* tab and add your custom domains. 

![Figure 2: Use the service's Custom Domains tab to add your domains.](../../images/custom-domains.png)

Alternatively, you can add your custom domains via the `customDomains` property 
in the service's `LCP.json`: 

```json
{
  "id": "liferay",
  "loadBalancer": {
    "customDomains": ["acme.com", "www.acme.com"]
  }
}
```

Note that DXP Cloud restricts its Ingress Load Balancer to 50 custom domains. 

## Verifying a Custom Domain's Status

Once you have added a custom domain, you must wait until the service endpoint is 
reachable and stops responding with a `default backend - 404` error. 

Behind the scenes, a couple things occur. First, the route must be added to the 
Ingress Load Balancer, which can take around 30 minutes depending on the region. 
After this, Liferay DXP Cloud reaches out to 
[Let's Encrypt](https://letsencrypt.org/) 
for an SSL Server Certificate. Let's Encrypt responds with a challenge. Once the 
challenge is passed, the Ingress Load Balancer is updated with the certificate 
and the service is reachable and secure. If you try to reach the domain during 
the challenge process, your browser will display security warnings. You can 
safely ignore these warnings because the process is not yet complete. 

Apart from trying to reach the service endpoint through a browser, you can 
verify its status on the Network page. 

To learn more about using SSL certificates in Liferay DXP Cloud, including how 
to set up your own custom SSL certificate, see 
[Load Balancer](/docs/-/knowledge_base/dxp-cloud/load-balancer). 

![Figure 3: View all your endpoints and custom domains on the Network page.](../../images/custom-domains-status.png)
