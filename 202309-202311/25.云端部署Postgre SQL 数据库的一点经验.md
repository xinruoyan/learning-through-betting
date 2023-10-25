###  云端部署Postgre SQL 数据库的一点实战经验

- （by dada 2023.10.10 pm）

  #### 一、背景

​        前期一直以来使用的比较多的数据库平台是Sqlite，其使用方便，入门简单、部署容易等特点，得到了开发者广泛使用。在Nodejs环 境中，Sqlite通过Sequelize模块功能，提供的对象和方法（而不是SQL查询），实现数据库进行交互；从个人实践的几个项目观察，数据库文件是非常轻量级的，一个4000条记录的文件也不足1MBytes;百行内的往往几十K Bytes；其还有一个优点，就是可以灵活通过copy/pase 的方式，直接实现数据库文件的迁移到新的应用执行文件，非常方便高效。不足之处是，没有类似Mysql /Postgre SQL等大型数据库，拥有强大的后台管理app，以可以方便使用SQL命令行或图形化界面，对数据进行SQL查询、修改、备份等离线操作。

   Sqlite如此高效简单，为什么还要部署其他数据库？一个主要的原因是安全备份。记得3个月前某一天，当运行接龙程序执行文件时，Sqlite失灵了，重新npm install 了很多次，都无法解决，当时一个感觉就是麻烦了，没有其他备份的数据库；万一运行不了，影响程序上线了；而且之前所有的运行数据都是该数据库保存和运行支撑的，非常大的运行风险。赶紧执行了一下其他程序，还好，没有受到影响，基本定位到是当前程序的问题，通过多次卸载安装，最终解决。通过这次事情后，一直在想，一定要有一个备份的方案，来实现对数据的日常管理，确保数据安全和程序正常运行。

​       通过对比了主流的Mysql 和Postgre 数据库，决定先学习Postgre数据库，一个是其开源特点，同时Sequelize模块功能配置相对简单，特别是在数据类型上，基本和之前使用的Sqlite相同，基本可以共用数据库模型文件，省时省力。

#### 二、云端部署步骤

​     基于Window平台的PC版的Postgre,按着官网提供的 文档，一步步执行就可以顺利部署。在这里,我主要分享的是基于Linux平台的，在云上部署的一些经验；借助ChatGPT，快速实现了云端部署，供大家一起交流探讨。

###### Q1:如何在云上安装部署porgresql 数据库，并通过web端查询到数据库数据？

````
  在云上安装和部署PostgreSQL数据库与在本地环境中的安装部署步骤相似。以下是一般的步骤：
1. 创建云服务器实例：在你的云服务提供商（如AWS、Google Cloud、Azure等）创建一个新的虚拟机实例。选择适当的操作系统（大多数情况下是Linux）。
2. 连接到服务器：使用SSH登录到你的新服务器。
3. 安装PostgreSQL：在服务器上安装PostgreSQL。对于基于Debian、Ubuntu的系统，可以使用以下命令：
```
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib
```
对于基于CentOS的系统，可以使用以下命令：
```
sudo yum install postgresql-server postgresql-contrib
```
4. 初始化数据库：安装完成后，你需要对数据库进行初始化：
```
sudo service postgresql initdb
```
5. 启动数据库服务：使用以下命令启动PostgreSQL服务：
```
sudo service postgresql start
```
6. 创建一个数据库和用户：登录到PostgreSQL，创建一个数据库和用户，并给予用户适当的权限。
7. 配置PostgreSQL以接受远程连接：编辑pg_hba.conf和postgresql.conf文件，允许你的web服务器的IP地址远程连接到数据库。
8. 创建数据库表并插入数据：根据你的需要创建数据库表并插入数据。
   现在，你可以通过web端查询数据库信息了。你需要一个可以远程连接到数据库的web应用程序。这可以通过在web服务器上安装和配置一个应用程序，如phpPgAdmin，或者使用一个桌面应用程序，如PgAdmin或DBeaver，来实现。
````

###### Q2:如何配置 pgAdmin4，以实现对云上postgresql管理？

```
若要使用pgAdmin管理云上的PostgreSQL数据库，需要执行以下步骤：
1. 在你的本地机器上安装pgAdmin。
2. 打开pgAdmin，点击"File"（文件）菜单，然后选择"Add Server"（添加服务器）。
3. 在弹出的窗口中，提供以下信息：
   - "Name"（名称）：为你的数据库服务器提供一个名称。
   - "Host"（主机）：输入你的云服务器的IP地址。
   - "Port"（端口）：如果你没有改变默认的PostgreSQL端口，这个值应该是5432。
   - "Maintenance DB"（维护数据库）：通常，这个值应该是"postgres"。
   - "Username"（用户名）：输入"postgres"或者你创建的任何其他用户。
   - "Password"（密码）：输入你为PostgreSQL设置的密码。（初始化时输入的密码）
   - 可选：你可以勾选"Store password"（保存密码）以避免每次连接时都要输入密码。
4. 点击"Ok"（确定）。pgAdmin会尝试连接到你的云服务器的PostgreSQL数据库。

如果你无法连接到你的数据库，可能需要检查几项内容：
- 确保你的云服务器的防火墙允许从你的IP地址进行远程连接。
- 确保你的PostgreSQL配置文件（通常位于/etc/postgresql/版本号/main/）允许远程连接。
- 确保你正确输入了所有信息，特别是主机名和密码。
```

###### Q3.如何配置`postgresql.conf`和`pg_hba.conf`文件？

````
要允许PostgreSQL接受远程连接，需要修改两个配置文件：`postgresql.conf`和`pg_hba.conf`。
1. `postgresql.conf`： 这个文件控制PostgreSQL服务器的大部分设置。
   - 首先，找到`postgresql.conf`文件，它通常位于`/etc/postgresql/<版本>/main/`目录下。
   - 打开此配置文件，找到`listen_addresses`这一行，并修改为以下内容：
    listen_addresses = '*'
 ```
 这里的`*`意味着PostgreSQL将会监听来自所有IP地址的连接请求。如果你希望只允许特定IP地址的请求，可以将`*`替换为那个IP地址。
 `pg_hba.conf`： 这个文件控制哪些主机、用户和数据库可以进行连接，以及可以使用的认证方式。

- 这个文件也通常位于`/etc/postgresql/<版本>/main/`目录下。

- 在此文件的最后，添加以下一行来允许所有IP地址通过密码认证连接到所有数据库：
  ```
  host all all 0.0.0.0/0 md5
  ```
  这里的`0.0.0.0/0`表示所有IP地址。如果你只希望允许特定IP地址连接，可以将其替换为相应的IP地址和子网掩码。
  完成这些修改后，记得重启PostgreSQL服务以使这些配置生效：
  ```
  sudo systemctl restart postgresql
  ```
 ( 注意：打开远程数据库连接可能会增加被攻击的风险。在生产环境中，你应该尽可能地限制可以连接到数据库的IP地址，并使用强密码和/或其它安全措施。)
````

######   Q4.如何login 数据库？

```
 ···bash 
  sudo -u postgres psql
  ···
```


  <img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20231010160333504.png" alt="image-20231010160333504" style="zoom:67%;" />

 <img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20231010160618122.png" alt="image-20231010160618122" style="zoom:67%;" />

#### 三、PC端 Node.js(Sequelize模块)配置文件

​    按以上步骤，基本完成了基础数据库的安装部署，pc版和云端最大的不同是在host 的配置参数上，本机上为“localhost‘，而当调用云端数据库时，host 参数需要修改为”云服务器ip地址“，这是最主要和关键的配置参数。以下是通过sequelize模块实现对数据库连接管理的基础配置文件：

###### 1.数据库对象配置文件config.js  

```
const { Sequelize} = require('sequelize');
const dbConfig = 
{
    dialect: 'postgres',     // 数据库类型
    username: 'postgres',   // 用户名
    host: 'xxx.xxx.xxx.xxx',      // 云服务器IP 
    
    password: '？？？？',    // 数据库初始化时的密码
    database: 'my_database',  // "postgres"为默认的一个数据库;可以通过手工添加自己
    
  }
  module.exports  = new Sequelize(
    dbConfig.database,
    dbConfig.username,
    dbConfig.password,
    {
      host: dbConfig.host,
      dialect: dbConfig.dialect, //数据库类型(postgres)
    }
)
```

2. ###### 数据库表模型文件 table.js 

```
// Database Setup

const { Sequelize, DataTypes, Model, STRING } = require('sequelize');
const db = require('./dbconfig')

// 1.raw table
const Ra = db.define('ras', {
  id: {
    type: DataTypes.INTEGER,
    allowNull: false,
    primaryKey: true,
    autoIncrement: true
  },
  type: DataTypes.STRING,  
  user_id: DataTypes.UUID,
  full_name: DataTypes.STRING,
  user_id: DataTypes.UUID,
  identity_number: DataTypes.INTEGER,
  symbol: DataTypes.STRING,
  opponent_threshold: DataTypes.INTEGER,
  snapshot_id: DataTypes.UUID,
  asset_id: DataTypes.UUID,
  amount: DataTypes.FLOAT,
  opening_balance: DataTypes.FLOAT,
  closing_balance: DataTypes.FLOAT,
  trace_id: DataTypes.UUID,
  state: DataTypes.STRING,
  created_at: DataTypes.DATE,
  transaction_hash: DataTypes.STRING,
})

module.exports = {Ra}
```

3. ###### 数据查询

  通过Pgadmin4 后台管理APP，可实现对数据库表离线查询、修改等操作。

<img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20231010162128187.png" alt="image-20231010162128187" style="zoom:80%;" />

#### 四、复盘小结

​     以上是本人通过借助ChatGPT,在云上部署Postgre SQL 的一点实战做法；其过程非常快速和顺利，当数据呈现在眼前时，自己都点不敢相信，在此与大伙一起分享；实践证明，数据学习安装部署的门槛没有想象中的多高大上的，Just do it ！同时也希望有数据库需求的小伙伴们，一起来探讨交流，共同成长。