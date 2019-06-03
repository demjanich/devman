# Docker

If you accidentally removed your container with MySQL data trying to free up some space on the computer using such a command:

```
docker image prune
docker volume prune
```

you can still try to find your volume. 

For Mac use something like that (first command): 

Connect to tty on Docker for Mac VM: ```$ screen ~/Library/Containers/com.docker.docker/Data/vms/0/tty```

Disconnect that session but leave it open in background: ```Ctrl-a d```

List that session that's still running in background: ```screen -ls```

Reconnect to that session (don't open a new one, that won't work and 2nd tty will give you garbled screen): ```screen -r```

Kill this session (window) and exit: ```Ctrl-a k```

Ok. so first command opens an VM terminal. 

This is your volumes: ```# ls -la /var/lib/docker/volumes/```

Every volume folder has ```_data``` folder where all MySQL data stored. So try to find you old data by name of database:

```
# cd /var/lib/docker/volumes/
# find . -name "[your database name]" -print
```

If you find it in any of your volumes, thats good! Now you can start new container and check where is mounted:

```
docker ps
$ docker inspect -f '{{ .Mounts }}' [CONTAINER ID]
```

You get something like that:

```
$ docker inspect -f '{{ .Mounts }}' cd20a8c5f64b
[{volume 2d1486d0c348179082b5962a7c2eccaac68d0e62df26aaa0aa9b5d23f21247d5 /var/lib/docker/volumes/2d1486d0c348179082b5962a7c2eccaac68d0e62df26aaa0aa9b5d23f21247d5/_data /var/lib/mysql local  true }]
```

Now you can stop your new container. And copy data from old volume to the new volue.

```
cp -fR /var/lib/docker/volumes/[OLD VOLUME]/_data/[YOUR DATABASE] /var/lib/docker/volumes/[NEW VOLUME]/_data/[YOUR DATABASE]
cp -fR /var/lib/docker/volumes/[OLD VOLUME]/_data/mysql /var/lib/docker/volumes/[NEW VOLUME]/_data/mysql
cp -fR /var/lib/docker/volumes/[OLD VOLUME]/_data/mysql.ibd /var/lib/docker/volumes/[NEW VOLUME]/_data
cp -fR /var/lib/docker/volumes/[OLD VOLUME]/_data/ibdata1 /var/lib/docker/volumes/[NEW VOLUME]/_data
cp -fR /var/lib/docker/volumes/[OLD VOLUME]/_data/ib_logfile0 /var/lib/docker/volumes/[NEW VOLUME]/_data
cp -fR /var/lib/docker/volumes/[OLD VOLUME]/_data/ib_logfile1 /var/lib/docker/volumes/[NEW VOLUME]/_data
```

No you can start your docker container. If you use separate docker container with Adminer, ```down``` it and create new one, becase it can cash list of databases.

