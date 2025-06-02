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



      

      

    
    



    
    
  

  
