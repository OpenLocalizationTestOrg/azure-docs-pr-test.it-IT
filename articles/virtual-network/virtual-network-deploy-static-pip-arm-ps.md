---
title: Creare una VM con un indirizzo IP pubblico statico - Azure PowerShell | Documentazione Microsoft
description: Informazioni su come creare una VM con un indirizzo IP pubblico statico mediante Azure PowerShell.
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
ms.openlocfilehash: e4c413d3cb5c242a16f3e534dafe322785a35141
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="d0088-103">Creare una VM con un indirizzo IP pubblico statico mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0088-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d0088-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d0088-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="d0088-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0088-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="d0088-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d0088-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="d0088-107">Modello</span><span class="sxs-lookup"><span data-stu-id="d0088-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * <span data-ttu-id="d0088-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="d0088-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md)</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d0088-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d0088-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d0088-110">Questo articolo illustra l'uso del modello di distribuzione Resource Manager che Microsoft consiglia di usare invece del modello di distribuzione classica per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="d0088-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="d0088-111">Passaggio 1 - avviare lo script</span><span class="sxs-lookup"><span data-stu-id="d0088-111">Step 1 - Start your script</span></span>
<span data-ttu-id="d0088-112">È possibile scaricare lo script di PowerShell completo utilizzato [qui](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="d0088-112">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="d0088-113">Attenersi alla procedura seguente per modificare lo script da usare nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d0088-113">Follow the steps below to change the script to work in your environment.</span></span>

<span data-ttu-id="d0088-114">Modificare i valori delle variabili indicate di seguito in base ai valori che si desidera usare per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d0088-114">Change the values of the variables below based on the values you want to use for your deployment.</span></span> <span data-ttu-id="d0088-115">I valori seguenti si riferiscono allo scenario usato in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="d0088-115">The following values map to the scenario used in this article:</span></span>

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

## <a name="step-2---create-the-necessary-resources-for-your-vm"></a><span data-ttu-id="d0088-116">Passaggio 2 - Creare le risorse necessarie per la VM</span><span class="sxs-lookup"><span data-stu-id="d0088-116">Step 2 - Create the necessary resources for your VM</span></span>
<span data-ttu-id="d0088-117">Prima di creare una VM, è necessario disporre di un gruppo di risorse, una rete virtuale, un IP pubblico e una scheda di rete utilizzabili dalla VM.</span><span class="sxs-lookup"><span data-stu-id="d0088-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC to be used by the VM.</span></span>

1. <span data-ttu-id="d0088-118">Creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d0088-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="d0088-119">Creare rete virtuale e subnet.</span><span class="sxs-lookup"><span data-stu-id="d0088-119">Create the VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="d0088-120">Creare la risorsa di IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="d0088-120">Create the public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="d0088-121">Creare l'interfaccia di rete (NIC) per la VM nella subnet creata in precedenza, con l'IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="d0088-121">Create the network interface (NIC) for the VM in the subnet created above, with the public IP.</span></span> <span data-ttu-id="d0088-122">Notare che il primo cmdlet che recupera la rete virtuale da Azure è necessario perché `Set-AzureRmVirtualNetwork` è stato eseguito per modificare la rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="d0088-122">Notice the first cmdlet retrieving the VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed to change the existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="d0088-123">Creare un account di archiviazione per ospitare l'unità del sistema operativo della VM.</span><span class="sxs-lookup"><span data-stu-id="d0088-123">Create a storage account to host the VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-the-vm"></a><span data-ttu-id="d0088-124">Passaggio 3 - Creare la VM</span><span class="sxs-lookup"><span data-stu-id="d0088-124">Step 3 - Create the VM</span></span>
<span data-ttu-id="d0088-125">Ora che tutte le risorse necessarie sono presenti, è possibile creare una nuova VM.</span><span class="sxs-lookup"><span data-stu-id="d0088-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="d0088-126">Creare l'oggetto di configurazione per la VM.</span><span class="sxs-lookup"><span data-stu-id="d0088-126">Create the configuration object for the VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="d0088-127">Ottenere le credenziali per l'account amministratore locale della VM.</span><span class="sxs-lookup"><span data-stu-id="d0088-127">Get credentials for the VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

3. <span data-ttu-id="d0088-128">Creare un oggetto di configurazione della VM.</span><span class="sxs-lookup"><span data-stu-id="d0088-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="d0088-129">Impostare l'immagine del sistema operativo per la VM.</span><span class="sxs-lookup"><span data-stu-id="d0088-129">Set the operating system image for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="d0088-130">Configurare il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d0088-130">Configure the OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="d0088-131">Aggiungere la scheda di rete alla VM.</span><span class="sxs-lookup"><span data-stu-id="d0088-131">Add the NIC to the VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="d0088-132">Creare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="d0088-132">Create the VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="d0088-133">Salvare il file di script.</span><span class="sxs-lookup"><span data-stu-id="d0088-133">Save the script file.</span></span>

## <a name="step-4---run-the-script"></a><span data-ttu-id="d0088-134">Passaggio 4 - eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="d0088-134">Step 4 - Run the script</span></span>
<span data-ttu-id="d0088-135">Dopo aver apportato tutte le modifiche necessarie e aver compreso il funzionamento dello script illustrato sopra, eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="d0088-135">After making any necessary changes, and understanding the script show above, run the script.</span></span> 

1. <span data-ttu-id="d0088-136">Dalla console di PowerShell o PowerShell ISE, eseguire lo script sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="d0088-136">From a PowerShell console, or PowerShell ISE, run the script above.</span></span>
2. <span data-ttu-id="d0088-137">L'output seguente deve essere visualizzato dopo pochi minuti:</span><span class="sxs-lookup"><span data-stu-id="d0088-137">The following output should be displayed after a few minutes:</span></span>
   
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

