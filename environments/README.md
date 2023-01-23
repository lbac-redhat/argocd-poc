# ArgoCD Applications

All applications defined in this directory will be automatically picked up by the [`0cpinfra01-config`][1] _Application_ and managed by ArgoCD.

Most, if not all, of these _Applications_ should be pulling Helm Charts from the [ocp-helmcharts][3] repository, tracking a release tag from that repository.

Generally, all _Applications_ here **should** have the <u>automated sync policy</u>, <u>self healing</u> and <u>pruning</u> enabled.

## Changing releaseversion

Sed oneliner to replace current releasetag with the new one:
```bash
sed -i -e 's/1.0.0/1.0.1/g' ./*.yaml
```

## Creating a new Application

Simply create a new [_Application_][2] YAML manifest describing your _Application_ and, if it is deploying a Helm Chart, any values overrides as a block file.

Example manifest:
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: <APPLICATION_NAME>
  namespace: argocd
spec:
  destination:
    namespace: <DESTINATION_NAMESPACE>
    server: https://kubernetes.default.svc
  project: infra
  source:
    helm:
      values: |
        <EXAMPLE_KEY>: <EXAMPLE_VALUE>
        <EXAMPLE_LIST>:
          - <EXAMPLE_ELEMENT1>
          - <EXAMPLE_ELEMENT2>

    path: <APPLICATION_NAME>
    repoURL: ssh://git@git.csnnet.int:7999/area-ocpinfra/ocp-helmcharts.git
    targetRevision: <RELEASETAG>
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

[1]:https://git.csnnet.int/projects/AREA-OCPINFRA/repos/ocpinfra01-config/browse/argocd/argocd-ocpinfra01-application.yaml
[2]:https://argoproj.github.io/argo-cd/operator-manual/declarative-setup/#applications
[3]:https://git.csnnet.int/projects/AREA-OCPINFRA/repos/ocp-helmcharts/browse
