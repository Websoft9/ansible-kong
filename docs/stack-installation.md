# Initial Installation

If you have completed the Kong deployment, follow the steps below to start a quick use.

## Preparation

1. Get the **Server's Internet IP** of Server on your Cloud Platform.
2. Check your **[Inbound of Security Group Rule](https://support.websoft9.com/docs/faq/tech-instance.html)** of Cloud Console to ensure the **TCP:8161** is allowed.
3. Make a domain resolution on your Cloud Console if you want to use domain for Kong.

## Kong Installation Wizard

1. Use local Chrome or Firefox to access the URL _http://DNS:15672_ or _http://Server's Internet IP:15672_. You will enter installation wizard of Kong.
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-login-websoft9.png)

2. Log in Kong web console. ([Don't have password?](/stack-accounts.md#kong))
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-bk-websoft9.png)

3. Set you new password from: 【Users】>【Admin】>【Permissions】>【Update this user】
   ![](https://libs.websoft9.com/Websoft9/DocsPicture/zh/kong/kong-pw-websoft9.png)

> More guide about Kong, please refer to [Kong Documentation](https://www.kong.com/documentation.html).

## Kong Setup wizard

## Q&A

#### Can't visit the start page of Kong?

Your TCP:15672 of Security Group Rules is not allowed, so there is no response from Chrome or Firefox.

#### Kong service can't start?

Reason:  
Solution:
