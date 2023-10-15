# 🍔 Lanchonete do Bairro - Kubernetes Infrastructure

## Como rodar o projeto

### Kubernetes

Todos os arquivos necessários para utilizar o Kubernetes se encontram na pasta `infra` deste projeto. Uma vez que o Docker esteja rodando com as configurações necessárias para a utilizacao do kubernetes, ou minikube, rode o seguinte comando:

Como estamos usando minikube para o desenvolvimento, é necessário rodar o seguinte comando para que o minikube possa usar as imagens do docker:

```shell
minikube start
```

Uma vez que o minikube esteja rodando, rode o seguinte comando para subir a infraestrutura do Kubernetes:

```sh
kubectl apply -f infra/config
kubectl apply -f infra/db
kubectl apply -f infra/project
```

Este comando irá subir toda a infraestrutura do Kubernetes, que pode ser visualizada na [documentação geral](https://www.notion.so/danielmariadasilva/Lanchonete-do-Bairro-97145985ac3e4b65a077ff13866e66ad#927eb1f24e804f34b9aa1e8a70c30644).

Caso queira, você pode acompanhar a subida e o estado de cada POD com o seguinte comando:

```sh
kubectl get pods --watch
```

Como estamos usando minikube, a porta da aplicação deve ser descoberta antes de podermos usar o sistema. Para isso, rode o comando a seguir que retornará a porta onde a aplicação está rodando:

```sh
minikube service svc-lanchonetebairro-replica --url
```
Este comando deve estar rodando em um terminal separado, pois ele , ele cria um túnel entre a porta do seu ambiente local e o serviço Kubernetes dentro do cluster Minikube. Esse túnel permite que as solicitações feitas à porta local sejam redirecionadas para o serviço dentro do cluster.

Feito isso, entre no swagger utilizando a url fornecida.

Caso precise, para parar todos os serviços rode o seguinte comando:

```sh
kubectl delete -f infra/config
kubectl delete -f infra/db
kubectl delete -f infra/project
```
