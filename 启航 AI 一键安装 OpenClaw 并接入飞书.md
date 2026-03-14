# 启航 AI 一键安装 OpenClaw 并接入飞书

> 本教程使用一键脚本安装，适用于 Windows WSL/MacOS/Linux 三种平台

## Windows 的前置操作

> 用于安装 WSL，mac 和 Linux 系统不需要看这个，直接进入第一步即可

### 前置要求：

- Windows 10 2004+（Build 19041）或 Windows 11

- 已开启 **CPU 虚拟化**（任务管理器 → 性能 → CPU 查看），开启方法：[https://www.doubao.com/thread/w0b54e883ab684dd0](https://www.doubao.com/thread/w0b54e883ab684dd0)

![image-20260314144609572](https://img.thelazy.top/2026/03/14/image-20260314144609572.png)



然后打开此链接：[ms-windows-store://pdp/?ProductId=9PN20MSR04DW](ms-windows-store://pdp/?ProductId=9PN20MSR04DW)

然后打开到 Microsoft 应用商店：点击获取进行安装

稍等一会儿后，提示输入用户名

这里我输入“test”

然后输入密码，输入密码是不显示的，输入完成后回车

然后再重复输一次，回车后就完成了

![](https://img.thelazy.top/2026/03/14/image-20260314190023003.png)

然后粘贴这个指令：

```
curl -fsSL "https://opendoc.qhaigc.net/openclaw/install.sh" | bash
```

回车，输入密码（依然不显示，直接回车就是），开始进行安装

![image-20260314190117013](https://img.thelazy.top/2026/03/14/image-20260314190117013.png)

等待十几分钟后

开始输入启航 AI 的 API Key

![image-20260314194048556](https://img.thelazy.top/2026/03/14/image-20260314194048556.png)

前往此页面：[https://www.qhaigc.net/console/apikeys](https://www.qhaigc.net/console/apikeys)

获取启航 AI API Key

然后粘贴即可

接着开始配置飞书

访问 [飞书开放平台](https://open.feishu.cn/app)，使用飞书账号登录。

然后创建企业自建应用

![创建企业自建应用](https://img.thelazy.top/2026/03/14/feishu-step2-create-app.png)

填写应用名称和描述即可

接下来配置应用权限

![配置应用权限](https://img.thelazy.top/2026/03/14/feishu-step4-permissions.png)

在 **权限管理** 页面，点击 **批量导入** 按钮，粘贴以下 JSON 配置一键导入所需权限：

```
{
  "scopes": {
    "tenant": [
      "aily:file:read",
      "aily:file:write",
      "application:application.app_message_stats.overview:readonly",
      "application:application:self_manage",
      "application:bot.menu:write",
      "cardkit:card:write",
      "contact:user.employee_id:readonly",
      "corehr:file:download",
      "docs:document.content:read",
      "event:ip_list",
      "im:chat",
      "im:chat.access_event.bot_p2p_chat:read",
      "im:chat.members:bot_access",
      "im:message",
      "im:message.group_at_msg:readonly",
      "im:message.group_msg",
      "im:message.p2p_msg:readonly",
      "im:message:readonly",
      "im:message:send_as_bot",
      "im:resource",
      "sheets:spreadsheet",
      "wiki:wiki:readonly"
    ],
    "user": ["aily:file:read", "aily:file:write", "im:chat.access_event.bot_p2p_chat:read"]
  }
}
```

然后启用机器人能力

在 **应用能力** > **机器人** 页面：

开启机器人能力，配置机器人名称，例如“测试机器人”

![启用机器人能力](https://img.thelazy.top/2026/03/14/feishu-step5-bot-capability.png)

在事件与回调页面

选择 **使用长连接接收事件**（WebSocket 模式），添加事件：`im.message.receive_v1`（接收消息）

![配置事件订阅](https://img.thelazy.top/2026/03/14/feishu-step6-event-subscription.png)

最后点在 **版本管理与发布** 页面创建版本，提交审核并发布

![image-20260314184119336](https://img.thelazy.top/2026/03/14/image-20260314184119336.png)

然后在 **凭证与基础信息** 页面

![image-20260314194156206](https://img.thelazy.top/2026/03/14/image-20260314194156206.png)

复制 App ID，粘贴到命令行，并回车

复制 App Secret，粘贴到命令行，并回车

此时就配置完成了

![image-20260314194324980](https://img.thelazy.top/2026/03/14/image-20260314194324980.png)

会提示 webui 配置页面的链接和令牌

![image-20260314194402225](https://img.thelazy.top/2026/03/14/image-20260314194402225.png)

复制到浏览器打开即可，此后可以在这里进行配置

![image-20260314194443176](https://img.thelazy.top/2026/03/14/image-20260314194443176.png)

现在我们到飞书进行测试

打开飞书 app，右上角点击创建群组，直接创建即可

然后进入群聊设置，点击 **群机器人**，点击机器人，进入下面这个界面，点击发送消息

![image-20260314184834282](https://img.thelazy.top/2026/03/14/image-20260314184834282.png)

然后发送一个测试消息，如“你好”，可以看到回复了一串英文

![image-20260314194751725](https://img.thelazy.top/2026/03/14/image-20260314194751725.png)

将“`Ask the bot owner to approve with:`”这句话后面的命令复制下来，例如我这里的是：`openclaw pairing approve feishu URPJSW9K`

点击打开 Ubuntu，将这个：`openclaw pairing approve feishu URPJSW9K`粘贴到命令行并回车

![image-20260314194518584](https://img.thelazy.top/2026/03/14/image-20260314194518584.png)

![image-20260314194633917](https://img.thelazy.top/2026/03/14/image-20260314194633917.png)

可以看到配置完成

![image-20260314194645802](https://img.thelazy.top/2026/03/14/image-20260314194645802.png)

然后再发送消息就正常了

![Screenshot_2026-03-14-19-48-29-098_com.ss.android](https://img.thelazy.top/2026/03/14/Screenshot_2026-03-14-19-48-29-098_com.ss.android.jpg)





> 卸载 OpenClaw 的方式：
>
> 执行此命令即可`openclaw uninstall`