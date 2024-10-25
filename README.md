# twn-devops-bootcamp-module05
Cloud &amp; Infrastructure as Service Basics with DigitalOcean

### Setup Server on Digital Ocean
1. Login
2. Choose **Droplets** in the left side menu
3. Click **Create Droplet**
4. Provide the Droplet configuration:
    - Region: Singapore
    - OS: Ubuntu
    - Droplet Type: Basic
    - CPU options:
        - Regular (Disk type: SSD)
        - 1 CPU, 512 MB Memory, 10 GB SSD Disk, 500 GB transfer
5. Create an SSH key or provide an existing one
    - On your workstation, generate a new SSH key:
    ```
    ❯ ssh-keygen -t rsa -b 4096
    Generating public/private rsa key pair.
    Enter file in which to save the key (/Users/ericksonsantos/.ssh/id_rsa): /Users/ericksonsantos/.ssh/digitalocean
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in /Users/ericksonsantos/.ssh/digitalocean
    Your public key has been saved in /Users/ericksonsantos/.ssh/digitalocean.pub
    The key fingerprint is:
    SHA256:tfUMXp4N0G7XN2aweoI51STtR6SIQMv8o2IZZmbxJf0 ericksonsantos@US-F6Q4P3J43X
    The key's randomart image is:
    +---[RSA 4096]----+
    |      .o    o... |
    |      o + ...=o. |
    |     . = +..Bo* .|
    |      o +..= XoO+|
    |     * .So=Eo.O.+|
    |    = o .+.o .   |
    |     + .  . o    |
    |    . .          |
    |                 |
    +----[SHA256]-----+

    ❯ cat /Users/ericksonsantos/.ssh/digitalocean.pub
    ssh-rsa XXXXXXXX
    ```
    - Upload the public SSH key to DigitalOcean by choosing the **SSH Key** for **Choose Authentication Method** instead of **Password**, then click **Add SSH Key**, paste the content of the public key and save.
6. Click **Create Droplet** and wait for the Droplet to boot and initalized