# 从Mac访问SSH

### 1.）打开终端客户端

打开**Finder**。进到**Applications** > **Utilities**，然后打开名字叫**Terminal**的应用程序

### 2.）验证密钥对的位置

默认情况下，你的密钥对应该在*Downloads*目录中。通过粘贴以下命令验证它是否存在：

```
ls ~/Downloads/[MY KEYPAIR NAME].pem
```

确保将*[MY KEYPAIR NAME]*替换为你给出的密钥对名称。例如，如果我创建了一个名为`banana-smith-keypair`的密钥对，那么我的命令应该是这样的：

```
ls ~/Downloads/banana-smith-keypair.pem
```

### 3.）更改密钥对文件的所有权

请记住：这个密钥对是你登录实例的方式！因此，它只能由你访问。我们通过执行以下命令来执行此操作：

```
chmod 600 ~/Downloads/[MY KEYPAIR NAME].pem
```

同样，你需要确保用钥匙对的名称替换*[MY KEYPAIR NAME]*。所以对于`banana-smith-keypair`，我们会执行这个命令：

```
chmod 600 ~/Downloads/banana-smith-keypair.pem
```

### 4.）复制你的实例IP或URL

还记得我们怎样记录了你的EC2实例的*Public IP*吗？现在我们需要使用它。基本上，我们想要做的是使用我们创建的密钥对登录到实例IP。将它放在剪贴板中，或在记事本中记下它。

### 5.）登录

最后，我们登录到实例。我们使用如下命令执行此操作：

```
ssh ec2-user@[MY IP ADDRESS] -i ~/Downloads/[MY KEYPAIR NAME].pem
```

假设我们的*Public IP*为22.22.22.22，并且我们有一个名为`banana-smith-keypair`的密钥对，你的命令应该是这样的：

```
ssh ec2-user@22.22.22.22 -i ~/Downloads/banana-smith-keypair.pem
```
