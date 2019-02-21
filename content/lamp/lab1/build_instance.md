+++
title = "1.1 - Build the LAMP instance"
weight = 10
+++

The first step in deploying the sample application is creating a LAMP stack instance in Lightsail. 

{{% notice tip %}}
Be sure to create all the resources for this workshop in the same region
{{% /notice %}}

* From the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> click ***Create Instance***

    ![](../../images/1-1-1.jpg?classes=border)

* Make sure that ***Linux/Unix*** is selected under ***Select a platform***, and then under ***Blueprint*** choose ***LAMP (PHP5)***
    
    ![](../../images/lamp-blueprint.jpg?classes=border)

* Click '+Add Launch Script' and paste the code below into the window. These commands will run the first time the instance boots up.

        echo "removing default website"
        cd /opt/bitnami/apache2/htdocs 
        rm -rf *

        echo "cloning github repo"
        git clone -b loft https://github.com/mikegcoleman/todo-php .

        echo "setting ownership on settings file"
        chown bitnami:daemon connectvalues.php
        chmod 666 connectvalues.php

        echo "adding db password to settings file"
        sed -i.bak "s/<password>/$(cat /home/bitnami/bitnami_application_password)/;" /opt/bitnami/apache2/htdocs/connectvalues.php

        echo "creating tasks database"
        cat /home/bitnami/htdocs/data/init.sql | /opt/bitnami/mysql/bin/mysql -u root -p$(cat /home/bitnami/bitnami_application_password)
    
    The script does the following:

    * The Bitnami image has a default web page installed which needs to be removed. The script starts by changing into the root directory of the web server (`/opt/bitnami/apache2/htdocs`) and deleting the existing files

    * Next the script clones the application code to render the web front-end from the lab's Github repo

    * To ensure that the PHP application can write to the settings file (`connectvalues.php`), the script changes the ownership (`chown`) on the file to match the account under which the Apache web server runs, as well as ensuring that account can write to the file (via `chmod`)

    * Each Bitnami-based instance generates a unique password for the locally installed MySQL database, this next command in the script opens the settings file and updates it with this password (which can be found at `/home/bitnami/bitnami_application_password`)

    * Finally the script issues a set of SQL commands to MySQL (via the MySQL command line tool) that will initialize the local database

* Name the instance ***php-fe-1***

    ![](../../images/lamp-name.jpg?classes=border)

* Click ***Create instance***

    ![](../../images/lamp-create.jpg?classes=border)

