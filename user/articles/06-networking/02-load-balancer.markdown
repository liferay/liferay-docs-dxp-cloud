---
header-id: load-balancer
---

# Load Balancer

The Ingress load balancer gives Internet access to your environment's services 
via proxied HTTP(S) connections. Each load balancer has a static IP that can set 
up custom domains. 

![Figure 1: Environment load balancer configured with a custom domain.](../../images/load-balancer.png)

Having a dedicated load balancer comes with a myriad of enhanced features,
including CDN, port configuration, and custom SSL certificates. 

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

![Figure 2: The CDN's status is visible in DXP Cloud.](../../images/cdn-active.png)

## Port

You can set which internal port (`targetPort`) to route to your service's 
external endpoints on the load balancer. DXP Cloud automatically configures the 
correct port for the services it provides, but custom services may need further 
configuration. 

```json
"targetPort": 3000
```

![Figure 3: The load balancer shows your port configurations.](../../images/load-balancer-port.png)

## Custom SSL

The system provisions an SSL certificate to every service on DXP Cloud. These 
certificates can be used indefinitely, but you can customize them via SSL 
configurations. To do so, provide a key and certificate in Base64 format: 

```json
"ssl": {
  "key": "...",
  "crt": "..."
}
```

![Figure 4: DXP Cloud shows the status of SSL certificates for services configured on the load balancer.](../../images/load-balancer-ssl-cert.png)
