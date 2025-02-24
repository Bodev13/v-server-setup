# v-server-setup

# SSH Key Pair Setup and Nginx Configuration

This document outlines the steps taken to set up an SSH key pair, configure SSH authentication, set up Nginx, and link the SSH key with GitHub.

- [x] [Generated SSH key](#generated-ssh-key)  
- [x] [Added public key to server](#added-public-key-to-server)  
- [x] [Configured SSH access / updated the config file](#configured-ssh-access)
- [x] [SSH Alias setup](#ssh-alias-setup)
- [x] [Set up Nginx web page](#set-up-nginx-web-page)
- [x] [Added SSH key to GitHub](#adding-ssh-key-to-github)
- [x] [Configuring Git on the Server](#configuring-git-on-the-server)
- [x] [Authenticated with GitHub](#authenticated-with-github) 
- [x] [Cloned Git Repository](#cloned-git-repository)

## Generated SSH key

   Created an SSH key pair using the command:

```bash
   ssh-keygen -t ~/.ssh/demo_ed25519 -C "DA live call demo key"
```

## Added public key to server

   1. Used ssh-copy-id to add the public key to the remote server for passwordless login:

```bash
   ssh-copy-id username@host
```
   1. Test ssh connection before disabling password-based login

```bash
   ssh servername@host
```

## Configured SSH access

1. Updated the SSH server configuration file to allow login only via SSH key, disabling password-based login:

```bash
   /etc/ssh/sshd_config
```
1. In the config file changed the "PasswordAuthentication" to "no"

1. Restarted the SSH service to apply the changes:

```bash
   sudo systemctl restart sshd
```

1. Successfully logged in to the server using the SSH key (passwordless login).


## SSH Alias Setup

1. Created an SSH alias to avoid using the full path to the SSH key every time:

```bash
   alias dal_connect="ssh -o StrictHostKeyChecking=False -i ~/Users/macUserName/.ssh/id_ed25519 username@host"
```
1. Checking if the alias is existing
   
```bash
   alias | grep dal
```
1. Testing that a login with alias is working:

```bash
   dal_connect
```

## Set up Nginx webserver 

1. Installed NGINX package and set up a basic webpage:

```bash
sudo apt install nginx -y
```

1. Created a custom Nginx page by editing the default HTML content
   
```bash
   sudo mkdir var/www/alternatives
   sudo touch /var/www/alternatives/alternate-index.html
```
1. Updated the page content in the configuration:

```bash
   sudo nano /etc/nginx/sites-enabled/alternatives
```
1. Added server blocks with port 8081 and html

1. Ensured the Nginx service was running:
   
```bash
   sudo service nginx restart
```

1. Opening the NGINX webpage using the IP address
1. Adding a port 8081 to see the changed HTML page after updating the configuration:
   
```bash
   localhost:8081
```

## Adding SSH Key to GitHub

1. Added the public SSH key to GitHub to authenticate Git operations from the server under "Settings > SSH and GPG Keys".
1. Retrieved the public key using:
```bash
     cat ~/.ssh/id_ed25519.pub
```

## Configuring Git on the Server

  Configured Git on the server to use the same username and email as on GitHub for consistency:

```bash
   git config --global user.name "GitHub Name"
   git config --global user.email "my-email@example.com"
```

## Authenticated with GitHub

  Verified SSH authentication with GitHub by running:

```bash
  ssh -T git@github.com
```

## Cloned Git Repository

```bash
   git clone git@github.com:Bodev13/v-server-setup.git
```





