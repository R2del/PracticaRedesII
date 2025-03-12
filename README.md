# PracticaRedesII

Creación de la Estructura del Proyecto:

Carpeta Principal: Creaste una carpeta llamada docker-nginx-phpmyadmin.
Subcarpetas: Dentro de docker-nginx-phpmyadmin, creaste:
nginx: Para la configuración de Nginx.
app: Para los archivos PHP.
2. Creación del Archivo docker-compose.yml:

En la carpeta docker-nginx-phpmyadmin, creaste un archivo docker-compose.yml con la siguiente configuración:

YAML

services:
  mysql_db:
    image: mysql:8.0
    container_name: mysql_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: my_database
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    volumes:
      - mysql_data:/var/lib/mysql
    ports:
      - "3306:3306"

  phpmyadmin:
    image: phpmyadmin:latest
    container_name: phpmyadmin
    restart: always
    environment:
      PMA_HOST: mysql_db
      MYSQL_ROOT_PASSWORD: root
    ports:
      - "8081:80"
    depends_on:
      - mysql_db

  nginx_server:
    image: nginx:latest
    container_name: nginx_server
    restart: always
    ports:
      - "8080:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
      - ./app:/var/www/html
    depends_on:
      - php_fpm

  php_fpm:
    image: php:8.1-fpm
    container_name: php_fpm
    restart: always
    volumes:
      - ./app:/var/www/html

volumes:
  mysql_data:
3. Configuración de Nginx:

En la carpeta nginx, creaste un archivo default.conf con la configuración de Nginx.
4. Creación de un Archivo PHP de Prueba:

En la carpeta app, creaste un archivo index.php para probar la configuración.
5. Inicio de los Contenedores:

Abriste PowerShell y navegaste a la carpeta docker-nginx-phpmyadmin.
Ejecutaste el comando: docker-compose up -d
6. Verificación de los Servicios:

Verificaste que los servicios estuvieran funcionando correctamente accediendo a:
http://localhost:8080 (para Nginx).
http://localhost:8081 (para phpMyAdmin).
7. Resolución de Problemas (La "Carpeta Fantasma"):

Problema: Se creó automáticamente una carpeta default.conf en la carpeta nginx, impidiendo el montaje correcto del archivo default.conf.
Pasos de Solución:
Detención y eliminación de contenedores, redes, imágenes y volúmenes.
Reinicio de Docker Desktop y la computadora.
Ejecución con --remove-orphans.
Aislamiento del problema en un nuevo proyecto.
Verificación del sistema de archivos y permisos.
Modificación del montaje de volúmenes (usando rutas absolutas y scripts de inicio).
Creación de un archivo .dockerignore.
Verificación de logs y uso de herramientas de diagnóstico.
Reinstalación de Docker Desktop (si fuera necesario).
