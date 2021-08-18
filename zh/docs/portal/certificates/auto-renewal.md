# Auto-Renewing a Certificate through Let's Encrypt

Let's Encrypt (LE) is a Certificate Authority (CA) that issues free certificates to the public. It provides a set of API and CLI tools to help you apply for and renew certificates automatically. If you want a certificate to cover one or more hostnames, you must prove to LE that you are the owner of all the hostnames. LE provides several ways (or "challenges") for you to prove ownership. Currently, CDN360 supports the "HTTP-01 challenge." To pass the challenge, you must make sure that all hostnames using the certificate are already pointed (through CNAME records) to a CDN360 edge hostname. Otherwise, some challenge requests from LE may go to undesired destinations.

To use the CDN360 auto-renew feature, you need an initial certificate to "bootstrap" the process. If you don't want your current service to be interrupted, make sure this initial certificate is a valid one so your clients' browsers won't complain. Otherwise you can simply use the portal to generate a self-signed certificate for this purpose. The content of the certificate, such as common name or subject alternate names (SAN), is not important. The auto-renew process will populate the new certificate with the correct content.

The following procedure describes how to use the auto-renew feature:

1. [Create the initial certificate](</docs/portal/certificates/creating-certificates.md>).
2. On the Create Certificate form, make sure **Auto Renew** is set to **Let's Encrypt**. You can also do this on the Certificate Details page any time after the certificate is created.
3. Create the property that contains the hostname(s) to be accelerated. In the **Advanced Settings** of the Property page, make sure **Disable Certificate Renew Automation** is set to **No**.

**Note:** The property cannot contain wildcard characters in the hostname because HTTP-01 challenges do not support wildcard domains.

4. Attach the initial certificate to the property created in the previous step.
5. Deploy the property and certificate to production.
6. Update your DNS server to point all the hostnames in this property to a CDN360 edge hostname. If you do not have an edge hostname, [create one](</docs/portal/traffic-management/creating-edge-hostname.md>).
7. After you perform the steps above, and if the initial certificate's expiration date is within 25 days, CDN360 renews the certificate automatically through LE within one hour. You will receive notifications about the success or failure of the renewal. The SAN of the new certificate will contain all hostnames in this property.
