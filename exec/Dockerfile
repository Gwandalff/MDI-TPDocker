FROM frolvlad/alpine-glibc

RUN apk add wget

RUN wget http://mirror.cnop.net/jdk/linux/jdk-8u131-linux-x64.tar.gz \
 && mkdir java && tar xvzf /jdk-8u131-linux-x64.tar.gz -C java --strip-components 1

ENV JAVA_HOME /java
ENV JRE_HOME $JAVA_HOME/jre
ENV CLASSPATH .:$JAVA_HOME/lib:$JRE_HOME/lib
ENV PATH $PATH:$JAVA_HOME/bin

RUN mkdir -p /home/barais/git/opencv/data/

RUN mkdir /app_docker_exec
COPY /app_docker/* /app_docker_exec/
RUN java -Djava.library.path=/app_docker_exec/opencv/release/share/OpenCV/java/ -jar /app_docker_exec/fatjar-0.0.1-SNAPSHOT.jar