# myapp-service
Implantando aplicativo criado com Dockerfile.

<strong> Objetivos: </strong> 

 - Criar um Deployment para a aplicação que foi criada no treinamento de Docker chamada webserver10.
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

