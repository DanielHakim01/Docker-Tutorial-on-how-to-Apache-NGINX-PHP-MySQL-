# How to use MySQL in Docker container

1. Go to the docker hub website https://hub.docker.com/
2. Search for the image that we want to use(MySQL)
3. Scroll until you see how to use this image
4. copy the code
5. ```docker run --name some-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag```
6. Open cmd
7. Log in into the Docker first by typing ```docker log in```
8. Put your username and password according to your docker account
9. Type in this command ```docker run --name some-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag```
10. You can also change the name and the password according to what you want
11. ![](gp/Screenshot%20(289).png)
12. Wait until it completed
13. ![](gp/Screenshot%20(291).png)
14. If it says file already existed then you can start the existing by typing ```docker start some-mysql``` or try to change the name in the previous command
15. To check the status of the container you can run the command ```docker ps```
16. This will show all the images that are running
17. ![](gp/Screenshot%20(292).png)
18. The status should be UP -s for example UP 3s
19. Open tour MySQL workbench or if you do not have MySQL workbench just use whatever IDE you have
20. You can download MySQL workbench from https://www.mysql.com/products/workbench/
21. Click create a new connection
22. ![](gp/Screenshot%20(293).png)
23. Set the correction name to Local Docker
24. Just leave the hostname
25. Username enter root
26. For the password put in the same password you have provided in the cmd earlier in the line ```-e MYSQL_ROOT_PASSWORD=my-secret-pw```
27. If no changes made then by default it is ```my-secret-pw```
28. ![](gp/Screenshot%20(294).png)
29. Then click test connection
30. If there is no error then click ok
31. ![](gp/Screenshot%20(295).png)
32. Click on the new connection that you have created
33. ![](gp/Screenshot%20(296).png)
34. You will be redirected into the query
35. ![](gp/Screenshot%20(297).png)
36. Enter some simple query to test
37. ![](gp/Screenshot%20(298).png)
38. Congratulations you have succesfully created a connection to MySQL using Docker container
39. If you want to stop using it open cmd and type ```docker stop some-mysql``` 
40. ![](gp/Screenshot%20(299).png)
