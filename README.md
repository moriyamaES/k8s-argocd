# k8s-argocd
Kubernetes と ArgoCdの連携

# 参考にしたサイト
- 以下のサイトの内容を検証
https://selfnote.work/20220703/programming/kubernetes-microservices-volumes-2/
- Udemyの講座より参考
https://github.com/nakamasato/kubernetes-basics/tree/master/09-cicd

# 前提
~~~
# minikube status 
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
~~~
# 手順
## NameSpaceの作成
~~~
# kubectl create ns argocd
~~~
~~~

~~~
~~~
# kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
~~~
