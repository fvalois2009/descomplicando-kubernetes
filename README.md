# descomplicando-kubernetes

## Detalhes do ambiente utilizado

- Foi utilizado uma VM do Kali LInux, com 8GB de RAM e 4 CPUs;

## Instalando e customizando o Kubectl

Instalado o `kubctl` com os seguintes comandos:

```
$curl -LO https://storage.google.com/kubernetes-release/`curl -s https://storage.googleapis.com/kubernetes-releases/stable.txt` /bin/linux/amd64/kubectl
$chmod +x ./kubectl
$sudo mv ./kubectl /usr/local/bin
$kubectl version --client
```

# Criando um cluster kubernetes em maquina local

## Requisitos basicos

- Processamento: minimo 1 core;
- Memoria: 2GB;
- HD: 20GB

## Instalando o KIND no Linux 

Aqui estarei instalando o KIND. Mas, importante salientar que existem o `minikube` que eh o mais utilizado comumente:

```
$curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14/kind-linux-amd64
$chmod +x ./kind
$sudo mv ./kind /usr/local/bin/kind
```

## Criando um cluster com kind

Apos realizar a instalacao do Kind, vamos iniciar o nosso cluster.
```
#kind create cluster

Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.32.0) 🖼
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Thanks for using kind! 😊

```

Para visualizar os seus clusters utilizando o kind, execute o comando a seguir.
```
kind get clusters
```

Para listar os nos do cluster.
```
kubectl get nodes
```

Para deletar/excluir o cluster
```
kind delete clusters kind
```

## Criando um cluster com multiplus nos com o kind

Para esta aula do DAY-1 criar um arquivo de definicao para criar um cluster com 1 control-plane e 2 workers.

Antes, excluir todos os clusters que porventura tinha sido criados para fins de testes, executando o seguinte comando:

```
#kind delete clusters $(kind get clusters)
```

Crie o seguinte arquivos de configuracao para definir quantos tipos de nos no cluster que voce deseja, conforme exemplo a seguir:

```
cat << EOF > $HOME/kind-cluster.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
EOF
```

Agora executar o seguinte comando para criar o kind-multinodes:
```
#kind create cluster --name kind-mulinodes --config $HOME/kind-cluster.yaml
Creating cluster "kind-multinodes" ...
 ✓ Ensuring node image (kindest/node:v1.32.0) 🖼
 ✓ Preparing nodes 📦 📦 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
 ✓ Joining worker nodes 🚜 
Set kubectl context to "kind-kind-multinodes"
You can now use your cluster with:

kubectl cluster-info --context kind-kind-multinodes

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/

```

Valide a criacao do cluster com o seguinte comando:
```
#kubectl get nodes

NAME                            STATUS   ROLES           AGE    VERSION
kind-multinodes-control-plane   Ready    control-plane   101s   v1.32.0
kind-multinodes-worker          Ready    <none>          89s    v1.32.0
kind-multinodes-worker2         Ready    <none>          89s    v1.32.0

```
