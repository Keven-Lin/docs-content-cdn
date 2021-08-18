## AWS S3 Bucket Acceleration

In this example, let’s assume we have a domain called `waytoo.digital`, and that we want to set up an Amazon Web Services (AWS) bucket on a subdomain called `files.waytoo.digital` so users can access the data in that bucket through this subdomain.
We'll start by creating and accessing the public AWS bucket, and then we'll look into how to access the private AWS bucket.

### Setting Up an S3 Bucket

1. Log in to the AWS S3 console and create a new bucket. The creation wizard appears.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/create-bucket.png" alt="create bucket" width="720"></p>

2. Enter the following bucket name(DNS qualified prefix): **files-waytoo-digital**

3. Click **Next**.

4. Skip **Configure Options**.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/create-bucket-set-permissions.png" alt="create bucket" width="720"></p>

5. For now, accept the default **Block all public access** permissions; otherwise, AWS prevents you from clicking **Next**. 

6. Click **Next** followed by **Save**. Your bucket is now created.

7. Assign appropriate permissions for accessing the bucket contents.
    
<p align=center><img src="/docs/resources/images/recipes/aws-bucket/modify-bucket-settings-permissions.png" alt="create bucket" width="720"></p>

8. Uncheck the **Block all public access** check box and click **Save**.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/modify-bucket-settings-cors.png" alt="create bucket" width="720"></p>

9. Set up cross-origin resource sharing (CORS) by copying the following code and pasting it into the CORS configuration editor:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
<CORSRule>
    <AllowedOrigin>*</AllowedOrigin>
    <AllowedMethod>GET</AllowedMethod>
    <MaxAgeSeconds>3000</MaxAgeSeconds>
    <AllowedHeader>Authorization</AllowedHeader>
</CORSRule>
</CORSConfiguration>
```

10. Upload a file to the bucket to test our setup and grant public read access to the uploaded object.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/bucket-upload-file.png" alt="create bucket" width="720"></p>

11. Click on the uploaded file in the bucket to check the uploaded object URL.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/bucket-uploaded-file-info.png" alt="create bucket" width="500"></p>

Amazon S3 uses the following URI syntax to access bucket names: `<BUCKET_NAME>.<REGION>.amazonaws.com`. Instead of returning the region, Amazon S3 returns `s3`. Regardless, we can use the bucket domain name to set up CDN360.

### Setting Up CDN360

Log in to the CDN360 management console at https://console.cdnetworks.com.

#### Traffic Management 
1. In the Traffic Management page, create an edge hostname.
   
<p align=center><img src="/docs/resources/images/recipes/aws-bucket/create-edge-hostname.png" alt="create bucket" width="720"></p>

2. After creating the edge hostname, access it in terminal to make sure it works:

```bash
$ping files-waytoo-digital.qtlcdn.com
PING files-waytoo-digital.qtlcdn.com (14.0.119.186): 56 data bytes
64 bytes from 14.0.119.186: icmp_seq=0 ttl=56 time=3.775 ms
64 bytes from 14.0.119.186: icmp_seq=1 ttl=56 time=3.953 ms
64 bytes from 14.0.119.186: icmp_seq=2 ttl=56 time=3.739 ms
64 bytes from 14.0.119.186: icmp_seq=3 ttl=56 time=4.733 ms
```

#### Certificates 
Now let's generate a certificate and renew it automatically with Let’s Encrypt.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/create-certificate.png" alt="create bucket" width="600"></p>

1. In the Certificates page, click **Create Certificate**.
2. Complete the **Certificate Name** and **Certificate Description** fields. 
3. Set **Auto Renew** to **Let’s Encrypt**. 
4. Click the **"Auto Generate Certificate"** tab, and then enter **files.waytoo.digital** in the **Common Name** and **SAN** fields.
5. Click **Save Certificate** to save the settings.

#### Deploy a Certificate to the Staging Environment
Because we saved the certificate earlier, we can now deploy it. To make sure the certificate meets our needs, we are going to deploy it to a staging environment to test our setup before releasing the certificate to production.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/deploy-to-staging.png" alt="create bucket" width="500"></p>

#### Edge Configurations
1. In the Edge Configurations page, click **Create Property**.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/create-property.png" alt="create bucket" width="720"></p>

2. Enter the **Property Name**, an optional **Description** for the property, and a **Description** of the configuration version. 

3. Enter at least one hostname in the **Hostnames** field. The cache identifies and handles requests for property configurations by matching the request header `Host` value with *Hostnames* field values.
    
4. Under **Origins**, click **Add New** to add our S3 bucket as the origin.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/create-property-origin.png" alt="create bucket" width="720"></p>

5. **Origin name** will be used in the edge logic script (in our example, it's called `aws_origin`). In the **Servers** field, add our S3 bucket domain: `files-waytoo-digital.s3.amazonaws.com`.

6. Click **Validate** to make sure everything is satisfactory.

7. Expand **Advanced Settings**, and then enter the origin hostname `files-waytoo-digital.s3.amazonaws.com` in the **Host Header** field. This value will be set as `Host` in the request header between the Edge and the Origin. This is an important step because if it is omitted, the Host's value will be `files.waytoo.digital` and Amazon S3 will respond with a `Bucket not found` error. 

8. Click **Save**.

We have created an origin. Next we will create an initial edge logic configuration. 

9. Click the **Wizard** button.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/create-property-wizard.png" alt="create bucket" width="600"></p>

10. Select the previously configured origin, set cache time to 3600 minutes, and ignore cache-control headers from origin to handle cache behavior on the edge. 

11. Click **"OK"**. The system generates the following edge logic script:

 ```nginx
        location / { #This is the default location.
            origin_pass aws_origin;
            proxy_cache_valid 3600m; #200, 301, and 302 responses will be cached for 3600m
            proxy_ignore_headers Cache-Control Expires; #This will force the cache server to ignore cache control headers from origin.
        }
 ```

You can edit this script and set up any logic you need to address your requirements. 

In our example, we have everything we need for this property, except for one thing: the certificate we want to add.

12. Expand the **TLS Settings** tab. In the **TLS Certificate** field, enter the name of the certificate we created and deployed to staging.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/create-property-tls.png" alt="create bucket" width="600"></p>
	
13. Click **Save and Validate** to make sure that everything is configured properly.

Assuming that no issues occurred after saving and validating, you can now deploy the property to the staging environment for testing.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/deploy-to-staging.png" alt="create bucket" width="500"></p>

#### Testing(Staging) 

To test staging deployments, you should know the IP addresses of the staging server:

```bash
$ dig staging.qtlgslb.com
...
;; ANSWER SECTION:
staging.qtlgslb.com.    59  IN  A   163.171.228.89
staging.qtlgslb.com.    59  IN  A   163.171.230.47
...
```

Pick one of the returned IP addresses, and check whether everything we set up and deployed works properly.

```bash
❯ curl -I https://files.waytoo.digital/file_1m.bin --resolve files.waytoo.digital:443:163.171.228.89
HTTP/2 200
content-type: application/octet-stream
content-length: 1024000
x-amz-id-2: eQa0SXtgPk3A+jASSyarZLw6FgFtXg+7m+Br6Xr/YBXQ0aot/dBTKBf5QSoE0x8TwzqBKXJ+MBw=
x-amz-request-id: 4Z0SEN8YER8PBYAG
date: Fri, 16 Oct 2020 03:30:16 GMT
last-modified: Fri, 16 Oct 2020 02:36:45 GMT
etag: "fcaebe20d9b3e73086dcb0ba5def8e52"
x-cache-status: MISS
x-qtl-request-id: 4c394e8fd8cc514c5f1e437ac3daf969
x-via: 2.0 na-us-iad1-cache-0003 [MISS 200]
age: 19
server: QTL_Cache/1.2.03
accept-ranges: bytes
```

By requesting the same item again, we will see that the cache status is **HIT**.

```bash
❯ curl -I https://files.waytoo.digital/file_1m.bin --resolve files.waytoo.digital:443:163.171.228.89
HTTP/2 200
content-type: application/octet-stream
content-length: 1024000
x-amz-id-2: eQa0SXtgPk3A+jASSyarZLw6FgFtXg+7m+Br6Xr/YBXQ0aot/dBTKBf5QSoE0x8TwzqBKXJ+MBw=
x-amz-request-id: 4Z0SEN8YER8PBYAG
date: Fri, 16 Oct 2020 03:30:16 GMT
last-modified: Fri, 16 Oct 2020 02:36:45 GMT
etag: "fcaebe20d9b3e73086dcb0ba5def8e52"
x-cache-status: HIT
x-qtl-request-id: dfa55f3549ee4fd0824472f83d06c6c5
x-via: 2.0 na-us-iad1-cache-0003 [HIT]
age: 13
server: QTL_Cache/1.2.03
accept-ranges: bytes
```

Our configuration is working as expected, so let's deploy it to production.

#### Deployment to Production

To deploy the configuration to production, use the Certificates and Edge Configurations pages. 

1. Go to the Certificates page first. Then select the certificate, set **Deployment Destination** to **Production**, and click **Deploy Configuration**.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/deploy-to-production.png" alt="create bucket" width="500"></p>

2. Go to the to Edge Configurations page, set **Deployment Destination** to **Production**, and click **Deploy Configuration**. 

#### Testing(Production)

Before we release the property to production, we should create or change the CNAME record of our DNS and point it to the edge hostname we created earlier (`files-waytoo-digital.qtlcdn.com`).

```bash
❯ dig files.waytoo.digital
...
;; ANSWER SECTION:
files.waytoo.digital.	299	IN	CNAME	files-waytoo-digital.qtlcdn.com.
files-waytoo-digital.qtlcdn.com. 19 IN	A	14.0.119.186
...
```

You can use the production IP address to check whether everything is satisfactory before you change the DNS record:

```bash
❯ curl -I https://files.waytoo.digital/file_1m.bin --resolve files.waytoo.digital:443:14.0.119.186
HTTP/2 200
content-type: application/octet-stream
content-length: 1024000
x-amz-id-2: gdpoBl4Uk1FbJ6i8tMHXYZRcPxAAR9NTY/EziqHr6Kbrni887rU+suUINzNof4sltrCRCq4I4TE=
x-amz-request-id: C30F30F6BE2B081E
date: Fri, 16 Oct 2020 03:21:14 GMT
last-modified: Fri, 16 Oct 2020 02:36:45 GMT
etag: "fcaebe20d9b3e73086dcb0ba5def8e52"
x-cache-status: HIT
x-qtl-request-id: 16a3be4dfdc381e44b90c86bec087f47
x-via: 2.0 as-kr-icn1-cache-0003 [HIT]
age: 5575
server: QTL_Cache/1.2.03
accept-ranges: bytes
```

Congratulations. You've just accelerated the Amazon S3 bucket with **CDN360**!

### Accessing Private Buckets

Now let's block the public access to our bucket and set up CDN360 to access it.

#### Block Public Access

Previously we made our bucket public. Now, in bucket settings, we will return the default permissions to their previous settings to make the bucket private again.

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/bucket-permissions-private.png" alt="create bucket" width="720"></p>

#### Enable Origin Authentication

Now we can edit our property settings and set up the `Origin Authentication for S3`. Before doing that, make sure you know the following items:

- AWS bucket region
- AWS access key
- AWS access secret

1. Go to the Edge Configurations page and select the property you configured previously:

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/modify-property-clone.png" alt="create bucket" width="720"></p>

2. Click **Clone** to create a new configuration version. Now we can edit it. 

3. At the right side of the **Origins** field, click **Edit**.

4. Expand **Advanced Settings**. 

5. Set **Authentication** to **AWS S3** and fill the required fields as follows:

<p align=center><img src="/docs/resources/images/recipes/aws-bucket/modify-origin-auth.png" alt="create bucket" width="600"></p>

6. Click **Save**, and then deploy this configuration to staging. Make sure it works.

```bash
curl -I https://files.waytoo.digital/file_1m.bin --resolve files.waytoo.digital:443:163.171.228.89
HTTP/2 200
content-type: application/octet-stream
content-length: 1024000
x-amz-id-2: oTixActu2B9rtfEvOUDkmelQxPIgFYfRdC4T950YuXL/tv7Zu+pSHgkCXiAuouaRpjLpqTyf3xE=
x-amz-request-id: AQ7S4P0H1K0H0R9G
date: Fri, 16 Oct 2020 09:04:34 GMT
last-modified: Fri, 16 Oct 2020 09:04:10 GMT
etag: "fcaebe20d9b3e73086dcb0ba5def8e52"
x-cache-status: HIT
x-qtl-request-id: 105b10794ee438213fac428c0ef60379
x-via: 2.0 na-us-iad1-cache-0003 [HIT]
age: 16
server: QTL_Cache/1.2.03
accept-ranges: bytes
```

That's all there is to it!
Now you can place your property into production.
