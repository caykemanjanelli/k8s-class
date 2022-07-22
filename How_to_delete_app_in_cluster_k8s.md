# How to delete app in Cluster K8s

## Login in cluster

1. Para fazer login no cluster e realizar a ação abaixo, é necessario ter acesso ao grupo `GL_CLOUD_DEVOPS`
2. Configurar contexto AWS-CLI na maquina local incluindo 2 profiles no arquivo `$HOME/.aws/config`:

```txt
[profile qa-admin]
sso_start_url = https://dftech.awsapps.com/start
sso_region = us-east-1
sso_account_id = 678591175058
sso_role_name = AdministratorAccess
region = us-east-1
output = json
[profile live-admin]
sso_start_url = https://dftech.awsapps.com/start
sso_region = us-east-1
sso_account_id = 556684128444
sso_role_name = AdministratorAccess
region = us-east-1
output = json
```

1. Comando para fazer login no cluster `EKS`, informando:
   - `Profile`
   - `Cluster`

```sh
aws sso login --profile qa-admin
aws sts get-caller-identity --profile qa-admin
aws eks update-kubeconfig --profile qa-admin --name eks-dafiti-qa
```

> para pegar a lista de nome dos cluster no contexto, execute o comando abaixo:

## Delete Application (namespace)

1. Listando aplicação no cluster, no exemplo `freight-service`:

```sh
aws eks list-clusters --profile qa-admin
kubectl get all -n freight-service
```

1. Delete aplicação:

```sh
kubectl delete all --all -n freight-service
```
