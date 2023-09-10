# k8s-argocd
Kubernetes と ArgoCdの連携
→ ★★上手くいった

## 参考にしたサイト
- 以下のサイトの内容を検証
    https://selfnote.work/20220703/programming/kubernetes-microservices-volumes-2/
- Udemyの講座より参考
    https://github.com/nakamasato/kubernetes-basics/tree/master/09-cicd

## 前提
    ~~~
    # minikube status 
    minikube
    type: Control Plane
    host: Running
    kubelet: Running
    apiserver: Running
    kubeconfig: Configured
    ~~~

## 手順
1. NameSpaceの作成
    ~~~
    # kubectl create ns argocd
    ~~~
   
1. NameSpaceの作成の確認
    ~~~
    # kubectl get ns
    ~~~

1. ArgoCDのデプロイ
    ~~~
    # kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    ~~~

1. ArgoCDのデプロイの確認
    ~~~
    # kubectl get svc -n argocd
    ~~~

1. Create Service with NodePort type (port: 30080)

    ```sh
    $ cd ~/kubernetes-basics/
    ```

    ```sh
    ll
    合計 12
    drwxr-xr-x. 2 root root  168  8月 12 08:40 03-environment-setup
    drwxr-xr-x. 2 root root   64  8月 12 08:40 04-kubectl
    drwxr-xr-x. 9 root root  154  8月 12 08:40 05-kubernetes-resources
    drwxr-xr-x. 2 root root 4096  8月 12 10:50 06-run-simple-application-in-kubernetes
    drwxr-xr-x. 2 root root 4096  8月 12 10:50 07-debug-kubernetes
    drwxr-xr-x. 2 root root   23  8月 12 10:50 08-setup-eks-cluster
    drwxr-xr-x. 2 root root  249  8月 12 08:40 09-assignment
    drwxr-xr-x. 5 root root  191  8月 12 10:50 09-cicd
    -rw-r--r--. 1 root root  750  8月 12 08:40 README.md
    drwxr-xr-x. 2 root root   35  8月 12 08:40 argocd-test
    ```

    ~~~
    kubectl apply -f 09-cicd/argocd-install/argocd-server-node-port.yaml -n argocd
    ~~~

1. Port forward the service (port: 30080)
    ~~~
    kubectl -n argocd port-forward service/argocd-server 30080:80
    ~~~

1. Login

    Open https://localhost:30080, click on `Advanced` and `Proceed to localhost (unsafe)` (this is ok because we're connecting to the argocd running in our local computer)

    - username: `admin`
    - password: `kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath='{.data.password}' | base64 --decode`

1. 以降

    以下のサイトの「検証環境の構築」以降を実施

    https://selfnote.work/20220703/programming/kubernetes-microservices-volumes-2/#%E6%A4%9C%E8%A8%BC%E7%92%B0%E5%A2%83%E3%81%AE%E6%A7%8B%E7%AF%89
