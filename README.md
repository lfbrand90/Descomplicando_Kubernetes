# Descomplicando_Kubernetes

## Criando um cluster com o Kind
Após realizar a instalação do Kind, vamos iniciar o nosso cluster.
```
kind create cluster

Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.24.0) 🖼
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Not sure what to do next? 😅  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
```
  É possível criar mais de um cluster e personalizar o seu nome.
```
kind create cluster --name giropops

Creating cluster "giropops" ...
 ✓ Ensuring node image (kindest/node:v1.24.0) 🖼
 ✓ Preparing nodes 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
Set kubectl context to "kind-giropops"
You can now use your cluster with:

kubectl cluster-info --context kind-giropops

Thanks for using kind! 😊
```
  Para visualizar os seus clusters utilizando o kind, execute o comando a seguir.
```
kind get clusters
```
  Liste os nodes do cluster.
```
kubectl get nodes
``` 

## Criando um cluster com múltiplos nós locais com o Kind
É possível para essa aula incluir múltiplos nós na estrutura do Kind, que foi mencionado anteriormente.

Execute o comando a seguir para selecionar e remover todos os clusters locais criados no Kind.
```
kind delete clusters $(kind get clusters)

Deleted clusters: ["giropops" "kind"]
```
  Crie um arquivo de configuração para definir quantos e o tipo de nós no cluster que você deseja. No exemplo a seguir, será criado o arquivo de configuração kind-3nodes.yaml para especificar um cluster com 1 nó control-plane (que executará o control plane) e 2 workers.
```
cat << EOF > $HOME/kind-3nodes.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
EOF
```
  Agora vamos criar um cluster chamado kind-multinodes utilizando as especificações definidas no arquivo kind-3nodes.yaml.
```
kind create cluster --name kind-multinodes --config $HOME/kind-3nodes.yaml

Creating cluster "kind-multinodes" ...
 ✓ Ensuring node image (kindest/node:v1.24.0) 🖼
 ✓ Preparing nodes 📦 📦 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
 ✓ Joining worker nodes 🚜 
Set kubectl context to "kind-kind-multinodes"
You can now use your cluster with:

kubectl cluster-info --context kind-kind-multinodes

Have a question, bug, or feature request? Let us know! https://kind.sigs.k8s.io/#community 🙂
```
  Valide a criação do cluster com o comando a seguir.
```
kubectl get nodes
```
  Mais informações sobre o Kind estão disponíveis em: https://kind.sigs.k8s.io
