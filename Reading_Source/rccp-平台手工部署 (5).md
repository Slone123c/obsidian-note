# 刷机部署

## 1. 虚拟机/服务器刷机

## 2. TUI设置管理节点与计算节点网络

## 3. 添加节点

在主节点上执行以下 restful请求

```shell
curl --location --request POST '172.28.110.40:5000/restful' \
--header 'Content-Type: application/json' \
--data '{
    "method": "post",
    "commsg": "True",
    "cert_reqs": "True",
    "url": "https://<集群的vip地址>:9002/v1/nodes",
    "content": {
        "id": "<添加节点的主机名>",
        "ip": "<添加节点的管理网IP>",
        "role": "<添加节点的角色 MANAGER 管理节点，WORKER 节点 >" 
    }
}'
```

## 4. 部署数据集群

在主节点上执行以下shell命令

```shell
 ./rccpctrl deploy database --all
```

# 手动部署

## 1. 设置主机名（可选）

虚拟机环境下，如果主机名称一致请修改主机名称并重启机器

```shell
uuidgen > /etc/hostname
```

## 2. 配置平台ID

配置 `/etc/rcos_global/platform_id` 文件，**所有节点**执行以下命令

```shell
echo '{"platform_id": "3d28815f-b6a6-44e1-92bf-d796858cc3ea", "managed": false}' > platform_id
```

## 3. 配置VIP信息

配置 vip 文件，**所有节点**执行以下命令（vip信息参考第一个节点的同名文件）

```shell
cat << EOF > /etc/rcos_global/server_net.conf
[management]
management_uplink = bond0  
management_nic = rcosmgmt 
virtual_ip = < vip 地址 >
vip_netmask = < vip 地址掩码 >
vip_gateway = < vip dizhi 网关>
EOF

cat << EOF > /etc/rcos_global/server_net.conf
[management]
management_uplink = bond0  
management_nic = rcosmgmt 
virtual_ip = < 172.28.112.17 >
vip_netmask = < 255.255.255.0 >
vip_gateway = < 172.28.112.14 >
EOF
```

## 4. 部署基础应用

执行以下命令（**只需要在主节点执行**）：

```shell
kubectl apply -f - <<EOF
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  annotations:
    storageclass.beta.kubernetes.io/is-default-class: "true"
  labels:
  name: local
provisioner: rancher.io/local-path
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
EOF

cd /etc/product/rcos/global/component/docker/charts/

helm  upgrade  --install ntp          ntp.tgz          -n rccp --create-namespace
helm  upgrade  --install rabbitmq     rabbitmq.tgz     -n rccp --create-namespace
helm  upgrade  --install rccpshennong rccpshennong.tgz -n rccp --create-namespace --set persistence.storageClassName=local
helm  upgrade  --install rccptaiyi    rccptaiyi.tgz    -n rccp --create-namespace --set persistence.storageClassName=local
helm  upgrade  --install rccpcangjie /etc/product/rcos/global/component/docker/charts/rccpcangjie.tgz -n rccp --create-namespace
```

## 5. 添加节点

在主节点上执行以下 restful请求

```shell
curl --location --request POST '172.28.110.40:5000/restful' \
--header 'Content-Type: application/json' \
--data '{
    "method": "post",
    "commsg": "True",
    "cert_reqs": "True",
    "url": "https://<集群的vip地址>:9002/v1/nodes",
    "content": {
        "id": "<添加节点的主机名>",
        "ip": "<添加节点的管理网IP>",
        "role": "<添加节点的角色 MANAGER 管理节点，WORKER 节点 >" 
    }
}'
```


## 6. 部署数据集群

数据库集群每个节点需要部署一个实例，在需要部署数据库的节点执行以下命令

```shell
helm  upgrade --install rccpdatabase-$HOSTNAME /etc/product/rcos/global/component/docker/charts/rccpdatabase.tgz -n rccp --create-namespace --set patroni.statefulsetId=$HOSTNAME
```





```shell
Name:               rccpdatabase-0d0a4577-7342-5bb0-b785-e50b1c81173a
Namespace:          rccp
CreationTimestamp:  Wed, 26 Oct 2022 14:05:59 +0800
Selector:           application=patroni,cluster-name=rccpdatabase,statefulset-id=rccpdatabase-0d0a4577-7342-5bb0-b785-e50b1c81173a
Labels:             app.kubernetes.io/managed-by=Helm
                    application=patroni
                    cluster-name=rccpdatabase
                    statefulset-id=rccpdatabase-0d0a4577-7342-5bb0-b785-e50b1c81173a
Annotations:        meta.helm.sh/release-name: rccpdatabase-0d0a4577-7342-5bb0-b785-e50b1c81173a
                    meta.helm.sh/release-namespace: rccp
Replicas:           1 desired | 1 total
Update Strategy:    RollingUpdate
  Partition:        0
Pods Status:        1 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:           application=patroni
                    cluster-name=rccpdatabase
                    statefulset-id=rccpdatabase-0d0a4577-7342-5bb0-b785-e50b1c81173a
  Service Account:  rccpdatabase-serviceaccount
  Containers:
   postgres:
    Image:       rcos-dockerimage_pgsql-patroni:v11.0.1
    Ports:       8008/TCP, 5432/TCP
    Host Ports:  0/TCP, 0/TCP
    Readiness:   http-get http://:8008/readiness delay=3s timeout=5s period=10s #success=1 #failure=3
    Environment:
      PATRONI_KUBERNETES_POD_IP:               (v1:status.podIP)
      PATRONI_KUBERNETES_NAMESPACE:            (v1:metadata.namespace)
      PATRONI_KUBERNETES_BYPASS_API_SERVICE:  true
      PATRONI_KUBERNETES_USE_ENDPOINTS:       true
      PATRONI_KUBERNETES_LABELS:              {application: patroni, cluster-name: rccpdatabase}
      PATRONI_SUPERUSER_USERNAME:             postgres
      PATRONI_SUPERUSER_PASSWORD:             pgsqlPASSWORD0
      PATRONI_REPLICATION_USERNAME:           standby
      PATRONI_REPLICATION_PASSWORD:           pgsqlPASSWORD0
      PATRONI_SCOPE:                          rccpdatabase
      PATRONI_NAME:                            (v1:metadata.name)
      PATRONI_POSTGRESQL_DATA_DIR:            /home/postgres/pgdata/pgroot/data
      PATRONI_POSTGRESQL_PGPASS:              /tmp/pgpass
      PATRONI_POSTGRESQL_LISTEN:              0.0.0.0:5432
      PATRONI_RESTAPI_LISTEN:                 0.0.0.0:8008
      PATRONI_SYNCHRONOUS_NODE_COUNT:         1
      PATRONI_SYNCHRONOUS_MODE:               false
      PATRONI_SYNCHRONOUS_MODE_STRICT:        false
    Mounts:
      /home/postgres/pgdata from pgdata (rw)
  Volumes:  <none>
Volume Claims:
  Name:          pgdata
  StorageClass:  postgres
  Labels:        application=patroni
                 statefulset-id=rccpdatabase-0d0a4577-7342-5bb0-b785-e50b1c81173a
  Annotations:   <none>
  Capacity:      500Gi
  Access Modes:  [ReadWriteOnce]
Events:
  Type    Reason            Age                    From                    Message
  ----    ------            ----                   ----                    -------
  Normal  SuccessfulCreate  7m45s (x2 over 8m30s)  statefulset-controller  create Pod rccpdatabase-0d0a4577-7342-5bb0-b785-e50b1c81173a-0 in StatefulSet rccpdatabase-0d0a4577-7342-5bb0-b785-e50b1c81173a successful
  
netstat -lntp

```

