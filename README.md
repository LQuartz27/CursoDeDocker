# Curso De Docker
   https://platzi.com/clases/docker/
# 1. Introducción
# Class#1
    Bienvenida al curso
# Class#2
    Las tres áreas en el desarrollo de software profesional
        1. Construir:
            ➔ Entorno de desarrollo
            ➔ Dependencias
            ➔ Entorno de ejecución
            ➔ Equivalencia con entorno productivo
            ➔ Servicios externos
        2. Distribuir:
            ➔ Divergencia de repositorios
            ➔ Divergencia de artefactos
            ➔ Versionado
            ➔ Equivalencia con entorno productivo
            ➔ Servicios externos
        3. Ejecutar:
            ➔ Dependencias de aplicación
            ➔ Compatibilidad del entorno productivo
            ➔ Disponibilidad de servicios externos
            ➔ Recursos de hardware
# Class#3
    Virtualización
        Problemas de las VMs
           Peso:
               En el orden de los GBs. Repiten archivos en común. Inicio lento.
           Costo de administración:
               Necesita mantenimiento igual que cualquier otra computadora.
           Múltiples de formatos:
               VDI, VMDK, VHD, raw, etc.
        Containerización
           ➔ Flexibles
           ➔ Livianos
           ➔ Portables
           ➔ Bajo acoplamiento
           ➔ Escalables
           ➔ Seguros
# Class#4
    Preparando tu entorno de trabajo
        docker run hello-world;
        docker info;
# Class#5
    [Bonus] Play with Docker
# Class#6
    Qué es y cómo funciona Docker
# 2. Contenedores
# Class#7
    Primeros pasos: hola mundo
       ➔ docker run hello-world;
# Class#8
    Conceptos fundamentales de Docker: contenedores
# Class#9
    Comprendiendo el estado de Docker
       ➔ docker inspect CONTAINER ID;
       ➔ docker inspect NAME;
       ➔ docker run --name hello-sc hello-world;
       ➔ docker rename hello-sc helo;
       ➔ docker container prune;<!-- Remove all containers. -->
# Class#10
    El modo interactivo
       ➔ docker run ubuntu;<!-- Create docker with Ubuntu. -->
       ➔ docker run -it ubuntu; <!-- Running container in interactive mode-->
# Class#11
    Ciclo de vida de un contenedor
       ➔ docker run --name SO -d ubuntu tail -f /dev/null;
       ➔ docker exec -it ${nameContainer} bash;
       ➔ docker inspect --format '{{.State.Pid}}' ${nameContainer};
# Class#12
# Exponiendo contenedores
    ➔ docker run -d --name proxy nginx;      
    ➔ docker run --name proxy -p 8080:80 nginx;
                                   |   |__
                               Local Port | 
                                    Container port
    ➔ docker logs -f proxy;
    ➔ docker logs --tail -f proxy;
# 3. Datos en Docke
# Class#13
    Bind mounts
       ➔ docker rm -f ${nameContainer};
       ➔ docker run -d --name dataBaseMongo -v ~/Documents/github/CursoDeDocker/dockerData:/data/db mongo;
       ➔ docker run -d --name ${nameContainer} -v ${localPath}:${containerPath} ${nameContainer] ${RemoteContainer};
            mongo
            show dbs
            use nameNewDb
            db.users.insert({"nombre":"name", "":"", "":"", "":""})
            db.users.find()
# Class#14
    Volúmenes
       ➔ docker volume ls;
       ➔ docker volume create ${nameContainer};
       ➔ docker run -d --name ${nameContainer} --mount src=${nameVolume},dst=/data/db mongo
       ➔ docker run -d --name ${nameContainer} --mount src=${nameVolume},dst=${containerPath} ${RemoteContainer};
       ➔ docker inspect ${nameContainer};
# Class#15
    Insertar y extraer archivos de un contenedor
       ➔ docker run -d --name ${nameContainer} {RemoteContainer} tail -f /dev/null;
       ➔ docker cp ${LocalNameFile} copytest:/${DirRempteName}/${RemoteFileName};
       ➔ docker cp text.log ubuntu:/test/log.log
       ➔ docker cp  ${nameContainer}:/${DirRemoteName} ${DirLocalName};
       ➔ docker cp ubuntu:/test/log.log:/text.log 
# 4. Imágenes
# Class#16
    Conceptos fundamentales de Docker: imágenes
       ➔ docker image ls;
            Imagenes: plantillas o moldes a partir de la que se crean contenedores.
       ➔ docker pull ubuntu:${tag};
# Class#17
    Construyendo una imagen propia
       ➔ docker build -t ubuntu:platzi ~/Documents/github/CursoDeDocker/dockerFiles;
       ➔ docker build -t ubuntu:${tagName} .;
       ➔ docker run -it ubuntu:${tag};
       ➔ docker tag ${REPOSITORY}:${TAG} ${propietario}/${so}:${tag};
       ➔ docker push gsuscastelsc/ubuntu:platzi;
# Class#18
    El sistema de capas
       ➔ docker history ubuntu:platzi;
       ➔ dive ubuntu:platzi;
# 5. Docker como herramienta de desarrollo**    
# Class#19
    Usando Docker para desarrollar aplicaciones
       ➔ git clone https://github.com/platzi/docker;
       ➔ docker build -t platziapp .; 
       ➔ docker run --rm -p 3000:3000 platziapp;
# Class#20
    Aprovechando el caché de capas para estructurar correctamente tus imágenes
       ➔ docker run --rm -p 3000:3000 -v /home/sc/Documents/github/CursoDeDocker/index.js:/usr/src/index.js platziapp
# Class#21
    Docker networking: colaboración entre contenedores
       ➔ docker network ls;
       ➔ docker network create --attachable(permite que otros contenedores se conecten) platziNet;
       ➔ docker network inspect platziNet;
       ➔ docker run -d --name db mongo;
       ➔ docker network connect platziNet db;
       ➔ docker run -d --name app -p 3000:3000 --env(asignar valiables de entorno) MONGO_URL=mongodb://db:27017/test platziapp;
       ➔ docker network connect platziNet app;
# 6. Docker Compose: la herramienta todo en uno
# Class#22
    Docker Compose: la herramienta todo en uno
        Install dockerCompose:
            ➔  sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose;
            ➔ sudo chmod +x /usr/local/bin/docker-compose;
            ➔ docker-compose --version;
        Up docker compose:
            ➔ docker-compose up;
            ➔ docker-compose up -d;
# Class#23
    Subcomandos de Docker Compose
       ➔ docker-compose ps;
       ➔ docker-compose logs -f ${nameContainer};
       ➔ docker-compose exec ${nameContainer} bash;
       ➔ docker-compose down;
# Class#24
    Docker Compose como herramienta de desarrollo
       ➔ docker-compose build;
# Class#25
   **Compose en equipo: override
       ➔ touch docker-compose.override.yml;
       ➔ docker-compose down;
       ➔ docker-compose up -d --scale app=2;
# 7. Doker Avanzado
# Class#26
    Administrando tu ambiente de Docker
       ➔ docker ps -a;
       ➔ docker container prune;<!-- Remove all containers. -->
       ➔ docker rm -f $(docker ps -aq);
       ➔ docker system prune;<!-- Remove all containers. example: tag none-->
       ➔ docker rmi -f $(docker images -aq);
       ➔ docker volume prune;
       ➔ docker network prune
       ➔ docker stats;
       ➔ docker run -d --name ${name} --memory 1g ${tag};
# Class#27
    Deteniendo contenedores correctamente: SHELL vs. EXEC
       ➔ docker ps -l;
       ➔ docker kill looper;
       ➔ docker exec -ti looper ps -ef;
# Class#28
    Contenedores ejecutables: ENTRYPOINT vs CMD
       ➔ run -d --name pinger ping google.com;
# Class#29
    El contexto de build
       ➔ touch .dockerignore;
# Class#30
    Multi-stage build
       ➔ docker build -t prodapp -f build/production.Dockerfile . ;
# Class#31
    Docker-in-Docker
       ➔ docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock docker:19.03.12;
# 8. Cierre
# Class#32
    Cierre del curso
# Notes
    Commands:
       ➔ docker info
       ➔ docker --version
       ➔ docker run hello-world
       ➔ docker images
       ➔ docker run: 
            Realizaa 2 acciones, 
                1. Crea el contenedor
                2. Ejecuta el contenedor
       ➔ Banderas: 
            docker run -it: 
             ➔ -i: STDIN del contenedor.             ➔ -t: Indica que se requiere una pseudo terminal.
             ➔ -d: Ejecutar contenedores de fondo(background)
       ➔ docker attach 6a33(idContainer or name)     
    Imagen:
       ➔ Es una plantilla de lectura, apartir de la que se crean los contenedores.
    Cliclos de Vida:
       ➔ Se crea el contenedor a partir de una imagen
       ➔ Se ejecuta un proceso determinado en el contenedor
       ➔ El proceso finaliza y el contenedor se detiene
       ➔ Se destruye el contenedor
    Cliclos de Vida avanzado:
       ➔ Se crea el contenedor a partir de una imagen
       ➔ Se ejecuta un proceso determinado en el contenedor
       ➔ Realizar acciones dentro del contenedor
       ➔ Detener el contenedor
       ➔ Lanzaar el contenedor nuevamente
    Tips:
        timedatectl set-timezone America/Bogota
        sudo /etc/init.d/docker start || sudo service docker start || /etc/init.d/docker start
    How install:
        weblogic:
            ➔ docker login -u jesuscastellanospaez@gmail.com
            ➔ docker run -d --network host --name wl -v /root/weblogic:/u01/oracle/properties container-registry.oracle.com/middleware/weblogic:12.2.1.3
            ➔ docker exec -it wl bash
            ➔ cd /u01/oracle/user_projects/domains/base_domain/nodemanager
            ➔ sed -i 's/SecureListener=true/SecureListener=false/g' nodemanager.properties
            ➔ cat nodemanager.properties
            ➔ cd /u01/oracle/user_projects/domains/base_domain/bin && nohup ./startNodeManager.sh > nodemanager.log 2>&1 &
            ➔ cd /u01/oracle/user_projects/domains/base_domain/autodeploy
            ➔ java weblogic.Deployer -adminurl t3://167.172.141.179:9005 -username weblogic -password Bolivar2021* -deploy -source /u01/oracle/user_projects/domains/base_domain/TestSegurosBolivar-1.2.war -targets Server-0
               java weblogic.Deployer -adminurl t3://167.172.141.179:9005 -username weblogic -password Bolivar2021* -deploy -source /u01/oracle/user_projects/domains/base_domain/TestSegurosBolivar-1.2.war -targets AdminServer
               java -cp ${pathWlClient} weblogic.Deployer -debug -remote -verbose -name ${war} -targets ${target} -adminurl t3s://${urlConsola} -user ${USERNAME} -password ${PASSWORD} -deploy
               java -cp ${pathWlClient} weblogic.Deployer -adminurl t3s://${urlConsola} -username ${userW} -password ${passW} -deploy -source ${war} -targets ${target} 


                java -cp /opt/wlfullclient.jar weblogic.Deployer -adminurl t3://167.172.141.179:9005 -username weblogic -password Bolivar2021* -deploy -source /u01/oracle/user_projects/domains/base_domain/TestSegurosBolivar.war -targets Server-0
                
               java -cp ${pathWlClient} weblogic.Deployer -debug -remote -verbose -name ${war} -targets ${target} -adminurl t3://${urlConsola} -user ${userW} -password ${passW} -deploy -stage -upload


               java -cp /opt/wlfullclient.jar weblogic.Deployer -adminurl t3://167.172.141.179:9005 -username weblogic -password Bolivar2021* -deploy -source /u01/oracle/user_projects/domains/base_domain/TestSegurosBolivar.war -targets Server-0
        
        Oracle Data Base:
            docker login container-registry.oracle.com;
            docker run -d -it --name bd -p 1521:1521 -p 2222:22 -v OracleDBData:/ORCL container-registry.oracle.com/database/enterprise:19.3.0.0 tail -f /dev/null;
            docker run -d --name bd -p 1521:1521 -p 2222:22 container-registry.oracle.com/database/enterprise:latest;
            docker log db;
        Postgres: 
            ➔ docker run -d -p 5432:5432 --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword postgres -c shared_buffers=256MB -c max_connections=200
        Jenkins:
             docker build -t gsuscastelsc/jenkins:0.0.x .;
            docker run --privileged -d --name jenkinsSB -p 9999:8080 -v /var/run/docker.sock:/var/run/docker.sock gsuscastelsc/jenkins:0.0.6
            sudo /etc/init.d/jenkins start
        mysql:
            mysql -h localhost -u root -pexample;
# Clear:
    docker rm -f $(docker ps -aq) && docker rmi -f $(docker images -aq);
# Links
    Insall dockerCompose:
        https://docs.docker.com/compose/install/
    Wagodman:
        https://github.com/wagoodman/dive
    Hub Docker:
        https://hub.docker.com/
    Play with Docker:
        https://labs.play-with-docker.com/
    Slides Curso Docker:
        https://static.platzi.com/media/public/uploads/slides-curso-docker_d04a71e1-4aa5-4b52-9dea-ba3ad2724202.pdf
