# ScyllaDB

## Scylla Cluster
ref: https://gist.github.com/tzach/66c8d0ce76ae50fd6ead36f263b5bedf
### Install
#### Build images and run compose, after check docker status
```
docker-compose up --build -d
docker-compose ps
```
#### Validate cluster is up and running
```
> docker-compose exec scylla00 nodetool status
Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address     Load       Tokens       Owns    Host ID                               Rack
UN  172.18.0.2  110.77 KB  256          ?       63ef531d-13a4-4ffa-9d28-3985aeb5dc18  rack1
UN  172.18.0.3  104.88 KB  256          ?       7e985ea1-66d8-4c47-a517-2ef22f70d29c  rack1
UN  172.18.0.4  110.58 KB  256          ?       c5c0bd6f-c7b4-4dee-8fe9-0ca495b02a2b  rack1
```
## Scylla Manager
ref: https://manager.docs.scylladb.com/stable/docker/index.html
### Scylla Backup
ref: https://manager.docs.scylladb.com/stable/backup/examples.html

ref: https://manager.docs.scylladb.com/stable/backup/setup-s3-compatible-storage.html

ref: https://manager.docs.scylladb.com/stable/backup/setup-aws-s3.html#aws-iam-policy

### Scylla Restore
ref: https://manager.docs.scylladb.com/stable/restore/index.html
### Run scylla manager
```
cd monitor/
docker-compose up -d
```
### Validate is up and running
```
docker-compose ps
```
### Add cluster scylla to manager
```
docker-compose exec scylla-manager sctool cluster add --name test --host=scylla00 --auth-token=token


defe1ffe-c992-4ca2-9fad-82a61f39ad9e
 __
/  \     Cluster added! You can set it as default, by exporting its name or ID as env variable:
@  @     $ export SCYLLA_MANAGER_CLUSTER=defe1ffe-c992-4ca2-9fad-82a61f39ad9e
|  |     $ export SCYLLA_MANAGER_CLUSTER=<name>
|| |/
|| ||    Now run:
|\_/|    $ sctool status -c defe1ffe-c992-4ca2-9fad-82a61f39ad9e
\___/    $ sctool task list -c defe1ffe-c992-4ca2-9fad-82a61f39ad9e
```
## Prometheus+Loki+Grafana
ref: https://monitoring.docs.scylladb.com/stable/install/docker_compose.html

#### Pre-config 
```
cd monitor/scylla-monitoring/prometheus/
vim scylla-server.yaml and add scylla nodes IPs
```
### Run compose and check
```
docker-compose up -d
docker-compose ps
```
### Check prometheus Targets and Grafana panel
```
Prometheus:
http://<your ip>:9090
Grafana:
http://<your IP>:3000
```

## Diagram
![Topology example](https://github.com/ivanrzk/ScyllaDB/blob/244135dd406bf40d96fe018c71e14ee7e342ab5e/ScyllaDB-MMS.JPG)



