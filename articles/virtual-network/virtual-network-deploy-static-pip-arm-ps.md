---
title: una macchina virtuale con un indirizzo IP pubblico statico - Azure PowerShell aaaCreate | Documenti Microsoft
description: Informazioni su come una macchina virtuale con un indirizzo IP pubblico statico toocreate indirizzo tramite PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ad975ab9-d69f-45c1-9e45-0d3f0f51e87e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d2b88319cb114b8616f60dbee41e8fdc6d8b1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="5770b-103">Creare una VM con un indirizzo IP pubblico statico mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5770b-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5770b-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5770b-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="5770b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5770b-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="5770b-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5770b-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="5770b-107">Modello</span><span class="sxs-lookup"><span data-stu-id="5770b-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * <span data-ttu-id="5770b-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="5770b-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md)</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="5770b-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5770b-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5770b-110">In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="5770b-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="5770b-111">Passaggio 1 - avviare lo script</span><span class="sxs-lookup"><span data-stu-id="5770b-111">Step 1 - Start your script</span></span>
<span data-ttu-id="5770b-112">È possibile scaricare hello completo script di PowerShell utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="5770b-112">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="5770b-113">Eseguire operazioni di hello seguenti toochange hello script toowork nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="5770b-113">Follow hello steps below toochange hello script toowork in your environment.</span></span>

<span data-ttu-id="5770b-114">Modificare i valori hello di variabili di hello riportate di seguito in base ai valori hello desiderato toouse per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5770b-114">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="5770b-115">Hello segue valori mappa toohello scenario usato in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="5770b-115">hello following values map toohello scenario used in this article:</span></span>

```powershell
# Set variables resource group
$rgName                = "IaaSStory"
$location              = "West US"

# Set variables for VNet
$vnetName              = "WTestVNet"
$vnetPrefix            = "192.168.0.0/16"
$subnetName            = "FrontEnd"
$subnetPrefix          = "192.168.1.0/24"

# Set variables for storage
$stdStorageAccountName = "iaasstorystorage"

# Set variables for VM
$vmSize                = "Standard_A1"
$diskSize              = 127
$publisher             = "MicrosoftWindowsServer"
$offer                 = "WindowsServer"
$sku                   = "2012-R2-Datacenter"
$version               = "latest"
$vmName                = "WEB1"
$osDiskName            = "osdisk"
$nicName               = "NICWEB1"
$privateIPAddress      = "192.168.1.101"
$pipName               = "PIPWEB1"
$dnsName               = "iaasstoryws1"
```

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="5770b-116">Passaggio 2: creare hello le risorse necessarie per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5770b-116">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="5770b-117">Prima di creare una macchina virtuale, è necessario un gruppo di risorse tra reti virtuali, public IP e NIC toobe utilizzato da hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5770b-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="5770b-118">Creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5770b-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="5770b-119">Creare hello rete virtuale e una subnet.</span><span class="sxs-lookup"><span data-stu-id="5770b-119">Create hello VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="5770b-120">Creare una risorsa IP pubblica hello.</span><span class="sxs-lookup"><span data-stu-id="5770b-120">Create hello public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="5770b-121">Creare l'interfaccia di rete (NIC) hello per hello VM nella subnet hello creato in precedenza, con l'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="5770b-121">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="5770b-122">Si noti hello primo cmdlet recupero hello rete virtuale da Azure, è necessario perché un `Set-AzureRmVirtualNetwork` è stato eseguito toochange hello rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="5770b-122">Notice hello first cmdlet retrieving hello VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed toochange hello existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="5770b-123">Creare un hello toohost account di archiviazione unità del sistema operativo VM.</span><span class="sxs-lookup"><span data-stu-id="5770b-123">Create a storage account toohost hello VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="5770b-124">Passaggio 3: creare hello VM</span><span class="sxs-lookup"><span data-stu-id="5770b-124">Step 3 - Create hello VM</span></span>
<span data-ttu-id="5770b-125">Ora che tutte le risorse necessarie sono presenti, è possibile creare una nuova VM.</span><span class="sxs-lookup"><span data-stu-id="5770b-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="5770b-126">Creare l'oggetto di configurazione di hello per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5770b-126">Create hello configuration object for hello VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="5770b-127">Ottenere le credenziali per hello account amministratore locale della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5770b-127">Get credentials for hello VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

3. <span data-ttu-id="5770b-128">Creare un oggetto di configurazione della VM.</span><span class="sxs-lookup"><span data-stu-id="5770b-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="5770b-129">Impostare l'immagine del sistema operativo hello per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5770b-129">Set hello operating system image for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="5770b-130">Configurare un disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="5770b-130">Configure hello OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="5770b-131">Aggiungere hello NIC toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5770b-131">Add hello NIC toohello VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="5770b-132">Creare VM hello.</span><span class="sxs-lookup"><span data-stu-id="5770b-132">Create hello VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="5770b-133">Salvare il file di script hello.</span><span class="sxs-lookup"><span data-stu-id="5770b-133">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="5770b-134">Passaggio 4: hello Esegui script</span><span class="sxs-lookup"><span data-stu-id="5770b-134">Step 4 - Run hello script</span></span>
<span data-ttu-id="5770b-135">Dopo aver apportato le modifiche necessarie e comprendere script hello illustrato sopra, eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="5770b-135">After making any necessary changes, and understanding hello script show above, run hello script.</span></span> 

1. <span data-ttu-id="5770b-136">Dalla console di PowerShell o PowerShell ISE, eseguire lo script hello precedente.</span><span class="sxs-lookup"><span data-stu-id="5770b-136">From a PowerShell console, or PowerShell ISE, run hello script above.</span></span>
2. <span data-ttu-id="5770b-137">Dopo l'output di Hello dovrebbe essere visualizzato dopo pochi minuti:</span><span class="sxs-lookup"><span data-stu-id="5770b-137">hello following output should be displayed after a few minutes:</span></span>
   
        ResourceGroupName : IaaSStory
        Location          : westus
        ProvisioningState : Succeeded
        Tags              : 
        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {}
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "AddressPrefix": "192.168.1.0/24"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        Id                : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {
                              "DnsServers": []
                            }
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "Etag": [Id],
                                "Id": "/subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "ProvisioningState": "Succeeded"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : [Id]
        Id                : /subscriptions/[Subscription Id]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        TrackingOperationId : [Id]
        RequestId           : [Id]
        Status              : Succeeded
        StatusCode          : OK
        Output              : 
        StartTime           : [Subscription Id]
        EndTime             : [Subscription Id]
        Error               : 
        ErrorText           : 

