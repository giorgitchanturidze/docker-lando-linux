Here's a comprehensive guide for installing Docker and Lando on a Linux Mint system, focusing on addressing the specific issue with docker-compose:

### Installing Docker

1. **Update System Packages**
   Open a terminal and run:
   ```bash
   sudo apt update
   sudo apt upgrade
   ```

2. **Install Docker**
   The best practice is to install Docker from the official Docker repository.
   - First, install required packages:
     ```bash
     sudo apt install apt-transport-https ca-certificates curl software-properties-common
     ```
   - Add the GPG key for the official Docker repository to your system:
     ```bash
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
     ```
   - Add the Docker repository to APT sources:
     ```bash
     sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
     ```
   - Update the package database with the Docker packages from the newly added repo:
     ```bash
     sudo apt update
     ```
   - Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:
     ```bash
     apt-cache policy docker-ce
     ```
   - Finally, install Docker:
     ```bash
     sudo apt install docker-ce
     ```

3. **Post-installation Steps for Docker**
   - To avoid typing `sudo` whenever you run the `docker` command, add your username to the `docker` group:
     ```bash
     sudo usermod -aG docker ${USER}
     su - ${USER}
     ```
   - Confirm that Docker is installed correctly by running the hello-world image:
     ```bash
     docker run hello-world
     ```

### Installing Lando

1. **Install Lando**
   - First, download the latest Lando binary from the [official releases page](https://github.com/lando/lando/releases). Make sure to select the appropriate version for Linux.
   - Once downloaded, navigate to the directory containing the downloaded file and install Lando:
     ```bash
     sudo install -o root -g root -m 0755 lando-stable.deb /usr/local/bin/lando
     ```

2. **Troubleshooting Docker Compose with Lando**
   - Lando may have issues detecting or downloading the correct version of docker-compose. If this happens, you can manually download and set up docker-compose.
   - First, remove any existing versions of docker-compose:
     ```bash
     sudo apt-get remove docker-compose
     ```
   - Download the specific version of docker-compose required by Lando:
     ```bash
     sudo curl -L "https://github.com/docker/compose/releases/download/v2.21.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
     ```
   - Apply executable permissions to the binary:
     ```bash
     sudo chmod +x /usr/local/bin/docker-compose
     ```
   - Verify the installation:
     ```bash
     docker-compose --version
     ```

3. **Final Steps and Verification**
   - Restart your system to ensure all changes are applied.
   - Once the system is back up, verify the installation of Lando:
     ```bash
     lando version
     ```
   - Optionally, run `lando init` in a test project directory to ensure it initializes correctly.

### Additional Notes
- Always ensure your system's firewall or security software is not blocking Docker or Lando.
- If you encounter specific errors, refer to the official documentation or community forums for Docker and Lando for troubleshooting tips.
- Remember that Docker and Lando are constantly updated, so it's good practice to check for the latest installation instructions on their official websites.
