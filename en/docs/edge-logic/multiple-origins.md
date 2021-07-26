## Multiple Origins with `if`

This section describes a use case that is a little bit more complicated than the previous one. Assume a domain needs to load content from two different origins based on the value of a request header `x-origin`. For origin #2, you want to modify the URI by adding an extra root folder "/images" for all the images, HTML, and CSS objects. You need to send a header `x-msg2origin` to the origin, but the value is different for the two origins. The Edge Logic should resemble the following:
```nginx
location / {
  origin_pass origin1; # the default origin
  origin_set_header x-msg2origin "message for origin 1";
  if ($http_x_origin = "origin2") { # check the request header
    origin_pass origin2; # the alternate origin
    origin_set_header x-msg2origin "message for origin 2";
    rewrite /.*\.(html?|css|png|js|jpe?g) /image$uri break;
  }
}
```
<a id="ifcaution"></a>This example uses the [`if` directive in the rewrite module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#if) to check the value in the request header `x-origin` and define different behaviors. However, `if` is a tricky directive due to the conflict between the "[declarative](https://tylermcginnis.com/imperative-vs-declarative-programming/)" nature of the NGINX configuration and the "imperative" nature of the rewrite module. If you need to use `if` in your Edge Logic, observe the following rules:

*   Read the [documentation of the rewrite module](http://nginx.org/en/docs/http/ngx_http_rewrite_module.html) carefully. In particular, try to understand why the `break` parameter is necessary for the `rewrite` directive in the example above.
*   Keep in mind that only the directives in the rewrite module ([`if`](</docs/edge-logic/supported-directives.md#if>), [`set`](</docs/edge-logic/supported-directives.md#set>), [`rewrite`](</docs/edge-logic/supported-directives.md#rewrite>), [`return`](</docs/edge-logic/supported-directives.md#return>), [`break`](</docs/edge-logic/supported-directives.md#break>), [`eval_func`](</docs/edge-logic/supported-directives.md#eval_func>), etc.) are executed in the order they appear (imperatively) in the location block. They are executed in an early phase which precedes most other actions defined by the declarative directives. In the edge logic editor on the portal, the imperative directives are colored in blue while the declarative ones are colored in red so you can tell them apart easily. When there are declarative directives enclosed in `if` blocks, only the ones in the **last** matching `if` block will take effect. For example, consider the following configuration:
```nginx
location / {
  if ($http_header_a != '') {
    add_header has-header-a 1;
  }
  if ($http_header_b != '') {
    add_header has-header-b 1;
  }
  ...
}
```
When both `header-a` and `header-b` are present in the request, only `has-header-b` will be added to the response. This is not a bug, just how NGINX works. However, this behavior can be confusing to new users.
*   Due to the issue mentioned above, you are recommended to refrain from using any declarative directive in `if` blocks, unless there is no other way around. This makes the configuration more readable, especially to people who are not NGINX experts. The example above can be rewritten as follows to achieve the desired result:
```nginx
location / {
  if ($http_header_a != '') {
    set $has_header_a 1;
  }
  if ($http_header_b != '') {
    set $has_header_b 1;
  }
  add_header has-header-a $has_header_a;
  add_header has-header-b $has_header_b;
  ...
}
```
*   Not all directives can be used in an `if` block. This is specified in the "Context" of each directive. For the ones not allowed in an `if` block, if they support variable as parameter, you can still control their behavior based on `if` conditions using the [`set`](</docs/edge-logic/supported-directives.md#set>) directive. For example: [`proxy_cache_valid`](</docs/edge-logic/supported-directives.md#proxy_cache_valid>), [`proxy_redirect`](</docs/edge-logic/supported-directives.md#proxy_redirect>) and [`proxy_cookie_domain`](</docs/edge-logic/supported-directives.md#proxy_cookie_domain>).
*   Another way to manipulate the request and response headers conditionally is to use the proprietary `if()` parameter introduced to the [`add_header`](</docs/edge-logic/supported-directives.md#add_header>), [`origin_set_header`](</docs/edge-logic/supported-directives.md#origin_set_header>), and [`origin_header_modify`](</docs/edge-logic/supported-directives.md#origin_header_modify>) directives. When the condition involves the response from the origin, this is actually the only way to achieve it. Here is another way to rewrite the example above:
```nginx
location / {
  add_header has-header-a 1 if($http_header_a != '');
  add_header has-header-b 1 if($http_header_b != '');
  ...
}
```