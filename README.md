# yhpg-12-rpmbuild

自定义生成PG 12的RPM软件包。参考项目：<https://github.com/dennis-apter/pgrpms>.

1. 配置yum仓库，并安装依赖：

```
cat << EOF > /etc/yum.repos.d/c7-devtoolset-7-x86_64.repo
[c7-devtoolset-7]
name=c7-devtoolset-7
baseurl=https://buildlogs.centos.org/c7-devtoolset-7.x86_64/
gpgcheck=0
enabled=1

[c7-llvm-toolset-7]
name=c7-llvm-toolset-7
baseurl=https://buildlogs.centos.org/c7-llvm-toolset-7.x86_64/
gpgcheck=0
enabled=1

[fedoraproject-epel-7]
name=fedoraproject-epel-7
baseurl=https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/
gpgcheck=0
enabled=1
EOF

yum install -y llvm5.0-devel llvm-toolset-7-clang devtoolset-7-gcc devtoolset-7-gcc-c++
```

2. 安装编译工具包：

```
yum install -y libxslt libxslt-devel
yum install -y libxml2 libxml2-devel
yum install -y systemd-devel
yum install -y rpm-build
```

3. 

