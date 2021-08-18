# Updating a Certificate

On CDN360, each certificate is versioned, and each version is not editable once saved. You can deploy each version independently to the staging and production environments. There can be only one version deployed in each environment at any time. Deploying a new version replaces the old one automatically. Therefore, if you need to update an expiring certificate in production, create a new version of that certificate and deploy to production to replace the old one. All properties using the old certificate in production pick up the new version automatically.

CDN360 sends an email notification when a certificate used in production is close to its expiration date. For convenience, CDN360 supports certificate [auto-renewal](</docs/portal/certificates/auto-renewal.md>) through [Let's Encrypt](<https://letsencrypt.org/docs/challenge-types/>), so you never need to worry about the expiration of your certificates. If you prefer to renew your certificates manually, perform one of the following procedures.

## If you already have a new CA-signed certificate with private key and chain certificate
1. In the left pane, click **Certificates**.
2. Click a certificate name.
    <br><u>OR </u></br>
  In the **Actions** column, click the vertical ellipsis for the certificate you want to edit, and then select **Edit**.
3. To change the name of the certificate, move your mouse to the right of the certificate name at the top of the form. When the pencil icon appears, click it and enter the new name. When done, click the checkmark at the bottom right of the field in which you typed the name.
4. Edit the **Share With** setting now or after step 5 if desired.
5. Click **Create Version**.
<p align="center"><img src="/docs/resources/images/certificates/certificate-versions.png" alt="Upload Certificate Version" width="700"></p>

5. Set the **Creation Method** setting to **Upload**. Then upload the private key, certificate, and chain certificate files. Click **Save Version** followed by **OK** at the confirmation pop-up.
<p align="center"><img src="/docs/resources/images/certificates/certificate-versions-upload.png" alt="Upload Certificate Version" width="700"></p>

6. Scroll down to the <strong>Deployment</strong> section, and then select <strong>Production</strong> from the <strong>Deployment Destination</strong> drop-down list to deploy the new version to production.<br>
<strong>Note:</strong> To view the deployment history of the property before deploying it, click the <strong>Deployment History</strong> button.</br></br>
7. To deploy the certificate now, click <strong>Deploy Now</strong>. To deploy it at a later time, click <strong>Add to Standby task</strong> to add this task to the [standby queue](</docs/portal/managing-standby-tasks.md>).
<p align="center"><img src="/docs/resources/images/certificates/certificate-deployment.png" alt="Upload Certificate Version" width="700"></p>

## If you need a CSR to apply for the new certificate from a CA
If your company's security policy requires the new certificate to have a new private key that is different from the expiring one, perform the following procedure to create a self-signed version. Otherwise, skip steps 3 and 4.

1. In the left pane, click **Certificates**.
2. Click a certificate name.
3. To change the name of the certificate, move your mouse to the right of the certificate name at the top of the form. When the pencil icon appears, click it and enter the new name. When done, click the checkmark at the bottom right of the field in which you typed the name.
4. Edit the **Share With** setting now or after step 5 if desired.
5. Click **Create Version**.
6. Set the **Creation Method** setting to **Auto-Generate**. Then complete the required fields (refer to [details here](</docs/portal/certificates/creating-certificates.md#auto-generating-a-self-signed-certificate>)) and click **Save Version**.
<p align="center"><img src="/docs/resources/images/certificates/certificate-versions-autogenerate.png" alt="Certificate New Self-Signed Version" width="700"></p>

7. Click the **Download CSR** button at the top of the Certificate Details page to generate the CSR from the latest version.
8. Send the downloaded CSR to the CA to apply for a new certificate.
9. When you receive the new CA-signed certificate, return to the same Certificate Details page and click **Create Version**.
10. With **Creation Method** set  to **Upload**, upload the new certificate and, optionally, the chain certificate. Click **Save Version**. Do not worry about the private key because it will be the same one as the last version.
11. Scroll down to the **Deployment** section, and then select **Production** from the **Deployment Destination** drop-down list to deploy the new version to production.<br><br><strong>Note:</strong> To view the deployment history of the certificate before deploying it, click the **Deployment History** button.</br></br>
12. To deploy the certificate now, click **Deploy Now**. To deploy it at a later time, click **Add to Standby task** to add this task to the [standby queue](</docs/portal/managing-standby-tasks.md>).</br>
**Note**: To update a certificate, you must be the owner of the certificate.
