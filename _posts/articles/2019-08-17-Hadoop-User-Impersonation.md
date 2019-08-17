---
published: true
---
## Hadoop User Impersonation

Any software product comes with its applicative user. This user is the one that is owner for the product processes when in running state. 

In Hadoop ecosystem for instance, if you run a Hive service, which is a service that helps to do almost SQL and manage Relational Databases on top of Hadoop, the super user or applicative user is called hive by default. This user is the one that appear when you execute a command that looks if the service hive is running or just to check for hive service processes.

```
ps -ef  | grep hive  --color
```

Therefore even though you created users that could connect to Hive and create tables and Databases, the user that does all the job is the applicative user _hive_.   For cluster administrators and security managers, that is a big problem.  Since we don't know who is doing what in the cluster. We only see a generic user doing everything.

Here come then the impersonation. It gives the possibility to a super user to run jobs on behalf of a nominative users or other users. The super user will run the job, but with the credential of another user. Now we know who is doing what.

**But How to implement it?**

We need to configure the core-site.xml file by adding proxyuser (the user that can imitate other user, the super user) like below:

```
<property>
   <name>hadoop.proxyuser.hive.users</name>
   <value>user_1,user_2</value>
</property>
```

or by groups

```
<property>
   <name>hadoop.proxyuser.hive.groups</name>
   <value>group_1,group_2</value>
</property>
```
we can also limit the host from which this imitation game (the impersonation) is done.

```
<property>
   <name>hadoop.proxyuser.hive.hosts</name>
   <value>host_1,host_2</value>
</property>
```
