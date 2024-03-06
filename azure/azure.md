# Azure

## Virtual machines
Virtual machines are simulated computers created by software. They allow you to run multiple operating systems on the same physical computer.

   <img src="../assets/single-vm-diagram.png" alt="SSH" width="400px">

## How To...

### Login to Azure

- Go to [Azure Portal](https://portal.azure.com/).
- Sign in with your Azure credentials. <!--Log in with the permissions you need, not more than that.-->

### Create a Virtual Network in Azure

1. In the search bar of the Azure Portal, type and select "Virtual networks".
2. Click "Create".
3. Under Project details:
   - Subscriptions: choose "Azure Training"
   - Resource group: choose "tech257"
5. Under Instance details:
   - Virtual network name:Type "tech257-[your-name]-test-vnet"
   - Region: choose "UK South (Europe)"
6. In the Tags tab:
   - Name: type "Owner"
   - Value: [type-name]
   - Resources: choose "All resources selected"
7. Click "Review + create".
8. Then click "Create".
9. Click "Go to resource" to see the new Virtual Network.

### Setup SSH Key on Azure

1. Open your terminal.

2. Navigate into your .ssh directory:
    ```bash
    cd ~/.ssh/
    ```
3. Generate a new SSH key pair:
    ```bash
    ssh-keygen -t rsa -b 2048 -C "[your-email]"
    ```

   - You'll be prompted to enter a filename for the key. Enter `[your-firstname]-az-key` e.g. `tee-az-key`.


4. Copy the public key:

    ```bash
    cat ~/.ssh/tee-az-key.pub
    ```

5. Add SSH Key to Azure:
   - Go to your Azure Portal. 
   - Type in `SSH keys`, then `Create`
   - Subscription: choose `Azure Training`
   - Resource group: choose `tech257`
   - Key paid name: tidi-az-key 
   - SSH public key source: choose `Upload existing public key`
   - Click `Review + create`
   - Click `Create`