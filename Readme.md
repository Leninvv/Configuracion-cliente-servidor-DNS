
# Comandos apt-install

- apt install sudo
- apt install iputils-ping
- apt install iputils-tracepath
- apt install traceroute
- apt install mtr
- apt install net-tools
- apt install ifupdown
- apt install dnsutils
- apt install ifplugd
- apt install whois
- apt install curl
- apt install wget

# Comprobación dig

 dig google.es

; <<>> DiG 9.16.1-Ubuntu <<>> google.es  
;; global options: +cmd  
;; Got answer:  
;; ->>HEADER<<- opcode: QUERY, status: SERVFAIL, id: 64882  
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:  
; EDNS: version: 0, flags:; udp: 1232  
; COOKIE: 06a64a5d38f98a7001000000617027b88b58323ca29ea502 (good)  
;; QUESTION SECTION:  
;google.es.                     IN      A

;; Query time: 520 msec  
**;; SERVER: 172.23.0.3#53(172.23.0.3)**   
;; WHEN: Wed Oct 20 16:29:12 CEST 2021  
;; MSG SIZE  rcvd: 66  

# Explicación Docker-compose.yml

version: "3.3" #Elegimos la versión del docker-compose.  
services: #Iniciamos la zona de configuración de contenedores.  
  asir_bind9: #Creamos un contenedor llamado asir_bind9  
    image: internetsystemsconsortium/bind9:9.16 #usamos la imagen aquí escrita  
    network_mode: bridge #tipo de network en puente  
    ports: #configuramos los puertos  
      - 53:53 #el puerto 53 del host corresponde con el puerto 53 del contenedor  
    volumes: #configuramos los volumenes  
      - conf:/etc/bind #volumen conf corresponde a /etc/bind  
      - options:/var/cache/bind #volumen options corresponde a /var/cache/bind  
      - secondaryzones:/var/lib/bind #volumen secondaryzones corresponde a /var/lib/bind  
      - logfiles:/var/log #volumen logfiles corresponde a /var/log  
  asir_cliente: #Creamos un segundo contenedor llamado asir_cliente  
    image: leninvv/cliente_ubuntu:net-tools #usamos esta imagen  
    network_mode: bridge #tipo de network en puente
    stdin_open: true  # docker run -i  
    tty: true         # docker run -t  
    dns: #configuramos el dns que va a usar el contenedor  
      - 172.17.0.2  #ip del dns  
volumes: #creamos los volumenes  
  conf: #volumen conf  
    external: true  #condición external que mantiene los cambios realizados a los archivos del volumen  
  options: #volumen options  
  secondaryzones: #volumen secondaryzones  
  logfiles: #volumen logfiles  


# Iniciar docker-compose

- docker-compose up  

Esto crea los dos contenedores con las preferencias indicadas en el docker-compose.  
Para parar los contenedores docker-compose stop y para iniciarlos de nuevo docker-compose start.

# Modificar configuración Bind9

Para modificar la configuración accedemos al volumen conf que hemos creado previamente. Para esto en el docker accedemos a el con un contenedor de desarrollo y modificamos los archivos.  
Modificamos named.conf.options y cambiamos los forwarders así como el archivo named.conf.local en el cual añadimos las zonas que creamos nosotros.  
Una vez realizados los cambios reiniciamos el servicio de Bind9 para esto simplemente reiniciamos el contenedor y comprobamos que todo sigue en como lo dejamos.


