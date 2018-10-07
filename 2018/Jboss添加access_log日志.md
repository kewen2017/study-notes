好久好久不用Jboss了，其实跟Tomcat一样，access_log的参数是统一的，这里记录一下。
插一个官方的说明文档： https://docs.jboss.org/jbossweb/2.1.x/config/valve.html

**主要目的：**由于现网为记录access.log日志，导致实际出现问题时定位问题困难，目前添加access.log配置进行记录，方便问题定位。

**影响点：**对服务功能无影响，会在指定路径记录日志文件，周期很长之后可能会占用一定磁盘空间需要进行手动清理和归档（按照现网实际的访问和操作量决定）。

**配置方法：**

1.进入服务器路径（下面的数字为项目号） 
${JBOSS_HOME}/server/defaul/deploy/jboss-web.deployer/server.xml
找到 server.xml 配置文件

2.修改server.xml
代码如下：

    < Valve className="org.apache.catalina.valves.AccessLogValve" 
                                         prefix="sdm_access." suffix=".log" pattern="%h %l %u %t %r %s %b" 
                                         directory="${jboss.server.home.dir}/log" resolveHosts="false" />

3.修改保存后进行重启

4.重启环境后进入服务器路径："${jboss.server.home.dir}/log" 检查
如果配置生效，会出现如图所示的sdm_access.log的文件，记录用户的访问时间和具体的操作。
