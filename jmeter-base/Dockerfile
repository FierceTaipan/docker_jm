# Use Java 8
FROM openjdk:8-jre-slim

# JMeter version
ARG JMETER_VERSION=5.1.1


# Install few utilities
RUN apt-get clean && \
    apt-get update && \
    apt-get -qy install \
                wget \
                telnet \
                iputils-ping \
                unzip \
		curl

# Install JMeter
RUN   mkdir /jmeter \
      && cd /jmeter/ \
      && wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-$JMETER_VERSION.tgz \
      && tar -xzf apache-jmeter-$JMETER_VERSION.tgz \
      && rm apache-jmeter-$JMETER_VERSION.tgz


RUN cd /jmeter/ && wget -P apache-jmeter-$JMETER_VERSION/lib/ext https://repo1.maven.org/maven2/kg/apc/jmeter-plugins-manager/1.3/jmeter-plugins-manager-1.3.jar && \
    wget -P apache-jmeter-$JMETER_VERSION/lib https://repo1.maven.org/maven2/kg/apc/cmdrunner/2.2/cmdrunner-2.2.jar && \
    java -cp apache-jmeter-$JMETER_VERSION/lib/ext/jmeter-plugins-manager-1.3.jar org.jmeterplugins.repository.PluginManagerCMDInstaller


RUN /jmeter/apache-jmeter-$JMETER_VERSION/bin/PluginsManagerCMD.sh install jpgc-casutg,jpgc-graphs-basic,jpgc-graphs-composite,jpgc-graphs-vs,jpgc-graphs-additional,jpgc-ggl,jpgc-cmd,jpgc-synthesis,jpgc-graphs-dist

# Set JMeter Home
ENV JMETER_HOME /jmeter/apache-jmeter-$JMETER_VERSION/

# Add JMeter to the Path
ENV PATH $JMETER_HOME/bin:$PATH
