FROM	centos:8.1.1911

RUN		sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* \
		&& sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

RUN		yum install -y \
			sudo \
			git \
		&& yum update -y

RUN		sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* \
		&& sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

RUN		curl -O https://download.java.net/java/GA/jdk17.0.2/dfd4a8d0985749f896bed50d7138ee7f/8/GPL/openjdk-17.0.2_linux-x64_bin.tar.gz \
		&& tar -xf openjdk-17.0.2_linux-x64_bin.tar.gz -C /usr/local/ \
		&& rm -f openjdk-17.0.2_linux-x64_bin.tar.gz \
		&& ln -s /usr/local/jdk-17.0.2/bin/java /usr/bin/java \
		&& ln -s /usr/local/jdk-17.0.2/bin/javac /usr/bin/javac
ENV		JAVA_HOME=/usr/local/jdk-17.0.2
		
RUN 	curl -O https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz \
		&& tar -xf apache-maven-3.9.9-bin.tar.gz -C /usr/local/ \
		&& rm -f apache-maven-3.9.9-bin.tar.gz \
		&& ln -s /usr/local/apache-maven-3.9.9/bin/mvn /usr/bin/mvn


RUN		useradd -m -s /bin/bash ubimex \
		&& echo ubimex:ubimex | chpasswd \
		&& usermod -aG wheel ubimex

COPY	.m2 /home/ubimex/.m2
RUN		chown ubimex:ubimex -R /home/ubimex/.m2

RUN		mkdir /test/
RUN		chown ubimex:ubimex -R /test/
		
USER	ubimex
		
RUN		mkdir -p /home/ubimex/amhs/in \
		&& mkdir -p /home/ubimex/amhs/out