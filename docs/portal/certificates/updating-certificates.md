# Updating a Certificate

On CDN360, each certificate is versioned, and each version is not editable once saved. You can deploy each version independently to the staging and production environments. There can be only one version deployed in each environment at any time. Deploying a new version replaces the old one automatically. Therefore, if you need to update an expiring certificate in production, create a new version of that certificate and deploy to production to replace the old one. All properties using the old certificate in production pick up the new version automatically.

CDN360 sends an email notification when a certificate used in production is close to its expiration date. For convenience, CDN360 supports certificate [auto-renewal](</docs/portal/certificates/auto-renewal.md>) through [Let's Encrypt](<https://letsencrypt.org/docs/challenge-types/>), so you never need to worry about the expiration of your certificates. If you prefer to renew your certificates manually, perform one of the following procedures.

## If you already have a new CA-signed certificate with private key and chain certificate
1. In the left pane, click **Certificates**.
2. Click a certificate name.
3. In the certificate details form, click **Create Version**.
<p align="center"><img src="/docs/resources/images/CreateCertVersion.png" alt="Upload Certificate Version" width="700"></p>

4. In the **Upload Certificate** tab, upload the private key, certificate, and chain certificate files. Then click **Save Version** followed by **OK** at the confirmation pop-up.
<p align="center"><img src="/docs/resources/images/Buttons for Uploading Certs.png" alt="Upload Certificate Version" width="700"></p>
5. Scroll down to the <strong>Deployment</strong> section, and then select <strong>Production</strong> from the <strong>Deployment Destination</strong> drop-down list to deploy the new version to production.<br>
6. Click <strong>Deploy Configuration</strong>.</br>

<p align="center"><img src="/docs/resources/images/CertificateDeploy.png" alt="Upload Certificate Version" width="500"></p>

## If you need a CSR to apply for the new certificate from a CA
If your company's security policy requires the new certificate to have a new private key that is different from the expiring one, follow steps 1 and 2 below to create a self-signed version. Otherwise, you can skip to step 3.

1. In the left pane, click **Certificates**.
2. Click a certificate name.
3. Click **Create Version**.
4. Click the **Auto Generate Certificate** tab, complete the required fields (refer to [details here](</docs/portal/certificates/creating-certificates.md#auto-generating-a-self-signed-certificate>)), and click **Save Version**.
<p align="center"><img src="/docs/resources/images/CertificateSelfSignedVersion.png" alt="Certificate New Self-Signed Version" width="700"></p>

5. Click the **Download CSR** button at the top of the Certificate Details page to generate the CSR from the latest version.
6. Send the downloaded CSR to the CA to apply for a new certificate.
7. When you receive the new CA-signed certificate, return to the same Certificates Details page and click **Create Version**.
8. On the **Upload Certificate** tab, upload the new certificate and, optionally, the chain certificate. Click **Save Version**. You don't need to worry about the private key because it will be the same one as the last version.
9. Scroll down to the **Deployment** section, and then select **Production** from the **Deployment Destination** drop-down list to deploy the new version to production.
10. Click **Deploy Configuration**.

**Note**: To update a certificate, you must be the owner of the certificate.