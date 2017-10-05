---
title: Come creare immagini di macchine virtuali di Windows in Azure con Packer | Microsoft Docs
description: Informazioni su come usare Packer per creare immagini di macchine virtuali di Windows in Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 11a4a4d65be09e6c518836c25bb455a6df738dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="6450e-103">Come usare Packer per creare immagini di macchine virtuali di Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="6450e-103">How to use Packer to create Windows virtual machine images in Azure</span></span>
<span data-ttu-id="6450e-104">Ogni macchina virtuale (VM, Virtual Machine) in Azure viene creata a partire da un'immagine che ne definisce la distribuzione di Windows e la versione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="6450e-104">Each virtual machine (VM) in Azure is created from an image that defines the Windows distribution and OS version.</span></span> <span data-ttu-id="6450e-105">Le immagini possono includere applicazioni e configurazioni preinstallate.</span><span class="sxs-lookup"><span data-stu-id="6450e-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="6450e-106">In Microsoft Azure Marketplace sono disponibili molte prime immagini e immagini di terze parti per i sistemi operativi e gli ambienti applicativi più diffusi. In alternativa, è possibile creare immagini personalizzate su misura per le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="6450e-106">The Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="6450e-107">Questo articolo illustra in dettaglio come definire e compilare immagini personalizzate in Azure tramite lo strumento open source [Packer](https://www.packer.io/).</span><span class="sxs-lookup"><span data-stu-id="6450e-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="6450e-108">Creare un gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="6450e-108">Create Azure resource group</span></span>
<span data-ttu-id="6450e-109">Durante il processo di compilazione della macchina virtuale di origine Packer crea risorse di Azure temporanee.</span><span class="sxs-lookup"><span data-stu-id="6450e-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="6450e-110">Per acquisire la macchina virtuale di origine per usarla come immagine, è necessario definire un gruppo di risorse,</span><span class="sxs-lookup"><span data-stu-id="6450e-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="6450e-111">nel quale verrà archiviato l'output del processo di compilazione di Packer.</span><span class="sxs-lookup"><span data-stu-id="6450e-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="6450e-112">Creare un gruppo di risorse con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="6450e-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="6450e-113">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="6450e-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="6450e-114">Creare credenziali di Azure</span><span class="sxs-lookup"><span data-stu-id="6450e-114">Create Azure credentials</span></span>
<span data-ttu-id="6450e-115">Per eseguire l'autenticazione con Azure, Packer usa un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="6450e-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="6450e-116">Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come Packer.</span><span class="sxs-lookup"><span data-stu-id="6450e-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="6450e-117">Le autorizzazioni per le operazioni che l'entità servizio può eseguire in Azure vengono controllate e definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="6450e-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="6450e-118">Creare un'entità servizio con [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) e assegnare le autorizzazioni per consentire all'entità servizio di creare e gestire risorse con [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="6450e-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for the service principal to create and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="6450e-119">Per eseguire l'autenticazione in Azure è anche necessario ottenere l'ID del tenant e l'ID della sottoscrizione di Azure con [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="6450e-119">To authenticate to Azure, you also need to obtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="6450e-120">Questi due ID verranno usati nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="6450e-120">You use these two IDs in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="6450e-121">Definire un modello di Packer</span><span class="sxs-lookup"><span data-stu-id="6450e-121">Define Packer template</span></span>
<span data-ttu-id="6450e-122">Per compilare immagini, è necessario creare un modello come file JSON.</span><span class="sxs-lookup"><span data-stu-id="6450e-122">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="6450e-123">Nel modello si definiscono i compilatori e gli strumenti di provisioning che eseguono il processo di compilazione effettivo.</span><span class="sxs-lookup"><span data-stu-id="6450e-123">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="6450e-124">Packer è dotato di uno [strumento di provisioning per Azure](https://www.packer.io/docs/builders/azure.html) che consente di definire risorse di Azure, ad esempio le credenziali delle entità servizio create nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="6450e-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="6450e-125">Creare un file con nome *windows.json* e incollare al suo interno il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="6450e-125">Create a file named *windows.json* and paste the following content.</span></span> <span data-ttu-id="6450e-126">Immettere valori personalizzati per i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="6450e-126">Enter your own values for the following:</span></span>

| <span data-ttu-id="6450e-127">Parametro</span><span class="sxs-lookup"><span data-stu-id="6450e-127">Parameter</span></span>                           | <span data-ttu-id="6450e-128">Origine</span><span class="sxs-lookup"><span data-stu-id="6450e-128">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="6450e-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="6450e-129">*client_id*</span></span>                         | <span data-ttu-id="6450e-130">ID entità servizio di visualizzazione con `$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="6450e-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="6450e-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="6450e-131">*client_secret*</span></span>                     | <span data-ttu-id="6450e-132">Password specificata in`$securePassword`</span><span class="sxs-lookup"><span data-stu-id="6450e-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="6450e-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="6450e-133">*tenant_id*</span></span>                         | <span data-ttu-id="6450e-134">Output del comando `$sub.TenantId`</span><span class="sxs-lookup"><span data-stu-id="6450e-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="6450e-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="6450e-135">*subscription_id*</span></span>                   | <span data-ttu-id="6450e-136">Output del comando `$sub.SubscriptionId`</span><span class="sxs-lookup"><span data-stu-id="6450e-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="6450e-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="6450e-137">*object_id*</span></span>                         | <span data-ttu-id="6450e-138">ID oggetto entità servizio di visualizzazione con `$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="6450e-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="6450e-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="6450e-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="6450e-140">Nome del gruppo di risorse creato nel primo passaggio</span><span class="sxs-lookup"><span data-stu-id="6450e-140">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="6450e-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="6450e-141">*managed_image_name*</span></span>                | <span data-ttu-id="6450e-142">Nome per l'immagine del disco gestito che viene creata</span><span class="sxs-lookup"><span data-stu-id="6450e-142">Name for the managed disk image that is created</span></span> |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

<span data-ttu-id="6450e-143">Questo modello compila una macchina virtuale di Windows Server 2016, installa IIS e quindi generalizza la macchina virtuale con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="6450e-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes the VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="6450e-144">Compilare l'immagine in Packer</span><span class="sxs-lookup"><span data-stu-id="6450e-144">Build Packer image</span></span>
<span data-ttu-id="6450e-145">Se Packer non è installato nel computer locale, [seguire le istruzioni di installazione di Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="6450e-145">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="6450e-146">Compilare l'immagine specificando il file del modello di Packer come segue:</span><span class="sxs-lookup"><span data-stu-id="6450e-146">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="6450e-147">Ecco un esempio di output dei comandi precedenti:</span><span class="sxs-lookup"><span data-stu-id="6450e-147">An example of the output from the preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting the certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting the certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM to become available...
==> azure-arm: Connected to WinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying the machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="6450e-148">Packer impiega alcuni minuti per compilare la macchina virtuale, eseguire gli strumenti di provisioning e pulire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6450e-148">It takes a few minutes for Packer to build the VM, run the provisioners, and clean up the deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="6450e-149">Creare una macchina virtuale da un'immagine di Azure</span><span class="sxs-lookup"><span data-stu-id="6450e-149">Create VM from Azure Image</span></span>
<span data-ttu-id="6450e-150">Impostare nome utente e password dell'amministratore delle macchine virtuali con il comando [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="6450e-150">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="6450e-151">È ora possibile creare una macchina virtuale dall'immagine con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="6450e-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="6450e-152">L'esempio seguente crea una macchina virtuale denominata *myVM* da *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="6450e-152">The following example creates a VM named *myVM* from *myPackerImage*.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define the image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="6450e-153">La creazione della macchina virtuale richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="6450e-153">It takes a few minutes to create the VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="6450e-154">Testare la macchina virtuale e IIS</span><span class="sxs-lookup"><span data-stu-id="6450e-154">Test VM and IIS</span></span>
<span data-ttu-id="6450e-155">Ottenere l'indirizzo IP pubblico della macchina virtuale con il comando [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="6450e-155">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="6450e-156">L'esempio seguente ottiene l'indirizzo IP per *myPublicIP* creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="6450e-156">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="6450e-157">Sarà quindi possibile immettere l'indirizzo IP pubblico in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="6450e-157">You can then enter the public IP address in to a web browser.</span></span>

![Sito IIS predefinito](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="6450e-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6450e-159">Next steps</span></span>
<span data-ttu-id="6450e-160">In questo esempio Packer è stato usato per creare un'immagine di macchina virtuale con IIS già installato.</span><span class="sxs-lookup"><span data-stu-id="6450e-160">In this example, you used Packer to create a VM image with IIS already installed.</span></span> <span data-ttu-id="6450e-161">È possibile usare questa immagine di macchina virtuale insieme a flussi di lavoro di distribuzione esistenti, ad esempio per distribuire app in macchine virtuali create dall'immagine con Team Services, Ansible, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="6450e-161">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="6450e-162">Per altri modelli di Packer di esempio per distribuzioni di Windows di altro tipo, vedere [questo repository di GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="6450e-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>