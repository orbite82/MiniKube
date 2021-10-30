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
    🎉  Opening service default/hello-minikube in default browser...
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
   | dashboard                   | minikube | enabled ✅   | kubernetes            |
   | default-storageclass        | minikube | enabled ✅   | kubernetes            |
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
   | storage-provisioner         | minikube | enabled ✅   | kubernetes            |
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
  ┌─[orbite]@[Navita]:~/MiniKube/hello-k8s

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

* __Consuntando os nós__

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



