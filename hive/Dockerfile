FROM centos:7
ENV JAVA_HOME /usr/lib/jvm/jre-1.8.0-openjdk
COPY hdp.repo /etc/yum.repos.d/
COPY mysql-connector-java-8.0.14-1.el7.noarch.rpm /root/

RUN yum updateinfo \
    && yum install -y sudo java-1.8.0-openjdk-devel hadoop-yarn hadoop-mapreduce  hive hive-metastore tez \
    && yum clean all

RUN yum localinstall -y /root/mysql-connector-java-8.0.14-1.el7.noarch.rpm

RUN cp /usr/share/java/mysql-connector-java-8.0.14.jar /usr/hdp/3.1.0.0-78/hive/lib/mysql-connector-java.jar
