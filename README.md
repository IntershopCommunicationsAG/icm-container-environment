Development Environment for ICM 7.10 and older
==============================================

This project provides some compose files to run some necessary development resources on a local machine.

- SolrCloud development instance with one Zookeeper node and one Solr node
- Development Mail Server (MailHog)
- Database - an Oracle XE server or an MSSQL Server instance

This running instances does not make use of persistent storage, data are stored in the docker images. It is possible to adapt the hostname for the Solr server. If necessary you can change the environment variable `SOLR_HOST`in the compose files. 

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