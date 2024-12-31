# cCloud Virtual Appliance Images in Microsoft Azure

*Prerequisite*: The user will need cCloud Azure SAS URLs to be shared by cPacket via a text file named `ccloud-urls.txt`. These URLs enable temporary access to securely download cPacket images and expire 14 days from the date of creation.

## Detailed Instructions

1. Obtain the cCloud Azure SAS URLs from a cPacket representative (`ccloud-urls.txt`).
2. Login to the desired Azure account and open Azure Cloud Shell.
3. Ensure that the Azure Cloud Shell storage account is in the same subscription as the destination for the images.
4. Upload the SAS URL txt file to Azure Cloud Shell.
5. Download and execute the ccloud-azure-images script.

### 1. Obtain the Appliance URLs File

Contact cPacket Networks to obtain the SAS URLs utilized to deploy cCloud virtual appliances. The filename is `ccloud-urls.txt` by default and is referenced in the script below.

### 2. Open the Azure Cloud Shell

In the Azure portal, open the Azure Cloud Shell by clicking on the icon in the upper right corner of the Azure portal.

![Open the shell](/static-assets/open-shell.png "Open the Azure cloud shell")

### 3. Ensure Proper Cloud Shell Storage Configuration

For the `ccloud-azure-images` script to correctly copy images, if using the Azure Cloud Shell, the Cloud Shell storage account must be in the same subscription as the destination for the images. This ensures that the resources are properly accessible and manageable.

### 4. Upload the Appliance URLs

Upload the `ccloud-urls.txt` file to the Azure Cloud Shell. (The root directory of the Cloud Shell is expected, and it is the default upload location.)

![Upload file](/static-assets/upload-file-to-shell.png "Upload the 'ccloud-urls.txt' file to cloud shell")

### 5. Create the Images

The `ccloud-azure-images` script will create the images in your Azure subscription using the URLs provided in `ccloud-urls.txt`.

The following command creates a resource group called `cpacket` in the `westus2` region. Pipe the script directly through the shell as in the following invocation:

```bash
curl -L https://raw.githubusercontent.com/cPacketNetworks/ccloud-images/main/ccloud-azure-images | bash -s -- -g cpacket -l westus2
```

This creates a new resource group with a name such as `cpacket` in the `westus2` region.

## Customizing the deployment

If you have an existing resource group or would like to create the resource group with a specific name, first download the script and then supply it with the name of your resource group.

Download the script:

```bash
curl -L https://raw.githubusercontent.com/cPacketNetworks/ccloud-images/main/ccloud-azure-images > ccloud-azure-images
```

Make it executable:

```bash
chmod +x ccloud-azure-images
```

Run it:

```bash
./ccloud-azure-images -g resource-group-name -l region
```

After executing the script, you should have new resources in your resource group corresponding to the cCloud appliances in the URL file above:

![New resources](/static-assets/new-resources.png "cCloud images")

[cloudshell]: https://learn.microsoft.com/en-us/azure/cloud-shell/overview
