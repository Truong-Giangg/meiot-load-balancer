# meiot-load-balancer
# meiot-load-balancer
Install rancher using helm
```
helm repo add rancher-latest https://releases.rancher.com/server-charts/latest
helm repo update
kubectl create namespace cattle-system
helm install rancher rancher-latest/rancher \
  --namespace cattle-system \
  --set hostname=rancher.my.org \
  --set replicas=1 \
  --set bootstrapPassword=admin

```
Install jenkins, after install it is waiting for PVC to attach PV
```
helm install jenkins-release jenkins/jenkins  \
  --namespace jenkins \
  --create-namespace   \
  --set controller.admin.username=admin  \
  --set controller.admin.password=secret
```
Create jenkins pv and pvc, then reinstall jenkins
```
helm uninstall jenkins-release -n jenkins

helm install jenkins-release jenkins/jenkins \
  --namespace jenkins \
  --set persistence.existingClaim=jenkins-release \
  --set controller.admin.username=admin \
  --set controller.admin.password=secret

```
