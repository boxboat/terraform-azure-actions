# Reusable Terraform Actions for Azure

An action that can be used to deploy to Azure with Terraform.

Create a workflow from your repository that looks like this. 

``` yaml
jobs:
  terraform:
    runs-on: ubuntu-latest
    name: Terraform
    environment: canary # if you want to use secrets tied to an environment, define an environment in your repository (e.g. 'canary')
    steps:
      - uses: actions/checkout@v3
      - uses: boxboat/terraform-azure-actions@v1.0.0
        with:
          client-id: '<< service principal client id >>'
          client-secret: ${{ secrets.CLIENT_SECRET }}
          default-subscription-id: '<< some subscription id >>'
          tenant-id: '<< some aad tenant id >>'
          working-directory: '.' # or another file path like canary/another-folder
          plan-title: 'Canary :bird:'
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          terraform-version: 1.1.9
```

Make sure you add the following permissions in the GitHub workflow.

``` yaml
permissions:
  contents: read
  pull-requests: write
```
      
