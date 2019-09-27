# cfssl
cfssl创建证书
稍微改改就可以用了
```bash
cfssl gencert -initca ca-csr.json | cfssljson -bare ca  
cfssl gencert -ca ca.pem -ca-key ca-key.pem -config ca-config.json -profile server server-csr.json | cfssljson -bare server
cfssl gencert -ca ca.pem -ca-key ca-key.pem -config ca-config.json -profile client client-csr.json | cfssljson -bare client
cfssl gencert -ca ca.pem -ca-key ca-key.pem -config ca-config.json -profile peer peer-csr.json | cfssljson -bare peer
```

#附上ETCD的一些启动，方便快速创建集群

```bash
etcd --name infra0 --initial-advertise-peer-urls https://172.17.0.2:2380 \
  --listen-peer-urls https://172.17.0.2:2380 \
  --listen-client-urls https://172.17.0.2:2379,https://127.0.0.1:2379 \
  --advertise-client-urls https://172.17.0.2:2379 \
  --initial-cluster-token etcd-cluster-1 \
  --initial-cluster infra0=https://172.17.0.2:2380,infra1=https://172.17.0.3:2380,infra2=https://172.17.0.4:2380 \
  --initial-cluster-state new \
  --client-cert-auth --trusted-ca-file=/aaa/xxx/ca.pem \
  --cert-file=/aaa/xxx/server.pem --key-file=/aaa/xxx/server-key.pem \
  --peer-client-cert-auth --peer-trusted-ca-file=/aaa/xxx/ca.pem \
  --peer-cert-file=/aaa/xxx/peer.pem --peer-key-file=/aaa/xxx/peer-key.pem
  
  
  
etcd --name infra1 --initial-advertise-peer-urls https://172.17.0.3:2380 \
  --listen-peer-urls https://172.17.0.3:2380 \
  --listen-client-urls https://172.17.0.3:2379,https://127.0.0.1:2379 \
  --advertise-client-urls https://172.17.0.3:2379 \
  --initial-cluster-token etcd-cluster-1 \
  --initial-cluster infra0=https://172.17.0.2:2380,infra1=https://172.17.0.3:2380,infra2=https://172.17.0.4:2380 \
  --initial-cluster-state new \
  --client-cert-auth --trusted-ca-file=/aaa/xxx/ca.pem \
  --cert-file=/aaa/xxx/server.pem --key-file=/aaa/xxx/server-key.pem \
  --peer-client-cert-auth --peer-trusted-ca-file=/aaa/xxx/ca.pem \
  --peer-cert-file=/aaa/xxx/peer.pem --peer-key-file=/aaa/xxx/peer-key.pem
  
  
etcd --name infra2 --initial-advertise-peer-urls https://172.17.0.4:2380 \
  --listen-peer-urls https://172.17.0.4:2380 \
  --listen-client-urls https://172.17.0.4:2379,https://127.0.0.1:2379 \
  --advertise-client-urls https://172.17.0.4:2379 \
  --initial-cluster-token etcd-cluster-1 \
  --initial-cluster infra0=https://172.17.0.2:2380,infra1=https://172.17.0.3:2380,infra2=https://172.17.0.4:2380 \
  --initial-cluster-state new \
  --client-cert-auth --trusted-ca-file=/aaa/xxx/ca.pem \
  --cert-file=/aaa/xxx/server.pem --key-file=/aaa/xxx/server-key.pem \
  --peer-client-cert-auth --peer-trusted-ca-file=/aaa/xxx/ca.pem \
  --peer-cert-file=/aaa/xxx/peer.pem --peer-key-file=/aaa/xxx/peer-key.pem
```
