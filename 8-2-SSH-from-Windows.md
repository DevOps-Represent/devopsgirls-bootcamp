# Windows环境SSH方式

因为Windows最好的SSH客户端也需要自己的格式，所以Windows环境的步骤将包含两部分: A.）生成密钥， B.）使用密钥

## 生成密钥

### 1.）转到PuTTY网页

打开浏览器并访问: http://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

### 2.）下载PuTTY

右键单击最新安装程序的链接，选择 *另存为* 。截至撰写本文时，它是 **putty-0.67-installer.msi**

### 3.）运行安装程序

执行MSI文件，然后完成安装。它会安装几个程序，但我们只需要两个: *PuTTY* 和 *PuTTYGen*。

### 4.）启动PuTTYGen

从`开始`菜单中，选择 **所有程序 > PuTTY > PuTTYGen**。

在 **生成的密钥类型** 下面，选择**SSH-2 RSA**。

### 5.）加载密钥对

点击 **加载**。默认情况下，PuTTYgen仅显示扩展名为`.ppk`的文件。要找到`.pem`文件，请选择显示*所有文件*的选项。

转到下载密钥对的目录，打开文件，然后单击*打开*。

### 6.）保存你的私钥

选择 **保存私钥**，以PuTTY可以使用的格式保存密钥。 PuTTYgen显示关于在没有密码短语的情况下保存密钥的警告。选择*是*。

### 7.）为你的秘钥命名

为密钥对使用的密钥指定相同的名称（例如，`banana-smith-keypair`）


## 登录

### 1.）启动PuTTY

从`开始`菜单中，选择 **所有程序 > PuTTY > PuTTY**

### 2.）设置你的登录信息

在 *Category* 窗格中，选择 **Session** 并填写以下字段: 


```
 Host: ec2-user@[PUBLIC IP]
 Port: 22
 Connection type: SSH
```

确保将 *[PUBLIC IP]* 替换为EC2实例的 *Public IP*。例如: 

```
 Host: ec2-user@22.33.44.55
 Port: 22
 Connection type: SSH
```


### 3.）选择你的密钥文件

在 *Category* 窗格中，展开 **Connection**，展开 **SSH**，然后选择 **Auth**。

点击 **Browse**。选择为密钥对生成的`.ppk`文件，然后选择 **Open**。

### 4.）保存你的会话

在 *Category* 窗格中，选择 **Session**。在 **Saved Sessions** 下输入会话名称。

选择 **Save**。

### 5.）登录

最后，单击**Open**以启动SSH会话 - 它将显示你可以安全忽略的安全警报（至少对于此会话）。
