# etcd-clusters
etcd集群搭建
### etcd v3(推荐)
构建
```
cd v3
docker build -t etcdv3 .
```
运行
```
#node1
docker run -d -it \
-p 2371:2379 \
-p 2381:2380 \
-v /data/etcdv3/node1:/data \
--name node1 \
etcdv3 \
--name node1 --initial-cluster-token etcdv3-cluster --advertise-client-urls http://127.0.0.1:2371 --initial-advertise-peer-urls http://127.0.0.1:2381 --listen-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-cluster node1=http://127.0.0.1:2381,node2=http://127.0.0.1:2382,node3=http://127.0.0.1:2383 --initial-cluster-state new

#node2
docker run -d -it \
-p 2372:2379 \
-p 2382:2380 \
-v /data/etcdv3/node2:/data \
--name node2 \
etcdv3 \
--name node2 --initial-cluster-token etcdv3-cluster --advertise-client-urls http://127.0.0.1:2372 --initial-advertise-peer-urls http://127.0.0.1:2382 --listen-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-cluster node1=http://127.0.0.1:2381,node2=http://127.0.0.1:2382,node3=http://127.0.0.1:2383 --initial-cluster-state new

#node3
docker run -d -it \
-p 2373:2379 \
-p 2383:2380 \
-v /data/etcdv3/node3:/data \
--name node3 \
etcdv3 \
--name node3 --initial-cluster-token etcdv3-cluster --advertise-client-urls http://127.0.0.1:2373 --initial-advertise-peer-urls http://127.0.0.1:2383 --listen-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-cluster node1=http://127.0.0.1:2381,node2=http://127.0.0.1:2382,node3=http://127.0.0.1:2383 --initial-cluster-state new
```
### etcd v2(不推荐)
构建
```
cd v2
docker build -t etcdv2 .
```
运行
```
#node1
docker run -d -it \
-p 2371:2379 \
-p 2381:2380 \
-v /data/etcdv3/node1:/data \
--name node1 \
etcdv2 \
--name node1 --initial-cluster-token etcdv3-cluster --advertise-client-urls http://127.0.0.1:2371 --initial-advertise-peer-urls http://127.0.0.1:2381 --listen-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-cluster node1=http://127.0.0.1:2381,node2=http://127.0.0.1:2382,node3=http://127.0.0.1:2383 --initial-cluster-state new

#node2
docker run -d -it \
-p 2372:2379 \
-p 2382:2380 \
-v /data/etcdv3/node2:/data \
--name node2 \
etcdv2 \
--name node2 --initial-cluster-token etcdv3-cluster --advertise-client-urls http://127.0.0.1:2372 --initial-advertise-peer-urls http://127.0.0.1:2382 --listen-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-cluster node1=http://127.0.0.1:2381,node2=http://127.0.0.1:2382,node3=http://127.0.0.1:2383 --initial-cluster-state new

#node3
docker run -d -it \
-p 2373:2379 \
-p 2383:2380 \
-v /data/etcdv3/node3:/data \
--name node3 \
etcdv2 \
--name node3 --initial-cluster-token etcdv3-cluster --advertise-client-urls http://127.0.0.1:2373 --initial-advertise-peer-urls http://127.0.0.1:2383 --listen-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-cluster node1=http://127.0.0.1:2381,node2=http://127.0.0.1:2382,node3=http://127.0.0.1:2383 --initial-cluster-state new
```