---
header-id: load-balancer
---

# Load Balancer

The Ingress Load Balancer gives Internet access to your environment's services 
via proxied HTTP(S) connections. Each load balancer has a static IP that can set 
up custom domains. 

![Figure 1: You can configure your environment's load balancer with a custom domain.](../../images/load-balancer.png)

Having a dedicated load balancer provides a myriad of enhanced features, such as 
port configuration, custom SSL certificates, and a CDN. Here's an example 
configuration for a load balancer in an `LCP.json` file: 

```json
{
  "id": "webserver",
  "loadBalancer": {
    "cdn": true,
    "targetPort": 80,
    "customDomains": ["acme.liferay.cloud"],
    "ssl": {
      "key": "...",
      "crt": "..."
    }
  }
}
```

## CDN

Liferay's Content Delivery Network (CDN) is a built-in feature provided with DXP 
Cloud. This CDN caches your content globally, greatly enhancing your delivery 
speed. 

This CDN is disabled by default but you can turn it on in your `LCP.json`: 

```json
"cdn": true
```

![Figure 2: The CDN's status is visible on the Network page.](../../images/cdn-active.png)

## Port

You can set which internal port (`targetPort`) the load balancer's service 
endpoint routes to. DXP Cloud automatically configures the correct port for the 
services it provides. 


```json
"targetPort": 3000
```

![Figure 3: The load balancer shows your port configurations.](../../images/load-balancer-port.png)

## Custom SSL

When you specify the load balancer attribute for a service, it adds a service 
endpoint named after this pattern: 

-   `<SERVICE-NAME>-<PROJECT-NAME>-<ENVIRONMENT-NAME>.lfr.cloud`

Consider this example: 

-   Service: webserver
-   Project: acme
-   Environment: prd
-   Service endpoint name: `webserver-acme-prd.lfr.cloud`

These domains created by DXP Cloud's infrastructure at `.lfr.cloud` are covered 
by a wildcard certificate that will not display in the Network page's SSL 
certificates section. 

Also, for all custom domains added through the console or `LCP.json`, Liferay 
DXP Cloud reaches out to 
[Let's Encrypt](https://letsencrypt.org/) 
for a certificate that renews automatically and covers all custom domains you 
create. 

You can, however, add your own SSL certificate to cover any custom domains that 
you want to create. Only one custom certificate can be added to `LCP.json`, so 
it must cover all custom domains. Also, only one certificate at a time can exist 
for a service's custom domains: the one Let's Encrypt provides, or the custom 
one you specify in `LCP.json`. If both exist, your custom certificate takes 
precedent. 

Note that you must manage your custom certificate. This includes updating it 
when new custom domains are added and renewing it when it expires. To add a 
custom certificate, provide a key and certificate in Base64 format: 

```json
"ssl": {
  "key": "...",
  "crt": "..."
}
```

The Network page shows any custom certificates, with a maximum of one per 
service. 

For more information, see 
[Custom Domains](/docs/-/knowledge_base/dxp-cloud/custom-domains). 

![Figure 4: DXP Cloud shows the status of SSL certificates that cover custom domains.](../../images/load-balancer-ssl-cert.png)
