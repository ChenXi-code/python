#### 4、额外功能
除此之外，pip-tools 还提供了其他便利功能，你可以探索这些功能以使流程更加轻松。 

要升级包，请使用以下命令（以 Django 为例）：

```bash
pip-compile --upgrade-package django
```
![](https://files.mdnice.com/user/3721/d2644362-9ae4-4160-a9e5-27d9c4eb4548.png)
这将自动更新你 requirements.txt 文件，包括这些更改。只需记住删除"小于版本4"的约束以允许它。

为了使你的 virtualenv 与当前的 requirements.txt 文件同步，可以简单地运行以下命令：

```bash
pip-sync
```

这将安装、升级或卸载您的 requirements.txt 文件中未包含的任何包。

希望这篇文章对所有开始探索这条道路的人有所帮助，因为我试图包含所有必要的知识来完成它

### 安装

这次怎么安装呢
