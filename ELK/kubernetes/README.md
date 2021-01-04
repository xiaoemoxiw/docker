#### 官方指南
> 地址：https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-deploy-eck.html

#### 部署ECK环境
* 应用yaml文件
```shell script
kubectl apply -f https://download.elastic.co/downloads/eck/1.3.1/all-in-one.yaml
```

* 启动成功以后，监控日志信息
```shell script
kubectl -n elastic-system logs -f statefulset.apps/elastic-operator
```

#### 操作集群
```shell script
]# kubectl get sts -n elastic-system
NAME               READY   AGE
elastic-operator   1/1     9m16s
```

#### 部署elasticsearch集群
```shell script
cat <<EOF | kubectl apply -f -
apiVersion: elasticsearch.k8s.elastic.co/v1
kind: Elasticsearch
metadata:
  name: quickstart
spec:
  version: 7.10.1
  nodeSets:
  - name: default
    count: 1
    config:
      node.store.allow_mmap: false
EOF
```

