---
title: "Più indirizzi IP per le macchine virtuali di Azure - PowerShell | Documentazione Microsoft"
description: "Informazioni su come assegnare più indirizzi IP a una macchina virtuale usando PowerShell | Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: 29f64aeefc2a7deb1f84d759c2323347536b9c27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-powershell"></a><span data-ttu-id="1b57a-103">Assegnare più indirizzi IP alle macchine virtuali usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b57a-103">Assign multiple IP addresses to virtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="1b57a-104">Questo articolo spiega come creare una macchina virtuale (VM) tramite il modello di distribuzione Azure Resource Manager usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b57a-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="1b57a-105">Non è possibile a assegnare più indirizzi IP alle risorse create tramite il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="1b57a-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="1b57a-106">Per altre informazioni sui modelli di distribuzione di Azure, leggere l'articolo [Understand Azure deployment models](../resource-manager-deployment-model.md) (Informazioni sui modelli di distribuzione di Azure).</span><span class="sxs-lookup"><span data-stu-id="1b57a-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="1b57a-107"><a name = "create"></a>Creare una macchina virtuale con più indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="1b57a-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="1b57a-108">La procedura seguente illustra come creare una macchina virtuale di esempio con più indirizzi IP, come descritto nello scenario.</span><span class="sxs-lookup"><span data-stu-id="1b57a-108">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="1b57a-109">Modificare i valori delle variabili come necessario per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="1b57a-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="1b57a-110">Aprire un prompt dei comandi di PowerShell e completare i passaggi rimanenti in questa sezione in una singola sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b57a-110">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="1b57a-111">Se PowerShell non è già installato e configurato, completare la procedura disponibile nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="1b57a-111">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="1b57a-112">Accedere al proprio account con il comando `login-azurermaccount`.</span><span class="sxs-lookup"><span data-stu-id="1b57a-112">Login to your account with the `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="1b57a-113">Sostituire *myResourceGroup* e *westus* con un nome e una località di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="1b57a-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="1b57a-114">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1b57a-114">Create a resource group.</span></span> <span data-ttu-id="1b57a-115">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="1b57a-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="1b57a-116">Creare una rete virtuale (VNet) e una subnet nella stessa località del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="1b57a-116">Create a virtual network (VNet) and subnet in the same location as the resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get the subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="1b57a-117">Creare un gruppo di sicurezza di rete e una regola.</span><span class="sxs-lookup"><span data-stu-id="1b57a-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="1b57a-118">Il gruppo di sicurezza di rete protegge la macchina virtuale usando regole in entrata e in uscita.</span><span class="sxs-lookup"><span data-stu-id="1b57a-118">The NSG secures the VM using inbound and outbound rules.</span></span> <span data-ttu-id="1b57a-119">In questo caso viene creata una regola in entrata per la porta 3389 che consente connessioni desktop remoto in ingresso.</span><span class="sxs-lookup"><span data-stu-id="1b57a-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="1b57a-120">Definire la configurazione IP primaria della scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="1b57a-120">Define the primary IP configuration for the NIC.</span></span> <span data-ttu-id="1b57a-121">Modificare 10.0.0.4 in un indirizzo valido nella subnet creata, se il valore definito in precedenza non è stato usato.</span><span class="sxs-lookup"><span data-stu-id="1b57a-121">Change 10.0.0.4 to a valid address in the subnet you created, if you didn't use the value defined previously.</span></span> <span data-ttu-id="1b57a-122">Prima di assegnare un indirizzo IP statico, è consigliabile verificare che non sia già in uso.</span><span class="sxs-lookup"><span data-stu-id="1b57a-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="1b57a-123">Immettere il comando `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="1b57a-123">Enter the command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="1b57a-124">Se l'indirizzo è disponibile, l'output restituisce *True*.</span><span class="sxs-lookup"><span data-stu-id="1b57a-124">If the address is available, the output returns *True*.</span></span> <span data-ttu-id="1b57a-125">Se non è disponibile, l'output restituisce *False* e un elenco di indirizzi disponibili.</span><span class="sxs-lookup"><span data-stu-id="1b57a-125">If it's not available, the output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="1b57a-126">Nei comandi seguenti, **sostituire <replace-with-your-unique-name> con il nome DNS univoco da usare.**</span><span class="sxs-lookup"><span data-stu-id="1b57a-126">In the following commands, **Replace <replace-with-your-unique-name> with the unique DNS name to use.**</span></span> <span data-ttu-id="1b57a-127">Il nome deve essere univoco tra tutti gli indirizzi IP pubblici all'interno di un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b57a-127">The name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="1b57a-128">Questo è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="1b57a-128">This is an optional parameter.</span></span> <span data-ttu-id="1b57a-129">Può essere rimosso se si intende connettersi alla macchina virtuale tramite l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="1b57a-129">It can be removed if you only want to connect to the VM using the public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="1b57a-130">Quando si assegnano più configurazioni IP a un'interfaccia di rete, è necessario assegnare una configurazione a *Primary*.</span><span class="sxs-lookup"><span data-stu-id="1b57a-130">When you assign multiple IP configurations to a NIC, one configuration must be assigned as the *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1b57a-131">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="1b57a-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="1b57a-132">Per altre informazioni sui prezzi degli indirizzi IP, vedere la pagina [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="1b57a-132">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="1b57a-133">È previsto un limite per il numero di indirizzi IP pubblici che possono essere usati in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1b57a-133">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="1b57a-134">Per altre informazioni sui limiti, vedere l'articolo [Limiti di Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="1b57a-134">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="1b57a-135">Definire la configurazione IP secondaria della schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="1b57a-135">Define the secondary IP configurations for the NIC.</span></span> <span data-ttu-id="1b57a-136">È possibile aggiungere o rimuovere le configurazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1b57a-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="1b57a-137">Ogni configurazione IP deve avere un indirizzo IP privato assegnato.</span><span class="sxs-lookup"><span data-stu-id="1b57a-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="1b57a-138">Ogni configurazione può avere facoltativamente un indirizzo IP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="1b57a-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="1b57a-139">Creare la scheda di interfaccia di rete e associarvi le tre configurazioni IP:</span><span class="sxs-lookup"><span data-stu-id="1b57a-139">Create the NIC and associate the three IP configurations to it:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="1b57a-140">Anche se in questo articolo tutte le configurazioni vengono assegnate a una sola scheda di interfaccia di rete, è possibile assegnare più configurazioni IP a ogni scheda di interfaccia di rete collegata alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1b57a-140">Though all configurations are assigned to one NIC in this article, you can assign multiple IP configurations to every NIC attached to the VM.</span></span> <span data-ttu-id="1b57a-141">Per informazioni su come creare una VM con più interfacce di rete, leggere l'articolo [Creare una macchina virtuale con più schede di interfaccia di rete usando PowerShell](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1b57a-141">To learn how to create a VM with multiple NICs, read the [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="1b57a-142">Creare la macchina virtuale immettendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b57a-142">Create the VM by entering the following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted to enter a sername and password for the VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create the VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="1b57a-143">Aggiungere gli indirizzi IP privati al sistema operativo della macchina virtuale seguendo la procedura per il proprio sistema operativo riportata nella sezione [Aggiungere indirizzi IP a una macchina virtuale](#os-config) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1b57a-143">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="1b57a-144">Non aggiungere gli indirizzi IP pubblici al sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="1b57a-144">Do not add the public IP addresses to the operating system.</span></span>

## <span data-ttu-id="1b57a-145"><a name="add"></a>Aggiungere indirizzi IP a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1b57a-145"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="1b57a-146">È possibile aggiungere indirizzi IP privati e pubblici a una scheda di interfaccia di rete esistente completando la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="1b57a-146">You can add private and public IP addresses to a NIC by completing the steps that follow.</span></span> <span data-ttu-id="1b57a-147">Gli esempi delle sezioni seguenti presuppongono che si disponga già di una VM con le tre configurazioni IP descritte nello [scenario](#Scenario) di questo articolo, ma questa condizione non è indispensabile.</span><span class="sxs-lookup"><span data-stu-id="1b57a-147">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="1b57a-148">Aprire un prompt dei comandi di PowerShell e completare i passaggi rimanenti in questa sezione in una singola sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b57a-148">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="1b57a-149">Se PowerShell non è già installato e configurato, completare la procedura disponibile nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="1b57a-149">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="1b57a-150">Cambiare i "valori" delle variabili $Variables seguenti specificando il nome dell'interfaccia di rete a cui si vogliono aggiungere l'indirizzo IP, il gruppo di risorse e la località in cui esiste la scheda di interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="1b57a-150">Change the "values" of the following $Variables to the name of the NIC you want to add IP address to and the resource group and location the NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="1b57a-151">Se non si conosce il nome dell'interfaccia di rete da modificare, immettere i comandi seguenti e quindi cambiare i valori delle variabili precedenti:</span><span class="sxs-lookup"><span data-stu-id="1b57a-151">If you don't know the name of the NIC you want to change, enter the following commands, then change the values of the previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="1b57a-152">Creare una variabile e impostarla sull'interfaccia di rete esistente digitando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b57a-152">Create a variable and set it to the existing NIC by typing the following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="1b57a-153">Nei comandi seguenti modificare *myVNet* e *mySubnet* con i nomi della rete virtuale e della subnet a cui la scheda di interfaccia di rete è connessa.</span><span class="sxs-lookup"><span data-stu-id="1b57a-153">In the following commands, change *MyVNet* and *MySubnet* to the names of the VNet and subnet the NIC is connected to.</span></span> <span data-ttu-id="1b57a-154">Immettere i comandi per recuperare gli oggetti della rete virtuale e della subnet a cui la scheda di interfaccia di rete è connessa:</span><span class="sxs-lookup"><span data-stu-id="1b57a-154">Enter the commands to retrieve the VNet and subnet objects the NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="1b57a-155">Se non si conosce il nome di rete virtuale o una subnet che la scheda di interfaccia di rete è connesso, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b57a-155">If you don't know the VNet or subnet name the NIC is connected to, enter the following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="1b57a-156">Cercare un testo simile al seguente nell'output restituito:</span><span class="sxs-lookup"><span data-stu-id="1b57a-156">In the output, look for text similar to the following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="1b57a-157">In questo output *MyVnet* è la rete virtuale e *MySubnet* è la subnet a cui la scheda di interfaccia di rete è connessa.</span><span class="sxs-lookup"><span data-stu-id="1b57a-157">In this output, *MyVnet* is the VNet and *MySubnet* is the subnet the NIC is connected to.</span></span>

5. <span data-ttu-id="1b57a-158">Completare i passaggi in una delle sezioni seguenti, a seconda delle esigenze:</span><span class="sxs-lookup"><span data-stu-id="1b57a-158">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="1b57a-159">**Aggiungere un indirizzo IP privato**</span><span class="sxs-lookup"><span data-stu-id="1b57a-159">**Add a private IP address**</span></span>

    <span data-ttu-id="1b57a-160">Per aggiungere un indirizzo IP privato a una scheda di interfaccia di rete, è necessario creare una configurazione IP.</span><span class="sxs-lookup"><span data-stu-id="1b57a-160">To add a private IP address to a NIC, you must create an IP configuration.</span></span> <span data-ttu-id="1b57a-161">Il comando seguente crea una configurazione con un indirizzo IP statico 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="1b57a-161">The following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="1b57a-162">Quando si specifica un indirizzo IP statico, deve essere un indirizzo non usato per la subnet.</span><span class="sxs-lookup"><span data-stu-id="1b57a-162">When specifying a static IP address, it must be an unused address for the subnet.</span></span> <span data-ttu-id="1b57a-163">Si consiglia di verificare l'indirizzo per assicurarsi che sia disponibile tramite il comando `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet`.</span><span class="sxs-lookup"><span data-stu-id="1b57a-163">It's recommended that you first test the address to ensure it's available by entering the `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="1b57a-164">Se l'indirizzo IP è disponibile, l'output restituisce *True*.</span><span class="sxs-lookup"><span data-stu-id="1b57a-164">If the IP address is available, the output returns *True*.</span></span> <span data-ttu-id="1b57a-165">Se non è disponibile, l'output restituisce *False* e un elenco di indirizzi disponibili.</span><span class="sxs-lookup"><span data-stu-id="1b57a-165">If it's not available, the output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="1b57a-166">Creare tutte le configurazioni usando nomi di configurazione univoci e indirizzi IP privati (per le configurazioni con indirizzi IP statici).</span><span class="sxs-lookup"><span data-stu-id="1b57a-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="1b57a-167">Aggiungere l'indirizzo IP privato al sistema operativo della VM completando i passaggi relativi al sistema operativo indicati nella sezione [Aggiungere indirizzi IP al sistema operativo di una VM](#os-config) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1b57a-167">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="1b57a-168">**Aggiungere un indirizzo IP pubblico**</span><span class="sxs-lookup"><span data-stu-id="1b57a-168">**Add a public IP address**</span></span>

    <span data-ttu-id="1b57a-169">Per aggiungere un indirizzo IP pubblico è necessario associare una risorsa indirizzo IP pubblico a una configurazione IP nuova o esistente.</span><span class="sxs-lookup"><span data-stu-id="1b57a-169">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="1b57a-170">Completare i passaggi in una delle sezioni che seguono, a seconda del caso.</span><span class="sxs-lookup"><span data-stu-id="1b57a-170">Complete the steps in one of the sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1b57a-171">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="1b57a-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="1b57a-172">Per altre informazioni sui prezzi degli indirizzi IP, vedere la pagina [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="1b57a-172">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="1b57a-173">È previsto un limite per il numero di indirizzi IP pubblici che possono essere usati in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1b57a-173">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="1b57a-174">Per altre informazioni sui limiti, vedere l'articolo [Limiti di Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="1b57a-174">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="1b57a-175">**Associare la risorsa indirizzo IP pubblico a una nuova configurazione IP**</span><span class="sxs-lookup"><span data-stu-id="1b57a-175">**Associate the public IP address resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="1b57a-176">Ogni volta che si aggiunge un indirizzo IP pubblico a una nuova configurazione IP, è necessario aggiungere anche un indirizzo IP privato, perché tutte le configurazioni IP devono avere un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="1b57a-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="1b57a-177">È possibile aggiungere una risorsa indirizzo IP pubblico esistente o crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="1b57a-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="1b57a-178">Per crearne una nuova, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b57a-178">To create a new one, enter the following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="1b57a-179">Per creare una nuova configurazione IP con un indirizzo IP privato statico e la risorsa indirizzo IP pubblico *myPublicIp3* associata, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b57a-179">To create a new IP configuration with a static private IP address and the associated *myPublicIp3* public IP address resource, enter the following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="1b57a-180">**Associare la risorsa indirizzo IP pubblico a una configurazione IP esistente**</span><span class="sxs-lookup"><span data-stu-id="1b57a-180">**Associate the public IP address resource to an existing IP configuration**</span></span>

        <span data-ttu-id="1b57a-181">Una risorsa indirizzo IP pubblico può essere associata a una configurazione IP cui non ne sia associata alcuna.</span><span class="sxs-lookup"><span data-stu-id="1b57a-181">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="1b57a-182">È possibile stabilire se una configurazione IP dispone di un indirizzo IP pubblico associato immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b57a-182">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="1b57a-183">L'output sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1b57a-183">You see output similar to the following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="1b57a-184">Poiché la colonna **PublicIpAddress** per *IpConfig-3* è vuota, nessuna risorsa di indirizzo IP pubblico è attualmente associata.</span><span class="sxs-lookup"><span data-stu-id="1b57a-184">Since the **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="1b57a-185">È possibile aggiungere una risorsa indirizzo IP pubblico esistente a IpConfig-3 o immettere il comando seguente per crearne una:</span><span class="sxs-lookup"><span data-stu-id="1b57a-185">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="1b57a-186">Immettere il comando seguente per associare la risorsa indirizzo IP pubblico alla configurazione IP esistente denominata *IpConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="1b57a-186">Enter the following command to associate the public IP address resource to the existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="1b57a-187">Configurare l'interfaccia di rete con la configurazione IP immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b57a-187">Set the NIC with the new IP configuration by entering the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="1b57a-188">Visualizzare le risorse indirizzo IP privato e indirizzo IP pubblico assegnate alla scheda di interfaccia di rete immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1b57a-188">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="1b57a-189">Aggiungere l'indirizzo IP privato al sistema operativo della VM completando i passaggi relativi al sistema operativo indicati nella sezione [Aggiungere indirizzi IP al sistema operativo di una VM](#os-config) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1b57a-189">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="1b57a-190">Non aggiungere l'indirizzo IP pubblico al sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="1b57a-190">Do not add the public IP address to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
