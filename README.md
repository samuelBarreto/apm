Datadog
    $ helm install datadog-agent -f values.yaml -n datadog-agent --create-namespace --set datadog.apiKey=e5bcd35313bf432686c28c9cfbd2f0d9 datadog/datadog
    
     $ helm upgrade -f values.yaml -n datadog-agent datadog-agent datadog/datadog

    kubectl get pods datadog-agent-fkmkp-o jsonpath='{.spec.containers[*].name}' -n datadog-agent 

registry 

    $ kubectl create secret docker-registry gcr-json-key --docker-server=us-east1-docker.pkg.dev --docker-username=_json_key --docker-password="$(cat registry.json)"

    $ kubectl describe sa Name: default Namespace: default Labels: Annotations: Image pull secrets: Mountable secrets: Tokens: Events:

    $ kubectl patch serviceaccount default -p '{"imagePullSecrets": [{"name": "gcr-json-key"}]}' $ kubectl describe sa Name: default Namespace: default Labels: Annotations: Image pull secrets: gcr-json-key Mountable secrets: Tokens: Events:

editar aquirvo deployment image registry imagePullSecrets: - name: gcr-json-key containers: - name: java-spring image: us-east1-docker.pkg.dev/datadog-402618/datadog-appoena/java-spring:latest imagePullPolicy: Always

    $ kubectl apply -f datadogpoweruser/apm/java/java-spring.yaml deployment.apps/java-spring created service/java-spring created 
    
    $ kubectl apply -f datadogpoweruser/apm/python/python-flask.yaml deployment.apps/python-flask created service/python-flask created $ kubectl apply -f datadogpoweruser/apm/dotnet/dotnet-todoapi.yaml deployment.apps/dotnet-todoapi created service/dotnet-todoapi created

$ kubectl get pods -A

''' NAMESPACE NAME READY STATUS RESTARTS AGE datadog-agent datadog-agent-5thjn 3/3 Running 0 7m30s datadog-agent datadog-agent-cluster-agent-9dc5b6cf7-9s5ht 1/1 Running 0 7m1s datadog-agent datadog-agent-cluster-agent-9dc5b6cf7-gpdxx 1/1 Running 0 7m32s datadog-agent datadog-agent-d2f5n 3/3 Running 0 7m31s datadog-agent datadog-agent-f8zn9 3/3 Running 0 7m31s datadog-agent datadog-agent-lr9pp 3/3 Running 0 7m31s default dotnet-todoapi-5b77f7569-w6zpd 1/1 Running 0 96s default java-spring-778f599866-gp9xb 1/1 Running 0 3m6s default python-flask-64f977644f-f2jm9 1/1 Running 0 112s gmp-system alertmanager-0 2/2 Running 0 10m gmp-system collector-cqwqp 2/2 Running 0 15m gmp-system collector-fgsqk 2/2 Running 0 15m gmp-system collector-vbhkt 2/2 Running 0 10m gmp-system collector-xcjlc 2/2 Running 0 15m gmp-system gmp-operator-5549dfdbd5-zvqmc 1/1 Running 0 10m gmp-system rule-evaluator-6fc7cc5489-ghpkq 2/2 Running 2 (15m ago) 15m kube-system event-exporter-gke-7bf6c99dcb-2dd5m 2/2 Running 0 10m kube-system fluentbit-gke-ht7g6 2/2 Running 0 15m kube-system fluentbit-gke-jw25n 2/2 Running 0 15m kube-system fluentbit-gke-mz27f 2/2 Running 0 10m kube-system fluentbit-gke-n47gk 2/2 Running 0 15m kube-system gke-metrics-agent-4l58j 2/2 Running 0 15m kube-system gke-metrics-agent-7v52d 2/2 Running 0 10m kube-system gke-metrics-agent-b6bqd 2/2 Running 0 15m kube-system gke-metrics-agent-z5fgz 2/2 Running 0 15m kube-system konnectivity-agent-9546c8b4d-8n68k 1/1 Running 0 10m kube-system konnectivity-agent-9546c8b4d-dxh29 1/1 Running 0 15m kube-system konnectivity-agent-9546c8b4d-slhds 1/1 Running 0 15m kube-system konnectivity-agent-9546c8b4d-xs45k 1/1 Running 0 15m kube-system konnectivity-agent-autoscaler-5d9dbcc6d8-ctpwq 1/1 Running 0 10m kube-system kube-dns-5bfd847c64-s75qg 4/4 Running 0 10m kube-system kube-dns-5bfd847c64-vdfsd 4/4 Running 0 15m kube-system kube-dns-autoscaler-84b8db4dc7-5zfds 1/1 Running 0 10m kube-system kube-proxy-gke-cluster-cluster-pool-0256414b-9bkr 1/1 Running 0 15m kube-system kube-proxy-gke-cluster-cluster-pool-0256414b-k328 1/1 Running 0 15m kube-system kube-proxy-gke-cluster-cluster-pool-9c80879e-1n8t 1/1 Running 0 8m53s kube-system kube-proxy-gke-cluster-cluster-pool-9c80879e-v9lg 1/1 Running 0 15m kube-system l7-default-backend-d86c96845-rqp4r 1/1 Running 0 10m kube-system metrics-server-v0.5.2-6bf74b5d5f-vqrc6 2/2 Running 0 15m kube-system pdcsi-node-7k244 2/2 Running 0 10m kube-system pdcsi-node-k2xvb 2/2 Running 0 15m kube-system pdcsi-node-rtwh2 2/2 Running 0 15m kube-system pdcsi-node-tnjft
''''

./datadogpoweruser/apm/python/populate.sh ./datadogpoweruser/apm/java/populate.sh


Install ARGOD

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

userr admin senha

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

kubectl get pods -ns datadog-agent 

kubectl logs -f datadog-agent-vp669 agent -n datadog-agent | grep redis


APM

apm 

 # datadog.apm.portEnabled -- Enable APM over TCP communication (port 8126 by default)

    ## ref: https://docs.datadoghq.com/agent/kubernetes/apm/
    portEnabled: true


kubectl logs -f datadog-agent-69fpm -c trace-agent -n datadog-agent