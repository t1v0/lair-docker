# lair-docker
This is a dockerized version of the [Lair Framework](https://github.com/lair-framework/lair). An attempt to take all the steps from the [Installation Instructions](https://github.com/lair-framework/lair/wiki/Installation) and simplify it to a few simple commands.

It also includes [ngrok](https://ngrok.com/), to help automate the process of sharing your Lair instance with co-workers.

This is a private fork of the [lair-docker](https://github.com/ryhanson/lair-docker) repository.  It's modified from the original to allow for real-time editing of the lair source code for development purposes.


The original project was inspired and built off the initial work done by [b00stfr3ak](https://github.com/b00stfr3ak) here: [https://github.com/b00stfr3ak/dockerfiles/tree/master/lair](https://github.com/b00stfr3ak/dockerfiles/tree/master/lair);

## Installation

First make sure you have docker installed. Here are [OS X Beta](https://docs.docker.com/docker-for-mac/) and [Linux](https://docs.docker.com/linux/step_one/) instructions.

```bash
$ git clone https://github.com/t1v0/lair-docker.git
$ cd lair-docker
```

Then you will need to modify the docker-compose.yml file to point to the volume location of the lair source code.  Once that is set to the correct path:

```
$ docker-compose build
$ docker-compose up
```

If everything worked, you should see something like:
```bash
lair_lair    | => Started proxy.
lair_lair    | => Started your app.
lair_lair    | 
lair_lair    | => App running at: http://0.0.0.0
```

On first run the admin password will be created and displayed in the messages.  Copy, paste, save, or write down your admin credentials. Then you can press `Ctrl+C` to stop all the services.

## Usage

Before running any `docker-compose` commands, make sure you are in the `lair-docker` directory.

When you are ready to start up Lair again, run: 
```bash
$ docker-compose start
```

To stop all Lair services, run:
```bash
$ docker-compose stop
```

To use ngrok, set `ENABLED: 1` in docker-compose.yml and run:
```bash
$ docker-compose up ngrok
```

Once you've done this, you can press `Ctrl+C` and use `start` and `stop` like below. The `up` command has to be ran any time you update the docker-compose.yml file.

### Moving existing MongoDB database

If you previously used this environment with /usr/local/mongodb configured as the volume for MongoDB, 
you'll need to copy your database files to the new volume location. You can do so by running:

```bash
$ mkdir ~/.lair
$ cp -R /usr/local/mongodb ~/.lair/
```

This update was made due to issues with Docker on OS X and not having proper permissions to create the /usr/local/mongodb folder. 
If you haven't used this Docker environment, you won't have a database to move and you can ignore the instructions above.

### Using ngrok

NOTE: If you used this Docker envrionment before the `ENABLED` flag was added, you'll need to rebuild ngrok by running:
```bash
$ docker-compose build ngrok
```

To re-start ngrok after it has been stopped, run:
```bash
$ docker-compose start ngrok
```

To find the ngrok URL after running `start`, you can run:
```bash
$ docker logs lair_ngrok
```

To stop ngrok, run:
```bash
$ docker-compose stop ngrok
```