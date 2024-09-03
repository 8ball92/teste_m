# Yoda Web app 

Em sua VM, criei um path com o seguinte comando para podermos atrelar ao k3d nos próximos passos.

   

     mkdir -p /data/k3dvol

Antes de começar é muito importante ter criado o seu cluster, no meu exemplo estou utilizando o k3d, basta executar o seguinte comando!

    k3d cluster create  lab  --agents 2 -p "80:30000@loadbalancer" --volume /data/k3dvol:/data/k3dvol

Realize o deploy do ingress:

    `kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.5.1/deploy/static/provider/baremetal/deploy.yaml

O build  será feito  na raiz do projeto clonado. Haverá um script la que fara o build e o push:

    sh docker.sh

Crie a namespace lab:

    kubectl create namespace lab

 
Para aplicar os manifestos em seu cluster, acesse a raiz do seu repo que acabou de efetuar o git clone e Execute na pasta k8s:
  ```

    kubectl create -f k8s/

Valide a criação do seu pod na namespace:

    kubectl get po -n lab 

Agora vamos testar  nossa chamada.

    curl -v http://yoda.127.0.0.1.nip.io

Ou abrir nosso browser

    http://yoda.127.0.0.1.nip.io 

Em caso de monitoramento  /metrics esta ativo na app.

    http://yoda.127.0.0.1.nip.io/metrics