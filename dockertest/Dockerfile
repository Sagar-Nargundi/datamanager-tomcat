FROM centos


COPY wait-for-it.sh /wait-for-it.sh
RUN chmod +x /wait-for-it.sh

RUN mkdir /opt/tomcat/



WORKDIR /opt/tomcat
RUN curl -O https://raw.githubusercontent.com/Sagar-Nargundi/datamanager-tomcat/master/tomcat.tar.gz

RUN tar xvfz tomcat.tar.gz

RUN mv tomcat/* /opt/tomcat/.

WORKDIR /opt/tomcat/datamanager-deploy

RUN curl -O https://raw.githubusercontent.com/Sagar-Nargundi/datamanager-tomcat/master/datamanager.war

RUN ls -l

RUN groupadd tomcat

RUN useradd -s /sbin/nologin -g tomcat -d /opt/tomcat tomcat

RUN chown tomcat:tomcat properties/

WORKDIR /opt/tomcat/datamanager-deploy/properties


RUN chown tomcat:tomcat *

RUN yum -y install java

RUN java -version

ENV CATALINA_HOME=/opt/tomcat

EXPOSE 8080

CMD ["./wait-for-mysql.sh", "mysql-docker-container:3306", "--", "echo", "connecting to mysqldb ... !!!"]

CMD ["/opt/tomcat/bin/catalina.sh", "run"]
