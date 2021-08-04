Adicionar https com acme no rancher + kubernetes 
 
 
Para começar os passos abaixo, é necesário você ter adicionado o acme no catalog do rancher (TODO Fazer um tutorial para isso)
![image](https://user-images.githubusercontent.com/6400074/128235021-b09e61e4-da02-4dc0-b61f-f454eedfc6a5.png)

 
1º - Crie uma pasta chamada .kube 
  ```
  Mkdir .kube
  ```
2º - Entre na pasta .kube
  ```
  cd .kube
  ```
3º Obtenha o kubeconfig do seu cluster
![image](https://user-images.githubusercontent.com/6400074/128233931-1b4a2bc7-ea73-40c6-b928-85c0060b5700.png)

4º Crie um arquivo chamado config dentro da pasta .kube, após isso cole o conteúdo do kubeconfig neste novo arquivo
  ```
  vi
  config
  i
  ctrl + c
  esc
  :wq
  ```
  ps: caso queira verificar se o arquivo salvou corretamente basta executar o comando
  ```
   cat config
  ```
5º Volte 1 nível de pasta
  ```
  cd..
  ```
  ps: caso queira visualizar os arquivos criados basta utilizar o comando:
  ```
  ls
  ```
6º Criar o issuer.yml  (Fazer um tutorial para explicar linha a linha)
  ```
  vi issuer.yml
  i
  ctrl + c
  pressione esc
  :wq
  ```
  ps: caso queira verificar se o arquivo salvou corretamente basta executar o comando 
  ```
   cat issuer.yml
  ```
7º Rode os comandos a seguir
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

echo "$(<kubectl.sha256) kubectl" | sha256sum --check

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

kubectl version --client

kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.3.1/cert-manager.yaml

kubectl apply -f issuer.yml


Referências:
https://cert-manager.io/docs/configuration/acme/
