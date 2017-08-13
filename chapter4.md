# javaapi实践



log4j:WARN No appenders could be found for logger \(org.apache.hadoop.metrics2.lib.MutableMetricsFactory\).

log4j:WARN Please initialize the log4j system properly.

log4j:WARN See http://logging.apache.org/log4j/1.2/faq.html\#noconfig for more info.



这种情况一般是由于log4j这个日志信息打印模块的配置信息没有给出造成的，可以在项目的src目录下，新建一个文件new-&gt;other-&gt;general-&gt;file，命名为“log4j.properties”，填入以下信息：



log4j.rootLogger=INFO, stdout

log4j.appender.stdout=org.apache.log4j.ConsoleAppender

log4j.appender.stdout.layout=org.apache.log4j.PatternLayout

log4j.appender.stdout.layout.ConversionPattern=%d %p \[%c\] - %m%n

log4j.appender.logfile=org.apache.log4j.FileAppender

log4j.appender.logfile.File=target/spring.log

log4j.appender.logfile.layout=org.apache.log4j.PatternLayout

log4j.appender.logfile.layout.ConversionPattern=%d %p \[%c\] - %m%n

保存后重新运行即可成功。

