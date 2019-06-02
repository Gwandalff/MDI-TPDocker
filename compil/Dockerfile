FROM centos:7.4.1708

MAINTAINER noasking

RUN yum update -y \
        && yum install -y git gcc gcc-c++ autoconf automake cmake \
                          freetype-devel libtool make mercurial nasm \
                          pkgconfig zlib-devel \
                          bzip2-devel hostname \
                          openssl \
                          openssl-devel \
                          wget \
                          which \
                          boost* \
        && yum clean all


ADD jdk-8u131-linux-x64.tar.gz /

RUN wget https://github.com/opencv/opencv/archive/3.4.6.tar.gz

RUN yum install -y java-1.8.0-openjdk-devel

RUN yum install -y ant

RUN cd \
    && mkdir opencv && tar xvzf /3.4.6.tar.gz -C opencv --strip-components 1 \
    && cd opencv \
    && mkdir build \
    && cd build \
    && cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/opencv/release -D BUILD_TESTS=OFF .. \
    && make -j8 \
    && make install \
    && cp /opencv/release/share/OpenCV/java/libopencv_java346.so /usr/local/lib/ \
    && cd \
    && rm -f /opencv-3.4.6.tar.gz

RUN git clone https://github.com/barais/ESIRTPDockerSampleApp.git

WORKDIR /ESIRTPDockerSampleApp

RUN yum install -y maven \
    && mvn install:install-file -Dfile=/opencv/release/share/OpenCV/java/opencv-346.jar -DgroupId=org.opencv -DartifactId=opencv -Dversion=3.4.6 -Dpackaging=jar \
    && mvn install \
    && mvn package \
    && ls -a

RUN mkdir -p /app_docker
RUN chmod -R 777 /app_docker
RUN cp -r /ESIRTPDockerSampleApp/target/ /app_docker/
RUN cp -r /opencv/ /app_docker/opencv/

CMD ["/bin/bash"]
