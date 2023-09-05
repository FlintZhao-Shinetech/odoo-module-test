# 开发笔记  
debian版本有11：bullseye 12: bookworm，不打算尝试slim版本

经核对，debian官方bookworm版本已发行，且python docker hub主页最新版为3.12，因此选择python:3.12-rc-bookworm镜像
```bash
# python 3.12 debian 12
# 安装依赖
apt-get update && apt-get install python3-virtualenv libsasl2-dev python-dev-is-python3 libldap2-dev libssl-dev
# 创建虚拟环境
virtualenv venv
# 激活虚拟环境
source ./venv/bin/active
# 升级包管理器
pip install --upgrade pip
# 安装依赖
pip install -r requirements.txt
```
Odoo用的postgres，可以使用命令行：psql -U 用户名  
```sql
create user odoo with password 'odoo2023' createdb;

-- odoo 不需要新建数据库，除非是数据库迁移
-- create database odoo;
-- grant all privileges on database odoo to odoo;
-- odoo数据库管理 密码 g8sv-ujkf-pbtk
-- 删除用户
revoke all on database odoo from odoo;
drop user odoo;
drop role odoo;
```
odoo的配置文件在用户目录下的.odoorc文件里，配置格式为
```
[options]
db_host = pg15
db_port = 5432
db_user = odoo
db_password = odoo2023
```

## 运行  
```bash
source venv/bin/activate
python3 odoo-bin
```

## 安装  
```bash
# 假设克隆到/opt/odoo/addons  
git clone git@github.com:FlintZhao-Shinetech/odoo-module-test.git /opt/odoo/addons/module-test
source venv/bin/activate
python3 odoo-bin --addons-path="addons/,/opt/odoo/addons"
```

<font color="red">odoo是LGPL，不能改源码，而是开发插件</font>
