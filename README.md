# myapp-service
<strong> Atividade 2 - Treinamento Trilha Orquestração de Containers  </strong>
<br>

Implantando aplicativo criado com Dockerfile.

<strong> Objetivos: </strong> 

 - Criar um Deployment para a aplicação que foi criada no treinamento de Docker chamada myk8sapp.
 - Expor a aplicação através de um Service.

# Passos:

<strong> 1 Crie um Deployment: </strong>

 - Crie um arquivo YAML chamado myapp-deployment.yaml.
 - Defina um Deployment para a aplicação chamada “myapp”.
 - Use uma imagem Docker que você criou anteriormente.
 - Configure o número de réplicas para 2.
 - Defina um rótulo adequado para o Deployment.

<strong> 2 Crie um Service: </strong>

 - Crie um arquivo YAML chamado myapp-service.yaml.
 - Defina um Service chamado “myapp-service”.
 - Exponha a porta 80 do Deployment.
 - Use um seletor adequado para direcionar o tráfego para as réplicas corretas.

<strong> 3 Implante a Aplicação: </strong>

 - Aplique os arquivos YAML na ordem:Deployment e Service.
 - Verifique se a aplicação está em execução corretamente.


# Implantação: 

<strong> Passo 1: Download da aplicação HTML CSS e JS </strong>
  - GitHub:
```bash
git clone https://github.com/oanderoficial/infrabank.git
cd /infrabank
```
<strong> Passo 2: Crie a imagem Docker </strong> 

 - Crie um Dockerfile no mesmo diretório:

```Dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
```

 - Construa a imagem Docker:

```bash
docker build -t myk8sapp:latest .
```

![image](https://github.com/oanderoficial/myapp-service/assets/32654298/485f93d2-e24f-4f60-90f1-250815a24a3a)

- Faça o upload da imagem para um registro de contêiner, como Docker Hub:

```bash
docker tag myk8sapp:latest yourusername/myk8sapp:latest
docker push yourusername/myk8sapp:latest
```

<strong> Passo 3: Criando o Deployment </strong> 

 - Crie um arquivo chamado myapp-deployment.yaml

```yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myk8sapp
        image: yourusername/myk8sapp:latest
        ports:
        - containerPort: 80
```

<strong> Passo 4: Criando o Service </strong> 

 - Crie um arquivo chamado myapp-service.yaml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```

<strong> Passo 5: Implante a Aplicação </strong> 

- Aplique o Deployment:
```bash
kubectl apply -f myapp-deployment.yaml
```
- Aplique o Service:
```bash
kubectl apply -f myapp-service.yaml
```
- Verifique se a aplicação está em execução corretamente:
```bash
kubectl get deployments
kubectl get pods
kubectl get services
```
![image](https://github.com/oanderoficial/myapp-service/assets/32654298/59dec23d-bde4-43bc-8532-e7e3b6fbb7ba)


<strong>  Start com o Minikube </strong> 

<p>Se você estiver usando Minikube, você pode expor o serviço com o comando minikube service:</p>

```bash
minikube service myapp-service
```
<strong> Bind de portas </strong> 

```
kubectl port-forward svc/myapp-service 8080:80 --address='0.0.0.0'
```
![image](https://github.com/oanderoficial/myapp-service/assets/32654298/99e9f68d-3270-4243-b843-b6bdd43a2bb4)

# Saída 

![image](https://github.com/oanderoficial/myapp-service/assets/32654298/0fdfa793-4b8c-421f-8904-0713504fb8b2)



