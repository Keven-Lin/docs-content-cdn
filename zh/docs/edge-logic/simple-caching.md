## Simple Caching

A property that always returns a fixed string is not very interesting. A typical CDN configuration usually requires the proxy servers to fetch some content from some origin servers and cache the content for a certain period of time for end users to retrieve. Assume you need to accelerate the hostname "faster.cdnetworks.com" and that the origin server’s hostname is "[www.cdnetworks.com](https://www.cdnetworks.com)". By default, you want the CDN360’s proxy server to cache the content following the `cache-control` and `expires` headers from the origin. If the origin does not specify an object’s cache time, you want to cache for 10 minutes. Because you know that HTML, CSS, PNG, JS, and JPEG files won’t be updated frequently, you want to cache them for a day if the origin’s instruction is shorter than a day. The Edge Logic should resemble the following:
```nginx
location / { # the default location
  proxy_cache_valid 10m; # cache for 10 min if no instruction from the origin
  origin_pass www_origin; # fetch content from this origin
}
location ~ /.*\.(html?|css|png|js|jpe?g) { # static content
  proxy_cache_valid 1d; # cache for a day if no instruction from the origin
  proxy_cache_min_age 1d; # cache for a day even if origin's 
                          # max-age is less than a day.
  origin_pass www_origin; # fetch content from this origin
}
```
There are two "[location](http://nginx.org/en/docs/http/ngx_http_core_module.html#location)" directives:

*   The first is a prefix matching.
*   The second is a regular expression matching. 

Based on the description of the directive in the [official NGINX documentation](http://nginx.org/en/docs/http/ngx_http_core_module.html#location), the regex matching has higher priority than the prefix matching. So all the matching file types are handled with the settings in the second location block, while the others are handled by the first one. 
*   [`proxy_cache_valid`](</docs/edge-logic/supported-directives.md#proxy_cache_valid>) – this directive is the standard NGINX way of specifying cache time for objects without caching instructions from the origin. By default, the specified cache time (in this case, 10 minutes) is applied to origin responses with status codes 200, 301, and 302. Again, you can follow the [official NGINX documentation](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache_valid) to apply it to other status codes. 
*   [`proxy_cache_min_age`](</docs/edge-logic/supported-directives.md#proxy_cache_min_age>)  – this is a CDN360-proprietary directive that takes one parameter. If the "max-age" value from origin is smaller than the specified value, it makes sure the content is cached for at least the specified duration. 
*   [`origin_pass`](</docs/edge-logic/supported-directives.md#origin_pass>) – this is another proprietary directive to access the origin. It is a wrapper of NGINX’s "[proxy_pass](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass)", "[proxy_set_header](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_set_header)", "[proxy_ssl_name](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_ssl_name)", and a few other proxy directives. 
*   `www_origin` – this is the name you assign to the origin, which should be defined in the "origins" field of the property.
