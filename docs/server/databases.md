# 多数据库服务支持

除了官配 LeanCloud 之外，Waline 还支持多种数据库，包括 MySQL, PostgreSQL, SQLite 以及 MongoDB。所有的这些支持仅需要配置环境变量即可，Waline 会自动根据你配置的环境变量切换到对应的数据存储服务。

## MongoDB

<https://mongodb.com> 官网免费提供了 512M 的 MongoDB 数据库支持，我们也可以使用 MongoDB 作为 Waline 的数据存储服务。以下是使用 MongoDB 存储需要配置的环境变量。

| 环境变量名称 | 必填 | 默认值 | 备注 |
|------------|---------|------|------|
| `MONGO_HOST` |  | 127.0.0.1 | MongoDB 服务的地址，支持数组格式 |
| `MONGO_PORT` |  | 27017 | MongoDB 服务的端口，支持数组格式 |
| `MONGO_USER` | √ | | MongoDB 服务的用户名 |
| `MONGO_PASSWORD` | √ | | MongoDB 服务的密码 |
| `MONGO_REPLICASET` | | | MongoDB 集群 |
| `MONGO_AUTHSOURCE` | | | MongoDB 认证源 |
| `MONGO_OPT_SSL` | | | 是否使用 SSL 进行连接 |

## MySQL

如果想要使用 MySQL 作为存储服务，需要先导入 [waline.sql](https://github.com/lizheming/waline/blob/master/assets/waline.sql) 创建好表和表结构。之后在项目中配置如下环境变量即可。

| 环境变量名称 | 必填 | 默认值 | 备注 |
|------------|---------|------|------|
| `MYSQL_HOST` | | 127.0.0.1 | MySQL 服务的地址 |
| `MYSQL_PORT` | | 3306 | MySQL 服务的端口 |
| `MYSQL_DB` | √ | | MySQL 数据库库名 |
| `MYSQL_USER` | √ | | MySQL 数据库的用户名 |
| `MYSQL_PASSWORD` | √ | | MySQL 数据库的密码 |
| `MYSQL_PREFIX` | | `wl_` | MySQL 数据表的表前缀 |

## SQLite

使用 SQLite 进行数据存储前，需要下载 [waline.sqlite](https://github.com/lizheming/waline/blob/master/assets/waline.sqlite) 文件至合适的位置。之后在项目中配置如下环境变量即可。


| 环境变量名称 | 必填 | 默认值 | 备注 |
|------------|---------|------|------|
| `SQLITE_PATH` | √ | | SQLite 数据库文件的路径，该路径不包含文件名本身 |
| `SQLITE_DB` | | waline | SQLite 数据库文件名，若文件名变化需要修改该字段值 |
| `SQLITE_PREFIX` | | `wl_` | SQLite 数据表的表前缀 |

## PostgreSQL

[elephantSQL](https://www.elephantsql.com/) 提供了 20M 的免费空间，对于评论服务来说绰绰有余了。如果想要使用 PostgreSQL 的也可以使用它搭建 Waline。同 MySQL 一样，使用 PostgreSQL 作为数据存储服务的话，也需要先导入 [waline.sql](https://github.com/lizheming/waline/blob/master/assets/waline.sql) 创建好表和表结构。之后在项目中配置如下环境变量即可。

| 环境变量名称 | 必填 | 默认值 | 备注 |
|------------|---------|------|------|
| `PG_HOST` | | 127.0.0.1 | PostgreSQL 服务的地址 |
| `PG_PORT` | | 3211 | PostgreSQL 服务的端口 |
| `PG_DB` | √ | | PostgreSQL 数据库库名 |
| `PG_USER` | √ | | PostgreSQL 数据库的用户名 |
| `PG_PASSWORD` | √ | | PostgreSQL 数据库的密码 |
| `PG_PREFIX` | | `wl_` | PostgreSQL 数据表的表前缀 |


## CloudBase

腾讯云开发也一定了 [免费数据库](https://console.cloud.tencent.com/tcb/db/) 支持，即使不部署在腾讯云开发上也可以使用。如果部署在腾讯云开发上，不需要配置任何环境变量，Waline 默认会使用云开发的数据库。如果是部署在其它地方，需要配置以下环境变量。

| 环境变量名称 | 必填 | 默认值 | 备注 |
|------------|---------|------|------|
| `TCB_ENV` |√ |  | 腾讯云开发环境 ID |
| `TCB_ID` |√| | 腾讯云 API 密钥 ID，[在此](https://console.cloud.tencent.com/cam/capi)获取 |
| `TCB_KEY` | √ | | 腾讯云 API 密钥 Key，[在此](https://console.cloud.tencent.com/cam/capi)获取 |
| `JWT_TOKEN` | | | 用户登录密钥，如果没有配任何环境变量的话需要配置此变量，随机字符串即可 |
## 自定义

除了以上数据库存储之外，也可以添加其它存储服务的支持。如果你想帮助 Waline 支持更多的存储服务的话，可以 fork 项目，继承该 [基类](https://github.com/lizheming/waline/blob/master/packages/server/src/service/storage/base.js) 后分别实现对应存储服务的 `select()`, `add()`, `update()`, `delete()` 方法后提交 PR 即可。