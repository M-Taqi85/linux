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
![command2](https://github.com/user-attachments/assets/1216f6d0-e384-448e-8b0c-bce56af3434a)

# APT Package Management Assignment

## **Part 1: Understanding APT & System Updates**

### **1. Check APT Version**
```bash
apt --version
```
**Output:**  _(apt --version
apt 2.7.14 (amd64))_  
**Screenshoot**
![Screenshot (313)](https://github.com/user-attachments/assets/adbbb036-921e-4348-b34e-edb9fb474247)

### **2. Update the Package List**
```bash
sudo apt update
```
**Explanation:** This command fetches the latest package lists from configured repositories, ensuring we get the latest versions and security updates.

### **3. Upgrade Installed Packages**
```bash
sudo apt upgrade -y
```
**Difference between `update` and `upgrade`:**  
- `update`: Refreshes the package list but doesn’t install updates.
- `upgrade`: Installs the latest versions of all packages listed in the updated package list.

### **4. View Pending Updates**
```bash
apt list --upgradable
```
**Pending Updates:**  _(M-Taqi85@Lab-robotics:~$ apt list --upgradable
Listing... Done)_  My system is upgraded.

---
## **Part 2: Installing & Managing Packages**

### **1. Search for an Image Editor**
```bash
apt search image editor
```
**Selected Package:**  _(gimp)_  
**Screenshoot**
![Screenshot (315)](https://github.com/user-attachments/assets/89295131-4a40-41d0-a4dd-a104decdcf36)

### **2. View Package Details**
```bash
apt show gimp
```
**Dependencies:** 
**Output (Key Information)**
Package Name: gimp
Version: 2.10.36-3ubuntu0.24.04.1
Priority: Optional
Section: universe/graphics
Maintainer: Ubuntu Developers
Download Size: 4680 kB
Installed Size: 20.0 MB
APT Source: http://azure.archive.ubuntu.com/ubuntu noble-updates/universe amd64 Packages
Homepage: GIMP Official Website
🔹 Dependencies (Required for Installation)
Before installing GIMP, the system requires these dependencies:

kotlin
Copy
Edit
libgimp2.0t64, gimp-data, graphviz, xdg-utils, libaa1, libcairo2, libfontconfig1, libglib2.0-0t64, libjpeg8, libpng16-16t64, libstdc++6, zlib1g, etc.
📌 Why are dependencies important?

These are libraries and tools that GIMP relies on to work properly.
APT automatically installs them when installing GIMP.
🔹 Recommended & Suggested Packages
Recommends: ghostscript
(Useful for handling PDFs and PostScript files in GIMP.)
Suggests:
gimp-help-en (Help documentation)
gimp-data-extras (Additional brushes and patterns)
gvfs-backends (Remote file access support)
🔹 Conflicts & Breaks
Conflicts with: gimp-dds
Breaks: gimp-plugin-registry (<< 7.20140602+nmu1~)

### **3. Install the Package**
```bash
sudo apt install gimp  -y
```
**Installation Confirmation:** _(M-Taqi85@Lab-robotics:~$ apt list --installed | grep gimp

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

gimp-data/noble-updates,now 2.10.36-3ubuntu0.24.04.1 all [installed,automatic]
gimp/noble-updates,now 2.10.36-3ubuntu0.24.04.1 amd64 [installed]
libgimp2.0t64/noble-updates,now 2.10.36-3ubuntu0.24.04.1 amd64 [installed,automatic])_  
**Screenshoot**
![Screenshot (316)](https://github.com/user-attachments/assets/be4b896a-56f0-494e-86f6-363617fe619b)
  

---
## **Part 3: Removing & Cleaning Packages**

### **1. Uninstall the Package**
```bash
sudo apt remove gimp -y
```
**Is the package fully removed?**  _(No, configuration files remain.)_  

### **2. Remove Configuration Files**
```bash
sudo apt purge gimp -y
```
**Difference between `remove` and `purge`:**  
- `remove`: Uninstalls the package but keeps configuration files.
- `purge`: Completely removes the package along with configuration files.

### **3. Remove Unused Dependencies**
```bash
sudo apt autoremove -y
```
**Why is this step important?**  
- It removes packages that were installed as dependencies but are no longer needed.

### **4. Clean Up Downloaded Package Files**
```bash
sudo apt clean
```
**What does this command do?**  
- It clears cached `.deb` files to free up disk space.

---
## **Part 4: Managing Repositories & Troubleshooting**

### **1. List All APT Repositories**
```bash
cat /etc/apt/sources.list
```
**Observations:** _(This file contains the list of repositories from which APT retrieves packages.)_  
**Screenshoot**
![Screenshot (317)](https://github.com/user-attachments/assets/044736a0-6d4c-43a6-9081-7b875358e311)

### **2. Add a New Repository (Universe Repository)**
```bash
sudo add-apt-repository universe
sudo apt update
```
**What does the universe repository contain?**
It includes community-maintained open-source software.
**Types of Packages in Universe Repository:** _(![Screenshot (318)](https://github.com/user-attachments/assets/2fa48141-1921-47c8-aa7e-a0d56dd0da84)
)_  

### **3. Simulate an Installation Failure**
```bash
sudo apt install fakepackage
```
**Error Message:** _(E: Unable to locate package fakepackage)_  

### **4. Troubleshooting the Issue**
- **Check for typos** in the package name.
- Run `sudo apt update` to refresh the package list.
- Search for available packages using `apt search <keyword>`.
- Check if additional repositories are needed.

---
## **Bonus Challenge: Using `apt-mark`**

### **Hold a Package** (Prevent it from being updated)
```bash
sudo apt-mark hold gimp
```
### **Unhold a Package** (Allow updates again)
```bash
sudo apt-mark unhold gimp
```
**Why would you hold a package?**  
- To prevent a specific package from being updated due to compatibility or stability reasons.

---




