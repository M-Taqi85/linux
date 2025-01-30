# Account Setup
- In  the first step, I'd create an Microsoft Azure account using email address that university provoded me.

- Then I got  to know about the cloud and it's importance. 

- Additionally, I explored student benefits  and open an student account and Azure give me **$100** worth of credits that I can use to purchase any pachage within the environment.


# Create Virtual Machine
- I created virtual machine where I have to work later on this course.

- Then I select Marketplace from **Ubuntu Server 24.04 LTS gen 2 Server** published by Canonical. 

- I named my machine **"lab-robotics"**.

- I choose B series version 2 which is **Standard_B2ls_v2**.

- Later, I create a new resource group for the machine and subnet to place the machine in.

# Link my HAMK email to my GitHub account

- I create a new repository named **"linux"** for the assignment.

- Then I add my HAMK email as a secondary mail for version control.

![mail]![Screenshot (278)](https://github.com/user-attachments/assets/6cfed329-0e3b-46ed-a562-51b0327bfa33)

# Assignment 3: User Management and File System Access

## Step 1: Creating Users
- Created two users: **tupu** and **lupu**.
- Set **passwords** and other necessary information to restrict access.
- Used `sudo` and `adduser` commands:

        sudo adduser tupu

## Step 2: Creating the Lupu User
- Used `useradd` command for `lupu`:

        sudo useradd -m -d /home/lupu -s /bin/bash -G lupu lupu

- Options explained:
  - `-m`: Create the home directory.
  - `-d /home/lupu`: Specify the home directory path.
  - `-s /bin/bash`: Set the login shell.
  - `-G lupu`: Add the user to the lupu group.

## Step 3: Creating the Hupu System User
- Created a system user `hupu` with login shell set to `/bin/false`:

       sudo useradd --system --shell /bin/false hupu

- Explanation:
  - `--system`: Create a system account.
  - `--shell /bin/false`: Prevent user login.

## Step 4: Granting Sudo Privileges
- Edited sudoers file using **visudo**:

        sudo visudo

- Added permissions:

        tupu ALL=(ALL:ALL) ALL
        lupu ALL=(ALL:ALL) ALL

- Alternatively, added users to the sudo group:

        sudo usermod -aG sudo tupu
        sudo usermod -aG sudo lupu

## Step 5: Setting Up `/opt/projekti` Directory
- Created directory:

        sudo mkdir /opt/projekti

- Created a group `projekti` and assigned both users:

        sudo groupadd projekti
        sudo usermod -aG projekti tupu
        sudo usermod -aG projekti lupu

- Set ownership and permissions:

        sudo chown :projekti /opt/projekti
        sudo chmod 770 /opt/projekti

- Ensured new files inherit `projekti` group ownership:

        sudo chmod g+s /opt/projekti

## Output
Expected directory permissions:

        drwxrws--- 2 root projekti 4096 Jan 30 16:02 /opt/projekti

## Screenshots
Here are the screenshots demonstrating the practical execution.
![command1](https://github.com/user-attachments/assets/5685935f-379d-4899-88e0-0edd39c5c65e)



