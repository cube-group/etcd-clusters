FROM alpine:3.8
#10m maximum client request size in bytes the server will accept.
#ENV MAX_REQUEST_BYTES '10485760'
#8G raise alarms when backend size exceeds the given quota (0 defaults to low space quota).
#ENV QUOTA_BACKEND_BYTES '8589934592'

ADD etcd-v2.3.8-linux-amd64.tar.gz /coreos/
RUN ls -al /coreos/ && \
    echo "https://mirrors.aliyun.com/alpine/v3.8/main/" > /etc/apk/repositories && \
    echo "https://mirrors.aliyun.com/alpine/v3.8/community/" >> /etc/apk/repositories && \
    apk update && \
    apk add --no-cache --virtual .build-deps tzdata bash curl && \
    /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo 'Asia/Shanghai' > /etc/timezone  && \
    cp /coreos/etcd-v2.3.8-linux-amd64/etcd /usr/local/bin/ && \
    cp /coreos/etcd-v2.3.8-linux-amd64/etcdctl /usr/local/bin/ && \
    mkdir -p /data

# Alpine Linux doesn't use pam, which means that there is no /etc/nsswitch.conf,
# but Golang relies on /etc/nsswitch.conf to check the order of DNS resolving
# (see https://github.com/golang/go/commit/9dee7771f561cf6aee081c0af6658cc81fac3918)
# To fix this we just create /etc/nsswitch.conf and add the following line:
RUN echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf

EXPOSE 2379 2380

# Define default command.
ENTRYPOINT ["/usr/local/bin/etcd","--data-dir","/data"]

#集群demo
#--name node1 --initial-cluster-token etcdv3-cluster --advertise-client-urls http://172.17.0.200:2371 --initial-advertise-peer-urls http://172.17.0.200:2381 --listen-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-cluster node1=http://172.17.0.200:2381,node2=http://172.17.0.200:2382,node3=http://172.17.0.200:2383 --initial-cluster-state new
#--name node2 --initial-cluster-token etcdv3-cluster --advertise-client-urls http://172.17.0.200:2372 --initial-advertise-peer-urls http://172.17.0.200:2382 --listen-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-cluster node1=http://172.17.0.200:2381,node2=http://172.17.0.200:2382,node3=http://172.17.0.200:2383 --initial-cluster-state new
#--name node3 --initial-cluster-token etcdv3-cluster --advertise-client-urls http://172.17.0.200:2373 --initial-advertise-peer-urls http://172.17.0.200:2383 --listen-client-urls http://0.0.0.0:2379 --listen-peer-urls http://0.0.0.0:2380 --initial-cluster node1=http://172.17.0.200:2381,node2=http://172.17.0.200:2382,node3=http://172.17.0.200:2383 --initial-cluster-state new
