---
header-id: services
---

# Services

DXP Cloud contains several built-in services that provide its functionality and 
help you manage your projects. You can use and configure these services to fit 
your project's needs. 

## Updating Service Images

Please check back to our 
[services changelog](https://help.liferay.com/hc/en-us/categories/360001192512-Liferay-DXP-Cloud-Announcements) 
frequently to make sure you are using the most up-to-date service images. In the 
future, we plan to notify customers when new images become available through the 
console. All Liferay DXP Cloud images are hosted at 
https://hub.docker.com/u/liferaycloud. After finding the latest images, update 
them in `gradle.properties` in your Liferay DXP Cloud workspace. 

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
