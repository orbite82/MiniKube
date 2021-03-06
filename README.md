<div align="center">
<img src="https://user-images.githubusercontent.com/47891196/139104117-aa9c2943-37da-4534-a584-e4e5ff5bf69a.png" width="350px" />
</div>

# MiniKube
Estudos com MiniKube

* __Install MiniKube on Linux:__ 

  * Link de referencia Instalando MineKube:

   * [link](https://minikube.sigs.k8s.io/docs/start/)

* __Install__

 ```
  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
  sudo dpkg -i minikube_latest_amd64.deb

 ```

* __Init Cluster__ 

 ```
  minikube start

 ```
* __Interact with your Cluster__

 ```
    kubectl get po -A
    NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
    kube-system   coredns-78fcd69978-6476f           1/1     Running   0          18s
    kube-system   etcd-minikube                      1/1     Running   0          31s
    kube-system   kube-apiserver-minikube            1/1     Running   0          31s
    kube-system   kube-controller-manager-minikube   1/1     Running   0          31s
    kube-system   kube-proxy-ztbnh                   1/1     Running   0          18s
    kube-system   kube-scheduler-minikube            1/1     Running   0          31s
    kube-system   storage-provisioner                1/1     Running   0          30s

 ```
 ```
    minikube kubectl -- get po -A
        > kubectl.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
        > kubectl: 44.73 MiB / 44.73 MiB [-------------] 100.00% 11.74 MiB p/s 4.0s
    NAMESPACE     NAME                               READY   STATUS    RESTARTS      AGE
    kube-system   coredns-78fcd69978-6476f           1/1     Running   0             111s
    kube-system   etcd-minikube                      1/1     Running   0             2m4s
    kube-system   kube-apiserver-minikube            1/1     Running   0             2m4s
    kube-system   kube-controller-manager-minikube   1/1     Running   0             2m4s
    kube-system   kube-proxy-ztbnh                   1/1     Running   0             111s
    kube-system   kube-scheduler-minikube            1/1     Running   0             2m4s
    kube-system   storage-provisioner                1/1     Running   1 (80s ago)   2m3s

 ```

* __Create Alias MiniKube__

 * [link](https://minikube.sigs.k8s.io/docs/start/)

 ```
  alias kubectl="minikube kubectl --"

 ```
 ```
  minikube dashboard

 ```
* __Deploy applications__

 ```
  kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4
  kubectl expose deployment hello-minikube --type=NodePort --port=8080

 ```
 ```
    kubectl get pod
    NAME                              READY   STATUS    RESTARTS   AGE
    hello-minikube-6ddfcc9757-sglbz   1/1     Running   0          23s

    kubectl get deployments
    NAME             READY   UP-TO-DATE   AVAILABLE   AGE
    hello-minikube   1/1     1            1           58s

    kubectl get services
    NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
    hello-minikube   NodePort    10.107.77.39   <none>        8080:32159/TCP   72s
    kubernetes       ClusterIP   10.96.0.1      <none>        443/TCP          7m47s

    kubectl get namespaces
    NAME                   STATUS   AGE
    default                Active   8m6s
    kube-node-lease        Active   8m7s
    kube-public            Active   8m7s
    kube-system            Active   8m7s
    kubernetes-dashboard   Active   3m18s
 ```

 ```
  kubectl get services hello-minikube
  NAME             TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
  hello-minikube   NodePort   10.107.77.39   <none>        8080:32159/TCP   2m4s
 ```
 ```
    minikube service hello-minikube
    |-----------|----------------|-------------|---------------------------|
    | NAMESPACE |      NAME      | TARGET PORT |            URL            |
    |-----------|----------------|-------------|---------------------------|
    | default   | hello-minikube |        8080 | http://192.168.49.2:32159 |
    |-----------|----------------|-------------|---------------------------|
    ????  Opening service default/hello-minikube in default browser...
 ```
* __Teste APP__

 http://localhost:7080/

* __LoadBalancer deployments__

 ```
  kubectl create deployment balanced --image=k8s.gcr.io/echoserver:1.4
  deployment.apps/balanced created

  kubectl expose deployment balanced --type=LoadBalancer --port=8080
  service/balanced exposed

 ```
 ```
   minikube addons list
   |-----------------------------|----------|--------------|-----------------------|
   |         ADDON NAME          | PROFILE  |    STATUS    |      MAINTAINER       |
   |-----------------------------|----------|--------------|-----------------------|
   | ambassador                  | minikube | disabled     | unknown (third-party) |
   | auto-pause                  | minikube | disabled     | google                |
   | csi-hostpath-driver         | minikube | disabled     | kubernetes            |
   | dashboard                   | minikube | enabled ???   | kubernetes            |
   | default-storageclass        | minikube | enabled ???   | kubernetes            |
   | efk                         | minikube | disabled     | unknown (third-party) |
   | freshpod                    | minikube | disabled     | google                |
   | gcp-auth                    | minikube | disabled     | google                |
   | gvisor                      | minikube | disabled     | google                |
   | helm-tiller                 | minikube | disabled     | unknown (third-party) |
   | ingress                     | minikube | disabled     | unknown (third-party) |
   | ingress-dns                 | minikube | disabled     | unknown (third-party) |
   | istio                       | minikube | disabled     | unknown (third-party) |
   | istio-provisioner           | minikube | disabled     | unknown (third-party) |
   | kubevirt                    | minikube | disabled     | unknown (third-party) |
   | logviewer                   | minikube | disabled     | google                |
   | metallb                     | minikube | disabled     | unknown (third-party) |
   | metrics-server              | minikube | disabled     | kubernetes            |
   | nvidia-driver-installer     | minikube | disabled     | google                |
   | nvidia-gpu-device-plugin    | minikube | disabled     | unknown (third-party) |
   | olm                         | minikube | disabled     | unknown (third-party) |
   | pod-security-policy         | minikube | disabled     | unknown (third-party) |
   | portainer                   | minikube | disabled     | portainer.io          |
   | registry                    | minikube | disabled     | google                |
   | registry-aliases            | minikube | disabled     | unknown (third-party) |
   | registry-creds              | minikube | disabled     | unknown (third-party) |
   | storage-provisioner         | minikube | enabled ???   | kubernetes            |
   | storage-provisioner-gluster | minikube | disabled     | unknown (third-party) |
   | volumesnapshots             | minikube | disabled     | kubernetes            |
   |-----------------------------|----------|--------------|-----------------------|


 ```

* __Create pod Demo Old__

 ```
  kubectl run demo --image=orbite82/myhello-v1 --port=9999 --labels app=demo
  kubectl port-forward  pod/demo 9999:8888
  http://localhost:9999/

 ```
 ```
   kubectl get pods
   NAME                              READY   STATUS    RESTARTS      AGE
   balanced-5744b548b4-lrt5x         1/1     Running   1 (41h ago)   42h
   demo                              1/1     Running   0             95s
   hello-minikube-6ddfcc9757-sglbz   1/1     Running   1 (41h ago)   43h
 ```  
 ```
   kubectl get pods --selector app=demo

 ```
 ```
   kubectl  get deployments
   NAME             READY   UP-TO-DATE   AVAILABLE   AGE
   balanced         1/1     1            1           42h
   hello-minikube   1/1     1            1           43h

 ```
* __Create pod Demo New__ 

 ```
  kubectl run demo --image=orbite82/myhello-v1 --port=9999 --labels app=demo
  kubectl port-forward  pod/demo 9999:8888
  http://localhost:9999/

 ```
 ```
  kubectl get pods
  NAME                              READY   STATUS    RESTARTS        AGE
  balanced-5744b548b4-lrt5x         1/1     Running   2 (3h18m ago)   45h
  demo                              1/1     Running   0               39s
  hello-minikube-6ddfcc9757-sglbz   1/1     Running   2 (3h18m ago)   47h
 ``` 
 ```
   kubectl get pods --selector app=demo
 ```
 ```
  kubectl port-forward pod/demo 9999:8888
  Forwarding from 127.0.0.1:9999 -> 8888
  Forwarding from [::1]:9999 -> 8888
  http://localhost:9999
 ```
 ```
  kubectl get pods --selector app=demo
  NAME   READY   STATUS    RESTARTS   AGE
  demo   1/1     Running   0          3m55s
 ```
 ```
  kubectl delete pods --selector app=demo
  pod "demo" deleted
  pod "demo-c77cc8d6f-rltpx" deleted
 ```
 ```
  kubectl get pods --selector app=demo
  NAME                   READY   STATUS    RESTARTS   AGE
  demo-c77cc8d6f-454h9   1/1     Running   0          5s
 ```
 ```
  kubectl delete all --selector app=demo
  pod "demo-c77cc8d6f-454h9" deleted
  deployment.apps "demo" deleted
  replicaset.apps "demo-c77cc8d6f" deleted
 ```

 * __Usando Apply New__
 ```
  ~/MiniKube/hello-k8s
  kubectl apply -f k8s/deployment.yaml
  deployment.apps/demo created

  kubectl get pods --selector app=demo
  NAME                   READY   STATUS    RESTARTS   AGE
  demo-c77cc8d6f-ckgp4   1/1     Running   0          31s
  [orbite]~/MiniKube/hello-k8s

 ```

* __Usando Apply old__

 ```
   ~/MiniKube/hello-k8s
   $ kubectl apply -f deployment.yaml 
   deployment.apps/demo created

   kubectl get pods --selector app=demo
   NAME                   READY   STATUS    RESTARTS   AGE
   demo-c77cc8d6f-jk2tv   1/1     Running   0          81s
 ```
* __Usando Service New__

 ```
  kubectl apply -f k8s/service.yaml 
  service/demo created 

  kubectl port-forward service/demo 9999:8888
  Forwarding from 127.0.0.1:9999 -> 8888
  Forwarding from [::1]:9999 -> 8888

  kubectl delete -f k8s/
  deployment.apps "demo" deleted
  service "demo" deleted
 ```

* __Usando Service Old__

 ```
   ~/MiniKube/hello-k8s
   $ kubectl apply -f service.yaml 
   service/demo created

   kubectl port-forward service/demo 9999:8888
   Forwarding from 127.0.0.1:9999 -> 8888
   Forwarding from [::1]:9999 -> 8888

   http://localhost:9999

 ```
* __Deletando o pod demo__

 ```
   kubectl delete pods --selector app=demo
   pod "demo-c77cc8d6f-k572h" deleted
 ```
 ```
   ~/MiniKube/hello-k8s
   $ kubectl delete -f deployment.yaml 
   deployment.apps "demo" deleted
 ```

* __Consuntando os n??s__

 ```
   kubectl get nodes
   NAME       STATUS   ROLES                  AGE   VERSION
   minikube   Ready    control-plane,master   46h   v1.22.2
 ``` 
* __Consultando todos recursos__

 ```
   kubectl get all
   NAME                                  READY   STATUS    RESTARTS       AGE
   pod/balanced-5744b548b4-lrt5x         1/1     Running   2 (154m ago)   45h
   pod/hello-minikube-6ddfcc9757-sglbz   1/1     Running   2 (154m ago)   46h

   NAME                     TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
   service/balanced         LoadBalancer   10.111.100.11   <pending>     8080:31044/TCP   45h
   service/demo             ClusterIP      10.100.92.83    <none>        8888/TCP         9m20s
   service/hello-minikube   NodePort       10.107.77.39    <none>        8080:32159/TCP   46h
   service/kubernetes       ClusterIP      10.96.0.1       <none>        443/TCP          46h

   NAME                             READY   UP-TO-DATE   AVAILABLE   AGE
   deployment.apps/balanced         1/1     1            1           45h
   deployment.apps/hello-minikube   1/1     1            1           46h

   NAME                                        DESIRED   CURRENT   READY   AGE
   replicaset.apps/balanced-5744b548b4         1         1         1       45h
   replicaset.apps/hello-minikube-6ddfcc9757   1         1         1       46h

 ```
---

* __Install Helm__ 

[Link Reference](https://helm.sh/docs/intro/)

[Helm](https://helm.sh/docs/intro/install/)

 ```
  curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
  chmod 700 get_helm.sh
  ./get_helm.sh 
  helm version
 ```
 ou

 ```
   curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
   sudo apt-get install apt-transport-https --yes
   echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
   sudo apt-get update
   sudo apt-get install helm
 ```
 ```
  kubectl delete all --selector app=demo
  service "demo" deleted
 ```
* __Install Helm chart__

 ```
  ~/MiniKube/hello-helm3

  helm install demo ./k8s/demo
  NAME: demo
  LAST DEPLOYED: Fri Oct  8 16:21:33 2021
  NAMESPACE: default
  STATUS: deployed
  REVISION: 1
  TEST SUITE: None

 ```
 ```
  kubectl get pods
  NAME                              READY   STATUS    RESTARTS        AGE
  balanced-5744b548b4-lrt5x         1/1     Running   2 (4h48m ago)   47h
  demo-5bf7bc95c7-b4s2s             1/1     Running   0               86s
  hello-minikube-6ddfcc9757-sglbz   1/1     Running   2 (4h48m ago)   2d
 ```

* __Listando releases do Helm__

 ```
  helm list
  NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
  demo    default         1               2021-10-08 16:21:33.32266034 -0300 -03  deployed        demo-1.0.1 
 ```

* __Listando o Status da release especifica__

 ```
  helm status demo
  NAME: demo
  LAST DEPLOYED: Fri Oct  8 16:21:33 2021
  NAMESPACE: default
  STATUS: deployed
  REVISION: 1
  TEST SUITE: None
 ```

* __Install GO__

[Ref Link Binario](https://golang.org/dl/)

[Ref Link Install](https://golang.org/doc/install)

```
sudo -i
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.17.2.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go version

```
* __grpc health probe__

[Ref Link](https://github.com/grpc-ecosystem/grpc-health-probe/blob/master/README.md)

[Ref Link 2](https://kubernetes.io/blog/2018/10/01/health-checking-grpc-servers-on-kubernetes/)

Obs: N??o testado ainda!

---
# hello-namespace

 * __NameSpace__

```
echo 'export PATH=$PATH:/snap/bin' >> ~/.bashrc
source ~/.bashrc
bash

```

```
kubectl apply -f hello-namespace/k8s/deployment.yaml

```

```
kubectl get deployments
NAME   READY   UP-TO-DATE   AVAILABLE   AGE
demo   1/1     1            1           2m52s

kubectl get deployments/demo
NAME   READY   UP-TO-DATE   AVAILABLE   AGE
demo   1/1     1            1           3m26s

kubectl get pods --selector app=demo
NAME                    READY   STATUS    RESTARTS   AGE
demo-6465d8f7c9-6pqd7   1/1     Running   0          4m32s

```

```
kubectl describe pod demo
Name:         demo-6465d8f7c9-6pqd7
Namespace:    default
Priority:     0
Node:         minikube/192.168.99.100
Start Time:   Sat, 30 Oct 2021 20:22:13 -0300
Labels:       app=demo
              pod-template-hash=6465d8f7c9
Annotations:  <none>
Status:       Running
IP:           172.17.0.5
IPs:
  IP:           172.17.0.5
Controlled By:  ReplicaSet/demo-6465d8f7c9
Containers:
  demo:
    Container ID:   docker://6d85102f8c68bb38ab9a0cfcaef245d173ef3105cbabaea2713b3e5dfb128ce2
    Image:          cloudnatived/demo:hello
    Image ID:       docker-pullable://cloudnatived/demo@sha256:bd04206ca8ab7025c465dc2b9d3282c2e0da216c71011d26d66ef51f5a5d3e34
    Port:           8888/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Sat, 30 Oct 2021 20:22:22 -0300
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:     250m
      memory:  20Mi
    Requests:
      cpu:        100m
      memory:     10Mi
    Liveness:     http-get http://:8888/ delay=3s timeout=1s period=3s #success=1 #failure=3
    Readiness:    http-get http://:8888/ delay=3s timeout=1s period=3s #success=1 #failure=3
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-fwfvv (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-fwfvv:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  5m51s  default-scheduler  Successfully assigned default/demo-6465d8f7c9-6pqd7 to minikube
  Normal  Pulling    5m47s  kubelet            Pulling image "cloudnatived/demo:hello"
  Normal  Pulled     5m42s  kubelet            Successfully pulled image "cloudnatived/demo:hello" in 4.199679829s
  Normal  Created    5m42s  kubelet            Created container demo
  Normal  Started    5m42s  kubelet            Started container demo

```
> **_Quota de recusos_** :
> Assim como podemos restringir o uso de CPU e de mem??ria em cont??ineres, podemos restringir o uso de recursos em um namespace com ResourceQuota no NameSpace!
```
~/MiniKube
?????????> $ cd hello-namespace

kubectl create namespace demo
namespace/demo created

~/MiniKube/hello-namespace
?????????> $ ls k8s/

~/MiniKube/hello-namespace
?????????> $ kubectl apply --namespace demo -f k8s/resourcequota.yaml 
resourcequota/demo-resourcequota created

```
* Verificar se o ResourceQuota esta ativo!

```
kubectl get resourcequotas -n demo
NAME                 AGE   REQUEST       LIMIT
demo-resourcequota   10m   pods: 0/100

```
---
# Verificando todos os namespaces

```
kubectl get deployment --all-namespaces
NAMESPACE              NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
default                demo                        1/1     1            1           22d
kube-system            coredns                     1/1     1            1           22d
kubernetes-dashboard   dashboard-metrics-scraper   1/1     1            1           22d
kubernetes-dashboard   kubernetes-dashboard        1/1     1            1           22d

```
---
# Verificando NameSpaces

```
kubectl get namespaces
NAME                   STATUS   AGE
default                Active   22d
demo                   Active   22d
kube-node-lease        Active   22d
kube-public            Active   22d
kube-system            Active   22d
kubernetes-dashboard   Active   22d

```
---
# Acessando Minikube e verificando ip

```
~/MiniKube$ minikube ip
192.168.99.200
~/MiniKube$ minikube ssh
                         _             _            
            _         _ ( )           ( )           
  ___ ___  (_)  ___  (_)| |/')  _   _ | |_      __  
/' _ ` _ `\| |/' _ `\| || , <  ( ) ( )| '_`\  /'__`\
| ( ) ( ) || || ( ) || || |\`\ | (_) || |_) )(  ___/
(_) (_) (_)(_)(_) (_)(_)(_) (_)`\___/'(_,__/'`\____)

$
```
---
# Start ou Delete Minikube 

> **_Start_** :

```
~/MiniKube$ minikube start
????  minikube v1.23.2 on Linuxmint 20
????  minikube 1.24.0 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.24.0
????  To disable this notice, run: 'minikube config set WantUpdateNotification false'

???  Using the virtualbox driver based on existing profile
????  Starting control plane node minikube in cluster minikube
????  Restarting existing virtualbox VM for "minikube" ...
????  Preparing Kubernetes v1.22.2 on Docker 20.10.8 ...
    ??? Using image gcr.io/k8s-minikube/storage-provisioner:v5
????  Verifying Kubernetes components...
    ??? Using image kubernetesui/metrics-scraper:v1.0.7
    ??? Using image kubernetesui/dashboard:v2.3.1
????  Enabled addons: storage-provisioner, default-storageclass, dashboard
????  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

```
> **_Delete_** :

```
~/MiniKube$ minikube delete

```

> **_Stop_** :

```
~/MiniKube$ minikube stop
???  Stopping node "minikube"  ...
????  1 nodes stopped.

```
---

> **_Describe nodes_** :

```
kubectl describe nodes minikube

```
> **_Bash Completion_** :

```
sudo apt-get install -y bash-complation
sudo su
kubectl completion bash > /etc/bash_completion.d/kubectl
~/MiniKube$ source <(kubectl completion bash

~/MiniKube
?????????> $ kube
kubectl  kubectx  kubens

kubectl get pods -n kube-system
NAME                               READY   STATUS    RESTARTS      AGE
coredns-78fcd69978-dmv9f           1/1     Running   4 (36m ago)   22d
etcd-minikube                      1/1     Running   4 (36m ago)   22d
kube-apiserver-minikube            1/1     Running   4 (36m ago)   22d
kube-controller-manager-minikube   1/1     Running   4 (36m ago)   22d
kube-proxy-fvjl2                   1/1     Running   4 (36m ago)   22d
kube-scheduler-minikube            1/1     Running   4 (36m ago)   22d
storage-provisioner                1/1     Running   5 (36m ago)   22d

```

# Criar Meu Primeiro Pod e Name Space

> **_Primeiro Pod e Name Space_** :

```
kubectl create namespace orbite-namespace
namespace/orbite-namespace created

```

```
kubectl get namespaces
NAME                   STATUS   AGE
default                Active   26d
demo                   Active   26d
kube-node-lease        Active   26d
kube-public            Active   26d
kube-system            Active   26d
kubernetes-dashboard   Active   26d
orbite-namespace       Active   27s

```

```
kubectl run nginx --image=nginx
pod/nginx created

```

```
kubectl get pods
NAME                    READY   STATUS    RESTARTS        AGE
demo-6465d8f7c9-6pqd7   1/1     Running   5 (3d17h ago)   26d
nginx                   1/1     Running   0               39s

```

```
kubectl describe pods nginx
Name:         nginx
Namespace:    default
Priority:     0
Node:         minikube/192.168.99.100
Start Time:   Fri, 26 Nov 2021 12:03:26 -0300
Labels:       run=nginx
Annotations:  <none>
Status:       Running
IP:           172.17.0.6
IPs:
  IP:  172.17.0.6
Containers:
  nginx:
    Container ID:   docker://382e94f94156b715b2d02b18165eb6588bbe427a4b6392968bc1c112964ae631
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:097c3a0913d7e3a5b01b6c685a60c03632fc7a2b50bc8e35bcaa3691d788226e
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Fri, 26 Nov 2021 12:03:45 -0300
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-stqrp (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-stqrp:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m38s  default-scheduler  Successfully assigned default/nginx to minikube
  Normal  Pulling    2m37s  kubelet            Pulling image "nginx"
  Normal  Pulled     2m21s  kubelet            Successfully pulled image "nginx" in 16.339025088s
  Normal  Created    2m20s  kubelet            Created container nginx
  Normal  Started    2m20s  kubelet            Started container nginx

```

```
kubectl get pods nginx -o wide
NAME    READY   STATUS    RESTARTS   AGE   IP           NODE       NOMINATED NODE   READINESS GATES
nginx   1/1     Running   0          23m   172.17.0.6   minikube   <none>           <none>

```

# Ver em formato yaml como foi criado

> **_Ver o manifesto do pod em yaml_** :

```
kubectl get pods nginx -o yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2021-11-26T15:03:26Z"
  labels:
    run: nginx
  name: nginx
  namespace: default
  resourceVersion: "14347"
  uid: 5b7ea8ad-ea95-4f71-9caf-829548d25a47
spec:
  containers:
  - image: nginx
    imagePullPolicy: Always
    name: nginx
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-stqrp
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: minikube
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: kube-api-access-stqrp
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2021-11-26T15:03:26Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2021-11-26T15:03:45Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2021-11-26T15:03:45Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2021-11-26T15:03:26Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: docker://382e94f94156b715b2d02b18165eb6588bbe427a4b6392968bc1c112964ae631
    image: nginx:latest
    imageID: docker-pullable://nginx@sha256:097c3a0913d7e3a5b01b6c685a60c03632fc7a2b50bc8e35bcaa3691d788226e
    lastState: {}
    name: nginx
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2021-11-26T15:03:45Z"
  hostIP: 192.168.99.100
  phase: Running
  podIP: 172.17.0.6
  podIPs:
  - ip: 172.17.0.6
  qosClass: BestEffort
  startTime: "2021-11-26T15:03:26Z"

```

# Redirecionando e criando o pod

> **_Meu primeiro pod em yaml_** :

```
kubectl get pods nginx -o yaml > primeiro_pod_orbite.yaml

```

```
ls -lha
total 116K
drwxrwxr-x  8 orbite orbite 4,0K Nov 26 12:33 .
drwxr-xr-x 43 orbite orbite 4,0K Nov 26 11:57 ..
-rw-------  1 orbite orbite  348 Nov 22 14:12 2021-11-22-17-12-26.076-VBoxHeadless-3167.log
-rwx------  1 orbite orbite  11K Oct 30 19:38 get_helm.sh
drwxrwxr-x  8 orbite orbite 4,0K Nov 22 18:26 .git
drwxrwxr-x  2 orbite orbite 4,0K Oct 30 19:27 hello
drwxrwxr-x  3 orbite orbite 4,0K Oct 30 19:27 hello-helm3
drwxrwxr-x  3 orbite orbite 4,0K Oct 30 19:27 hello-k8s
drwxrwxr-x  2 orbite orbite 4,0K Oct 30 19:27 hello-k8s-old
drwx------  3 orbite orbite 4,0K Oct 28 22:31 hello-namespace
-rw-rw-r--  1 orbite orbite  35K Oct 30 19:27 LICENSE
-rw-rw-r--  1 orbite orbite 2,5K Nov 26 12:33 primeiro_pod_orbite.yaml
-rw-rw-r--  1 orbite orbite  27K Nov 26 12:32 README.md

```

```
kubectl get pods -n default
NAME                    READY   STATUS    RESTARTS        AGE
demo-6465d8f7c9-6pqd7   1/1     Running   5 (3d17h ago)   26d
nginx                   1/1     Running   0               43m

```

> **_namespace sem nada_** :

```
kubectl get pods -n orbite-namespace
No resources found in orbite-namespace namespace.

```
# Criando pod

> **_Criando o primeiro pod_** :

```
kubectl create -f primeiro_pod_orbite.yaml
pod/nginx created

```

> **_namespace com o pod_** :

```
kubectl get pods -n orbite-namespace
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          97s

```
# Deletando pod

> **_Deletando o pod_** :

```
kubectl delete -f primeiro_pod_orbite.yaml
pod "nginx" deleted

```

```
kubectl get pods
NAME                    READY   STATUS    RESTARTS        AGE
demo-6465d8f7c9-6pqd7   1/1     Running   5 (3d18h ago)   26d
nginx

```

```
kubectl delete pods nginx
pod "nginx" deleted

```
# Criando um template para seus yaml

> **_Template yaml apenas pra simular_** :

```
kubectl run nginx --image=nginx --dry-run=client
pod/nginx created (dry run)

```

> **_Template yaml para visualizar_** :

```
kubectl run nginx --image=nginx --dry-run=client -o yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

```

> **_Template yaml redirecionando e crian do o arquivo yaml_** :

```
kubectl run nginx --image=nginx --dry-run=client -o yaml > segundo_pod_orbite.yaml

```
# Criando 2 Pod

> **_Criando segundo pod_** :

```
kubectl create -f segundo_pod_orbite.yaml 
pod/nginx created

```

```
kubectl get pods
NAME                    READY   STATUS    RESTARTS        AGE
demo-6465d8f7c9-6pqd7   1/1     Running   5 (3d18h ago)   26d
nginx                   1/1     Running   0               62s

```

```
kubectl delete pods nginx
pod "nginx" deleted

```
> **_Alterar yaml add linhas com a porta_** :

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx  
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
    ports:              # add
    - containerPort: 80 # add
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

```

```
kubectl create -f segundo_pod_orbite.yaml 
pod/nginx created

```

```
kubectl get pods
NAME                    READY   STATUS    RESTARTS        AGE
demo-6465d8f7c9-6pqd7   1/1     Running   5 (3d18h ago)   26d
nginx                   1/1     Running   0               99s

```
> **_Describe com a porta_** :

```
kubectl describe pods nginx
Name:         nginx
Namespace:    default
Priority:     0
Node:         minikube/192.168.99.100
Start Time:   Fri, 26 Nov 2021 13:23:19 -0300
Labels:       run=nginx
Annotations:  <none>
Status:       Running
IP:           172.17.0.6
IPs:
  IP:  172.17.0.6
Containers:
  nginx:
    Container ID:   docker://68765f16eb745e0b96d69c5a577e55611392c585a8e2ddacd9affb2cac3612ac
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:097c3a0913d7e3a5b01b6c685a60c03632fc7a2b50bc8e35bcaa3691d788226e
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Fri, 26 Nov 2021 13:23:23 -0300
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-xx949 (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-xx949:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  2m30s  default-scheduler  Successfully assigned default/nginx to minikube
  Normal  Pulling    2m29s  kubelet            Pulling image "nginx"
  Normal  Pulled     2m27s  kubelet            Successfully pulled image "nginx" in 1.92246513s
  Normal  Created    2m27s  kubelet            Created container nginx
  Normal  Started    2m27s  kubelet            Started container nginx

```  

# Expose no pod nginx

> **_Expondo a porta do nginx_** :

```
kubectl expose pod nginx
service/nginx exposed

```

```
kubectl get service
NAME         TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1     <none>        443/TCP   26d
nginx        ClusterIP   10.99.99.30   <none>        80/TCP    37s

```
# Describe services nginx

> **_Describe no service do nginx_** :

```
kubectl describe services nginx
Name:              nginx
Namespace:         default
Labels:            run=nginx
Annotations:       <none>
Selector:          run=nginx
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.99.99.30
IPs:               10.99.99.30
Port:              <unset>  80/TCP
TargetPort:        80/TCP
Endpoints:         172.17.0.6:80
Session Affinity:  None
Events:            <none>

```
# Edit service nginx

> **_Editando o service do nginx para NodePort_**

```
# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: "2021-11-26T16:27:54Z"
  labels:
    run: nginx
  name: nginx
  namespace: default
  resourceVersion: "17916"
  uid: 5926689d-cd0f-4e7f-b834-64508137206a
spec:
  clusterIP: 10.99.99.30
  clusterIPs:
  - 10.99.99.30
  internalTrafficPolicy: Cluster
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  sessionAffinity: None
  type: ClusterIP  #edite aqui para NodePort

```

```
kubectl edit service nginx
service/nginx edited

```
```
kubectl get service
NAME         TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP   10.96.0.1     <none>        443/TCP        26d
nginx        NodePort    10.99.99.30   <none>        80:32371/TCP   12m

```
# Verificando o ip do minicube e acessando o nginx no browser

> **_Verificando ip minikube_**

```
minikube ip
192.168.99.100

```

> **_Testando com a porta alterado do NodePort no browser_**

http://192.168.99.100:32371

> **_Click abaixo_**

[nginx-browser-test](nginx-browser-test.png)

> **_Test via curl_**

```
curl 192.168.99.100:32371
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

```


