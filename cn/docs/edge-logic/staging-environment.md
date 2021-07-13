## The Staging Environment

When you create or change a property configuration, you are basically coding with the NGINX configuration language. NGINX configuration is mostly a [declarative language](https://tylermcginnis.com/imperative-vs-declarative-programming/) because it tries to describe the end result instead of the steps to process each request. While it has its benefits, it can also sometimes be confusing. Some parts of this language are actually [imperative](https://tylermcginnis.com/imperative-vs-declarative-programming/), most notably the directives in the [rewrite module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html). For a complicated configuration, it is common that you will need a place to verify you achieve the behavior you expect. This is where the staging environment comes in handy. 

The staging environment has a few isolated CDN360 proxy servers on which you can test the property configuration. You can fully test a server’s behavior and make sure it meets your complete expectations before you deploy the property to the production servers. The staging environment serves as a run-time test environment for the code you write. For your reference, here is a workflow of the [CDN360 service provisioning](</docs/getting-started.md#quick-start>) and [how to test with the staging environment](</docs/portal/edge-configurations/testing-property.md#testing-property-in-staging>). You can also purge the staging servers to test the purging behavior. To find the IP addresses of the staging servers, run "dig staging.qtlcdn.com" in a bash console.