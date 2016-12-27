# Liara setup on Ubuntu Server 16.04 LTS

## Pre-flight checklist
* Make sure to designate a folder and user to Liara
* Make sure `git` is installed
* Make sure you have Python 3.5 or higher installed
    * discord.py needs to be installed too


##Installation

You need to install Redis, so the first thing we do is run
```bash
admin@demo:~$ sudo apt install redis-server
```
This installs Redis and starts it.

Next up, we are going to `sudo` into the designated user (I will refer to this user as `<user>` from now on).
```bash
admin@demo:~$ sudo -Hu <user> bash
```
This will get you a bash prompt with your specified user.
Navigate to your folder (I will refer to this folder as `<folder>` from now on.)

Run
```bash
liara@demo:~$ git clone https://github.com/Thessia/Liara.git <folder>
```
This will clone Liara to your machine.
You're almost done! You now only have to set up a service file (I will refer to the service file's name as `<service>` from now on.)
```bash
liara@demo:~$ exit
admin@demo:~$ sudo nano /etc/systemd/system/<service>.service
```
You'll want something along the lines of
```systemd
[Unit]
Description=Liara, a fully modular Discord bot

Wants=network.target
After=network.target

[Service]
User=<user>
Group=<user>

KillSignal=SIGINT
TimeoutStopSec=30
Restart=always

WorkingDirectory=<full path to <folder>>
ExecStart=/bin/bash ./liara.py <token>

[Install]
WantedBy=multi-user.target
```
`<token>` is your bot token you should've acquired from the [Discord developers website](https://discordapp.com/developers/applications/me).
 
`<full path to <folder>>` is the full path to your folder, so for example `/home/liara/bots/liara`.

After you've saved the file, you can do
```bash
admin@demo:~$ sudo systemctl enable <service>  # this will make Liara auto-start
admin@demo:~$ sudo systemctl start <service>
```
If you've done everything correctly, you should now have an instance of Liara running.

---
If you have any issues, feel free to ask in the [Discord server's support channel](https://discord.gg/KTGHafT).
