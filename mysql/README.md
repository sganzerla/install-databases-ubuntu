# install-mysql-ubuntu

## Install Mysql Ubuntu 20.04

    ```
    sudo apt install mysql-server

    sudo mysql_secure_installation
    ```

Writter `y` for questions in terminal and create password

## Config User Root

Tutorial by [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04-pt)

Now change config auth mysql plugin `auth_socket` for `caching_sha2_password`

    ```
    sudo mysql

    SELECT user,authentication_string,plugin,host FROM mysql.user;

    ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';

    FLUSH PRIVILEGES;

    SELECT user,authentication_string,plugin,host FROM mysql.user;

    exit

    ```

## Create User

Created user and grant all privileges

    ```
    sudo mysql -u root -p

    CREATE USER 'sammy'@'localhost' IDENTIFIED BY 'password';

    GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;

    exit
    ```

## Install Workbench

Tutorial by [Blog Edivado Brito](https://www.edivaldobrito.com.br/como-instalar-o-instalar-mysql-workbench-no-ubuntu-e-derivados/)

     ```
     wget http://cdn.mysql.com/Downloads/MySQLGUIToolsmysql-workbench-community_8.0.20-1ubuntu2004_amd64.deb -O mysql-workbench-community.deb
     sudo dpkg -i mysql-workbench-community.deb
     sudo apt-get -f install
     ```

Remove Workbench:

    ```
    sudo apt-get remove mysql-workbench-community-auto-remove
    ```

## Remove Mysql

Tutorial by [lgsalles](https://lgsalles.me/como-remover-completamente-o-mysql-do-ubuntu/)

    ```
    sudo apt-get purge mysql-server mysql-client mysql-common mysql-server-core-* mysql-client-core-*
 
    sudo apt-get remove mysql-server mysql-client mysql-common mysql-server-core-* mysql-client-core-*
 
    sudo rm -rf /etc/mysql /var/lib/mysql
 
    sudo apt-get autoremove
 
    sudo apt-get autoclean
    ```
