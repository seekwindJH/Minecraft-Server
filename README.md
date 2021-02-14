# 启动Minecraft JavaEdition Server

> 资源的[GitHub链接](https://github.com/seekwindJH/Minecraft-Server)

## 1. 下载对应版本的server.jar

从官方渠道或者第三方渠道下载对应的`server.jar`，放置在服务器主机内。需要注意的是，服务器主机需要有公网IP或者内网穿透，以便于客户端的访问。如果没有服务器，建议购买阿里云或腾讯云等云主机。如果有服务器，建议购买内网穿透服务。

## 2. 通过java -jar 命令启动server.jar文件

在终端输入如下命令，一段时间后，程序会自然退出，这是因为我们没有接受协议。（好比安装软件过程中，我们需要打钩钩）

```bash
java -Xms256m -Xmx512m -jar server.jar nogui
```

因此，我们需要接受协议。怎么接受呢？我们刷新server.jar所在的目录，会发现多了一个文件`eula.txt`，该文件中有一个名字为`eula=false`的配置项，我们需要把它改为`eula=true`。保存后重新执行以上命令，等待一段时间（大概三十秒不到？），就开服成功了。

这里需要注意的是，虽然我们开服成功了，但是当我们退出终端时，server.jar也就停止运行了。为了让server.jar在后台保持运行，我们需要用以下语句执行游戏启动命令。这时，就算我们退出终端，服务依然在后台运行。

```bash
nohup java -Xms256m -Xmx512m -jar server.jar nogui &
```

## 3. 如何关闭服务器

在终端关闭server服务，我们需要知道server服务的进程号。通过一下命令查看server.jar的进程号。

```bash
ps -aux | grep server.jar
```

你会得到类似如下的输出。其中，937141指的就是server.jar的进程号。

```bash
root      937141 78.5 36.4 2655164 742112 pts/2  Sl   20:10   3:16 java -Xms256m -Xmx512m -jar server.jar nogui
root      939556  0.0  0.1   9036  2316 pts/2    S+   20:14   0:00 grep --color=auto server.jar

```

然后，我们杀死该进程，就可以达到关闭服务的目的。

```bash
kill 937141
```

## 4. 关闭登入验证

在完成了以上三个步骤之后，你可以在我的世界中通过服务器的IP地址连接服务器了，但是，你可能会看到一个`null`。这是因为服务器端不认识你，在它那边没有你注册过。我们索性关闭服务器的登入验证。

我们修改server.jar路径下的server.properties文件中online-mode=true为false。重新启动服务器。这时我们再通过IP地址连接服务器，就可以成功了。

