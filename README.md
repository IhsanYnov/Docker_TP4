# Docker_TP4

Introduction à Kubernetes

1. Installation de Kubernetes

   a. Installation de Docker
         > sudo apt-get update
         > sudo apt-get install \ ca-certificates \ curl \ gnupg \ lsb-release
       On installe la clé GPT
         > sudo mkdir -p /etc/apt/keyrings
         > curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
       On installe le dépot 
         > echo \ "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
           $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
         > sudo apt-get update
       On peut installer Docker et ses plugins
         > sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
         
   b.Installation de kubernetes et minikube
         > curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
         > sudo install minikube-linux-amd64 /usr/local/bin/minikube
         > minikube start
         
 2.
   a.Installation du Pods NGINX
         > git clone https://github.com/collabnix/kubelabs
         > cd kubelabs/pods101
         > kubectl apply -f pods01.yaml
     On vérifie la bonne installation du pod 
         > kubectl get pods
     Nous pouvons voir le pods "webserver" installé
     
   b.Redirection vers le port 80 
         > minikube kubectl -- port-forward pods/webserver 80:80
         
3.
a.
  Création du pod MYSQL
  minikube kubectl -- create -f https://raw.githubusercontent.com/kubernetes/examples/master/mysql/mysql-pod.yaml

  Création du pod phpmyadmin:
  minikube kubectl --  create -f https://raw.githubusercontent.com/kubernetes/examples/master/mysql/phpmyadmin-pod.yaml

b.
  Création du service mysql:
  minikube kubectl --  create -f https://raw.githubusercontent.com/kubernetes/examples/master/mysql/mysql-service.yaml

  Création du service phpmyadmin:
  minikube kubectl --  create -f https://raw.githubusercontent.com/kubernetes/examples/master/mysql/phpmyadmin-service.yaml
 
 c.
  Création de la connexion entre phpmyadmin et mysql service :
  minikube kubectl -- set env pods <phpmyadmin-pod-name> MYSQL_ROOT_PASSWORD=<your-password>

  On récupère l'adresse de phpmyadmin
  minikube service phpmyadmin
   
 d.
   On redirige les requêtes entrantes sur un port local vers un port sur le pod dans le cluster Kubernetes
   minikube kubectl -- port-forward phpmyadmin 8080:80
 e.
   Ingress est un objet qui sert de fichier de configuration des regles d'accès d'un conteneur kubernetes.
   <fichier>
   Puis on applique le changement 
   minikube kubectl -- apply


