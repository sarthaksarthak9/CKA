## Lab Helm

1) How many helm chart repositories are there in the controlplane node now?

- `helm repo list`

2) Deploy the Apache application on the cluster using the apache from the bitnami repository. Set the release Name to: amaze-surf
- `helm repo add bitnami url`
- `helm install amaze-surf bitnami/apache`

9) - `helm list` (display all details there is also a chart sec)

Q11) Uninstall the nginx chart release happy-browse from the cluster.
`helm uninstall release-name`

12) Remove the Hashicorp helm repository from the cluster.
`helm repo remove hashicorp`

## Lab upgrading helm chart

Q5) The DevOps team has decided to upgrade the nginx version to 1.27.x and use the Helm chart version 18.3.6 from the Bitnami repository. Ensure that the nginx version running in the cluster is 1.27.x.

`helm upgrade dazzling-web<name of the revision> bitnami/nginx<name of the chart> --version 18.3.6`

Q6) `helm rollback dazzling-web`