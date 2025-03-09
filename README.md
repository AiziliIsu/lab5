# Lab 5: Raspberry Pi Networked Lab Setup

**1. General Lab Overview**

* **Goal:** Create a collaborative, networked learning environment using Raspberry Pi computers.
* **What We're Building:**
    * Interconnected network of Raspberry Pi computers.
    * Centralized website (Lab Hub) for project documentation.
    * Shared folder system for file exchange.
    * Remote access capabilities.
* **Core Concepts:**
    * Raspberry Pi OS
    * Networking
    * File Sharing
    * Nginx Web Server
    * Git Version Control
    * SSH Remote Access

**2. General Team Tasks**

* **2.1. Raspberry Pi Setup:**
    * Install Raspberry Pi OS Lite.
    * Configure user accounts and group permissions.
    * Create `/teamshare` folder with appropriate permissions.
    * Enable SSH access.
    * Setup a static IP address.
* **2.2. Documentation:**
    * Write detailed guides (README.md) using Markdown.
    * Store documentation in a local Git repository.
* **2.3. Networking:**
    * Ensure network connectivity between Raspberry Pis.

**3. Team 1: Nginx Web Server (Centralized Lab Hub)**

* **Role:** Create and manage the Lab Hub website.
* **Tasks:**
    * **3.1. Raspberry Pi OS Lite Configuration:**
        * **Version:** Latest stable release.
        * **Reason:** Minimal resource usage.
        * **Installation:** Flashed via Raspberry Pi Imager.
        * **User/Group Management:**
            * Group: `teamgroup` created.
            * Unique user accounts for team members.
            * `/teamshare` permissions: `2770` (group inheritance, read/write, owner delete).
        * **Shared Folder:**
            * Location: `/teamshare`.
            * Purpose: Centralized file sharing.
            * Implementation: `mkdir`, `chown`, `chmod`.
        * **SSH Access:**
            * Enabled via `raspi-config`.
            * Purpose: Remote management.
            * Security: Strong passwords.
        * **Network Configuration:**
            * Static IP in `/etc/dhcpcd.conf`.
            * Verification: `hostname -I` or `ip a`.
            * Connectivity: Ping tests.
        * **Terminal Font:**
            * Console: `sudo dpkg-reconfigure console-setup`.
    * **3.2. Nginx Web Server Configuration:**
        * **Installation:** `sudo apt install nginx`.
        * **Verification:** `sudo systemctl status nginx`.
        * **Virtual Hosts:**
            * Location: `/etc/nginx/sites-available/`.
            * Naming: Team-specific configuration files (e.g., `team2`).
            * Directives: `server_name`, `root`, `listen 80`.
            * Enabling: Symbolic links in `/etc/nginx/sites-enabled/`.
            * Reloading: `sudo systemctl reload nginx`.
        * **Website Security:**
            * HTTPS: Self-signed SSL certificate (openssl), port 443.
            * Basic Authentication: `.htpasswd` (htpasswd), Nginx `location` blocks.
        * **Documentation Integration:**
            * Git Cloning: Local repository to `/var/www/html/labhub`.
            * Markdown Conversion: `pandoc` (.md to .html), `convert_markdown.sh` script.
            * HTML Structure: Team folders in `/var/www/html/labhub/`.
        * **Centralized Hub:**
            * Index Page: `index.html` in `/var/www/html/labhub/`, links to team documentation.
        * **Automation:**
            * Cron Job: `crontab -e`, `convert_markdown.sh` and `git pull` (scheduled).

**4. Team 1 Workflow**

1.  Nginx Installation.
2.  Virtual Host Configuration.
3.  Git Integration.
4.  Markdown Conversion.
5.  Website Creation.
6.  Automation Setup.
7.  Security Implementation.
8.  Testing.

**5. Key Tools**

* Nginx
* Git
* Markdown
* Pandoc
* Cron
