# 记录相关常用处理意见

DNF 是新一代的rpm软件包管理器。他首先出现在 Fedora 18 这个发行版中。而最近，它取代了yum，正式成为 Fedora 22 的包管理器。

### rabbitmq-server centos8下安装

`curl -s https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.rpm.sh | bash`
`curl -s https://packagecloud.io/install/repositories/rabbitmq/erlang/script.rpm.sh | bash `

运行完成后显示“The repository is setup! You can now install packages”

安装erlang `dnf install erlang`

导入密钥 `rpm --import https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc`

在/etc/yum.repos.d目录下添加rabbitmq.repo文件
```
[bintray-rabbitmq-server]
name=bintray-rabbitmq-rpm
baseurl=https://dl.bintray.com/rabbitmq/rpm/rabbitmq-server/v3.8.x/el/8/
gpgcheck=0
repo_gpgcheck=0
enabled=1
```
下载 rabbitmq `wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.8.1/rabbitmq-server-3.8.1-1.el8.noarch.rpm`

安装 rabbitmq `dnf install rabbitmq-server-3.8.1-1.el8.noarch.rpm `

启动 
```
chkconfig rabbitmq-server on
/sbin/service rabbitmq-server start
```
启动插件 `rabbitmq-plugins enable rabbitmq_management`

使用http://ip:15672登录，默认用户为guest,密码为guest

