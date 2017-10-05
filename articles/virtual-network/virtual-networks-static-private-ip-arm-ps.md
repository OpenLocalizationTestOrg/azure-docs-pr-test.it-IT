---
title: Configurare indirizzi IP privati per le VM - Azure PowerShell | Documentazione Microsoft
description: Informazioni su come configurare indirizzi IP privati per le macchine virtuali mediante PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2810190897c44c944912ef3325b1f40479aa3078
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="06cf0-103">Configurare indirizzi IP privati per una macchina virtuale mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="06cf0-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="06cf0-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="06cf0-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="06cf0-105">Microsoft consiglia di creare le risorse tramite il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="06cf0-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="06cf0-106">Per altre informazioni sulle differenze tra i due modelli, leggere l'articolo [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Informazioni sui modelli di distribuzione di Azure).</span><span class="sxs-lookup"><span data-stu-id="06cf0-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="06cf0-107">Questo articolo illustra il modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="06cf0-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="06cf0-108">È anche possibile [gestire un indirizzo IP statico privato nel modello di distribuzione classico](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="06cf0-108">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="06cf0-109">I comandi di esempio PowerShell riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="06cf0-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="06cf0-110">Se si desidera eseguire i comandi illustrati in questo documento, creare innanzitutto l'ambiente di prova descritto in [creare una rete virtuale](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="06cf0-110">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="06cf0-111">Creare una VM con un indirizzo IP privato statico</span><span class="sxs-lookup"><span data-stu-id="06cf0-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="06cf0-112">Per creare una VM denominata *DNS01* nella subnet *FrontEnd* di una rete virtuale denominata *TestVNet* con un indirizzo IP statico privato di *192.168.1.101*, seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="06cf0-112">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="06cf0-113">Impostare le variabili per l'account di archiviazione, il percorso, il gruppo di risorse e le credenziali da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="06cf0-113">Set variables for the storage account, location, resource group, and credentials to be used.</span></span> <span data-ttu-id="06cf0-114">È necessario immettere un nome utente e una password per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="06cf0-114">You will need to enter a user name and password for the VM.</span></span> <span data-ttu-id="06cf0-115">L’account di archiviazione e il gruppo di risorse deve esistere già.</span><span class="sxs-lookup"><span data-stu-id="06cf0-115">The storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type the name and password of the local administrator account."
    ```

2. <span data-ttu-id="06cf0-116">Recuperare la rete virtuale e la subnet che si desidera creare nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="06cf0-116">Retrieve the virtual network and subnet you want to create the VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="06cf0-117">Se necessario, creare un indirizzo IP pubblico per accedere alla macchina virtuale da Internet.</span><span class="sxs-lookup"><span data-stu-id="06cf0-117">If necessary, create a public IP address to access the VM from the Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="06cf0-118">Creare una scheda di rete utilizzando l'indirizzo IP privato statico da assegnare alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="06cf0-118">Create a NIC using the static private IP address you want to assign to the VM.</span></span> <span data-ttu-id="06cf0-119">Assicurarsi che l'indirizzo IP venga dall'intervallo di subnet che si aggiunge alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="06cf0-119">Make sure the IP is from the subnet range you are adding the VM to.</span></span> <span data-ttu-id="06cf0-120">Questo è il passaggio principale di questo articolo, in cui si imposta l’IP privato che deve essere statico.</span><span class="sxs-lookup"><span data-stu-id="06cf0-120">This is the main step for this article, where you set the private IP to be static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="06cf0-121">Creare la macchina virtuale utilizzando la scheda di rete creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="06cf0-121">Create the VM using the NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="06cf0-122">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="06cf0-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="06cf0-123">Recuperare le informazioni relative all'indirizzo IP privato statico per un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="06cf0-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="06cf0-124">Per visualizzare le informazioni relative all'indirizzo IP privato statico per la macchina virtuale creata con lo script precedente, eseguire il comando PowerShell seguente e osservare i valori per *PrivateIpAddress* e *PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="06cf0-124">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="06cf0-125">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="06cf0-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="06cf0-126">Rimuovere un indirizzo IP privato statico da un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="06cf0-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="06cf0-127">Per rimuovere l'indirizzo IP privato statico aggiunto alla macchina virtuale nello script precedente, eseguire il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="06cf0-127">To remove the static private IP address added to the VM in the script above, run the following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="06cf0-128">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="06cf0-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-to-a-network-interface"></a><span data-ttu-id="06cf0-129">Aggiungere un indirizzo IP privato statico a un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="06cf0-129">Add a static private IP address to a network interface</span></span>
<span data-ttu-id="06cf0-130">Per aggiungere un indirizzo IP privato statico alla macchina virtuale creata usando lo script precedente, eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="06cf0-130">To add a static private IP address to the VM created using the script above, run the following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-the-allocation-method-for-a-private-ip-address-assigned-to-a-network-interface"></a><span data-ttu-id="06cf0-131">Modificare il metodo di allocazione per un indirizzo IP privato assegnato a un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="06cf0-131">Change the allocation method for a private IP address assigned to a network interface</span></span>

<span data-ttu-id="06cf0-132">Un indirizzo IP privato viene assegnato a una scheda di interfaccia di rete con il metodo di allocazione statico o dinamico.</span><span class="sxs-lookup"><span data-stu-id="06cf0-132">A private IP address is assigned to a NIC with the static or dynamic allocation method.</span></span> <span data-ttu-id="06cf0-133">Gli indirizzi IP dinamici possono cambiare dopo l'avvio di una VM che in precedenza era in stato di arresto (deallocazione).</span><span class="sxs-lookup"><span data-stu-id="06cf0-133">Dynamic IP addresses can change after starting a VM that was previously in the stopped (deallocated) state.</span></span> <span data-ttu-id="06cf0-134">Questo può causare problemi se la VM ospita un servizio che richiede lo stesso indirizzo IP, anche dopo il riavvio da uno stato di arresto (deallocazione).</span><span class="sxs-lookup"><span data-stu-id="06cf0-134">This can potentially cause issues if the VM is hosting a service that requires the same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="06cf0-135">Gli indirizzi IP statici vengono mantenuti fino a quando non viene eliminata la VM.</span><span class="sxs-lookup"><span data-stu-id="06cf0-135">Static IP addresses are retained until the VM is deleted.</span></span> <span data-ttu-id="06cf0-136">Per cambiare il metodo di allocazione di un indirizzo IP, eseguire lo script seguente, che cambia il metodo di allocazione da dinamico in statico.</span><span class="sxs-lookup"><span data-stu-id="06cf0-136">To change the allocation method of an IP address, run the following script, which changes the allocation method from dynamic to static.</span></span> <span data-ttu-id="06cf0-137">Se il metodo di allocazione per l'indirizzo IP privato corrente è statico, cambiare *Static* in *Dynamic* prima di eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="06cf0-137">If the allocation method for the current private IP address is static, change *Static* to *Dynamic* before executing the script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "The allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for the IP address" $IP"." -NoNewline
```

<span data-ttu-id="06cf0-138">Se non si conosce il nome della scheda di interfaccia di rete, è possibile visualizzare un elenco delle schede di rete all'interno di un gruppo di risorse immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="06cf0-138">If you don't know the name of the NIC, you can view a list of NICs within a resource group by entering the following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="06cf0-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06cf0-139">Next steps</span></span>
* <span data-ttu-id="06cf0-140">Informazioni su [indirizzi IP pubblici riservati](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="06cf0-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="06cf0-141">Informazioni su [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="06cf0-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="06cf0-142">Consultare le [API REST dell'indirizzo IP riservato](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="06cf0-142">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

