## Frequently Asked Questions

### How the cache time for an object is determined?

There are many directives you can use in the Edge Logic to control the cache time. If none of them is configured, the default behavior of CDN360 edge servers is to "honor the origin". That is, the instructions in the `Cache-Control` and `Expires` header fields are followed. If these two fields are not present in a response from the origin, the response is not cached. The presence of the `Set-Cookie` header field also prevents caching of the response. 

We modified the open-source NGINX to strictly follow the HTTP standard regarding 'zero-time cache'. When `no-cache` or `max-age=0` is present in the `Cache-Control` header field, the response is still cached but expires immediately. Any subsequent request for this object will result in a revalidation request to the origin with the `If-Modified-Since` header. If `no-store` is in the `Cache-Control` header field, the response will not be cached.

By default, the `Date` header field is [passed all the way](</docs/edge-logic/supported-directives.md#proxy_pass_header>) from the origin to the edge servers. Efforts have also been made to ensure the `Age` header field reflects the time since the response is retrieved from the origin, even when parent cache is used.

If the default behavior mentioned above does not meet your requirement, use the following directives to alter it.

* To ignore one or more of the three special header fields above, you can use the [`proxy_ignore_headers`](</docs/edge-logic/supported-directives.md#proxy_ignore_headers>) directive. For example:
```nginx
proxy_ignore_headers Set-Cookie;
```
In this case, the servers will behave as if the `Set-Cookie` header does not exist.
* [`proxy_cache_valid`](</docs/edge-logic/supported-directives.md#proxy_cache_valid>) can be used to set a cache time if the three special header fields are not present or ignored. You can use it multiple times to set different cache times for different status codes. For example:
```nginx
location / { # the default location
    proxy_cache_valid 5m; # cache 200, 301 and 302 for 5 minutes
    proxy_cache_valid 404 2m; # cache 404 for 2 minutes
}
location /no-cache {
    proxy_cache_valid 200 0; # cache 200 response, but revalidate every time.
}
```
* While [`proxy_ignore_headers`](</docs/edge-logic/supported-directives.md#proxy_ignore_headers>) ignores the specified header fields altogether, [`proxy_ignore_cache_control`](</docs/edge-logic/supported-directives.md#proxy_ignore_cache_control>) can be used to ignore specific directives in the `Cache-Control` header field. For example:
```nginx
proxy_ignore_cache_control no-cache no-store;
```
* The CDN360 proprietary directive [`proxy_cache_min_age`](</docs/edge-logic/supported-directives.md#proxy_cache_min_age>) can be used to override the `max-age` in the `Cache-Control` header field to enforce a minimum cache time.
* If you don't want a request to be served from the cache, you can use the [`proxy_cache_bypass`](</docs/edge-logic/supported-directives.md#proxy_cache_bypass>) directive. [`proxy_no_cache`](</docs/edge-logic/supported-directives.md#proxy_no_cache>) can be used to prevent a response from being cached.

Since you are interested in the caching behavior of CDN360, you may want to also learn how to [customized the cache key](#how-to-include-query-parameters-andor-request-headers-in-the-cache-key) and how [the `Vary` header is treated](#the-support-and-non-support-of-vary).

### How to include query parameters and/or request headers in the cache key?

By default, the CDN360 cache key includes only the hostname and URI without the query string in the request. It also includes a special variable that is accessible in the Edge Logic: `$cache_misc`. Therefore, if you want to add anything to the cache key, add it to this variable. For example, to keep the entire query string in the cache key:
```nginx
set $cache_misc "?$sorted_querystring_args";
```
If you want to include only some of the query parameters, the following example shows how to add parameters "abc" and "def" to the cache key:
```nginx
set $cache_misc "?abc=$arg_abc&def=$arg_def";
```
Similarly, the following example shows how to include some request headers in cache key:
```nginx
set $cache_misc "ae=$http_accept_encoding";
set $cache_misc $cache_misc."hdr1=$http_header1&hdr2=$http_header2";
```
If you want to keep any previously assigned value, you can append to this variable:
```nginx
set $cache_misc "${cache_misc}hdr1=$http_header1&hdr2=$http_header2";
```

### HTTP Header Manipulation

If you need to add, modify, or delete some header fields in the request to the origin, use the [`origin_set_header`](</docs/edge-logic/supported-directives.md#origin_set_header>) directive. For example:
```nginx
origin_set_header CDN-Name Quantil;
```
In particular, this is the code to send the client's IP address to the origin server:
```nginx
origin_set_header Client-IP $client_real_ip;
```
In order to consolidate the responses from the origin to improve the cache hit ratio, we created a dedicated directive [`sanitize_accept_encoding`](</docs/edge-logic/supported-directives.md#sanitize_accept_encoding>) to modify the `accept-encoding` request header received from the client.

If you need to add, modify, or delete some header fields in the response to clients, use the [`add_header`](</docs/edge-logic/supported-directives.md#add_header>) directive. For example:
```nginx
add_header CDN-Name Quantil;
```
We also created a proprietary directive [`origin_header_modify`](</docs/edge-logic/supported-directives.md#origin_header_modify>) to manipulate the response header from the origin prior to processing the response. This can be very useful if you need to override a header value (such as cache time) from the origin that may affect the CDN servers' behavior.


### The support (and non-support) of `Vary`

By default, CDN360 servers remove any `Vary` header in the response from origin servers. Therefore, every URL will have no more than one cached version. If you want to cache different versions based on a request header or cookie values, put them explicitly into the cache key by setting the `$cache_misc` variable mentioned above. For example:
```nginx
set $cache_misc "ae=$http_accept_encoding";
```
If you want to send a `Vary` header to the clients to make sure they cache different variations properly, use the [`add_header`](</docs/edge-logic/supported-directives.md#add_header>) directive. If you have to pass the `Vary` header from the origin to the client, use the following configuration to "undo" the default removal of the header:
```nginx
# preserve the Vary header from origin
origin_header_modify Vary "" policy=preserve;
# ignore the Vary header, just pass it to the client
proxy_ignore_headers Vary; 
```
In this case, the servers cache the content as if the `Vary` header does not exist. Without `proxy_ignore_headers Vary`, the preserved `Vary` header would prevent the response from being cached because [`proxy_cache_vary off`](</docs/edge-logic/supported-directives.md#proxy_cache_vary>) is configured by default. If it is absolutely important for the CDN360 servers to cache multiple versions based on the `Vary` header, contact CDNetworks customer support to obtain permission to set `proxy_cache_vary on`.

### How to follow redirections from origin?

When the origin responds with a 30x redirect, you may want the CDN servers to chase it until the redirection stops. Passing the redirection to the client takes more time to get the final content. If you want to turn on this feature, use the directive [`origin_follow_redirect`](</docs/edge-logic/supported-directives.md#origin_follow_redirect>) in the location where it is needed.

### China Delivery and Beian

The Chinese Ministry of Industry and Information Technology (MIIT) requires every domain served from a server in Mainland China to have a record in its system. This is called [ICP Beian (备案)](https://beian.miit.gov.cn/). For certain domains, a [Security Beian](https://www.beian.gov.cn/) is also required. As a CDN provider, CDNetworks cannot use our servers in China to serve domains without ICP Beian. Any violation may result in our China-based servers being blocked. Customers are responsible for filing and obtaining Beian for any domain that needs local delivery in China. We can provide consulting services to assist with this process. For domains without Beian, CDNetworks can use servers located in close proximity to Mainland China (for example, Hong Kong, Korea, and Japan) to deliver content to clients in Mainland China; however, the performance will not be as good as local delivery.

If you have one or more domains with ICP Beian and want them to be accelerated in China, contact customer service to ensure we have all the required information on file about your business. After confirming that we have the necessary information, your China Delivery service will be enabled. You can then perform the following steps to enable local delivery of domains in Mainland China: 

1. Create an [Edge Hostname](</docs/portal/traffic-management/creating-edge-hostname.md>) with "hasBeian" set to true, and use this edge hostname for the domain to be accelerated. This ensures that GSLB will direct traffic of this domain to our servers in Mainland China. 

2. Set "hasBeian" to true in the [property](</docs/portal/edge-configurations/creating-property.md>) of this domain. This ensures the configuration will be deployed to servers in China and that those servers will handle client requests to this domain. Otherwise, they will return status code 451.

### How to support WebSocket?

Use the directive [`enable_websocket`](</docs/edge-logic/supported-directives.md#enable_websocket>) in the location where the WebSocket protocol is needed. Make sure the client uses HTTP/1.1 (not HTTP/2) to connect. This directive also sets the read and send timeouts to 21s by default. They can be changed using the [`origin_read_timeout`](</docs/edge-logic/supported-directives.md#origin_read_timeout>) or [`origin_send_timeout`](</docs/edge-logic/supported-directives.md#origin_send_timeout>) directives.

### What about dynamic content?

Dynamic contents are usually generated on-the-fly for each request and are different for different visitors. Some examples are:
* Realtime stock prices, sports game scores
* Search results based on keywords entered by the visitor
* API calls that have lots of query parameters

If you only have the origin server in a central data center or in the cloud, the performance can be quite poor if the visitor is far away from or does not have a good connection to the data center. How can we accelerate those contents through CDN360? Here are a few things you can do:
* **Simply using CDN360 can shave off a few seconds**

If you use CDN360, your clients will connect to the PoP that is closest to them. The round trip time (RTT) can be a few hundred milliseconds faster than directly connecting to the origin server. The TCP and TLS handshakes usually take 3-4 RTTs which can be a second faster through the CDN. By default, the CDN360 servers maintain persistent connections to the origin. You can increase the [keep-alive timeout](/docs/portal/edge-configurations/managing-origins) to up to 10 minutes in the origin configurations. In the meantime, if you know the content is not cacheable at all, use [`proxy_no_cache 1;`](</docs/edge-logic/supported-directives.md#proxy_no_cache>) and [`proxy_cache_bypass 1;`](</docs/edge-logic/supported-directives.md#proxy_no_cache>) to completely skip caching to minimize latency.
* **Cache the response!**

In many cases, "dynamic" does not mean the content is not cacheable. For example, end users will not experiance the difference if you cache the score of a basketball game for 1 second. If you have 10 requests per second to fetch the score, you can save 90% of the bandwidth and processing power. If the response depends on some query parameter or request header values, make sure those variables are [included in the cache key](#how-do-you-include-query-parameters-andor-request-headers-in-the-cache-key).
* **Enable Fast Route to origin**

CDN360 has a directive [`origin_fast_route`](</docs/edge-logic/supported-directives.md#origin_fast_route>) that enables a "Fast Route" to access the origin. This powerful feature is based on our award-winning [High-speed Data Transmission](https://www.cdnetworks.com/enterprise-applications/high-speed-data-transmission/) (HDT) technology. It ensures that our servers always have the best possible channel to reach your origin, even under challenging situations. This directive can also be used for highly cacheable contents if the origin is hard to reach from certain networks or when the cache-miss performance is critical to you. However, the traffic served through the ""Fast Route" may be charged a higher price due to the extra cost associated with it. To try out this feature, contact the CDN360 support team.
