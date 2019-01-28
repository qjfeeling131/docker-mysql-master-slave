# docker-mysql-master-slave
It uses the docker to create the mysql server of master and slave


It also need to configure in your local after you run this dockerfile.yml in your local. and the confgiure as below:

#1.Enter the master container to get the mysql log information:

`docker exec -it <container name> /bin/bash `
`mysql -uroot -proot`

now you enter the mysql server, then input the command:

`mysql show master status;'

to get the master log information and record the 'file', and 'Position';

using the `exit` to quit the current master server;

#2. Enter the slave container to configure the master-salve setting:

`docker exec -it <container name> /bin/bash`
`mysql -urooot -proot`

` CHANGE MASTER TO
    MASTER_HOST='<master container name>',
    MASTER_USER='root',
    MASTER_PASSWORD='root',
    MASTER_LOG_FILE='<the 'file' name come from master status>',
    MASTER_LOG_POS=<the 'Position' name come from master status>;`
    
`stop slave`,
`start slave`,
`show slave status\G;` to check that configuration whether run normally.

