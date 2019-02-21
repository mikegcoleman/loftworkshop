+++
title = "3.1 - Reconfigure MySQL"
weight = 10
+++

In this section we'll update the application configuration to point to our highly-available Lightsail database. 

* From the <a href="https://lightsail.aws.amazon.com/ls/webapp/home/" target="_blank">Lightsail console home page</a> select ***Databases*** from the horizontal menu

    ![](../../images/databases-menu.jpg?classes=border)

* Click on the name of the Lightsail database you created earlier

* Under ***Connection details*** make copy the value for ***Endpoint***.

![](../../images/endpoint.jpg?classes=border)


* In the ToDo application click `settings` from the top menu


![](../../images/todo_settings.jpg?classes=border)

* Paste in the endpoint value of your Lightsail database under DB Hostname. Enter `dbmasteruser` for the DB Username, and `taskstasks` for the DB Password. Finally click save settings.

![](../../images/save_settings.jpg?classes=border)


* Test the new database by clicking `List Tasks` in the top menu. Since you have pointed the front-end at a the new database there shouldn't be any tasks to display. Also note at the bottom of the screen it should list your Lightsail database endpoint as value for `Database host`

{{% notice tip %}}
If your web app is still showing the previously deployed database (denoted by `localhost` as the database host), you may need to use either a new browser window or an incognito window. 
{{% /notice %}}

In a production environment you would now migrate the data from your local database to the Lightsail Database, but that is out of the scope of this lab. 
