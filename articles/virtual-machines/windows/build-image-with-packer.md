---
title: aaaHow toocreate immagini di macchina virtuale Windows Azure con chi | Documenti Microsoft
description: Informazioni su come le immagini di toocreate chi toouse delle macchine virtuali di Windows in Azure
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
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="425ad-103">Come le immagini di macchina virtuale Windows di toouse chi toocreate in Azure</span><span class="sxs-lookup"><span data-stu-id="425ad-103">How toouse Packer toocreate Windows virtual machine images in Azure</span></span>
<span data-ttu-id="425ad-104">Ogni macchina virtuale (VM) in Azure viene creato da un'immagine che definisce la distribuzione di Windows hello e versione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="425ad-104">Each virtual machine (VM) in Azure is created from an image that defines hello Windows distribution and OS version.</span></span> <span data-ttu-id="425ad-105">Le immagini possono includere applicazioni e configurazioni preinstallate.</span><span class="sxs-lookup"><span data-stu-id="425ad-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="425ad-106">Hello Azure Marketplace fornisce molte immagini prima e di terze parti per più comuni del sistema operativo e gli ambienti di applicazione, oppure è possibile creare le proprie esigenze tooyour immagini personalizzate personalizzate.</span><span class="sxs-lookup"><span data-stu-id="425ad-106">hello Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="425ad-107">In questo articolo illustra in dettaglio come hello toouse aprire lo strumento di origine [chi](https://www.packer.io/) toodefine e compilazione immagini personalizzate in Azure.</span><span class="sxs-lookup"><span data-stu-id="425ad-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="425ad-108">Creare un gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="425ad-108">Create Azure resource group</span></span>
<span data-ttu-id="425ad-109">Durante il processo di compilazione hello, chi crea risorse di Azure temporanee durante la compilazione di macchina virtuale di origine hello.</span><span class="sxs-lookup"><span data-stu-id="425ad-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="425ad-110">toocapture che VM di origine per l'utilizzo come un'immagine, è necessario definire un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="425ad-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="425ad-111">l'output dal processo di compilazione chi hello Hello viene archiviato in questo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="425ad-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="425ad-112">Creare un gruppo di risorse con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="425ad-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="425ad-113">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="425ad-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="425ad-114">Creare credenziali di Azure</span><span class="sxs-lookup"><span data-stu-id="425ad-114">Create Azure credentials</span></span>
<span data-ttu-id="425ad-115">Per eseguire l'autenticazione con Azure, Packer usa un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="425ad-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="425ad-116">Un'entità servizio di Azure è un'identità di sicurezza che è possibile usare con le app, con i servizi e con strumenti di automazione come Packer.</span><span class="sxs-lookup"><span data-stu-id="425ad-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="425ad-117">È controllare e definire le autorizzazioni di hello come entità di servizio toowhat operazioni hello è possibile eseguire in Azure.</span><span class="sxs-lookup"><span data-stu-id="425ad-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="425ad-118">Creare un servizio principale con [New AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) e assegnare le autorizzazioni per toocreate principale di servizio hello e gestire le risorse con [New AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="425ad-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for hello service principal toocreate and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="425ad-119">tooAzure tooauthenticate, è necessario anche tooobtain degli ID tenant e una sottoscrizione Azure con [Get AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="425ad-119">tooauthenticate tooAzure, you also need tooobtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="425ad-120">Utilizzare queste due ID nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="425ad-120">You use these two IDs in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="425ad-121">Definire un modello di Packer</span><span class="sxs-lookup"><span data-stu-id="425ad-121">Define Packer template</span></span>
<span data-ttu-id="425ad-122">immagini toobuild, si crea un modello come un file JSON.</span><span class="sxs-lookup"><span data-stu-id="425ad-122">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="425ad-123">Nel modello hello definisce generatori e provisioners per l'esecuzione di hello effettivo processo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="425ad-123">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="425ad-124">Chi ha un [strumento di provisioning per Azure](https://www.packer.io/docs/builders/azure.html) che consentono di toodefine Azure risorse, ad esempio credenziali dell'entità servizio hello create nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="425ad-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="425ad-125">Creare un file denominato *windows.json* e Incolla hello seguendo il contenuto.</span><span class="sxs-lookup"><span data-stu-id="425ad-125">Create a file named *windows.json* and paste hello following content.</span></span> <span data-ttu-id="425ad-126">Immettere i valori per i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="425ad-126">Enter your own values for hello following:</span></span>

| <span data-ttu-id="425ad-127">.</span><span class="sxs-lookup"><span data-stu-id="425ad-127">Parameter</span></span>                           | <span data-ttu-id="425ad-128">Dove tooobtain</span><span class="sxs-lookup"><span data-stu-id="425ad-128">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="425ad-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="425ad-129">*client_id*</span></span>                         | <span data-ttu-id="425ad-130">ID entità servizio di visualizzazione con `$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="425ad-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="425ad-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="425ad-131">*client_secret*</span></span>                     | <span data-ttu-id="425ad-132">Password specificata in`$securePassword`</span><span class="sxs-lookup"><span data-stu-id="425ad-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="425ad-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="425ad-133">*tenant_id*</span></span>                         | <span data-ttu-id="425ad-134">Output del comando `$sub.TenantId`</span><span class="sxs-lookup"><span data-stu-id="425ad-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="425ad-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="425ad-135">*subscription_id*</span></span>                   | <span data-ttu-id="425ad-136">Output del comando `$sub.SubscriptionId`</span><span class="sxs-lookup"><span data-stu-id="425ad-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="425ad-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="425ad-137">*object_id*</span></span>                         | <span data-ttu-id="425ad-138">ID oggetto entità servizio di visualizzazione con `$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="425ad-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="425ad-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="425ad-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="425ad-140">Nome del gruppo di risorse creato nel primo passaggio hello</span><span class="sxs-lookup"><span data-stu-id="425ad-140">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="425ad-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="425ad-141">*managed_image_name*</span></span>                | <span data-ttu-id="425ad-142">Nome dell'immagine di disco gestito hello creato</span><span class="sxs-lookup"><span data-stu-id="425ad-142">Name for hello managed disk image that is created</span></span> |

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

<span data-ttu-id="425ad-143">Questo modello crea una macchina virtuale di Windows Server 2016, viene installato IIS, quindi consente di generalizzare hello macchina virtuale con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="425ad-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes hello VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="425ad-144">Compilare l'immagine in Packer</span><span class="sxs-lookup"><span data-stu-id="425ad-144">Build Packer image</span></span>
<span data-ttu-id="425ad-145">Se non si dispone già installati nel computer locale, chi [seguire le istruzioni di installazione di hello chi](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="425ad-145">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="425ad-146">Creare immagini hello specificando il chi file modello nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="425ad-146">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="425ad-147">Un esempio di output di hello da hello precedenti comandi è la seguente:</span><span class="sxs-lookup"><span data-stu-id="425ad-147">An example of hello output from hello preceding commands is as follows:</span></span>

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
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
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
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="425ad-148">Sono necessari alcuni minuti per toobuild hello chi macchina virtuale, eseguire provisioners hello e pulizia hello distribuzione.</span><span class="sxs-lookup"><span data-stu-id="425ad-148">It takes a few minutes for Packer toobuild hello VM, run hello provisioners, and clean up hello deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="425ad-149">Creare una macchina virtuale da un'immagine di Azure</span><span class="sxs-lookup"><span data-stu-id="425ad-149">Create VM from Azure Image</span></span>
<span data-ttu-id="425ad-150">Impostare un amministratore di nome utente e password per le macchine virtuali hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="425ad-150">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="425ad-151">È ora possibile creare una macchina virtuale dall'immagine con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="425ad-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="425ad-152">esempio Hello crea una macchina virtuale denominata *myVM* da *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="425ad-152">hello following example creates a VM named *myVM* from *myPackerImage*.</span></span>

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

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="425ad-153">Sono necessari alcuni minuti toocreate hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="425ad-153">It takes a few minutes toocreate hello VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="425ad-154">Testare la macchina virtuale e IIS</span><span class="sxs-lookup"><span data-stu-id="425ad-154">Test VM and IIS</span></span>
<span data-ttu-id="425ad-155">Ottenere l'indirizzo IP pubblico hello della macchina virtuale con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="425ad-155">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="425ad-156">esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="425ad-156">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="425ad-157">È quindi possibile immettere l'indirizzo IP pubblico hello nel browser web tooa.</span><span class="sxs-lookup"><span data-stu-id="425ad-157">You can then enter hello public IP address in tooa web browser.</span></span>

![Sito IIS predefinito](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="425ad-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="425ad-159">Next steps</span></span>
<span data-ttu-id="425ad-160">In questo esempio, chi toocreate un'immagine di macchina virtuale è usato con installato IIS.</span><span class="sxs-lookup"><span data-stu-id="425ad-160">In this example, you used Packer toocreate a VM image with IIS already installed.</span></span> <span data-ttu-id="425ad-161">È possibile utilizzare questa immagine di macchina virtuale insieme a distribuzione flussi di lavoro esistenti, ad esempio toodeploy tooVMs l'app creata da hello immagine con Team Services, Ansible, Chef o Puppet.</span><span class="sxs-lookup"><span data-stu-id="425ad-161">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="425ad-162">Per altri modelli di Packer di esempio per distribuzioni di Windows di altro tipo, vedere [questo repository di GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="425ad-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>