- craft@HP:~$ docker pull node:15.14
- 15.14: Pulling from library/node
- bfde2ec33fbc: Pull complete
- 787f5e2f1047: Pull complete
- 7b6173a10eb8: Pull complete
- dc05be471d51: Pull complete
- 55fab5cadd3c: Pull complete
- bd821d20ef8c: Pull complete
- 6041b69671c6: Pull complete
- 989c5d2d2313: Pull complete
- 4b57d41e8391: Pull complete
- Digest: sha256:608bba799613b1ebf754034ae008849ba51e88b23271412427b76d60ae0d0627
- Status: Downloaded newer image for node:15.14
- docker.io/library/node:15.14
- craft@HP:~/data$ docker run --name first_node -v /home/craft/data:/var/first/data -i -d node:15.14
- 925aefe889cbcb59c991bd9f147188b75e8de98af6d2dcd2bcb45c9229c2714c
- craft@HP:~/data$ docker run --name second_node -v /home/craft/data:/var/second/data -i -d node:15.14
- f93f0e131d2db666ebcfab642278daa53d25ad5ee359b0c417e908f3004922f5
- craft@HP:~/data$ docker ps
- CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
- f93f0e131d2d node:15.14 "docker-entrypoint.s…" 9 seconds ago Up 4 seconds second_node
- 925aefe889cb node:15.14 "docker-entrypoint.s…" 26 seconds ago Up 22 seconds first_node
- craft@HP:~/data$ docker exec -i -t first_node /bin/bash
- root@925aefe889cb:/# echo "Привет мир." > Hello_world.txt
- root@925aefe889cb:/# cd var
- root@925aefe889cb:/var# cd first
- root@925aefe889cb:/var/first# cd data
- root@925aefe889cb:/var/first/data# echo "Привет мир." > Hello_world.txt
- root@925aefe889cb:/var/first/data# exit
- craft@HP:~/data$ docker exec -i -t second_node /bin/bash
- root@f93f0e131d2d:/# cd var
- root@f93f0e131d2d:/var# cd second
- root@f93f0e131d2d:/var/second# cd data
- root@f93f0e131d2d:/var/second/data# ls
- Hello_world.txt Hello_world_twice.txt
- root@f93f0e131d2d:/var/second/data# cat Hello_world.txt
- Привет мир.
- root@f93f0e131d2d:/var/second/data# cat Hello_world_twice.txt
- Привет мир.
- Привет мир.
- root@f93f0e131d2d:/var/second/data#
- root@f93f0e131d2d:/var/second/data# exit
- craft@HP:~/data$ docker stop first_node second_node
- first_node
- second_node
- craft@HP:~/data$ docker rm first_node second_node
- first_node
- second_node
