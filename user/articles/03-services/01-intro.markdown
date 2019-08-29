---
header-id: services
---

# Services

DXP Cloud contains several built-in services that provide its functionality and 
help you manage your projects. You can use and configure these services to fit 
your project's needs. 

## Available Services

**Backup Service:** Creates regular backups of your Liferay DXP database and 
Document Library. 

**Liferay DXP Service:** Runs your application's Liferay DXP instance. 

**Web Server Service:** Handles all traffic from your users and acts as a 
high-performance web server. 

**Database Service:** Provides a distributed relational database service that 
simplifies the setup, operation, and scaling of your applications. 

**Search Service:** Provides the full-text search engine for your Liferay DXP 
application. 

## Updating Service Images

Check the 
[services changelog](https://help.liferay.com/hc/en-us/categories/360001192512-Liferay-DXP-Cloud-Announcements) 
frequently to make sure you're using the most up-to-date service images. All 
Liferay DXP Cloud images are hosted at 
[https://hub.docker.com/u/liferaycloud](https://hub.docker.com/u/liferaycloud). 
After finding the latest images, update them in your DXP Cloud workspace's 
`gradle.properties`. 

Several services use third-party images as a foundation (e.g., Elasticsearch, 
NGINX, and Jenkins). Although these images get regular updates from their 
maintainers, we only update the corresponding service when necessary for a 
feature or security. This ensures stability. If you want to update an image's 
version, open a ticket 
[here](https://liferay-support.zendesk.com) 
and work with Liferay Support. The 
[services changelog](https://help.liferay.com/hc/en-us/categories/360001192512-Liferay-DXP-Cloud-Announcements) 
lists any such image updates. 
