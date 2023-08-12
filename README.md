# k8s-argocd
Kubernetes と ArgoCdの連携

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
