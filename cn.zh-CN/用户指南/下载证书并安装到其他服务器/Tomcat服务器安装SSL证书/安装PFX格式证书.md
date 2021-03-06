# 安装PFX格式证书 {#concept_omf_lxn_yfb .concept}

您可以将下载的证书安装到Tomcat服务器上。Tomcat支持PFX格式和JKS两种格式的证书，您可根据选您Tomcat的版本择其中一种格式的证书安装到Tomcat上。

## 前提条件 {#section_csz_fkx_yfb .section}

申请证书时需要选择**系统自动创建CSR**。

申请证书时如果选择**手动创建CSR**，则不会生成证书文件。您需要选择**其他服务器**下载.crt文件后，使用openssl命令将.crt文件的证书转换成.pfx格式。

## 操作指南 {#section_ygk_xhx_yfb .section}

1.  登录阿里云[SSL证书控制台](https://yundunnext.console.aliyun.com/?p=casnext#/overview/cn-hangzhou)。
2.  在SSL证书页面定位到需要下载的证书并单击证书卡片右下角的**下载**打开**证书下载**对话框。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/66242/154503772433499_zh-CN.png)

3.  在**证书下载**对话框中定位到Tomcat服务器，并单击右侧**操作**栏的**下载**将Tomcat版证书压缩包下载到本地。
4.  解压Tomcat证书。您将看到文件中有一个证书文件（以.pfx为后缀或文件类型）和一个秘钥文件（以.txt为后缀或文件类型）。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65316/154503772433514_zh-CN.png)

    **说明：** 每次下载证书都会产生新的密码，该密码仅匹配本次下载的证书。如果需要更新证书文件，同时也要更新匹配的密码。

5.  在**Tomcat安装目录**下新建**cert目录**，并将下载的Tomcat证书和密码文件拷贝到**cert目录**中。
6.  打开**Tomcat安装目录** \> **conf文件夹** \> **server.xml文件**，在**server.xml文件**中添加以下参数：

    ```
    
    #此处keystoreFile代表证书文件的路径，请用您证书的文件名替换cert/后面的内容。
    keystoreFile="cert/1570059_key.test.pfx"
    keystoreType="PKCS12"
    #此处证书密码，请用您证书密码文件的内容替换。
    keystorePass="证书密码"
    ```

    参考以下完整配置（其中port属性请根据您的实际情况修改）：

    ```
    <Connector port="8443"
        protocol="HTTP/1.1"
        SSLEnabled="true"
        scheme="https"
        secure="true"
        keystoreFile="cert/1570059_key.test.pfx"
        keystoreType="PKCS12"
        keystorePass="证书密码"
        clientAuth="false"
        SSLProtocol="TLSv1+TLSv1.1+TLSv1.2"
        ciphers="TLS_RSA_WITH_AES_128_CBC_SHA,TLS_RSA_WITH_AES_256_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_256_CBC_SHA256"/>
    ```

7.  保存server.xml文件配置。
8.  重启Tomcat。

