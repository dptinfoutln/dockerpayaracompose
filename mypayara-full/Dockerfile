FROM payara/server-full:5.2020.6-jdk11
#Allows autodeploy
RUN chown payara:payara $DEPLOY_DIR
#installs postgresql jdbc driver
#and adds a jdbc connection pool and ressource
ADD https://jdbc.postgresql.org/download/postgresql-42.2.18.jar /opt/payara/appserver/glassfish/lib/postgresql.jar  

RUN asadmin start-domain && \
    asadmin --user admin \
       				 --passwordfile=$PASSWORD_FILE \
    				 set-hazelcast-configuration --enabled=true --dynamic=true &&\
    asadmin --user admin \
                              --passwordfile=$PASSWORD_FILE \
			       create-jdbc-connection-pool \
			        --datasourceclassname org.postgresql.ds.PGConnectionPoolDataSource  \
			        --restype javax.sql.ConnectionPoolDataSource \
				--property portNumber=5432:password=glassfishdbpassword:user=glassfish:serverName=db:databaseName=glassfish \
				postgres-pool && \
    asadmin --user admin \                                                                                           
                              --passwordfile=$PASSWORD_FILE \
			       create-jdbc-resource --connectionpoolid postgres-pool jdbc/postgres-pool && \
    asadmin stop-domain
