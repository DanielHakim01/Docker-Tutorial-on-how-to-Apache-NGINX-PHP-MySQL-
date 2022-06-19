# How to use PHP in Docker container
Pre- requisite 
-Ensure that Docker demons are installed on your computer.
-Basic knowledge of PHP and SQL queries.
-Fundamental understating of how to build and run Docker hub images from a Docker file.
-Understand how containers work.
-Basic knowledge on how to execute Docker and docker-compose commands.

Steps:

1.Download Docker and check current version to confirm that it had been installed

2.Check whether there is any container running. If there is container running remove it as we going to create a new container.( Remove command: docker container rm 
<container's name>)

![](gp/Windows%20PowerShell%2019_6_2022%207_15_40%20PM.png)

3.Create a project folder which contain a .yml file which in this tutorial we are going to create docker-compose.yml.

4.To set a docker-compose we need to select the docker version that we need to use and this project we use 3.8 version

5.To set up a PHP Apache container, you need to specify the following environments,
The container name - this is just a random name that you would like to name your PHP container.
For example container_name: php-apache.
The container image - this the official PHP image, the version of PHP Apache you want to use. In this case, we are pulling image: php:8.0-apache from the Docker hub.
The volume - this will set up your present working src directory for your code/source files. If you were to run a PHP script, that file would have to be in that directory.
The port numbers- This defines the ports where the script will run from. It will set up an Apache server port mapping to the port on your local computer.
This is the example of  docker-compose.yml file.

![](gp/docker-compose.yml%20-%20Docker_project%20-%20Visual%20Studio%20Code%2019_6_2022%207_29_42%20PM.png)

6. Next, go to the termninal of the  project file directory that we have created and run  docker-compose up

![](gp/Windows%20PowerShell%2018_6_2022%206_07_10%20P)

7.Check docker desktop  engine and they will be a container running
![](gp/Containers%20-%20Docker%20Desktop%2018_6_2022%206_07_45%20PM.png)

8.To ensure the container is set to execute the PHP scripts, open your defined local host post in the browser,i.e., http://localhost:8000/.
![](gp/403%20Forbidden%20-%20Google%20Chrome%2018_6_2022%206_08_44%20PM.png)

9. Create index.php file in php/src directory and echo some coding to make sure that we are in a right track and refresh the browser.
  ![](gp/403%20Forbidden%20-%20Google%20Chrome%2018_6_2022%206_10_47%20PM.png)
  
10.Let’s add the MySQL service into the docker-compose.yml file. To setup MySQL, we need to customize some environment, such as:

-Password authentication. To use and access a MySQL server, you need to set authentication environments that will allow you to access the defined MySQL server and its services, such as a database. We will use MYSQL_USER: MYSQL_USER and MYSQL_PASSWORD: MYSQL_PASSWORD to connect to MySQL and access the MYSQL_DATABASE: MYSQL_DATABASE.
A restart policy set to restart: always. This restarts the service whenever any defined configuration changes.
-We need to add some MySQL support tools inside the PHP container for the two services (db and php-apache) to work correctly. This tool includes mysqli. Inside your project directory, head to the /php folder, create a Docker file, name it Dockerfile and add the following PHP configurations.

FROM php:8.0-apache
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN apt-get update && apt-get upgrade -y

11.Now we need to build this custom image inside php-apache service in the docker-compose.yml file. PHP Apache also depends on the db service to connect to MySQL. We need to configure it by specifying a depends_on: environment.

This is how your docker-compose.yml file should look like.
 ![](gp/docker-compose.yml%20-%20Docker_project%20-%20Visual%20Studio%20Code%2019_6_2022%2011_14_30%20PM.png)
 
 12.Check docker to see if the mysql container is running
 ![](gp/Containers%20-%20Docker%20Desktop%2018_6_2022%206_42_47%20PM.png)
 
 13.Run this sql query script in index.php file and check the connection succesfulk or fail

<?php
//These are the defined authentication environment in the db service

// The MySQL service named in the docker-compose.yml.
$host = 'db';

// Database use name
$user = 'MYSQL_USER';

//database user password
$pass = 'MYSQL_PASSWORD';

// check the MySQL connection status
$conn = new mysqli($host, $user, $pass);
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
} else {
    echo "Connected to MySQL server successfully!";
}
?>

The  page will be like this :
 ![](gp/PHP%20Websites%20using%20Docker%20Containers%20with%20PHP%20Apache%20and%20MySQL%20_%20Engineering%20Education%20(EngEd)%20Program%20_%20Section%20-%20Google%20Chrome%2018_6_2022%206_44_19%20PM.png)

14.Insert this code in under services in .yml file
phpmyadmin:
    image: phpmyadmin/phpmyadmin
    ports:
        - '8080:80'
    restart: always
    environment:
        PMA_HOST: db
    depends_on:
        - db
        
15.       Open http://localhost:8080/ on the browser to access the PHPMyAdmin and enter username as root and MYSQL_PASSWORD_ROOT as password then you will redicrect to phpmyadmin page.
     ![](gp/phpMyAdmin%20-%20Google%20Chrome%2019_6_2022%2012_50_57%20AM.png)
     ![](gp/phpMyAdmin%20-%20Google%20Chrome%2019_6_2022%2012_51_25%20AM.png)
16.   Click MYSQL_DATABSE  to create table and enter this code 
   
   drop table if exists `users`;
   create table `users` (
   id int not null auto_increment,
   username text not null,
   password text not null,
  primary key (id)
 );
insert into `users` (username, password) values
    ("admin","password"),
    ("Muhd","this is my password"),
    ("Job","Malam Sunyi");   
    
   This will create below table 
    
   ![](gp/phpMyAdmin%20-%20Google%20Chrome%2019_6_2022%2012_56_38%20AM.png)

17. Write this sql query in the php and  refresh http://localhost:8000/ to view the results.
 
 ![](gp/localhost_8000%20-%20Google%20Chrome%2019_6_2022%2012_59_33%20AM.png)


