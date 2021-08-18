## An Introduction to the CDN360 Edge Logic

CDN360’s proxy server is developed on top of the open-source software [NGINX](http://nginx.org), which is widely used to build powerful web servers and reverse proxy servers with superior performance. NGINX has its own configuration language, which is described in greater detail on their [documentation website](http://nginx.org/en/docs/).

Starting from 2016, CDNetworks has made significant changes to the open-source version of the software to enhance it as a CDN proxy server. One of CDN360’s main design goals is to give you as much control as possible to self-provision the service. Based on this commitment, we allow you to code directly in the NGINX language to control the proxy servers. We believe this gives you the maximum flexibility to achieve your business requirements.

This document is an introduction about how to accomplish this. Notice that the Edge Logic described in this document is part of the [property configuration](/apidocs#operation/createProperty). You still need to define the other essential parts, such as the hostname(s) to be accelerated, in order to create a complete property that can be deployed to the CDN360 servers. You can do this easily using the [product portal](https://console.cdnetworks.com/cdn) or [API](/apidocs).

Like any other introduction to a new language, let's get started with a "hello world" example.
