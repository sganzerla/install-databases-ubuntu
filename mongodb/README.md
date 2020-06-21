# install-mongodb-ubuntu

## TODO incomplete tutorial

There are two forms of use do [MongoDB](https://www.mongodb.com/):

- using MongoDB Atlas cloud instance
- installation on your own machine

## MongoDB Atlas

For to can to use this resource is necessary create a account MongoDB. This service is available for use with free tier cluster by selecting a region with free tier of the AWS, Google Cloud or Azure.

For more details read official [documentation](https://www.mongodb.com/cloud/atlas).

## Installation (in Ubuntu 20.04)

 Tutorial by [howtoforge](https://www.howtoforge.com/how-to-install-and-use-mongodb-on-ubuntu-2004/)

- Gnupg package

        ```
        apt-get install gnupg -y
        ```

- Download and add the MongoDB GPG key

        ```
        wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | apt-key add -
        ```

- Add the MongoDB repository source.list

        ```
        echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-4.2.list
        ```

- Update the repository and install the MongoDB

        ```
        apt-get update -y
        apt-get install mongodb-org -y
        ```

- Start the MongoDB service and enable it to start at reboot

        ```
        systemctl start mongod
        systemctl enable mongod
        ```

- Get connection string MongoDB

        ```
        mongo --eval 'db.runCommand({ connectionStatus: 1 })'
        ```

- Alter method of compression of the output

    Change `disable` for `snappy` or `zlib`

        ```
        mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
        ```

### Create MongoDB Admin User

Tutorial by [Docs Mongodb](https://docs.mongodb.com/manual/tutorial/enable-authentication/)

Access console MongoDB

        ```
        mongo
        ```

### Configure security MongoDB

MongoDB default configuration file is located at /etc/mongod.conf. By default, each user will have access to all databases and perform any action. For production environments, it is recommended to enable the MongoDB authentication.

Edit file:

        ```
        nano /etc/mongod.conf
        ```

Add code:

        ```
        security:
        authorization: enabled
        ```

Restart service:

        ```
        systemctl restart mongod
        ```

## Remove install MongoDB

Tutorial by [An Integrated World](https://www.anintegratedworld.com/uninstall-mongodb-in-ubuntu-via-command-line-in-3-easy-steps/)

Stop service:

        ```
        sudo service mongod stop
        ```
