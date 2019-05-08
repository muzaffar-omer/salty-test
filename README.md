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
root@70063dfb2997:/# salt '*' test.ping
17a180641ffc:
    True
82c048bd821d:
    True
3478130f3a2b:
    True
```

