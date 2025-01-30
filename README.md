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

`
$curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14/kind-linux-amd64
$chmod +x ./kind
$sudo mv ./kind /usr/local/bin/kind
`