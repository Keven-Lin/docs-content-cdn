# 证书的部署与卸载

创建或更新证书后，您必须将其部署到演练环境或生产环境，然后才能被加速项使用。如果这两个环境中没有任何一个加速项在使用证书，您应该将该证书卸载。如果您想从 CDN Pro 平台上删除证书，对该证书的卸载操作也是一个前提条件。

**注意**: 只有证书的所有者才有权限将证书部署到演练或生产环境，或从这两个上卸载证书。

## 部署证书

1. 在左边菜单栏，单击 **证书** 按钮。 
2. 在证书页面，单击您需要部署的证书名。
3. 在证书详情页面，单击 **部署** 按钮。
4. 如果您需要立即部署证书，请在 **部署目标** 消息框中选择 **演练** 或者 **生产** 环境，然后单击 **立即部署**。 在下个部署确认消息提示中，点击 **确定**。 <br><br><u><p>或者</br></br></u></li> 如果您需要稍后再部署证书，请选择 **添加到待命任务** 按钮，将此证书的部署存放到 [待命列表](</docs/portal/certificates/standby-tasks.md>) 中。<br><br><li>如果您单击**立即部署**，则大约需要 5 分钟来完成整个部署过程。您可以观看进度并等待它完成，或者单击 **Hide**让其继续部署。您可以随时单击左侧窗格中的 **查看任务** 来检查部署状态。</br></br></li>
<p align="center"><img src="/docs/resources/images/certificates/certificate-deployment-options.png" alt="Deployment Options" width="700"></p>

<strong>注意：</strong> 要在部署之前查看证书的部署历史，请单击 **部署历史** 按钮。


## 卸载证书

如果您在演练或生产环境中不再需要某本证书，则可以将该证书卸载。

1. 在左边菜单栏，单击 **证书** 按钮。 
2. 在“证书”页面的 **操作** 列中，点击要取消部署的证书的右边侧垂直省略号，然后选择 **从演练环境卸载** 或 **从生产环境卸载**。
<p align="center"><img src="/docs/resources/images/certificates/certificate-actions.png" alt="Certificate Actions" width="900"></p>

3. 当出现确认窗口时，单击 <strong>OK</strong> 来卸载掉证书（整个卸载操作预计需要 5 分钟）。<br><br><u>或者</u> <br><br> 单击 **添加到待命任务** 按钮，将此证书的卸载操作存放到 [待命列表](</docs/portal/certificates/standby-tasks.md>)中。</br></br>