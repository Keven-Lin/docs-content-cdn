## REST API Acceleration

API calls are usually considered dynamic HTTP requests since the responses are generated
by the server in real time based on some input parameters supplied in the request. As we
mentioned in the [FAQ](/docs/edge-logic/faq#what-about-dynamic-content), dynamic requests
such as REST API calls can be very effectively accelerated by CDN360. For example, the user
of a mobile or web app may repeatedly reload the same page generating lots of 
duplicate API calls in a short period of time. Some caching using a CDN can significantly 
improve the performance. In this article, we are going to use an example to illustrate how
to use the portal to create a property to accelerate an API server.

Here are the assumptions about this task:
* The API server to be accelerated has a hostname: `api.company.com`. The server requires
the request `Host` header to carry this value.
* You currently set up the DNS server to resolve this hostname to two IP addresses: `1.1.1.1`
and `1.1.1.2`
* The API server uses the standard HTTP methods: GET, POST, PUT, DELETE, PATCH.
* The client is using the `Authorization` request header to pass the credential to the
server following the **format** of [basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication).
This makes it easy for the CDN360 servers to obtain the API user name with the built-in
variable `$remote_user`. Please notice that you don't have to use the actual basic
authentication algorithm which transfers the secret password in clear text. You are free 
to use a more sophisticated algorithm like the one for [CDN360 API](https://docs.quantil.com/cdn/apidocs#section/Authentication)
to generate a signature to put after the colon.
* All the input parameters to the API server are specified in the request query string.

To use CDN360 to accelerate this service:
* Create a new DNS record `api-origin.company.com` to point to the two IP addresses. The 
CDN360 servers need to use it to reach the origin. The name `api.company.com` can
no longer be used because we will later CNAME it to a CDN360 edge hostname to direct
client's traffic to the platform to be accelerated.
* No API service should be running without the protection of TLS encryption. You need to
upload the certificate for `api.company.com` to the CDN360 platform. We recommend using 
[Let's Encrypt](/docs/portal/certificates/auto-renewal) to automatically renew the certificate.
<p align=center><img src="/docs/resources/images/recipes/api/upload-certificate.png" alt="upload certificate" width="700"></p>

* Go to the CDN360 portal to create a property to accelerate this API service. It is important
to enter the correct hostname to be accelerated: `api.company.com`.
<p align=center><img src="/docs/resources/images/recipes/api/create-property.png" alt="create property" width="720"></p>

* Enter the information about the origin. A few things to note on this page: The server
is specified with the new DNS record we just created. We are enforcing the HTTPS protocol
to reach the origin to ensure security. The `Host` header is set to the value
required by the origin. In this case, we can actually leave it empty because, by
default, CDN360 will pass the `Host` header value received from the client to the origin. We also
chose "Always Direct" to reach the origin without going through a parent cache because we want to
minimize latency and know there will not be any cache hit across different servers.
<p align=center><img src="/docs/resources/images/recipes/api/origin.png" alt="create origin" width="600"></p>

* Enter the following code into the Edge Logic field. The important thing to note here is
that the API user name and client IP are added to the cache key. This ensures that the 
cached content will be served only to the same user from the same IP address. Combined
with HTTPS and the short cache time of 1 minute, this should be reasonably safe for most 
applications in the industry. By default, only responses to `GET` method are cached. 
You can use the [proxy_cache_methods](/docs/edge-logic/supported-directives#proxy_cache_methods) directive to cache other responses.
Another thing to notice is that we allow the
clients to use the `Cache-Control: no-cache` header field to bypass the cache. When a CDN360
server sees this field value, it will go directly to the origin without looking up the cache.
Lastly, we enabled the [Fast Route to origin](/docs/edge-logic/supported-directives#origin_fast_route)
to ensure stable connections to the origin.

```nginx
location / { #This is the default location.
  # reject http
  if ($request_scheme = http) {
    return 400 "please use https!";
  }
  origin_pass api-origin; #the request URI and query string will be passed to the origin
  # add API user name and client IP into cache key
  set $cache_misc $cache_misc.$remote_user.$client_real_ip;
  # add sorted query string into cache key
  set $cache_misc $cache_misc.$sorted_querystring_args;
  # the client can use Cache-Control: no-cache to by pass cache
  if ($http_cache_control ~ (no-cache|no-store)) {
    set $bypass_cache 1;     #do not use cached copy
  }
  proxy_cache_bypass $bypass_cache;
  proxy_cache_valid 1m; #200, 301, and 302 responses will be cached for 1m
  origin_fast_route on; #enable the Fast Route to origin
}
```
* Make sure the correct certificate is attached to this property. You can configure the
TLS min/max versions and cipher suites based on your security requirements:
<p align=center><img src="/docs/resources/images/recipes/api/attach-certificate.png" alt="attach certificate" width="600"></p>
* Optionally test the above property [in staging](/docs/portal/edge-configurations/testing-property#testing-property-in-staging)
and then deploy to production.
* If you still don't have an edge hostname, create one based on your intended delivery
destination and performance/cost requirement. Then update the DNS record of `api.company.com`
to CNAME to this edge hostname.

Any request to `api.company.com` will now be routed to the CDN360 platform. Every cache miss
or expiration will be forwarded to the origin to validate the credential and fetch the latest content.
If the same request comes again from the same user and the same IP address before the 
cached copy expires, the content will be served immediately by the CDN360 server with
much a smaller turnaround time. The end user will experience improved performance and 
the origin server will not have to generate the same content repeatedly in a 
short period of time. 
