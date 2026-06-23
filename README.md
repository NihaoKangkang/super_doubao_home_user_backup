# super_doubao_home_user_backup

这是一个针对豆包（Doubao）办公模式沙盒中 `/home/user` 目录的完整备份项目。本项目完整保留了沙盒环境下的所有文件、路径结构、软件配置、缓存以及工作区，旨在帮助开发者和用户快速搭建、恢复或迁移原有的超级豆包运行时环境。

## 👤 作者信息
* **作者**: Kyi Wong
* **项目类型**: 环境备份 / 配置文件集

## 🌐 运行环境
* **操作系统**: Ubuntu 22.04.3 LTS

## 📦 备份内容介绍
在 `/home/user` 路径下，包含了以下核心目录与文件：

| 类型 | 名称 | 说明 |
| --- | --- | --- |
| 📁 | `.super_doubao` | 超级豆包运行时目录（核心工作区） |
| 📁 | `.doubao` | 豆包相关配置 |
| 📁 | `.cache` | 缓存目录（浏览器、Go 构建、字体等） |
| 📁 | `.config` | 配置目录 |
| 📁 | `.local` | 本地程序数据 |
| 📁 | `go` | Go 语言安装目录 |
| 📁 | `gopath` | Go 工作路径 |
| 📁 | `.npm` / `.npm-global` | Node.js 包管理 |
| 📁 | `.jupyter` / `.ipython` | Python 交互式环境 |
| 📁 | `.pki` | 公钥基础设施 |
| 📄 | `.bashrc` / `.bash_logout` / `.profile` | Shell 配置文件 |
| 📄 | `.Xauthority` | X11 认证文件 |
| 📄 | `output.txt`  | 包含本地权限提升检查（linpeas）的详细输出日志 |

## 🔗 备份下载链接
请通过以下云盘链接下载完整的备份压缩包（文件名为 **`my_home.tar.gz`**）：

1.  **百度网盘**: [点击下载](https://pan.baidu.com/s/1Kfrb9mFHGEDIAywsKvNVYA?pwd=gyxm) (提取码: `gyxm`)
2.  **夸克网盘**: [点击下载](https://pan.quark.cn/s/7e556e6c27d7)
3.  **Gofile**: [点击下载](https://gofile.io/d/Egnums)
4.  **Google Drive**: [点击下载](https://drive.google.com/drive/folders/1qfRdAD3MxC8hrD82tqybI_KYc7xUzfyF?usp=drive_link)

## 🚀 Ubuntu 22.04 部署与恢复指南

以下是详细的部署与恢复步骤。请在执行命令前仔细阅读说明，特别是注意备份您当前的本地数据。

### 1. 将备份包传到本地虚拟机

你可以使用 scp、SFTP 工具（如 FileZilla、MobaXterm）或者直接拖 reasonable 的方式，将 my_home.tar.gz 放进本地虚拟机的 /tmp 目录或当前用户的家目录下。

### 2. 执行还原命令（核心步骤）

为了确保文件的所有权（Ownership）和读写权限（Permissions）在解压后完全正确，强烈建议在本地使用 sudo 并带上 --numeric-owner 参数。

打开本地虚拟机的终端，执行以下命令：

```Bash
# 1. 切换到本地虚拟机的根目录 /
cd /

# 2. 使用 sudo 解压，将文件还原回其原本的绝对路径
sudo tar -xvpzf /path/to/my_home.tar.gz -C / --numeric-owner
🔍 关键参数解释：
```

### 3. 检查并修正用户所有权（视情况而定）

解压完成后，你需要确认本地虚拟机的当前用户是否能够正常读写这些还原回来的文件。

查看你本地用户的 UID 和 GID：
在本地终端输入：

```Bash
id
(通常 Ubuntu 第一个用户的 UID 是 1000，组 ID gid 也是 1000)
```

检查解压出来的文件夹属性：

```Bash
ls -ld /home/你的用户名
```

如果发现该目录的所有者变成了数字（例如 1001）或者别人的名字，说明原服务器的 UID 和本地不一致，这会导致你开机后无法写入文件、无法保存桌面配置。

一键修正权限（如果所有者不对应）：
在本地使用 root 权限把家目录重新夺回：

```Bash
sudo chown -R 你的用户名:你的用户组名 /home/你的用户名
```
例如：`sudo chown -R username:group /home/username`

## ⚖️ 免责声明与法律条款
用途限制: 本项目及关联下载链接中所包含的全部备份文件（包括 linpeas 的安全扫描输出结果），仅供个人学习、技术研究、环境恢复以及合法的安全排查之目的使用。请勿将其用于任何商业运作、非法谋利或未授权的生产环境。

风险承担: 作者 Kyi Wong 无法保证该备份文件在所有硬件架构或衍生系统上的绝对兼容性与安全性。由于直接操作、替换或覆盖 /home/user 目录产生的任何数据丢失、系统损坏或其他法律纠纷，均由使用者本人自行承担。作者对此不承担任何形式的法律责任。

版权保护与删除: 本项目坚决尊重并保护知识产权。若原权利方或相关利益相关者认为本项目的内容在任何形式上侵犯了其合法权益，请联系作者。作者在收到通知核实后，将第一时间无条件删除争议内容。

## 📄 开源协议
本项目执行 MIT License 协议。您可以自由地使用、修改和分发本项目的内容，但必须包含原作者的版权声明和许可声明。
