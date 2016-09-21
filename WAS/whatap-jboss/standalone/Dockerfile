FROM whatap/jdk8u102

# Set the WILDFLY_VERSION env variable
ENV WILDFLY_VERSION 8.2.1.Final
ENV WILDFLY_SHA1 77161d682005f26acb9d2df5548c8623ba3a4905
ENV JBOSS_HOME /opt/jboss/wildfly

# Add the WildFly distribution to /opt, and make wildfly the owner of the extracted tar content
# Make sure the distribution is available from a well-known place
#RUN cd $HOME \
#    && curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz \
#    && sha1sum wildfly-$WILDFLY_VERSION.tar.gz | grep $WILDFLY_SHA1 \
#    && tar xf wildfly-$WILDFLY_VERSION.tar.gz \
#    && mv $HOME/wildfly-$WILDFLY_VERSION $JBOSS_HOME \
#    && rm wildfly-$WILDFLY_VERSION.tar.gz
RUN mkdir /opt/jboss

RUN useradd -ms /bin/bash jboss

RUN cd $HOME \
    && curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz
RUN sha1sum wildfly-$WILDFLY_VERSION.tar.gz | grep $WILDFLY_SHA1
RUN tar xf wildfly-$WILDFLY_VERSION.tar.gz
RUN mv $HOME/wildfly-$WILDFLY_VERSION $JBOSS_HOME

RUN chown jboss:jboss -R $JBOSS_HOME

RUN rm wildfly-$WILDFLY_VERSION.tar.gz

WORKDIR $JBOSS_HOME

# Get whatap-apm
ADD https://s3.ap-northeast-2.amazonaws.com/apm-public/automation/whatap_run.sh $JBOSS_HOME
USER root
RUN chmod 777 whatap_run.sh
USER jboss



# Expose the ports we're interested in
EXPOSE 8080

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interface
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0"]
