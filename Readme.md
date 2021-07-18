## Kubernetes
### Simples aplicação para visualização do k8s em ambiente local

- **O que é esta tecnologia?**
	- É um orquestrador de containers
- **Quais problemas ela resolve?** 
	- Facilita no gerenciamento dos containers, com vários recursos como loadbalancer, service discovery, replicação de containers, monitoramento de containers (se um pod cair ele sobe novamente) Facilita no deploy garantindo que sempre terá ao menos um serviço rodando
- **Por que foi criada?**
	- Para resolver os problemas citados a cima
- **Onde ela se aplica?**
 	- Ela se aplica quando você tem um ambiente muito robusto e com várias aplicações e que demanda uma garantia de disponibilidade, e gerenciamento dessas aplicações
- **Aonde não se aplica?**
	- Em um ambiente que não existe muitas aplicações e não se necessita de um gerenciamento / alta demanda por estes serviços
- **Quais seus principais conceitos?**
	- Master: a máquina que controla os nós do Kubernetes. É nela que todas as atribuições de tarefas se originam.
	- Nó: são máquinas que realizam as tarefas solicitadas e atribuídas. A máquina mestre do Kubernetes controla os nós.
	- Pod: um grupo de um ou mais containers implantados em um único nó. Todos os containers em um pod compartilham o mesmo endereço IP, IPC, nome do host e outros recursos. Os pods separam a rede e o armazenamento do container subjacente. Isso facilita a movimentação dos containers pelo cluster.
	- Controlador de replicações: controla quantas cópias idênticas de um pod devem ser executadas em um determinado local do cluster.
	- Serviço: desacopla as definições de trabalho dos pods. Os proxies de serviço do Kubernetes automaticamente levam as solicitações de serviço para o pod correto, independentemente do local do pod no cluster ou se foi substituído.
	- Kubelet:um serviço executado nos nós que lê os manifestos do container e garante que os containers definidos foram iniciados e estão em execução.
	- kubectl: a ferramenta de configuração da linha de comando do Kubernetes.

## Passos para testar local
- instalar kubectl
- Instalar alguma das ferramentas que simulam o K8S, usei o Kind
- Gerar imagem e publicar em algum gerenciador( eg: Docker hub), ou utilizar alguma imagem existente publica (usei nginx)
- Criar cluster K8S a partir da ferramenta escolhida
- Criar aquivo do tipo deployment, com a imagem desejada, expondo a porta.
	- rodar o comando:
```
       kubectl apply -f deployment.yml
```
- Depois criar o arquivo de service, passando a porta que ele ficara disponível, e os pods que ele vai chamar
```
    kubectl apply -f service.yml
```
- Para validar se tudo está ok posso usar os seguintes comandos
```
kbectl get pods
kubectl get service
```
- Se tudo tiver dado ok, posso rodar o comando para ver se o meu service irá chamar meus pods:
```
kubectl  port-forward service/nomedoservice 80(porta que meu service está disponivel):3000(Porta que eu vou passar)
```
- Para validar que realmente a porta está funcionando pode-se executar o seguinte comando
```
curl http://localhost:3000/
```
Deverá exibir a página inicial do seu recurso, no meu caso o nginx
```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

```



### Referencias:

[https://www.redhat.com/pt-br/topics/containers/what-is-kubernetes#:~:text=Kubernetes%2C%20ou%20%E2%80%9Ck8s%E2%80%9D%2C,as%20opera%C3%A7%C3%B5es%20dos%20containers%20Linux.&text=Por%20isso%2C%20o%20Kubernetes%20%C3%A9,por%20meio%20do%20Apache%20Kafka][Red Hat - O que é o Kubernetes].

[Red Hat - O que é o Kubernetes]: https://www.redhat.com/pt-br/topics/containers/what-is-kubernetes#:~:text=Kubernetes%2C%20ou%20%E2%80%9Ck8s%E2%80%9D%2C,as%20opera%C3%A7%C3%B5es%20dos%20containers%20Linux.&text=Por%20isso%2C%20o%20Kubernetes%20%C3%A9,por%20meio%20do%20Apache%20Kafka

[https://kubernetes.io/docs/home/][Kubernetes documentation]


[Kubernetes documentation]: https://kubernetes.io/docs/home/