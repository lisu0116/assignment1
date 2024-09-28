# assignment1
<<<<<<< HEAD

## Introduction

This assignment will guide creating a remote server on DigitalOcean using Arch Linux. This assignment will show how to create SSH keys, add a custom Arch Linux image, create a Droplet, and use cloud-init for initial configuration.

## Prerequisites

- A DigitalOcean account
- Access to a terminal on your local machine
- Make a .ssh directory on your home directory
- Download the appropriate Arch Linux image ([Arch Linux Image](https://gitlab.archlinux.org/archlinux/arch-boxes/-/packages/)). It should be the most recent cloud image and ending with '.qcow2'.

## Step 1: Create SSH Keys

SSH keys are a secure way to log in to your server without needing to enter a password. Follow these steps to create your SSH keys:

1. Open your terminal.
2. Generate a new SSH key pair using the following command:

   ```bash
  ssh-keygen -t ed25519 -f ~/.ssh/new-key -C "your email"


This command generates a new SSH key of type ed25519 on .ssh directory, using the provided email.

ed25519 is a modern algorithm knows for its high security and fast performance.

After the keys are generated, you will find then in the ~/.ssh directory (~/.ssh/new-key.pub and ~/.ssh/new-key)

![to check the SSH key that you just made](assets/ls)

## Step 2: Upload Arch Linux Imange to Your DigitalOcean Account

1. Log in to your DigitalOcean account.
2. Go to Settings and Click Backups & Snapshots

![snapshots](assets/snapshots)

3. Choose Custom Images and click Upload Image
4. Upload Arch Linux Image that you already downloaded

![image upload](assets/image-upload)

5. Distribution - Arch Linux, Choose a datacenter region - San Francisco ,3 then click Upload Image

## Step 3: Add SSH Keys to Your DigitalOcean Account

1. Open your terminal and type the following command to display your SSH public key:

   ```bash
   cat ~/.ssh/new-key.pub

This command is used to display the contents of a specific file. cat refers to "concatenate".

Once that command shows the public key, copy the output.

2. Log in to your DigitalOcean Account
3. Click Settings > Security
4. Click Add SSH key

![Add SSH Key](assets/add-ssh-key)

5. Paste the SSH public key on SSH Key content and type any key name that you can remember then click Add SSH Key.

## Step 4: Create a Droplet Running Arch Linux
1. Click Droplets on dashboard and click Create Droplet.

![Droplet](asset/snapshots)

2. Create Droplets
    - choose region: San Francisco
    - Datacenter: Datacenter 3
    - choose image > Custon Images > click the file that you already uploaded
    - Choose size: Basic
    - CPU options: Premium AMD, $7/mo

![choose size](assets/choose-size)

3. Choose Authentication Method 

you should choose the SSH Key and then choose the SSH key that you made

![choose SSH Key](assets/new-key)

Pause at this stage and move on to the next step.

4. Click Advanced Option.

![Advanced option](assets/advanced-option)

5. Choose Add Initialization scripts (free)
6. Paste the cloud-init.yaml file that you made step 5 on Enter user data here.

![Enter user data here](assets/userdata)

7. Click Create Droplet


## Step 5: Use Cloud-init for Initial Setup

1. Open your terminal.

2. On your home directory, create a new file named `cloud-init.yaml` using your preferred text editor. For example, if you are using Visual Studio Code, run:

   ```bash
   code cloud-init.yaml

3. Add the following configuratin to your `cloud-init.yaml` file:

```yaml
#cloud-config
users:
  - name: user #change here
    ssh-authorized-keys:
      - ssh-ed25519 ... #change here
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    groups: sudo
    shell: /bin/bash

packages:
  - ripgrep
  - rsync
  - neovim
  - fd
  - less
  - man-db
  - bash-completion
  - tmux

disable_root: true
```
4. Copy this yaml file content. 

After you make cloud-init.yaml file, go back to step 4-3.

## Step 6: Connect to Your Droplet Using SSH
After the Droplet is set up, you can connect to it using SSH:
```bash
ssh user@your_droplet_ip
```
This command is used to establish a secure shell (SSH) connection to a remote server. 

## Conclusion
You have finished with remoting server using DigitalOcean and Arch Linux.

## References

1. DigitalOcean. (n.d.). *How to use cloud-config for your initial server setup*. Retrieved from [https://www.digitalocean.com/community/tutorials/how-to-use-cloud-config-for-your-initial-server-setup](https://www.digitalocean.com/community/tutorials/how-to-use-cloud-config-for-your-initial-server-setup)

2. Cloud-init. (n.d.). *Cloud-init documentation*. Retrieved from [https://docs.cloud-init.io/en/latest/index.html](https://docs.cloud-init.io/en/latest/index.html)

