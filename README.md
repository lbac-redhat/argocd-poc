# Environments

This repository contains the configuration and current state for application environments deployed by ArgoCD.

The `app-environments` _ApplicationSet_ defined in the `applicationset.yml` file uses the [Files Git generator][1] to create ArgoCD applications based on the `appset/*` directory, using the `environment` Helm Chart from the [helmcharts-poc][2] repository.

[1]:https://argocd-applicationset.readthedocs.io/en/stable/Generators-Git/#git-generator-files
[2]:https://github.com/lbac-redhat/helmcharts-poc
