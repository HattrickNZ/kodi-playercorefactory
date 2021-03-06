# SSH Client set up

* arch linux install ssh

```
sudo pacman -S openssh
```

* debian install ssh if not already installed

```
sudo apt install -y openssh-client
```

### Create ssh keys

```
ssh-keygen -b 4096
```

### copy ssh public key to your ssh server

```
ssh-copy-id username@sshserver
```

#### ssh client config 

edit your ~/.ssh/config 

```
vim ~/.ssh/config
```

and add the code below change username, 
host name and ip to match your server

```
# ffmpeg ssh server
Host ffmpegserver
User username
Port 22
HostName 192.168.1.2
```

#### ssh agent 

* arch linux ssh agent service

```
vim ~/.config/systemd/user/ssh-agent.service
```

```
[Unit]
Description=SSH key agent

[Service]
Type=forking
Environment=SSH_AUTH_SOCK=%t/ssh-agent.socket
ExecStart=/usr/bin/ssh-agent -a $SSH_AUTH_SOCK

[Install]
WantedBy=default.target
```

* edit your ~/.bashrc

```
vim ~/.bashrc
```

* add the following code to your ~/.bashrc

```
export SSH_AUTH_SOCK="$XDG_RUNTIME_DIR/ssh-agent.socket"
```

#### ssh agent daemon

* reload the ssh-agent.service

```
systemctl --user daemon-reload
```

* enable the ssh-agent service

```
systemctl --user enable ssh-agent
```

* cache your ssh private key password

```
ssh-add ~/.ssh/id_rsa
```

* at the prompt enter your ssh private key password

