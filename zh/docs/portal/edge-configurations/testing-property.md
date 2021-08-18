# Testing Property

Before you deploy your property to production, we recommend you test and verify your property to make sure it works as expected. CDN360 has a dedicated staging environment for this purpose. To deploy the property to the staging environment, perform the steps in [Deploying Your Property](</docs/portal/edge-configurations/deploying-property.md>).

## Testing Your Property in Staging

CDN360 provides a staging environment for you to test your property configurations without affecting production. Sending your test traffic to the servers in the staging environment is a way for you to make sure the behavior is what you expect. The staging servers can be found by the hostname `staging.qtlcdn.com`. You can also see their IP addresses by issuing the following command:

```bash
$ curl staging.qtlcdn.com
[
  { "ip":"163.171.230.47", "ipVersion":4,
    "code":"US.GA", "location":"United States" },
  { "ip":"115.223.12.247", "ipVersion":4,
    "code":"CN.ZJ", "location":"China" },
  { "ip":"163.171.228.89", "ipVersion":4,
    "code":"US.VA", "location":"United States" },
  { "ip":"112.240.57.248", "ipVersion":4, 
    "code":"CN.SD", "location":"China" },
  { "ip": "2401:c500:fd00:0002:1c7b:a470:f69b:6e2a", "ipVersion":6,
    "code": "RO.B", "location": "Romania" },
  { "ip": "2409:8c54:2000:060b:c35f:367c:72f3:6274", "ipVersion":6,
    "code": "CN.GD", "location": "China" }
  ...
]
```

Pick one of the IP addresses. The corresponding ```location``` field indicates its country. If your property hostname has an ICP Beian license, you can use an IP address in China. Otherwise, choose an IP address in another country to avoid getting an HTTP 451 'Unavailable for Legal Reasons' status error.

Once you have selected a staging IP address, use one of the following ways to send test traffic to the staging environment:

- Modify the ```hosts``` file to hard code the hostname to be accelerated to one of the staging server's IP addresses. 

  On Windows-based systems, edit ```%SystemRoot%\System32\drivers\etc\hosts```
  
  On Unix-based systems, edit ```/etc/hosts```
  
  For example:

```
163.171.230.47 cdn360.mydomain.com
```
- If you use the cURL command, you can add ```--resolve``` to directly map the hostname to be accelerated to the IP address of the CDN360 staging server(s). For example:

```bash
$ curl -v https://cdn360.mydomain.com/index.html --resolve cdn360.mydomain.com:443:163.171.230.47
```
