# twn-devops-bootcamp-module05
Cloud &amp; Infrastructure as Service Basics with DigitalOcean

### Setup Server on Digital Ocean
1. Login.
2. Choose **Droplets** in the left side menu.
3. Click **Create Droplet**.
4. Provide the Droplet configuration:
    - Region: Singapore
    - OS: Ubuntu
    - Droplet Type: Basic
    - CPU options:
        - Regular (Disk type: SSD)
        - 1 CPU, 512 MB Memory, 10 GB SSD Disk, 500 GB transfer
5. Create an SSH key or provide an existing one.
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
6. Click **Create Droplet** and wait for the Droplet to boot and initalized.

### Setup Firewall for your Droplet on Digital Ocean
1. Go to Networking > Firewall tab > Create Firewall button.
2. Configure:
    - Name: my-droplet-firewall
    - Inbound Rules:
        - Type: SSH
        - Protocol: TCP
        - Port Range: 22
        - Source: MY_PUBLIC_IP (go to what is my IP?)
    - Outbound Rules (leave the default)
3. Click **Create Firewall** button.
4. View the firewall by clicking its name. Go to Droplets tab then click Add Droplets, then choose the Ubuntu droplet.
5. Test SSH connection:
    ```
    # On your workstation, execute ssh command:
    $ ssh root@$MY_PUBLIC_IP
    ```

### Deploy and run application artifact on Droplet
1. Install java on the Ubuntu Droplet:
    ```
    $ apt update -y && apt upgrade -y
    $ apt install openjdk-8-jre-headless -y
    ```
2. Clone the project on your local machine, build it, then copy the artifact to the Ubuntu Droplet
    ```
    $ git clone git@gitlab.com:twn-devops-bootcamp/latest/05-cloud/java-react-example.git
    $ gradle build
    $ scp build/libs/java-react-example.jar root@206.189.80.97:/root
    ```
3. Run the application on the Ubuntu Droplet
    ```
    # SSH again if needed then run the app
    $ java -jar java-react-example.jar &
    ```
4. Test access the application
    ```
    # Modify the Droplet's firewall to open port 7071
    $ curl -sv http://206.189.80.97:7071

    # Optional install of net-tools to use netstat to check for active listening port
    # Use of ps to view the java running process
    $ sudo apt install net-tools
    $ netstat -lpnt
    $ ps aux | grep java
    ```
5. Create a non-root user to manage the Ubuntu Droplet
    ```
    # Create the user and password
    $ useradd test

    # Add the user to the sudoers
    $ usermod -aG sudo test

    # Test login the user
    $ su - test
    ```