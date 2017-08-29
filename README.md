Goal:
Set up Docker running WordPress locally where posts and plugins and stuff persist through machine restarts.

To Do:
- Step up Docker
- Step Up WordPress
- Figure out how to make it persist through machine restarts
- ???
- Profit

Steps I took:

Step One - Install Docker

Step Two - [Follow this Guide](https://docs.docker.com/compose/wordpress/)
  -- Make a file for environment variables, [docker compose uses .env file.](https://docs.docker.com/compose/environment-variables/#the-env-file)

Step Three - Set up WordPress User and create a new blog posts, make sure it's on localhost

![](http://i.imgur.com/IowISlV.png)

Step Four - Rip it down with `docker-compose down` (not using the `--volumes` flag should let the database persist)

Step Five - Bring it back to life with a little bit of Evanescence and a lot of `docker-compose up -d`

Step Six - Refresh and smile =)

Questions I had:

Where do I put all my passwords so I can put this on GitHub

-- Answer: Environment Variables are used to store your secrets. They're pretty dope, and you should use them, and use .gitignore to hide your .env files.

 What does the -d flag do in docker-compose

  -Answer: It says it makes it run in detached mode. [This article](https://stackoverflow.com/questions/34029680/docker-detached-mode) goes over it a bit. From what I understand when you run in detached mode your STDIN, STDOUT, and STDERR don't get attached to the docker container (so you can continue to run commands and not get thrown into the container?) but when you run in the default mode foreground your terminal becomes attached to the container.

Where does this volume go?

 --Answer: `docker volume ls` shows all the volumes running. [This Docker article](https://docs.docker.com/engine/admin/volumes/volumes/) explains how Volumes work and they live somewhere in /var/lib/docker/. There are different types of storage you can use also, such as tmpfs, bind (old), and named volumes which are used here. (tmpfs is [volatile storage](https://docs.docker.com/engine/admin/volumes/tmpfs/) that exists in your tmpfs or temporary filesystem and will not persist past a restart)

Cool, I get what temporary storage is, what's the different between bind mounts and named mounts?

--Answer: I think it's just how they're referenced? [This article](https://docs.docker.com/engine/admin/volumes/bind-mounts/) states:

*The file or directory is referenced by its full or relative path on the host machine. By contrast, when you use a volume, a new directory is created within Docker’s storage directory on the host machine, and Docker manages that directory’s contents.*

I'm sure there's more to it but I'm not finding anything on it yet.
