# Lab 0: Prerequisites for Oracle Cloud Labs

## Create a Private / Public Keys

To configure cloud services and to access them later you have to create a private / public key pair.

To create the keys [for Unix follow these instructions](https://docs.oracle.com/en/cloud/paas/database-dbaas-cloud/csdbi/generate-ssh-key-pair.html#GUID-2BD5B767-0659-4791-A170-279F469B2CC3), for Windows [follow the instructions here](https://docs.oracle.com/en/cloud/paas/database-dbaas-cloud/csdbi/create-ssh-tunnel.html#GUID-6929CE39-6CD7-46C9-8022-929A9844B1C5).

## Set Replication Policy

We will do this lab together. Without setting the replication policy you will have issues with Oracle PaaS services later. Always set this for a new idendity domain. To successfully work with the PaaS services it is less important how you set it, just that you set. (For legal and compliance reasons this is obviously different).

If you are working on your own, the details are described in my [blog post about geo replication](http://www.munzandmore.com/2017/ora/oracle-storage-geo-replication)


# Lab O1: Oracle ACCS

ACCS is short for application container cloud service. In this lab we will deploy a Java EE application to ACCS. Note, that you could also package a go, Spring Boot or Python application. ACCS provides the language runtime only and is therefore very flexible.

We will try one of the newest features, the deployment of a Java EE module. The steps to complete this lab are described here:

[ACCS with Java EE](https://github.com/oracle/weblogic-innovation-seminars/blob/caf-12.2.1/cloud.demos/jcs.basics/create.dbcs.ui.md).


# Lab O2: Oracle DB as a Service


## DB as Service in Oracle Cloud

Provision the database as described in [create DB as a Service](https://github.com/oracle/weblogic-innovation-seminars/blob/caf-12.2.1/cloud.demos/jcs.basics/create.dbcs.ui.md).

Note that there are some small changes in the UI compared to the instructions. The cloud is very dynamic and Oracle keeps improving it sometimes :-)

Provisioning the service will take about 20 minutes.

## Access your DB instance

Do this lab if you have an SQL client installed already or if you can install SQLcl which requires Java.
Basically there are several options to achieve this. We will use the easier one in this lab.

### SQLcl and Create SSL

The best option is [using an SSL Tunnel](http://barrymcgillin.blogspot.de/2015/05/sqlcl-cloud-connections-via-secure.html).

You are free to do this lab however you like. Another option that we don't follow in this lab is to use your [local SQL Developer](https://getpocket.com/a/read/1795373431), if you manage to do it. 

### Open DB Port Listen Port (Poor man Solution)

Yet another option is to open port 1521 to your DB as a service which is strongly discouraged. However then no SSL tunnel is needed.



