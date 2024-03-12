# cCloud virtual appliance images in Microsoft Azure

> Obtain the cCloud virtual appliance images before deploying them into Azure.

## tl;dr

You already have the SAS URLs of the cCloud virtual appliance images in a file called `ccloud-urls.txt` in the [Azure cloud shell][cloudshell].
You want to deploy these images into Azure in a resource group called `cpacket` in the `westus2` region.
Paste the following into the Azure cloud shell and press Enter:

```bash
curl -L https://raw.githubusercontent.com/cPacketNetworks/ccloud-images/main/ccloud-azure-images | bash -s -- -g cpacket -l westus2
```

## Detailed instructions

1. Obtain the appliance URL file from cPacket (default name `ccloud-urls.txt`).
1. Open the Azure cloud shell.
1. Upload it to the Azure cloud shell.
1. Download and execute the `ccloud-azure-images` script.

### 1. Obtain the appliance URLs file

Contact cPacket Networks to obtain the appliance URLs file.
This file contains the Shared Access Signature (SAS) URLs of the appliances.
(It is called `ccloud-urls.txt` by default.)

### 2. Open the Azure cloud shell

In the Azure portal, open the Azure cloud shell by clicking on the icon in the upper right corner of the Azure portal.

![Open the shell](/static-assets/open-shell.png "Open the Azure cloud shell")

### 3. Upload the appliance URLs

Upload the `ccloud-urls.txt` file to the Azure cloud shell.
(The root directory of the cloud shell is expected, and it is the default upload location.)

![Upload file](/static-assets/upload-file-to-shell.png "Upload the 'ccloud-urls.txt' file to cloud shell")

### 4. Create the images

The `ccloud-azure-images` script will create the images in your Azure subscription using the URLs provided in `ccloud-urls.txt`.

The following command creates a resource group called `cpacket` in the `westus2` region
Pipe the script directly through the shell as in the following invocation:

```bash
curl -L https://raw.githubusercontent.com/cPacketNetworks/ccloud-images/main/ccloud-azure-images | bash -s -- -g cpacket -l westus2
```

This creates a new resource group with a name such as `cpacket-ccloud-abc123` in the `eastus2` region.

## Customizing the deployment

Instead, if you have an existing resource group or would like to create the resource group with a specific name, first download the script and then supply it with the name of your resource group.

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
