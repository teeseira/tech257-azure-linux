## Automation

**Levels of automation ranked lowest to highest:**
  - Manual: Start off with manual commands to ensure they work and to avoid user input.
  - Script: Turn all manual commands into a script.
  - User data: Runs a script without needing to SSH in.
  - Image: a copy/snapshot of the VM disk.
## Forward Proxy

### Step 1: Create Azure VM 

1. Launch a Virtual Machine with *Ubuntu 22.04 LTS* as image, size *B1s*.
2. For Virtual network, create with a public subnet (to allow public facing app) and private subnet (for database).
3. Set up network security groups for port 22 (SSH), port 80 (HTTP) and port 3000 (Custom).
4. Complete the VM setup and review configurations.

### Step 2a: Manual App Deployment on Azure

#### Method 1: Copy App onto VM

1. Register private key in the terminal.

2. Use `scp` to copy the *app* folder from your local machine to the VM. _This app folder contains the application code and its dependencies._

    ```
    scp -r /path/to/local/app user@vm_ip:/path/to/remote/directory
    ```
3. SSH into the VM: `ssh user@vm_ip`
4. Navigate to the app directory and start the application with `npm start` or `node app.js`.
    ```
    cd tech257_sparta_app/app
    npm start
    ```
#### Method 2: Get app onto GitHub

1. Create a Git repository called *tech257_sparta_app* and push the app folder to it.
2. SSH into the VM from the terminal.
3. Then clone the remote GitHub repository into your Azure VM.
4. Navigate to the app directory and start the application with `npm start` or `node app.js`:
    ```
    cd tech257_sparta_app/app
    npm start
    ```