## 用CDN360安全地进行分发

Security and privacy protection have raised increasing concerns over the last few years — and for good reason. Hardly a day goes by when the headlines aren't filled with another major security breach. With these concerns in mind, CDN360 has adopted several features to help you achieve your security goals with smooth and uninterrupted service for your clients. This article describes these features, along with a few best practices to help you optimize security.

### 第4层DDoS防护
At the entry point of every CDN360 Point of Presence (PoP) is a high-performance Layer 4 distributed denial-of-service (DDoS) firewall. The firewall consists of a group of machines that analyze incoming traffic at line speed.
Based on regularly updated rules, the firewall rejects suspicious packets that may endanger services and forwards only the "safe" packets to the servers located behind the firewall. This feature is enabled by default and is transparent to all the users.

### 在边缘上进行访问控制
Access control is essential for protecting content from unauthorized users. It also plays an important role in mitigating some common Layer 7 attacks. CDN360 supports several access control methods. Many of them are based on enhanced features of the open-source NGINX. We also introduced a proprietary [`eval_func`](</docs/edge-logic/supported-directives.md#eval_func>) directive to support customized algorithms.
* Client IP restrictions with [`allow`](</docs/edge-logic/supported-directives.md#allow>) and [`deny`](</docs/edge-logic/supported-directives.md#deny>):
```nginx
allow 123.0.0.1/8;
allow 234.12.34.56;
deny all;
```
* Check the `Referer` request header with [`valid_referers`](</docs/edge-logic/supported-directives.md#valid_referers>):
```nginx
valid_referers none blocked server_names
               *.example.com example.* www.example.org/galleries/
               ~\.google\.;
if ($invalid_referer) {
    return 403;
}
```
* Based on any request header or query parameter value using the enhanced [`if`](</docs/edge-logic/supported-directives.md#if>) directive:
```nginx
if ($http_my_token != 'authorized' && $arg_my_token != 'authorized') {
    return 403;
}
```
* Based on a remote authorization server's response, with [`auth_request`](</docs/edge-logic/supported-directives.md#auth_request>):
```nginx
location /protected/ {
    auth_request /auth; # 2xx to grant access, 401 or 403 to reject
    ...
}

location = /auth { # calls a remote server to authenticate the request
    origin_pass remote-auth-server;
    proxy_method HEAD; # specify method required by the remote server
    proxy_pass_request_body off; # remove the request body, if any
    origin_set_header Content-Length "" policy=overwrite;
    # forward the original request URI to the remote server
    origin_set_header X-Original-URI $request_uri;
}
```
* Use the NGINX built-in [`secure_link`](</docs/edge-logic/supported-directives.md#secure_link>) algorithm. This feature allows clients to use a secret key to generate an MD5 HMAC from components in the HTTP request. An expiration time can also be specified. The edge server grants the request only after the MD5 value is validated and the request has not expired. For details, please refer to the [official NGINX documentation](http://nginx.org/en/docs/http/ngx_http_secure_link_module.html#secure_link).

* Even more complex algorithms can be achieved with the proprietary directive [`eval_func`](</docs/edge-logic/supported-directives.md#eval_func>). Here is an example of how to implement the validation of an HMAC authentication code
with SHA256:
```nginx
eval_func $binhash HMAC $secret_key $request_uri SHA256;
eval_func $b64hash BASE64_ENCODE $binhash;
# assume the client passes the hash through the X-Hash header
if ($b64hash != $http_x_hash) {
    return 403;
}
```

### 实现回源站的鉴权
It is always a good idea to set up some ACL rules on the origin to avoid spamming. In this case, the [`eval_func`](</docs/edge-logic/supported-directives.md#eval_func>) directive can also be used to generate the required token for accessing the origin. Here is an example of how to implement the [AWS Signature Version 2](https://docs.aws.amazon.com/AmazonS3/latest/userguide/RESTAuthentication.html):
```nginx
## required input variables: $awskey $awsseckey $awsbucket/$s3key

# Step 1: construct the STS
set $awsdatev2 $time_rfc822;
set $awssts "GET\n\n\n$awsdatev2\n/$awsbucket/$s3key";

# Step 2: sign the STS with secKey
eval_func $awssigv2 HMAC $awsseckey $awssts SHA1;
eval_func $awssigv2_b64 BASE64_ENCODE $awssigv2;

# Step 3: set the required header fields
origin_set_header Date $awsdatev2;
origin_set_header Authorization "$awsv2origin $awskey:$awssigv2_b64";
```

### 保密信息的管理
As shown in the sections above, access control algorithms using [`secure_link`](</docs/edge-logic/supported-directives.md#secure_link>) or [`eval_func`](</docs/edge-logic/supported-directives.md#eval_func>) usually require a secret key for HMAC generation or encryption. Since the portal may be accessible by operators who are not authorized to see those keys, you want to prevent the keys from being exposed in clear text in the Edge Logic. The [`保密信息`](</docs/portal/secrets/overview>) feature allows you to manage and apply secret keys with minimal exposure.

### 爬虫防护
Before the content is delivered to fulfill a request, there may be times when you want to make sure the request was made by a human using a browser instead of by a bot or crawler. The following Edge Logic code demonstrates how to prompt the users to click a button to receive the requested content:
```nginx
location /protected/ {
    if ($cookie_validated = '') { #check the existence of the cookie 'validated'
        add_header Set-Cookie 'validated=1; Max-Age=60';
        add_header Content-Type 'text/html' policy=overwrite;
        return 200 '<!DOCTYPE html>
<html>
  <script>
    alert("Human, click OK to proceed.");
    location.href="$request_uri";
  </script>
</html>';
    }
    # continue loading the page from origin or cache
    origin_pass my_origin;
}
```
More sophisticated methods can be adopted in this way to block more advanced bots.

### TLS相关配置
* CDN360 supports TLS certificates with both RSA and ECDSA algorithms. You can even configure two certificates with different algorithms in the same property and have the server pick one based on the client's capability and preference.
* We highly recommend that you set the minimum TLS version to 1.2. For maximum security and performance, however, you should really take advantage of TLSv1.3. The TLS version on both the client and origin sides can be configured.
* CDN360 also allows you to fully configure TLS ciphers based on your security requirements. For example, you can prioritize the ECDHE and EDH key exchange algorithms to ensure "[Perfect Forward Secrecy](https://www.digicert.com/kb/ssl-support/ssl-enabling-perfect-forward-secrecy.htm)".
* If a client request uses HTTPS, CDN360 contacts the origin with the same protocol to ensure that the entire path is encrypted. Although CDN360 supports "protocol downgrades," you should avoid using them unless absolutely necessary.
* To avoid "man-in-the-middle" attacks or DNS hijacking attempts of your origin's hostname, enable the validation of the origin's certificate.
* If your site supports HTTPS, a good practice is to redirect all HTTP requests to the HTTPS counterpart. You can enable this on the [CDN360 portal](/docs/portal/edge-configurations/creating-property.md#tls-settings) with the following dropdown list:
<p align=center><img src="/docs/resources/images/edge-logic/http-redirect.png" alt="HTTP redirect" width="500"></p>

### 防止缓存敏感数据
If you know that some information is extremely sensitive and should never be stored on the edge server, use the [`proxy_cache_bypass`](</docs/edge-logic/supported-directives.md#proxy_cache_bypass>) and [`proxy_no_cache`](</docs/edge-logic/supported-directives.md#proxy_no_cache>) directives to bypass caching of confidential content. For example:
```nginx
location /credit-card-info {
    proxy_cache_bypass 1;
    proxy_no_cache 1;
}
```
This is particularly important when meeting privacy standards such as PCI-DSS and HIPAA.
