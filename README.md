# v-server-setup

# SSH Key Pair Setup and Nginx Configuration

This document outlines the steps taken to set up an SSH key pair, configure SSH authentication, set up Nginx, and link the SSH key with GitHub.

## 1. SSH Key Pair Setup

1. Created an SSH key pair using the command:

   ssh-keygen -t ~/.ssh/demo_ed25519 -C "DA live call demo key"
   
2. Used ssh-copy-id to add the public key to the remote server for passwordless login:
   ssh-copy-id username@host

3. Updated the SSH server configuration file (/etc/ssh/sshd_config) to allow login only via SSH key, disabling password-based login:
   "PasswordAuthentication" = no

4. Restarted the SSH service to apply the changes:
   sudo systemctl restart sshd

5. Successfully logged in to the server using the SSH key (passwordless login).


## 2. Install Webserver NGINX Configuration

1. Installed Webserver NGINX and set up a basic webpage.
2. Created a custom Nginx page by editing the default HTML content in /var/www/html/index.html:
   Updated the page content in the configuration.
3. Ensured the Nginx service was running:
   sudo systemctl start nginx

## 3. SSH Alias Setup

  Created an SSH alias to avoid using the full path to the SSH key every time:
   alias dal_connect="ssh -o StrictHostKeyChecking=False -i ~/home/macUserName/.ssh/id_ed25519 username@host

## 4. Adding SSH Key to GitHub

1. Added the public SSH key to GitHub to authenticate Git operations from the server:
    Retrieved the public key using:
     cat ~/.ssh/id_ed25519.pub
2. Added the SSH public key to GitHub under Settings > SSH and GPG Keys.

## 5. Configuring Git on the Server

  Configured Git on the server to use the same username and email as on GitHub for consistency:
   git config --global user.name "GitHub Name"
   git config --global user.email "my-email@example.com"

## 6. Successfully Authenticated with GitHub

  Verified SSH authentication with GitHub by running:
  ssh -T git@github.com

## 7. Cloned Git Repository
   git clone git@github.com:Bodev13/v-server-setup.git





