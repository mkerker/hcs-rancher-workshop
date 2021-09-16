# Start Workshop

We werken voor deze workshop van
```sh
ssh <userXX>@bastion.hcs-rancher.com
```
Wachtwoord: HCSR@nch3r

```sh
ls -al
```

```sh
rke -v
```

```sh
kubectl version --client
```

```sh
helm version --client
```
# Rancher Cluster
## Stap: 

```sh
cat rancher-cluster.yml
```

```sh
rke up --config rancher-cluster.yml
```

## Stap: Check Rancher cluster

```sh
chmod 600 kube_config_rancher-cluster.yml
mkdir -p .kube
ln -s ~/kube_config_rancher-cluster.yml .kube/config
```

```sh
kubectl get nodes
kubectl get pods -A
```


```sh
helm repo add jetstack https://charts.jetstack.io 
helm repo update
```

```sh
kubectl create namespace cert-manager
helm install cert-manager jetstack/cert-manager --namespace cert-manager --set installCRDs=true 
```

```sh
kubectl -n cert-manager rollout status deploy/cert-manager
kubectl -n cert-manager rollout status deploy/cert-manager-webhook 
```

```sh
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
helm repo update
```

```sh
kubectl create namespace cattle-system
helm install rancher rancher-stable/rancher --namespace cattle-system --set hostname=${USER}.hcs-rancher.com --set replicas=1 
```

```sh
kubectl -n cattle-system rollout status deploy/rancher
```

```sh
https://<userXX>.hcs-rancher.com
```
# Voeg user cluster toe

# Upgrade User cluster

# K8s User cluster

```sh
# S3 Access Key and Password
ROOT_USER=AKIAIOSFODNN7MARCEL
ROOT_PASSWORD=wJalrXUtnFEMIK7MDENGbPxRfiCYKERKER
```

```sh
https://s3.hcs-rancher.com
```

```sh
# Create snapshot
rke etcd snapshot-save --config k8s-cluster.yml
```

poweroff 
```sh
stopk8s
```

```sh
cat node-cluster.yml
```

```sh
ssh -i id_rsa ${USER}@$(cat node-cluster.yml | grep address | awk '{print $3}')
```

```sh
docker version

docker images
```

Wijzig het _address_, _hostname_override_ en _kubernetes_version_ met de waarde: v1.20.4-rancher1-1

```sh
cat node-cluster.yml | grep address | awk '{print $3}'

echo node-${USER}-vm
```

```sh
vi k8s-cluster.yml
```

```sh
# Restore snapshot
rke etcd snapshot-restore --config k8s-cluster.yml
```

## Stap: Rancher cli

rancher login https:// .. /v3 --token dsfdsdsdsd


# Applicatie deployment

## Stap: Maak een project en een namespace aan

1. Navigeer in de Rancher UI naar het k8s cluster.
2. 

## Stap: Deploy nginx en rollback applicatie

## Stap: Werk met een private registry

rancher.azurecr.io

## Stap: Deploy een app uit de Catalogus

1. Navigeer naar het proje to a project in your k8s cluster.
2. Select Appsfrom the menu at the top. Click the Launchbutton in the top right.
3. Which apps you see depends on which catalogs you’ve enabled at the Global, Cluster, or Project scopes. At the very least you should have the Library apps available. Scroll down until you find Redisand select it.
4. This app will install into the redisnamespace by default. If there is already a redisnamespace, then it will create a new namespace derived from that name. 
5. For speed and ease of deployment in this lab, set Enable Master-Slave Topologyto False.
6. Enter a password or click Generateto have one filled in for you.
7. Leave the other options at their defaults and click Launch.
8. Wait for the app to show Activ

## Stap: Fleet

```sh
cat > example.yaml << "EOF"
apiVersion: fleet.cattle.io/v1alpha1
kind: GitRepo
metadata:
  name: sample
  # This namespace is special and auto-wired to deploy to the local cluster
  namespace: fleet-local
spec:
  # Everything from this repo will be ran in this cluster. You trust me right?
  repo: "https://github.com/rancher/fleet-examples"
  paths:
  - simple
EOF
```

```sh
kubectl apply -f example.yaml
```

```sh
kubectl -n fleet-local get fleet
```

```sh
kubectl get deploy frontend
```

```sh
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
frontend   3/3     3            3           116m
```

Meer voorbeelden kun je vinden op: https://github.com/rancher/fleet-examples/tree/master/single-cluster
Meer informatie over fleet: http://fleet.rancher.io

## Stap
```sh
```

```sh
```

# Monitoring en Logging
