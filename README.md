# assignment1

## Introduction
This assignment will guide to create a remote server on DigitalOcean using a custom Arch Linux image. This assignment will show how to generate SSH keys, use cloud-init for initial server configuration, and connect to Droplet securely.


## Step 1: Create SSH Keys
SSH keys are a secure way to log into your server without using passwords.

### Generating SSH Keys
Open your terminal and run the following command:
ssh-keygen -t ed25519 -f ~/.ssh/new-key -C "your email"

![generating ssh keys](assets/generating-ssh-keys)

