# GitHub Action Kubernetes Runner

GitHub Action missing official kubernetes integrated documents，but the community has a lot of solutions, here is one of the solution I have tested: [actions-runner-controller](https://github.com/actions-runner-controller/actions-runner-controller)

## Prerequisites

- A kubernetes cluster

- Cert-manager installed in the cluster

!!! note

    actions-runner-controller use [cert-manager](https://cert-manager.io/docs/installation/kubernetes/) to manage Admission Webhook certificates. [Installing cert-manager on Kubernetes](https://cert-manager.io/docs/installation/kubernetes/)

- Create organization level runner group

!!! note

    Used to limit the visibility of GitHub Runners
    [managing-access-to-self-hosted-runners-using-groups](https://docs.github.com/en/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups)

- Create PAT via organization PAT Page

!!! note

    ```
    https://<GITHUB_ENTERPRISE_URL>/settings/tokens
    ```

    Grant access to:

    - repo (Full control)
    - admin:org (Full control)
    - admin:public_key (read:public_key)
    - admin:repo_hook (read:repo_hook)
    - admin:org_hook (Full control)
    - notifications (Full control)
    - workflow (Full control)

- PAT Test

  Run follow commands:

  ```bash
  curl --header "Authorization: token <GTIHUB_TOKEN>" \
  -X GET \
  -H "Accept: application/vnd.github.v3+json" \
  https://<GITHUB_DOMAIN>/api/v3/orgs/<GITHUB_ORG>/actions/runners/registration-token
  ```

## Steps to run self-host runner on kubernetes

- Install `action-runner-controller`

  ```bash
  helm repo add actions-runner-controller https://actions-runner-controller.github.io/actions-runner-controller

  # Follow document to replace values file https://github.com/actions/actions-runner-controller/blob/master/charts/actions-runner-controller/README.md
  # githubEnterpriseServerURL
  # OR
  # githubURL
  # And authSecret.github_token
  helm upgrade --install --namespace actions-runner-system --create-namespace \
                --wait actions-runner-controller actions-runner-controller/actions-runner-controller
  ```

- Create `Runner`
  ```yaml
  apiVersion: actions.summerwind.dev/v1alpha1
  kind: RunnerDeployment
  metadata:
  name: <GitHub_Org_Name>-runner
  namespace: <Namespace_Name>
  spec:
  replicas: 2
  template:
    metadata:
    annotations:
      cluster-autoscaler.kubernetes.io/safe-to-evict: "true"
    spec:
    organization: <GitHub_Org_Name>
    env: []
    group: <GitHub_Group_Name>
    labels:
      - <GitHub_Org_Name>-runner
  ```
