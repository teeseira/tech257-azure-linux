# Azure

## Virtual machines
Virtual machines are simulated computers created by software. They allow you to run multiple operating systems on the same physical computer.

   <img src="../assets/single-vm-diagram.png" alt="SSH" width="400px">

## Login to Azure

- Go to [Azure Portal](https://portal.azure.com/).
- Sign in with your Azure credentials. <!--Log in with the permissions you need, not more than that.-->

## Create a Virtual Network
1. Search for "Virtual networks" in Azure Portal and select it.
2. Click `Create` and specify your Subscription, Resource group, Virtual network name, and Region.
3. In the `Tags` tab, add a name and value for `All resources selected`.
4. Click `Review + create`, then `Create`.

## Setup SSH Key on Azure

1. Generate SSH key in your **.ssh/** directory of your terminal:
    ```bash
    ssh-keygen -t rsa -b 2048 -C "[your-email]"
    ```
   Give the key a desired **keyname**.

2. Copy the public key:
    ```bash
    cat ~/.ssh/keyname.pub
    ```

3. Add SSH Key to Azure:
   - In Azure Portal, search for "SSH keys" and click `Create`. 
   - Choose Subscription and Resource group.
   - Specify Key pair name.
   - Select `Upload existing public key` for SSH public key source and paste the public key.
   - Click `Review + create`, then `Create`.
      
      <img src="../assets/makekey.png" alt="SSH" width="400px">

## Create a Virtual Machine

1. Go to Azure Portal and select `Virtual machines`.
2. Click `Create` and choose `Azure virtual machine`.
3. Specify your Subscription and Resource group.
4. For instance details:
   - Enter Virtual machine name, choose a Region e.g. `(Europe) UK South`.
   - Specify Availability options, Security type, Image and Size.
5. Set up Administrator account with SSH key.
6. Configure inbound port rules - `HTTPS` and `SSH`.
7. Click `Next` to choose Disk type and `Next` again to choose Networking options.
8. In the `Tags` tab, set Name as "Owner" and Value as your name.
9. Click `Review + create`, then `Create`.

## SSH into your Virtual Machine

1. Click `Connect` on the left-hand side Navigation.
2. Click `Select` for Native SSH.
      
   <img src="../assets/sshconnect.png" alt="SSH" width="400px">

3. For `Copy and execute SSH command`, provide the path to your SSH private key file: `~/.ssh/keyname`.
4. Copy the output command provided.
5. Paste the command into the terminal of your local machine to establish an SSH connection. You should be logged in as the Administrator account username you provided when creating a VM.
      
      <img src="../assets/sshadmin.png" alt="SSH" width="400px">

## Delete a Virtual Machine

1. In the Azure Portal, select `Virtual machines`.
2. Choose the virtual machine you want to delete.
3. Click `Delete`.
4. Confirm the deletion by following the on-screen prompts.

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




