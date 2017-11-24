# Lab 0: Prerequisites for Oracle Cloud Labs

## Create a Private / Public Keys

To configure cloud services and to access them later you have to create a public / private key pair.

To create the keys [for Unix follow these instructions](https://docs.oracle.com/en/cloud/paas/database-dbaas-cloud/csdbi/generate-ssh-key-pair.html#GUID-2BD5B767-0659-4791-A170-279F469B2CC3), for Windows [follow the instructions here](https://docs.oracle.com/en/cloud/paas/database-dbaas-cloud/csdbi/create-ssh-tunnel.html#GUID-6929CE39-6CD7-46C9-8022-929A9844B1C5).

## Set Replication Policy

We will do this lab together. Without setting the replication policy you will have issues with Oracle PaaS services later. Always set this first for a new idendity domain. Actually, to successfully work with the PaaS services it is less important how you set it, just that you set. (For legal and compliance reasons this is obviously different).

If you are working on your own, the details are described in my [blog post about geo replication](http://www.munzandmore.com/2017/ora/oracle-storage-geo-replication)


# Lab O1: Oracle ACCS

ACCS is short for application container cloud service. In this lab we will deploy a Java EE application to ACCS. Note, that you could also package a go, Spring Boot or Python application. ACCS provides the language runtime only and is therefore very flexible.

Access to to Java EE module to deploy as well as the detailed steps to complete this lab are described here:

[ACCS with Java EE](https://github.com/oracle/weblogic-innovation-seminars/blob/caf-12.2.1/cloud.demos/jcs.basics/create.dbcs.ui.md).


# Lab O2: Oracle DB as a Service


## DB as Service in Oracle Cloud

Provision the database as described in [create DB as a Service](https://github.com/oracle/weblogic-innovation-seminars/blob/caf-12.2.1/cloud.demos/jcs.basics/create.dbcs.ui.md). Unike in the description, please use the key that you just created.

Note that there are some small changes in the UI compared to the instructions. The cloud is very dynamic and Oracle keeps improving it sometimes :-)

Provisioning the service will take about 20 minutes.

## Access your DB instance

### Connect to the instance with ss

From a command prompt in Linux (or Putty on Windows) you can connect to the compute instance that is running the DB. This is a unique feature for the Oracle cloud and not possible for AWS (where you only the DB as a service, but no access to a VM).

In a shell, run the following command to your DB instance:

```
ssh -i YOUR_PRIV_keyfile oracle@PUBLIC_IP
```

Note, there is an oracle user, that you use to run sqlplus etc. and a opc user that also allows sudo access etc.
So run the following command to create a test user for the DB service (the whole block below is taken from Tim Hall's [oraclebase blog](https://oracle-base.com/articles/vm/oracle-cloud-database-as-a-service-dbaas-create-service#network) - I had no idea about the setting the session for the PDB1 container):

```
[oracle@obtest1 ~]$ sqlplus / as sysdba

SQL*Plus: Release 12.2.0.1.0 Production on Tue Nov 8 09:44:42 2016

Copyright (c) 1982, 2016, Oracle.  All rights reserved.


Connected to:
Oracle Database 12c Enterprise Edition Release 12.2.0.1.0 - 64bit Production

SQL> ALTER SESSION SET CONTAINER = pdb1;

Session altered.

SQL> CREATE USER test IDENTIFIED BY test;

User created.

SQL> GRANT CREATE SESSION TO test;

Grant succeeded.
```

### SQL Client? 

Do this lab if you need an SQL client installed locally already. Alternatively install [SQLcl from this location](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html) which requires Java JRE 8 installed.

## Option 1: Open DB Port Listen Port (Poor man solution and risky)

An option is to open port 1521 to your DB as a service (which is discouraged for security reasons, but possibly okay to try it out once?). To do so go the DB service and click on the hamburger icon, go to access rules and open the port for the listener (1521). 

### Connect to DB via Port 1521
From a terminal on your *local machine* connect using the following command. Get the connect string from the Oracle cloud console:

```

$ ./sql test/test@//111.222.333.444:1521/CONNECT_STRING

$ select 42 from dual;
```

## Option 2: Connect using an SSH tunnel

The better option is [using an SSL Tunnel](http://barrymcgillin.blogspot.de/2015/05/sqlcl-cloud-connections-via-secure.html).

You are free to do this lab however you like. Or another option that we don't follow in this lab is to use your [local SQL Developer](https://getpocket.com/a/read/1795373431).
