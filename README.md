# ASGBD-Practica2.3

### 1. Clientes instalados, versiones, origen y dependencias
- Oracle Database:
  - SQL Developer: Versión 26.2.0. Requisito instalar default-jdk y el paquete openjfx para la interfaz gráfica
  - VS Code: Extensión oficial "Oracle SQL Developer for VS Code"
  - SQL*Plus y SQLcl: Versión 23.26.4. Requeria configurar variables de entorno y la instalación de la librería libaio1t64

- PostgreSQL:
  - Cliente de terminal: Paquete postgresql-client, vesión v16
  - Cliente gráfico (pgAdmin 4): Instalado desde el repositorio oficial, Requeria utilidades como curl y gnupg

- MariaDB:
  - Cliente de terminal: Paquete mariadb-client
  - Cliente web (phpMyAdmin): Requeria el stack web completo (apache2, php, y módulos como php-mysql y php-mbstring)


### 2. Comandos principales de configuración utilizados

#### _Clientes para Oracle Database_
- SQL Developer (Cliente gráfico):
  - `sudo apt install default-jdk unzip libopenjfx-java`: Instalé Java, la herramienta para descomprimir y las librerías gráficas de JavaFX que necesitaba para que la interfaz del programa arrancara en Linux
  - `sudo unzip sqldeveloper-26.2.0.186.2220-no-jre.zip -d /opt/`: Para descomprimir la versión genérica de SQL Developer en el directorio `/opt`
  - `/opt/sqldeveloper/sqldeveloper.sh`: Script para lanzar el programa gráfico

- Visual Studio Code y extensión:
  - `sudo apt install ./code_1.143.0-1792533444_amd64.deb`: Instalé el paquete `.deb` de VS Code desde la carpeta de Descargas

- SQL*Plus y SQLcl (Clientes de terminal):
  - `mkdir -p ~/oracle-client`: Creé un directorio para guardar las herramientas de Oracle
  - `unzip instantclient-basic-...zip -d ~/oracle-client` y `unzip instantclient-sqlplus-...zip -d ~/oracle-client`: Para descomprimir los paquetes Basic y SQL*Plus en el mismo directorio
  - `export LD_LIBRARY_PATH="$HOME/oracle-client/instantclient_23_26:$LD_LIBRARY_PATH"` y `export PATH="$HOME/oracle-client/instantclient_23_26:$PATH"`: Añadí la ruta de la carpeta que extraí a las variables de entorno para que el sistema reconociera los comandos
  - `sudo apt install libaio1t64`: Instalé la librería que requiere Oracle para funcionar en las versiones modernas de Linux
  - `sudo ln -s /usr/lib/x86_64-linux-gnu/libaio.so.1t64 /usr/lib/x86_64-linux-gnu/libaio.so.1` y `sudo ldconfig`: Creé un enlace simbólico manual y reinicie la librerías para que Oracle pudriera encontrar el archivo con el nombre antiguo que estaba buscando
  - `echo 'export PATH="$HOME/sqlcl/sqlcl/bin:$PATH"' >> ~/.bashrc`: Añadí la ruta del ejecutable de SQLcl al archivo de configuración de la terminal

#### _Clientes para PostgreSQL_
- psql (Cliente de terminal):
  - `sudo apt update` y `sudo apt install postgresql-client`: Actualicé los repositorios, instalé el paquete del cliente de PostgreSQL

- pgAdmin 4 (Cliente gráfico):
  - `sudo apt install curl gnupg lsb-release`: Instalé las herramientas que se necesitaban para descargar y añadir repositorios externos
  - `curl -fsS https://www.pgadmin.org/... | sudo gpg --dearmor -o /etc/apt/keyrings/...`: Descargué la clave de seguridad de pgAdmin y la guardé
  - `sudo sh -c 'echo "deb [...] https://ftp.postgresql.org/.../$(. /etc/os-release && echo $UBUNTU_CODENAME) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list'`: Añadí el repositorio de pgAdmin
  - `sudo apt install pgadmin4-desktop`: Instalé la aplicación de escritorio

#### _Clientes para MariaDB_
- mariadb-client (Cliente de terminal)
  - `sudo apt install mariadb-client`: Instalé el cliente de MariaDB

- phpMyAdmin (Cliente web)
  - `sudo apt install apache2 php php-mysql php-mbstring php-zip php-gd php-curl phpmyadmin`: Instalé el servidor web Apache, el lenguaje PHP, los módulos necesarios y la herramienta phpMyAdmin
  - `sudo phpenmod mbstring`: Activé el módulo `mbstring` de PHP
  - `sudo a2enconf phpmyadmin` y `sudo systemctl reload apache2`: Activé la configuración de phpMyAdmin en Apache y reinicie el servidor web para que se apliquen los cambios y poder acceder desde el navegador


### 3. Pruebas de conexión realizadas
- Consola Oracle
  - [imagen]
  - _Oracle Database 23ai Free_
  - **Servidor:** `localhost`
  - **Puerto:** `1521`
  - **Servicio:** `FREEPDB1`
  - **Usuario:** `orauser`

- Gráfico Oracle
  - [imagen]

- Consola PostgreSQL
  - [imagen]
  - _PostgreSQL_
  - **Servidor:** `10.0.2.15`
  - **Puerto:** `5432`
  - **Base de datos:** `dbpg`
  - **Usuario:** `pguser`

- Gráfico PostgreSQL
  - [imagen]

- Consola MariaDB
  - [imagen]
  - _MariaDB_
  - **Servidor:** `localhost`
  - **Puerto:** `3306`
  - **Base de datos:** `dbm`
  - **Usuario:** `muser`

- Web MariaDB
  - [imagen]


### 4. Problemas surgidos y soluciones aplicadas
- Error de versión en SQL Developer: Descargue el ZIP que incluía el JDK de Windows
  - Solución: Borrar la instalación y descargar el ZIP genérico no-jre para "Otras plataformas"

- Librería que faltaba en SQL*Plus: Un error por falta de la librería libaio.so.1
  - Solución: Instalé el paquete moderno libaio1t64 y creé un enlace simbólico manual (sudo ln -s) hacia el nombre antiguo que buscaba Oracle.


### 5. Fuentes consultadas y evidencias
- Guion de la práctica proporcionado
- Documentación oficial de descargas de Oracle, PostgreSQL y MariaDB
