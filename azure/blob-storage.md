## Blob Storage

Blobs are a type of data storage in cloud computing, typically used for storing unstructured data such as images, videos, documents, and other file types. In Azure they are used within Azure Storage accounts. 

They allow you to store and retrieve data efficiently, and can access and manage your files from anywhere with an internet connection.

### Blob commands

Prerequisite: Install [Azure CLI Ubuntu Debian version](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt) on Azure VM machine:
     `curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash`

   - Create storage account: `az storage account create --name [storage-account-name] --resource-group [resource_group] --location uksouth --sku Standard_LRS`
   - Create container:
     `az storage container create --account-name [accountname] --name [containername] --auth-mode login`
   - Delete container:
     `az storage container delete --account-name [accountname] --name [containername] --auth-mode login`
   - Upload a file as a blob in our container:
     `az storage blob upload --account-name [storage-account-name] --container-name [containername]] --name [container-object-name] --file [original-object-name] --auth-mode login`

To clean resources:
```
az storage account delete -n MyStorageAccount -g MyResourceGroup
```
This will prompt you to say yes (`y`) or no (`n`).

### Script to download image from the internet to blob storage: 
`./use-blob.sh`

```
#!/bin/bash

az storage account create --name tech257tidistorage --resource-group tech257 --location uksouth --sku Standard_LRS

az storage container create --account-name tech257tidistorage --name mycontainer --auth-mode login

curl -o cat.jpg https://upload.wikimedia.org/wikipedia/commons/7/74/A-Cat.jpg

az storage blob upload --account-name tech257tidistorage --container-name mycontainer --name azurecat.jpg --file cat.jpg --auth-mode login

if [ ! -f /tech257_sparta_app/app/views/index2.ejs ]; then
    sudo cp /tech257_sparta_app/app/views/index.ejs /tech257_sparta_app/app/views/index2.ejs
fi

BLOB_URL=$(az storage blob url --account-name tech257tidistorage --container-name mycontainer --name azurecat.jpg --auth-mode login)

sudo sed -i "27s|<h2>The app is running correctly.</h2>|& <img src=$BLOB_URL>|" /tech257_sparta_app/app/views/index.ejs

az storage account update --name tech257tidistorage --allow-blob-public-access true

sleep 15

az storage container set-permission --account-name tech257tidistorage --name mycontainer --public-access blob
```

Results:
<br>
<img src="../assets/img33.png">
<img src="../assets/img34.png">

<!-- ### Script to remove the storage account: 
`./revert.sh` -->
