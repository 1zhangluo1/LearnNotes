## MySQL和MariaDB区别与联系

| 区别                | MySQL                                               | MariaDB                                                      |
| ------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| JSON                | MySQL 将 JSON 报告存储为二进制对象。                | MariaDB 将 JSON 报告存储在字符串中。MariaDB 的 JSON 数据类型是 *LONGTEXT* 的别名。 |
| Oracle 数据库兼容性 | MySQL 具有很高的兼容性，但不支持 PL/SQL。           | MariaDB 具有很高的兼容性，自 10.3 版本起支持 PL/SQL。        |
| 速度和性能          | 在复制和查询方面，MySQL 比 MariaDB 稍慢一些。       | 在复制和查询方面，MariaDB 比 MySQL 稍快一些。                |
| 功能                | MySQL 支持超级只读函数、动态列和数据掩码。          | MariaDB 支持隐形列和临时表空间。                             |
| 身份验证            | MySQL 有 *validate_password* 组件。                 | MariaDB 有三个密码验证器组件。                               |
| 加密                | MySQL 数据库使用 InnoDB 和 AES 对静态数据进行加密。 | MariaDB 支持临时日志加密和二进制日志加密。                   |
| 存储引擎            | MySQL 的存储引擎比 MariaDB 少。                     | MariaDB 的存储引擎比 MySQL 多，可以在一个表中使用多个引擎。  |
| 许可证              | MySQL 有两个版本：MySQL 企业版和 GPL 版本。         | MariaDB 完全采用 GPL 版本。                                  |
| 线程池              | MySQL 企业版带有线程池。                            | MariaDB 可以同时管理超过 20 万个连接，比 MySQL 更多。        |

### 渊源：

MySQL 和 MariaDB 都是开源数据库技术。您可以使用它们以包含行和列的表格格式存储数据。MySQL 是最广泛采用的开源数据库。它是许多热门网站、应用程序和商业产品的主要关系数据库。MariaDB 是 MySQL 的修改版本。在 MySQL 被 Oracle 公司收购后，出于许可和分发方面的问题，MySQL 的原始开发团队制作了 MariaDB。自收购以来，MySQL 和 MariaDB 经历了不同的发展。但是，MariaDB 采用 MySQL 的数据和表定义文件，还使用相同的客户端协议、客户端 API、端口和套接字。这是为了让 MySQL 用户能够轻松切换到 MariaDB。