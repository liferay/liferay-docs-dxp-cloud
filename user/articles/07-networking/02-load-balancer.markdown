---
header-id: load-balancer
---

# Load Balancer

The Ingress load balancer gives Internet access to your environment's services 
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

You can set which internal port (`targetPort`) the service endpoint on the load 
balancer will route to. DXP Cloud automatically configures the correct port for 
the services it provides. 

```json
"targetPort": 3000
```

![Figure 3: The load balancer shows your port configurations.](../../images/load-balancer-port.png)

## Custom SSL

When you specify the load balancer attribute for a service, it adds a service 
endpoint called `<SERVICE-NAME>-<PROJECT-NAME>-<ENVIRONMENT-NAME>.lfr.cloud` for 
you automatically. So for the *webserver* service in the *prd* environment in 
project *acme*, the endpoint would be `webserver-acme-prd.lfr.cloud`. These 
domains created by our infrastructure at `.lfr.cloud` are covered by a wildcard 
certificate that will not display in the SSL certificates section on the network 
page. 

In addition, for all custom domains that are added through the console or 
`LCP.json`, Liferay DXP Cloud will reach to to Let's Encrypt for a certificate 
that covers all custom domains you create and is renewed automatically for you. 

However, you also have the freedom to customize by adding your own SSL 
certificate to cover any *custom domains* that you want to create. Only one 
custom certificate can be added to `LCP.json`, so it needs to cover all of the 
custom domains. Basically only one certificate for custom domains can exist at a 
time for a service, either the one Let's Encrypt provides or the custom 
certificate you specify in `LCP.json`. This custom certificate you specify takes 
precedent over the one given by Let's Encrypt, in the case that Let's Encrypt 
had already granted a certificate to a service. 

Please note that management of the custom certificate is up to you, including 
updating it when new custom domains are added and renewing it when it expires. 
To add a custom certificate, provide a key and certificate in Base64 format: 

```json
"ssl": {
  "key": "...",
  "crt": "..."
}
```

The network page shows the custom certificates created, with a maximum of one 
per service. 

![Figure 4: DXP Cloud shows the status of SSL certificates that cover custom domains.](../../images/load-balancer-ssl-cert.png)

To find out more about custom domains, please read 
[this article](/docs/-/knowledge_base/dxp-cloud/custom-domains). 
