# Liara setup on Arch Linux

## Pre-flight checklist
* Make sure `git` is installed
* Make sure you have Python 3.5 or higher and `pip3` installed

## Installation

Install and enable Redis with the following commands:
```bash
admin@demo:~$ sudo pacman -S redis
admin@demo:~$ sudo systemctl enable redis.service
```
Run

```bash
liara@demo:~$ sudo -H pip3 install -U git+https://github.com/Rapptz/discord.py@rewrite redis-collections
```
To install discord.py and redis-collections.

Navigate to the directory you wish to install Liara in. (I will refer to this folder as `<folder>` from now on.)


```bash
liara@demo:~$ git clone https://github.com/Thessia/Liara.git <folder>
```

This will clone Liara to your machine.

To run Liara, run

```bash
liara@demo:~/<folder>$ python3 liara.py <token>
```
`<token>` is your bot token you should've acquired from the [Discord developers website](https://discordapp.com/developers/applications/me).

If you have any issues, feel free to ask in the [Discord server's support channel](https://discord.gg/KTGHafT).
