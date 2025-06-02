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



    
    
  

  
