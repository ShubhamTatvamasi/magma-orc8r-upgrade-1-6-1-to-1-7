# magma-orc8r-upgrade-1-6-1-to-1-7

Initialize terraform:
```bash
terraform init --upgrade
```

Setup Magma Infrastructure:
```bash
terraform apply -target=module.orc8r -auto-approve
```

Create secrets:
```bash
terraform apply -target=module.orc8r-app.null_resource.orc8r_seed_secrets -auto-approve
```

Install Magma:
```bash
terraform apply -auto-approve
```

Update kubeconfig:
```bash
cd ~/.kube
touch orc8r.magmacore.link
export KUBECONFIG=${PWD}/orc8r.magmacore.link

aws eks update-kubeconfig \
  --name orc8r \
  --region us-east-2
```
