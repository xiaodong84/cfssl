# cfssl
cfssl创建证书
稍微改改就可以用了
```bash
cfssl gencert -initca ca-csr.json | cfssljson -bare ca  
cfssl gencert -ca ca.pem -ca-key ca-key.pem -config ca-config.json -profile server server-csr.json | cfssljson -bare server
cfssl gencert -ca ca.pem -ca-key ca-key.pem -config ca-config.json -profile client client-csr.json | cfssljson -bare client
cfssl gencert -ca ca.pem -ca-key ca-key.pem -config ca-config.json -profile peer peer-csr.json | cfssljson -bare peer
```
