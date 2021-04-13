# 🍾 published helm charts 🍾
```
helm repo add springdo https://springdo.github.io/published-charts
```

Check for the latest chart versions
```bash
helm search repo springdo
```

![Pump It Up](https://i.pinimg.com/originals/c4/43/fc/c443fcf40abba3f9e098d5bd25ca20be.gif)

## Deploying Pet Battle using helm3

Login to OpenShift as cluster admin user

Add a `HelmChartRepository`

```bash
cat <<EOF | oc apply -f -
apiVersion: helm.openshift.io/v1beta1
kind: HelmChartRepository
metadata:
  name: springdo-charts
spec:
  name: springdo
  connectionConfig:
    url: https://springdo.github.io/published-charts
EOF
```

You can also use a nexus helm-chart repo as another entry as OpenShift supports relative chart urls as served by nexus:
```bash
url: https://nexus-labs-ci-cd.apps.openshift.example.com/repository/helm-charts
```

![pb-helm-charts-ocp.png](images/pb-helm-charts-ocp.png)

## Install apps
Install the helm cli if you don't already have it....

example install ....
```bash
helm upgrade --install APP_NAME springdo/APP --version=1.0.21 --set something=value 
```

## Delete apps

```bash
helm uninstall APP_NAME
```