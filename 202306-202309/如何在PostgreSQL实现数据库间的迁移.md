###  如何在PostgreSQL实现数据库间的迁移

- ​    (by dada 2023.10.13 pm)

#### 一、基本环境准备

1. PC和云端都安装了Postgre SQL数据库
2. 打开运行Pgadmin4管理app，并分别连接上本机Local 和云端 Cloud DB数据库
3. 本地local 数据库表格已存储数据。

#### 二、备份迁移步骤

​     Postgre 数据库提供了强大的后台管理APP:pgAdmin 4 管理平台;日常基础的SQL,都可以通过该app实现；尤其实用的数据库的备份和恢复，以下是个人初浅的实践，供大伙一起讨论参考。本案例实现的是：从PC 到 云端 Clound DB 即：windows平台到 Linux平台的执行过程。

具体的操作办法就是通过在PC上运行pgAdmin4.exe 执行文件,直接通过窗口界面，具体步骤：

1. ##### 创建目标数据库 

   <img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20231013165512438.png" alt="image-20231013165512438" style="zoom:50%;" />

2. ##### 在原数据库备份文件到指定目录

##### <img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20231013164655607.png" alt="image-20231013164655607" style="zoom: 50%;" />

<img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20231013164326824.png" alt="image-20231013164326824" style="zoom:50%;" />

##### 3.恢复数据库文件到目标数据库中

<img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20231013164911782.png" alt="image-20231013164911782" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20231013164443730.png" alt="image-20231013164443730" style="zoom: 67%;" />

##### 4.核查数据迁移结果

   打开俩数据库表核查，源备份和目标恢复数据库表格总数均为：7张；打开其中一张表格数据：ras记录数都是21条；并继续核对其中一条记录各列属性，数据都相符，因此备份迁移成功。

<img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20231013195551092.png" alt="image-20231013195551092" style="zoom: 70%;" />

#### 三、复盘小结

​      以上实战案例完成的是 从PC_DB to Clound_DB (windows 2 Linux)的过程；同理也可以非常方便地实现： PC_DB to PC_DB(Windows 2 windows、Clound_DB to Clound_DB （Linux 2 Linux）以及 Clound DB to PC DB（Linux to Windows）等不同平台或操作系统间的Postgres SQL数据库间的数据迁移和日常备份保存操作。另外，日常除了通过Pgadmin4 APP外，还可以通过命令行的方式来实现备份及恢复操作。

