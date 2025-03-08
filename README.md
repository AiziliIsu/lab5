# lab5
# Raspberry Pi Lab Setup - Initial Configuration

This document outlines the initial configuration steps performed on the Raspberry Pi for our team lab setup.

## 1. Operating System Installation

* **Operating System:** Raspberry Pi OS Lite (recommended for server tasks)
* **Installation Method:** Flashed the OS image to an SD card using Raspberry Pi Imager.

## 2. User and Group Configuration

* **Group Creation:**
    * Created a shared group named `teamgroup` to manage shared folder access.
    * Command: `sudo addgroup teamgroup`
* **User Creation:**
    * Created user accounts for each team member (e.g., `user1`, `user2`).
    * Command: `sudo adduser <username>`
    * Set strong passwords for each user.
    * Added users to the `teamgroup` group.
    * Command: `sudo usermod -aG teamgroup <username>`

## 3. Shared Folder Setup (/teamshare)

* **Folder Creation:**
    * Created a shared folder named `/teamshare`.
    * Command: `sudo mkdir /teamshare`
* **Group Ownership:**
    * Set the group ownership of the folder to `teamgroup`.
    * Command: `sudo chown :teamgroup /teamshare`
* **Permissions:**
    * Set permissions to allow read/write access for the group and owner, and to prevent non-owners from deleting files.
    * Command: `sudo chmod 2770 /teamshare`
    * `2770` Explanation:
        * `2`: Setgid bit (files inherit group ownership).
        * `7`: Owner (root) read, write, execute.
        * `7`: Group (teamgroup) read, write, execute.
        * `0`: Others no access.

## 4. SSH Access

* **Enabled SSH:**
    * Enabled SSH access for remote management.
    * Command: `sudo raspi-config` -> Interfacing Options -> SSH -> Enable.
* **Purpose:** Allows remote access to the Raspberry Pi for administration.

## 5. Network Configuration

* **IP Address Check:**
    * Checked the Raspberry Pi's IP address using `hostname -I` and `ip a`.
* **Purpose:** To confirm network connectivity and obtain the IP address for SSH access.
* **Static IP:**
    * Static IP address configured within the `/etc/dhcpcd.conf` file.
* **Purpose:** to insure that the ip address of the raspberry pi does not change.

## 6. Terminal Font Size

* **Console Font:**
    * Used `sudo dpkg-reconfigure console-setup` to configure the console's font size.
* **Purpose:** To enhance readability of the console.

## 7. Next Steps

* Install and configure Nginx for web hosting.
* Setup Git for version control.
* Convert Markdown documentation to HTML.
* Create an index page for the website.
* Automate website updates using cron jobs.
