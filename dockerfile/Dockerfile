FROM ubuntu:14.04

MAINTAINER wangsh<462620215@qq.com>

RUN sudo rm -f /etc/localtime \
    && sudo ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN sudo apt-get update \
    && sudo apt-get install -y openjdk-7-jdk \
    && sudo apt-get install -y openjdk-7-jre \
    && sudo apt-get install -y wget \
    && sudo apt-get install -y zip \
    && sudo apt-get install -y vim
 
RUN echo "export JAVA_HOME=/usr/lib/jvm/Java-7-openjdk-amd64">>/etc/profile
RUN echo "export JRE_HOME=$JAVA_HOME/jre">>/etc/profile
RUN echo "export CLASSPATH=$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH">>/etc/profile
RUN echo "export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH">>/etc/profile

RUN sudo apt-get install -y subversion

RUN wget http://brandpano-test.oss-cn-shenzhen.aliyuncs.com/docker-github/settings.xml \
    && mkdir -p /root/.m2/ && mv settings.xml /root/.m2/
    
RUN wget http://brandpano-test.oss-cn-shenzhen.aliyuncs.com/docker-github/java.security \
    && mv java.security /usr/lib/jvm/java-1.7.0-openjdk-amd64/jre/lib/security/
    
RUN wget http://brandpano-test.oss-cn-shenzhen.aliyuncs.com/docker-github/entrypoint.sh \
    && mkdir /work && mv entrypoint.sh /work/ 

RUN ["chmod", "+x", "/work/entrypoint.sh"]

WORKDIR /work

RUN wget http://brandpano-test.oss-cn-shenzhen.aliyuncs.com/docker-github/apache-tomcat-7.0.82.zip \
     && unzip apache-tomcat*.zip && rm -f apache-tomcat*.zip && mv apache-tomcat* tomcat

RUN wget http://brandpano-test.oss-cn-shenzhen.aliyuncs.com/docker-github/apache-maven-3.3.9-bin.zip \
    && unzip apache-maven*.zip && rm -f apache-maven*.zip && mv apache-maven* maven

RUN echo "export M2_HOME=/work/maven">>/etc/profile
RUN echo "export PATH=$M2_HOME/bin:$PATH">>/etc/profile

EXPOSE 8080

ENTRYPOINT ["/work/entrypoint.sh"]
