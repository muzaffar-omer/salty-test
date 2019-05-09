# SaltStack Test Cluster

SaltStack cluster with single ubuntu master connected to multiple ubuntu minions. It should be for testing/learning SaltStack only.

## Setup

Clone the repository using `git clone` and run`docker-compose` inside the cloned repository to start up the environment as below

```Bash
docker-compose up -d

Creating minion3 ... done
Creating master  ... done
Creating minion1 ... done
Creating minion2 ... done
```

This should start up the cluster and to verify the status of the cluster containers use the below command

```bash
docker-compose ps                                                                                                                                               Name                Command              State                       Ports
------------------------------------------------------------------------------------------------
master    /usr/bin/salt-master -l debug   Up      0.0.0.0:4505->4505/tcp, 0.0.0.0:4506->4506/tcp
minion1   /usr/bin/salt-minion -l debug   Up
minion2   /usr/bin/salt-minion -l debug   Up
minion3   /usr/bin/salt-minion -l debug   Up
```

To verify that Salt is working properly, connect to the master container and run `test.ping` Salt command

```bash
docker exec -it master /bin/bash
salt '*' test.ping
```

Output of the above command should be similar to the below

```bash
root@master:/# salt '*' test.ping
minion1:
    True
minion2:
    True
minion3:
    True
master:
    True
root@master:/#
```



## References

* Salt Installation in Ubuntu : https://docs.saltstack.com/en/latest/topics/installation/ubuntu.html#ubuntu 

* Running Salt https://docs.saltstack.com/en/latest/ref/configuration/index.html#running-salt

* Configuring master node hostname in minion https://docs.saltstack.com/en/latest/ref/configuration/minion.html#master

  