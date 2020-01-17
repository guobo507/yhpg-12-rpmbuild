# yhpg-12-rpmbuild

自定义生成PG 12的RPM软件包。本项目SOURCES目录下的`postgresql-12.spec`等文件参考了项目：<https://github.com/dennis-apter/pgrpms>来进行定制。

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

3. 克隆本项目：

    ```
    git clone https://github.com/guobo507/yhpg-12-rpmbuild.git
    cd yhpg-12-rpmbuild/rpmbuild/SOURCES/

    # 将PostgreSQL的源文件放到此目录下：
    wget http://192.168.18.3/tools/postgresql/pg_source/postgresql-12.1.tar.bz2
    wget http://192.168.18.3/tools/postgresql/pg_source/postgresql-12-A4.pdf
    ```

4. 开始执行打包：

    ```
    export PATH=/opt/rh/llvm-toolset-7/root/usr/bin:/opt/rh/devtoolset-7/root/usr/bin:$PATH
    rpmbuild -bb postgresql-12.spec
    ```

