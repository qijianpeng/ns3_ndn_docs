1. NS-3 based Named Data Networking (NDN) simulator ndnSIM: simulation of NDN, ICN, Information-Centric Networking <https://ndnsim.net/current/intro.html>
2. ndnSIM安装、源代码结构与修改兴趣包生存周期_书忆江南的IT博客-CSDN博客_ndnsim源码 <https://blog.csdn.net/qq_33588730/article/details/81061724>
3. NS3 <https://www.nsnam.org/>
4. TypeId in NS3 <https://segmentfault.com/a/1190000015805795>
  `IidManager`是一个数据库，`TypeId`是数据库的key，`Attribute`和`TraceSource`是数据库
  的两张表。每在`GetTypeId`里`AddAttribute`或者`AddTraceSouce`一次就相当于给表里加
  一行记录，所有与`Attribute`、`TraceSource`相关的操作都会去表里找自己需要的信息。
5. Adding custom fields to packets in ndnSIM 2.3 without forking the entire repository. <https://lo.calho.st/posts/ndnsim-custom-fields/>
