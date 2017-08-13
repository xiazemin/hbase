# log4j



og4j:WARN No appenders could be found for logger

\(org.springframework.context.support.ClassPathXmlApplicationContext\).

log4j:WARN Please initialize the log4j system properly.

Spring 使用了LOG4J 这个开源框架来输出信息，

要解决这个问题非常简单，建立LOG4J 的配置文件即可。在src 目录下创建配置文件，选

择菜单File &gt; New &gt; File，文件名输入log4j.properties，文件内容如下所示：

log4j.rootLogger=WARN, stdout

log4j.appender.stdout=org.apache.log4j.ConsoleAppender

log4j.appender.stdout.layout=org.apache.log4j.PatternLayout

log4j.appender.stdout.layout.ConversionPattern=%d %p \[%c\] - %m%n

清单10.6 log4j 的配置文件

加入了这个配置文件后，再次运行程序上面的警告就会消失。尤其在进行 Web 层开发的时

候，只有加入了这个文件后才能看到Spring 后台完整的出错信息。在开发Spring 整合应用

时，经常有人遇到出现404 错误但是却看不到任何出错信息的情况，这时你就需要检查一

下这个文件是不是存在。

org.springframework.core.CollectionFactory2008-05-17 18:50log4j:WARN No appenders could be found for logger \(org.springframework.core.CollectionFactory\).

log4j:WARN Please initialize the log4j system properly.

常用log4j配置，一般可以采用两种方式，.properties和.xml,下面举两个简单的例子：

一、log4j.properties

\#\#\# 设置org.zblog域对应的级别INFO,DEBUG,WARN,ERROR和输出地A1，A2 \#\#

log4j.category.org.zblog=ERROR,A1

log4j.category.org.zblog=INFO,A2

log4j.appender.A1=org.apache.log4j.ConsoleAppender

\#\#\# 设置输出地A1，为ConsoleAppender\(控制台\) \#\#

log4j.appender.A1.layout=org.apache.log4j.PatternLayout

\#\#\# 设置A1的输出布局格式PatterLayout,\(可以灵活地指定布局模式）\#\#

log4j.appender.A1.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss,SSS} \[%c\]-\[%p\] %m%n

\#\#\# 配置日志输出的格式\#\#

log4j.appender.A2=org.apache.log4j.RollingFileAppender

\#\#\# 设置输出地A2到文件（文件大小到达指定尺寸的时候产生一个新的文件）\#\#

log4j.appender.A2.File=E:/study/log4j/zhuwei.html

\#\#\# 文件位置\#\#

log4j.appender.A2.MaxFileSize=500KB

\#\#\# 文件大小\#\#

log4j.appender.A2.MaxBackupIndex=1

log4j.appender.A2.layout=org.apache.log4j.HTMLLayout

\#\#指定采用html方式输出

二、log4j.xml

&lt;?xml version="1.0" encoding="GB2312" ?&gt;

&lt;!DOCTYPE log4j:configuration SYSTEM "log4j.dtd"&gt;

&lt;log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/"&gt;

&lt;appender name="org.zblog.all" class="org.apache.log4j.RollingFileAppender"&gt;

&lt;!-- 设置通道ID:org.zblog.all和输出方式：org.apache.log4j.RollingFileAppender --&gt;

&lt;param name="File" value="E:/study/log4j/all.output.log" /&gt; &lt;!-- 设置File参数：日志输出文件名 --&gt;

&lt;param name="Append" value="false" /&gt; &lt;!-- 设置是否在重新启动服务时，在原有日志的基础添加新日志 --&gt;

&lt;param name="MaxBackupIndex" value="10" /&gt;

&lt;layout class="org.apache.log4j.PatternLayout"&gt;

&lt;param name="ConversionPattern" value="%p \(%c:%L\)- %m%n" /&gt; &lt;!-- 设置输出文件项目和格式 --&gt;

&lt;/layout&gt;

&lt;/appender&gt;

&lt;appender name="org.zblog.zcw" class="org.apache.log4j.RollingFileAppender"&gt;

&lt;param name="File" value="E:/study/log4j/zhuwei.output.log" /&gt;

&lt;param name="Append" value="true" /&gt;

&lt;param name="MaxFileSize" value="10240" /&gt; &lt;!-- 设置文件大小 --&gt;

&lt;param name="MaxBackupIndex" value="10" /&gt;

&lt;layout class="org.apache.log4j.PatternLayout"&gt;

&lt;param name="ConversionPattern" value="%p \(%c:%L\)- %m%n" /&gt;

&lt;/layout&gt;

&lt;/appender&gt;

&lt;logger name="zcw.log"&gt; &lt;!-- 设置域名限制，即zcw.log域及以下的日志均输出到下面对应的通道中 --&gt;

&lt;level value="debug" /&gt; &lt;!-- 设置级别 --&gt;

&lt;appender-ref ref="org.zblog.zcw" /&gt; &lt;!-- 与前面的通道id相对应 --&gt;

&lt;/logger&gt;

&lt;root&gt; &lt;!-- 设置接收所有输出的通道 --&gt;

&lt;appender-ref ref="org.zblog.all" /&gt; &lt;!-- 与前面的通道id相对应 --&gt;

&lt;/root&gt;

&lt;/log4j:configuration&gt;

三、配置文件加载方法：

import org.apache.log4j.Logger;

import org.apache.log4j.PropertyConfigurator;

import org.apache.log4j.xml.DOMConfigurator;

public class Log4jApp {

public static void main\(String\[\] args\) {

DOMConfigurator.configure\("E:/study/log4j/log4j.xml"\);//加载.xml文件

//PropertyConfigurator.configure\("E:/study/log4j/log4j.properties"\);//加载.properties文件

Logger log=Logger.getLogger\("org.zblog.test"\);

log.info\("测试"\);

}

}

