# Development Environment for ICM 7.10 and older

This project provides some compose files to run some necessary development resources on a local machine.

- SolrCloud development instance with one Zookeeper node and one Solr node
- Development Mail Server (MailHog)
- Database - an Oracle XE server or an MSSQL Server instance

This running instances does not make use of persistent storage, data are stored in the docker images. It is possible to adapt the hostname for the Solr server. If necessary you can change the environment variable `SOLR_HOST`in the compose files. 

## Commands

**Start environment**
```
docker-compose -f docker-compose-<databasetype>.yml up
```

**Stop environment**
```
docker-compose -f docker-compose-<databasetype>.yml stop
```

**Stop environment and remove containers**
```
docker-compose -f docker-compose-<databasetype>.yml down
```

## Development Environment Configuration

### Oracle

This is the configuration of the environment.properties file:
```
# Database configuration
databaseHost = localhost
databasePort = 1521
databaseSid = XE
databaseTnsAlias = isdb1.world
databaseUser = intershop
databasePassword = intershop
databaseType = oracle
jdbcUrl = jdbc:oracle:thin:@localhost:1521:XE

solrZooKeeperHostList = localhost:2181/solr8
solrClusterIndexPrefix = localicm
```

### MSSQL Server

This is the configuration of the environment.properties file:
```
# Database configuration
# only for legacy deployment
databaseHost = localhost
databasePort = 1234
databaseSid = SID
databaseTnsAlias = tns.world
# necessary for MSSQL
databaseUser = intershop
databasePassword = intershop
databaseType = mssql
jdbcUrl = jdbc:sqlserver://localhost:1433;database=ICMDB;

solrZooKeeperHostList = localhost:2181/solr8
solrClusterIndexPrefix = localicm
```

### Test Mail Server Configuration

```
# test.properties
mail.smtp.host=localhost
mail.smtp.port=1025

intershop.SMTPServer=localhost
intershop.mail.messageID.domain=localicm
```

### Environment Settings

**Linux / Mac**
```
export ORG_GRADLE_PROJECT_buildEnvironmentProperties=<path to config>/local-environment.properties
export ORG_GRADLE_PROJECT_testEnvironmentProperties=<path to config>/local-environment.properties
export ORG_GRADLE_PROJECT_test.properties=<path to config>/test.properties
```

**Windows Command Line**
```
set ORG_GRADLE_PROJECT_buildEnvironmentProperties=<path to config>/local-environment.properties
set ORG_GRADLE_PROJECT_testEnvironmentProperties=<path to config>/local-environment.properties
set ORG_GRADLE_PROJECT_test.properties=<path to config>/test.properties
```

