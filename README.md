# Helm

## Helm

- 쿠버네티스를 구축하게 되면 다양한 Yaml이 나오게 되고 이를 관리하기가 굉장히 어려움
- 이를 간편하게 해주는 것이 Helm
- Heml은 Template이나 설정파일의 모음인데 이 것을 Helm Chart라고 부름

## Helm Repo

- https://github.com/helm/helm
- install: https://helm.sh/ko/docs/intro/install/

### Helm Repo Add

```bash
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm repo add eks https://aws.github.io/eks-charts
helm repo add ncloud https://navercloudplatformdeveloper.github.io/helm-charts
```

### Helm Repo List

```bash
helm search repo stable
```

### Chart Update

```bash
helm repo update
```

