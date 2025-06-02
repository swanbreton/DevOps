Swan Breton
TP1 :
  3.a :
    docker run -d -p 3000:3000 httpd
    
    .b :
      docker images

    .c : 
      mkdir -p html
      echo "Hello World" > html/index.html

    .d : 
      docker run -d -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html


    .e :
      docker rm bold_gagarin (--force)

    .f : 
      docker run -d -p 8080:80 --name TP1 nginx
      docker cp ./html/index.html mon-nginx:/usr/share/nginx/html/index.html

  4.a :
    Dockerfile : 
      FROM nginx:latest

      COPY ./html/index.html /usr/share/nginx/html/index.html

    .b :
      docker build -t TPImage .

      docker run -d -p 8080:80 TPImage

    .c : 
      Le mount volume est plus compliqué à mettre en place que le COPY, mais le mount volume permet de ne pas rebuild l'image à chaque modification

   5.a :
    docker pull mysql
    docker pull phpmyadmin/phpmyadmin

    .b :
      Création de la pacerelle réseau :
        docker network create mynet

      Lancement du conteneur Mysql : 
        docker run -d \
        --name mysql-container \
        --network mynet \
        -e MYSQL_ROOT_PASSWORD=rootpass \
        -e MYSQL_DATABASE=ma_base \
        -e MYSQL_USER=utilisateur \
        -e MYSQL_PASSWORD=motdepasse \
        mysql

      Lancement du conteneur phpMyAdmin :
        docker run -d \
        --name myadmin \
        --network mynet \
        -e PMA_HOST=mysql-container \
        -p 8080:80 \
        phpmyadmin/phpmyadmin

    6.a :
    docker run = lancer un seul conteneur
    docker commpose = lancer plusieurs coneteneurs 

      .b :
      Commande qui permet de lancer tout les containers du fichier yami = docker-compose up
      Commande qui permet de stopper tout les containers = docker-compose down

      .c :
        version: '3.8'
      
      services:
        db:
          image: mysql
          container_name: mysql-container
          environment:
            MYSQL_ROOT_PASSWORD: rootpass
            MYSQL_DATABASE: ma_base
            MYSQL_USER: utilisateur
            MYSQL_PASSWORD: motdepasse
          ports:
            - "3306:3306"
          networks:
            - mynet
      
        phpmyadmin:
          image: phpmyadmin/phpmyadmin
          container_name: phpmyadmin-container
          environment:
            PMA_HOST: db
            PMA_USER: users
            PMA_PASSWORD: password
          ports:
            - "8080:80"
          depends_on:
            - db
          networks:
            - mynet
      
      networks:
        mynet:

      
  



      

      

    
    



    
    
  

  
