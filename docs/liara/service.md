Liara can be setup as a service, so that in case of a crash, connection failure, system restart, or other issue, Liara will automatically restart.

To do this with `systemd`, create `liara.service`.
```bash
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
