### Assignment 2 - Create your own server.
#### Due: July 9th by 1300 hours.

-----

>Follow the steps below to create your own server. If these steps aren't clear enough, you can 
view an online tutorial [here](https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet-virtual-server).

-----

#### 1. [Sign up](https://cloud.digitalocean.com/registrations/new) for Digital Ocean.

-----

#### 2. [Create a new Droplet](https://cloud.digitalocean.com/droplets/new)

- Droplet Hostname
> Pick a name for your computer. This is NOT a domain name that will be DNS resolvable.

- Select Size
> 512MB / 1 CPU<br>
20GB SSD DISK<br>
1TB TRANSFER<br>

- Select Region
> Pick the closest region to Texas.

- Select Image
> Ubuntu 14.04 x64

- Select Applications (Tab over from image)
> LAMP on Ubuntu 14.04

- Add optional SSH Keys
> Skip, we will address ssh keys later.

- Settings
> Leave default settings, and don't worry about backups (unless you want to pay).

-----

#### 3. IP Address & Password

- The IP address that is assigned to your "droplet", is your only connection to your server.
- The root password will be emailed to you.
- You need both IP address & password to access your new server.

#### 4. Accessing Your Server

- Open some type of "terminal" application and log into your server using:
    - The IP address given to you
    - The password emailed to you
- Change your root password!
    - Run the following command (note: the dollar `$` sign just implies "command line", don't use it in the command):
    - `$ passwd`
    - Follow the prompts.
- Add yourself as a user:
    - `$ useradd your-new-username`
    - Follow the prompts.
    - Stay root for now, but as soon as you add 'your-new-username' to `sudoers`, you should change to your new user:
    - `$ su your-new-username`
- Add me as a user:
    - `$ useradd griffin`
    - Set my password as `WebCourse2014!`, I will change it as necessary.
- Now we need to edit the `sudoers` file. `Sudoers` is a file that allows regular users to run commands as "root" as long as an entry is placed correctly in the file. 
- "Your-new-user" and "griffin" both need to be added:
    - A comprehensive tutorial about suders is available [Here](https://help.ubuntu.com/community/Sudoers).
    - Shortcut version:
        - (As root) $ nano /etc/suders
        - Edit sudoers and add two lines using the following example:

```txt
# User privilege specification
root	ALL=(ALL:ALL) ALL

# Add yourself:
your-new-username 	ALL=(ALL:ALL) ALL

# Add me:
griffin 	ALL=(ALL:ALL) ALL
```
