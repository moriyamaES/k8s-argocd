# k8s-argocd
Kubernetes と ArgoCdの連携

# 参考にしたサイト
https://selfnote.work/20220703/programming/kubernetes-microservices-volumes-2/

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
# kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
~~~
