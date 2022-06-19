# How to use PHP in Docker container
Pre- requisite 
-Ensure that Docker demons are installed on your computer.
-Basic knowledge of PHP and SQL queries.
-Fundamental understating of how to build and run Docker hub images from a Docker file.
-Understand how containers work.
-Basic knowledge on how to execute Docker and docker-compose commands.

Steps:

1.Download Docker and check current version to confirm that it had been installed
2.Check whether there is any container running. If there is container running remove it as we going to create a new container.( Remove command: docker container rm <container's name>)
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
-We need to add some MySQL support tools inside the PHP container for the two services (db and php-apache) to work correctly. This tool includes mysqli.


