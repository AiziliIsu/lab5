# lab5


**General Lab Overview**

**Goal:** To create a collaborative, networked learning environment using Raspberry Pi computers.

**What We're Building:**

* A small, interconnected network of Raspberry Pi computers.
* A centralized website that serves as a hub for all project documentation.
* A shared folder system for easy file exchange among team members.
* Remote access capabilities for convenient management.

**Core Concepts:**

* **Raspberry Pi OS:** The operating system that runs on each Raspberry Pi.
* **Networking:** Connecting the Raspberry Pis to communicate with each other.
* **File Sharing:** Allowing team members to share files easily and securely.
* **Web Server:** Using Nginx to host a central website.
* **Git:** Using version control to manage and share project documentation.
* **SSH:** Securely accessing and managing the Raspberry Pis remotely.

**General Team Tasks:**

1.  **Raspberry Pi Setup:**
    * Install Raspberry Pi OS Lite.
    * Create user accounts and set up group permissions for shared folders.
    * Create a shared folder (`/teamshare`) with appropriate permissions.
    * Enable SSH access for remote management.
    * Setup a static IP address.
2.  **Documentation:**
    * Write detailed guides (README.md) using Markdown.
    * Store documentation in a local Git repository.
3.  **Networking:**
    * Ensure the Raspberry Pi can communicate with other devices on the network.

**Team 1: Nginx Web Server (Centralized Lab Hub)**

**Role:** To create and manage the central website that hosts all team documentation.

**Tasks:**
Raspberry Pi OS Lite:
Version: The latest stable release of Raspberry Pi OS Lite.
Reason: Chosen for its minimal resource usage, ideal for server applications.
Installation: Flashed using Raspberry Pi Imager to a microSD card.
User and Group Management:
Group: A single group, teamgroup, is created.
Users: Each team member gets a unique user account.
Permissions:
/teamshare directory:
2770 permissions: Ensures group ownership inheritance and controlled access.
Users in teamgroup can read and write.
Only the file owner can delete.
Shared Folder (/teamshare):
Location: /teamshare on the root filesystem.
Purpose: Centralized location for file sharing and collaboration.
Implementation: mkdir, chown, and chmod commands are used.
SSH Access:
Configuration: Enabled via raspi-config.
Purpose: Remote administration and management.
Security: Strong passwords required for all user accounts.
Network Configuration:
Static IP: Configured in /etc/dhcpcd.conf to prevent IP address changes.
Verification: hostname -I or ip a commands used to verify IP address.
Connectivity: Ping tests between Raspberry Pis to confirm network connectivity.
Terminal Font:
Console: sudo dpkg-reconfigure console-setup used to set a larger, more readable font.
Team 1: Nginx Web Server - Detailed Specifications

Nginx Installation:
Method: sudo apt install nginx.
Verification: sudo systemctl status nginx to confirm successful installation and running status.
Virtual Host Configuration:
Location: Configuration files in /etc/nginx/sites-available/.
Naming: Each team gets a configuration file (e.g., team2, team3).
Directives:
server_name: Set to a unique "URL" (e.g., labhub/team2).
root: Points to the directory containing each team's HTML files (e.g., /var/www/html/team2).
listen 80: Listens for HTTP traffic on port 80.
Enabling: Symbolic links created in /etc/nginx/sites-enabled/.
Reloading: sudo systemctl reload nginx after configuration changes.
Website Security:
HTTPS:
Self-signed SSL certificate generated using openssl.
Nginx configured to use the certificate.
Listen on port 443.
Basic Authentication:
.htpasswd file created using htpasswd.
Nginx location blocks configured to require authentication.
Documentation Integration:
Git Cloning:
Local Git repository is cloned to /var/www/html/labhub.
Markdown Conversion:
pandoc used to convert .md files to .html.
A shell script (convert_markdown.sh) automates the process.
HTML Structure:
Each teams markdown files are converted to html files and placed into their own folder within the /var/www/html/labhub/ directory.
Centralized Hub:
Index Page:
index.html created in /var/www/html/labhub.
Provides links to each team's documentation.
Automation:
Cron Job:
crontab -e used to schedule a cron job.
Runs convert_markdown.sh and git pull every 5 minutes (or as configured).
Ensures the website is always up-to-date.

**Team 1 Workflow:**

1.  **Nginx Installation:** Install the Nginx web server.
2.  **Virtual Host Configuration:** Configure Nginx to serve multiple websites from the same server.
3.  **Git Integration:** Use Git to clone the project repository and retrieve documentation.
4.  **Markdown Conversion:** Convert Markdown files to HTML using a tool like Pandoc.
5.  **Website Creation:** Create the main website page and links to team documentation.
6.  **Automation Setup:** Set up a cron job to keep the website updated.
7.  **Security Implementation:** Enable HTTPS and basic authentication.
8.  **Testing:** Verify that the website is working correctly and that all documentation is accessible.

**Key Tools:**

* Nginx (web server)
* Git (version control)
* Markdown (documentation format)
* Pandoc (Markdown to HTML conversion).
* Cron (task scheduler)
