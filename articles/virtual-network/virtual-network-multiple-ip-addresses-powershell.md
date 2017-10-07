---
title: gli indirizzi IP aaaMultiple per macchine virtuali di Azure - PowerShell | Documenti Microsoft
description: "Informazioni su come tooassign più gli indirizzi IP macchina virtuale tooa mediante PowerShell | Gestore delle risorse."
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
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a><span data-ttu-id="fa21f-103">Assegnare più indirizzi IP macchine toovirtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa21f-103">Assign multiple IP addresses toovirtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="fa21f-104">In questo articolo viene illustrato come una macchina virtuale (VM) durante la distribuzione Azure Resource Manager hello toocreate modello tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa21f-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="fa21f-105">Impossibile assegnare più indirizzi IP tooresources creato tramite il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="fa21f-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="fa21f-106">ulteriori informazioni sui modelli di distribuzione di Azure, leggere hello toolearn [comprendere i modelli di distribuzione](../resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="fa21f-107"><a name = "create"></a>Creare una macchina virtuale con più indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="fa21f-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="fa21f-108">passaggi di Hello che seguono viene illustrato come toocreate un esempio di macchina virtuale con più IP risolve, come descritto nello scenario di hello.</span><span class="sxs-lookup"><span data-stu-id="fa21f-108">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="fa21f-109">Modificare i valori delle variabili come necessario per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="fa21f-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="fa21f-110">Aprire un prompt dei comandi di PowerShell e completato hello rimanenti passaggi in questa sezione all'interno di una singola sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa21f-110">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="fa21f-111">Se si dispone già di PowerShell installato e configurato, hello completato i passaggi in hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-111">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="fa21f-112">Account di accesso tooyour con hello `login-azurermaccount` comando.</span><span class="sxs-lookup"><span data-stu-id="fa21f-112">Login tooyour account with hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="fa21f-113">Sostituire *myResourceGroup* e *westus* con un nome e una località di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="fa21f-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="fa21f-114">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="fa21f-114">Create a resource group.</span></span> <span data-ttu-id="fa21f-115">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="fa21f-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="fa21f-116">Creare una rete virtuale (VNet) e la subnet in hello stesso percorso del gruppo di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="fa21f-116">Create a virtual network (VNet) and subnet in hello same location as hello resource group:</span></span>

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

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="fa21f-117">Creare un gruppo di sicurezza di rete e una regola.</span><span class="sxs-lookup"><span data-stu-id="fa21f-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="fa21f-118">Hello NSG protegge hello VM utilizzando le regole in entrata e in uscita.</span><span class="sxs-lookup"><span data-stu-id="fa21f-118">hello NSG secures hello VM using inbound and outbound rules.</span></span> <span data-ttu-id="fa21f-119">In questo caso viene creata una regola in entrata per la porta 3389 che consente connessioni desktop remoto in ingresso.</span><span class="sxs-lookup"><span data-stu-id="fa21f-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

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

6. <span data-ttu-id="fa21f-120">Definire una configurazione IP primaria hello per hello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="fa21f-120">Define hello primary IP configuration for hello NIC.</span></span> <span data-ttu-id="fa21f-121">Indirizzo tooa modifica 10.0.0.4 nella subnet hello è stato creato, se non è stato utilizzato il valore di hello definito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="fa21f-121">Change 10.0.0.4 tooa valid address in hello subnet you created, if you didn't use hello value defined previously.</span></span> <span data-ttu-id="fa21f-122">Prima di assegnare un indirizzo IP statico, è consigliabile verificare che non sia già in uso.</span><span class="sxs-lookup"><span data-stu-id="fa21f-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="fa21f-123">Immettere il comando hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="fa21f-123">Enter hello command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="fa21f-124">Se è disponibile l'indirizzo di hello, hello output restituisce *True*.</span><span class="sxs-lookup"><span data-stu-id="fa21f-124">If hello address is available, hello output returns *True*.</span></span> <span data-ttu-id="fa21f-125">Se non è disponibile, hello output restituisce *False* e un elenco di indirizzi disponibili.</span><span class="sxs-lookup"><span data-stu-id="fa21f-125">If it's not available, hello output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="fa21f-126">In seguito comandi, hello **sostituire < replace-con-your-univoco-name > con toouse di nome DNS univoco hello.**</span><span class="sxs-lookup"><span data-stu-id="fa21f-126">In hello following commands, **Replace <replace-with-your-unique-name> with hello unique DNS name toouse.**</span></span> <span data-ttu-id="fa21f-127">nome di Hello deve essere univoco tra tutti gli indirizzi IP pubblici all'interno di un'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa21f-127">hello name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="fa21f-128">Questo è un parametro facoltativo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-128">This is an optional parameter.</span></span> <span data-ttu-id="fa21f-129">Può essere rimosso se si desidera solo tooconnect toohello VM utilizzando l'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="fa21f-129">It can be removed if you only want tooconnect toohello VM using hello public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="fa21f-130">Quando si assegna più tooa di configurazioni IP NIC, una configurazione deve essere assegnata come hello *-primaria*.</span><span class="sxs-lookup"><span data-stu-id="fa21f-130">When you assign multiple IP configurations tooa NIC, one configuration must be assigned as hello *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa21f-131">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="fa21f-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="fa21f-132">ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="fa21f-132">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="fa21f-133">È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fa21f-133">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="fa21f-134">informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-134">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="fa21f-135">Definire configurazioni IP secondarie di hello per hello scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="fa21f-135">Define hello secondary IP configurations for hello NIC.</span></span> <span data-ttu-id="fa21f-136">È possibile aggiungere o rimuovere le configurazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="fa21f-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="fa21f-137">Ogni configurazione IP deve avere un indirizzo IP privato assegnato.</span><span class="sxs-lookup"><span data-stu-id="fa21f-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="fa21f-138">Ogni configurazione può avere facoltativamente un indirizzo IP pubblico assegnato.</span><span class="sxs-lookup"><span data-stu-id="fa21f-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
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

8. <span data-ttu-id="fa21f-139">Creare hello NIC e associare tooit di configurazioni IP tre hello:</span><span class="sxs-lookup"><span data-stu-id="fa21f-139">Create hello NIC and associate hello three IP configurations tooit:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="fa21f-140">Anche se tutte le configurazioni vengono assegnate tooone NIC in questo articolo, è possibile assegnare più IP configurazioni tooevery NIC associata toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fa21f-140">Though all configurations are assigned tooone NIC in this article, you can assign multiple IP configurations tooevery NIC attached toohello VM.</span></span> <span data-ttu-id="fa21f-141">modalità di lettura di una macchina virtuale con più schede di rete, toocreate toolearn hello [creare una macchina virtuale con più schede di rete](virtual-network-deploy-multinic-arm-ps.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-141">toolearn how toocreate a VM with multiple NICs, read hello [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="fa21f-142">Creare VM hello immettendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="fa21f-142">Create hello VM by entering hello following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
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
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="fa21f-143">Toohello macchina virtuale del sistema operativo di indirizzi IP privati di Aggiungi hello completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-143">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="fa21f-144">Non aggiungere hello pubblica IP indirizzi toohello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-144">Do not add hello public IP addresses toohello operating system.</span></span>

## <span data-ttu-id="fa21f-145"><a name="add"></a>Aggiungere tooa di indirizzi IP VM</span><span class="sxs-lookup"><span data-stu-id="fa21f-145"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="fa21f-146">È possibile aggiungere pubblica e privata IP indirizzi tooa NIC completando i passaggi di hello che seguono.</span><span class="sxs-lookup"><span data-stu-id="fa21f-146">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="fa21f-147">Hello esempi in hello nelle sezioni che seguono si presuppone che si dispone di una macchina virtuale con le configurazioni IP hello tre descritte in hello [scenario](#Scenario) in questo articolo, ma non è necessario eseguire.</span><span class="sxs-lookup"><span data-stu-id="fa21f-147">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="fa21f-148">Aprire un prompt dei comandi di PowerShell e completato hello rimanenti passaggi in questa sezione all'interno di una singola sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa21f-148">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="fa21f-149">Se si dispone già di PowerShell installato e configurato, hello completato i passaggi in hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-149">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="fa21f-150">Modificare hello "valori" hello dopo il nome di toohello $Variables di hello NIC desiderato tooadd IP indirizzo tooand hello risorsa gruppo e il percorso hello in che NIC esiste:</span><span class="sxs-lookup"><span data-stu-id="fa21f-150">Change hello "values" of hello following $Variables toohello name of hello NIC you want tooadd IP address tooand hello resource group and location hello NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="fa21f-151">Se non si conosce il nome di hello di hello NIC desiderato toochange, immettere i seguenti comandi hello, quindi modificare i valori hello variabili precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="fa21f-151">If you don't know hello name of hello NIC you want toochange, enter hello following commands, then change hello values of hello previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="fa21f-152">Creare una variabile e impostarlo toohello esistente NIC digitando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa21f-152">Create a variable and set it toohello existing NIC by typing hello following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="fa21f-153">In hello seguenti comandi, modificare *MyVNet* e *MySubnet* toohello nomi di hello hello rete virtuale e subnet, è connessa al.</span><span class="sxs-lookup"><span data-stu-id="fa21f-153">In hello following commands, change *MyVNet* and *MySubnet* toohello names of hello VNet and subnet hello NIC is connected to.</span></span> <span data-ttu-id="fa21f-154">Immettere hello comandi tooretrieve hello rete virtuale e subnet oggetti hello a che connessa:</span><span class="sxs-lookup"><span data-stu-id="fa21f-154">Enter hello commands tooretrieve hello VNet and subnet objects hello NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="fa21f-155">Se non si conosce hello rete virtuale o una subnet nome hello a che connessa, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa21f-155">If you don't know hello VNet or subnet name hello NIC is connected to, enter hello following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="fa21f-156">Nell'output di hello, cercare toohello di testo simili output di esempio riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fa21f-156">In hello output, look for text similar toohello following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="fa21f-157">In questo output *MyVnet* è hello rete virtuale e *MySubnet* è hello subnet hello è connessa al.</span><span class="sxs-lookup"><span data-stu-id="fa21f-157">In this output, *MyVnet* is hello VNet and *MySubnet* is hello subnet hello NIC is connected to.</span></span>

5. <span data-ttu-id="fa21f-158">Completare i passaggi di hello in uno di hello le sezioni, in base ai requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa21f-158">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="fa21f-159">**Aggiungere un indirizzo IP privato**</span><span class="sxs-lookup"><span data-stu-id="fa21f-159">**Add a private IP address**</span></span>

    <span data-ttu-id="fa21f-160">tooadd un tooa di indirizzo IP privato NIC, è necessario creare una configurazione IP.</span><span class="sxs-lookup"><span data-stu-id="fa21f-160">tooadd a private IP address tooa NIC, you must create an IP configuration.</span></span> <span data-ttu-id="fa21f-161">Hello seguente comando crea una configurazione con un indirizzo IP statico 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="fa21f-161">hello following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="fa21f-162">Quando si specifica un indirizzo IP statico, deve essere un indirizzo per subnet hello inutilizzato.</span><span class="sxs-lookup"><span data-stu-id="fa21f-162">When specifying a static IP address, it must be an unused address for hello subnet.</span></span> <span data-ttu-id="fa21f-163">È consigliabile testare tooensure indirizzo hello è disponibile tramite l'immissione di hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` comando.</span><span class="sxs-lookup"><span data-stu-id="fa21f-163">It's recommended that you first test hello address tooensure it's available by entering hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="fa21f-164">Se l'indirizzo IP hello è disponibile, hello output restituisce *True*.</span><span class="sxs-lookup"><span data-stu-id="fa21f-164">If hello IP address is available, hello output returns *True*.</span></span> <span data-ttu-id="fa21f-165">Se non è disponibile, hello output restituisce *False*e un elenco di indirizzi disponibili.</span><span class="sxs-lookup"><span data-stu-id="fa21f-165">If it's not available, hello output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="fa21f-166">Creare tutte le configurazioni usando nomi di configurazione univoci e indirizzi IP privati (per le configurazioni con indirizzi IP statici).</span><span class="sxs-lookup"><span data-stu-id="fa21f-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="fa21f-167">Aggiungere hello private IP indirizzo toohello macchina virtuale sistema operativo completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-167">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="fa21f-168">**Aggiungere un indirizzo IP pubblico**</span><span class="sxs-lookup"><span data-stu-id="fa21f-168">**Add a public IP address**</span></span>

    <span data-ttu-id="fa21f-169">Associando un tooeither di risorsa indirizzo IP pubblico, una nuova configurazione IP o una configurazione IP esistente, viene aggiunto un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="fa21f-169">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="fa21f-170">Completare i passaggi di hello nelle sezioni che seguono, hello necessari.</span><span class="sxs-lookup"><span data-stu-id="fa21f-170">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fa21f-171">Per gli indirizzi IP pubblici è prevista una tariffa nominale.</span><span class="sxs-lookup"><span data-stu-id="fa21f-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="fa21f-172">ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.</span><span class="sxs-lookup"><span data-stu-id="fa21f-172">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="fa21f-173">È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fa21f-173">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="fa21f-174">informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-174">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="fa21f-175">**Associare hello pubblica risorsa tooa nuovo IP configurazione degli indirizzi IP**</span><span class="sxs-lookup"><span data-stu-id="fa21f-175">**Associate hello public IP address resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="fa21f-176">Ogni volta che si aggiunge un indirizzo IP pubblico a una nuova configurazione IP, è necessario aggiungere anche un indirizzo IP privato, perché tutte le configurazioni IP devono avere un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="fa21f-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="fa21f-177">È possibile aggiungere una risorsa indirizzo IP pubblico esistente o crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="fa21f-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="fa21f-178">toocreate uno nuovo, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa21f-178">toocreate a new one, enter hello following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="fa21f-179">una nuova configurazione IP con un indirizzo IP privato statico e hello associata toocreate *myPublicIp3* indirizzo IP pubblico risorsa degli indirizzi, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa21f-179">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIp3* public IP address resource, enter hello following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="fa21f-180">**Associare hello pubblica risorsa tooan esistente IP configurazione degli indirizzi IP**</span><span class="sxs-lookup"><span data-stu-id="fa21f-180">**Associate hello public IP address resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="fa21f-181">Una risorsa di indirizzo IP pubblica può essere solo la configurazione IP tooan associato che non ha ancora associata.</span><span class="sxs-lookup"><span data-stu-id="fa21f-181">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="fa21f-182">È possibile determinare se una configurazione IP è un indirizzo IP pubblico associato immettendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa21f-182">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="fa21f-183">Viene visualizzato il seguente toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="fa21f-183">You see output similar toohello following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="fa21f-184">Poiché hello **PublicIpAddress** colonna per *IpConfig 3* è vuoto, nessuna risorsa dell'indirizzo IP pubblica è tooit attualmente associato.</span><span class="sxs-lookup"><span data-stu-id="fa21f-184">Since hello **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="fa21f-185">È possibile aggiungere un esistente pubblica IP indirizzo risorsa tooIpConfig-3 o immettere hello toocreate comando uno di seguito:</span><span class="sxs-lookup"><span data-stu-id="fa21f-185">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="fa21f-186">Immettere hello comando risorsa toohello configurazione IP esistente denominato di indirizzo IP pubblico di tooassociate hello seguente *IpConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="fa21f-186">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="fa21f-187">Impostare hello NIC con configurazione IP nuovo hello immettendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa21f-187">Set hello NIC with hello new IP configuration by entering hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="fa21f-188">Visualizzare gli indirizzi IP privati hello e hello pubblica IP indirizzo risorse assegnato toohello NIC immettendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fa21f-188">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="fa21f-189">Aggiungere hello private IP indirizzo toohello macchina virtuale sistema operativo completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-189">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="fa21f-190">Non aggiungere hello pubblica IP indirizzo toohello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="fa21f-190">Do not add hello public IP address toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
