---
title: "Rete per i set di scalabilità di macchine virtuali di Azure | Microsoft Docs"
description: "Configurazione delle proprietà della rete per i set di scalabilità di macchine virtuali di Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: a8520c6d8962cc362fc935f6b515a299c0ce75b3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="154ea-103">Rete per i set di scalabilità di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="154ea-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="154ea-104">Quando si distribuisce un set di scalabilità di macchine virtuali di Azure tramite il portale, determinate proprietà della rete sono predefinite, ad esempio un'istanza di Azure Load Balancer con regole NAT in ingresso.</span><span class="sxs-lookup"><span data-stu-id="154ea-104">When you deploy an Azure virtual machine scale set through the portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="154ea-105">Questo articolo descrive come usare alcune delle funzionalità più avanzate della rete che è possibile configurare con i set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="154ea-105">This article describes how to use some of the more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="154ea-106">È possibile configurare tutte le funzionalità illustrate in questo articolo usando i modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="154ea-106">You can configure all of the features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="154ea-107">Sono inclusi anche esempi dell'interfaccia della riga di comando di Azure e di PowerShell per le funzionalità selezionate.</span><span class="sxs-lookup"><span data-stu-id="154ea-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="154ea-108">Usare l'interfaccia della riga di comando 2.10 e PowerShell 4.2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="154ea-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="154ea-109">Rete accelerata</span><span class="sxs-lookup"><span data-stu-id="154ea-109">Accelerated Networking</span></span>
<span data-ttu-id="154ea-110">La [rete accelerata](../virtual-network/virtual-network-create-vm-accelerated-networking.md) di Azure migliora le prestazioni di rete abilitando Single-Root I/O Virtualization (SR-IOV) per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="154ea-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) to a virtual machine.</span></span> <span data-ttu-id="154ea-111">Per usare la rete accelerata con i set di scalabilità, impostare enableAcceleratedNetworking su **true** nelle impostazioni networkInterfaceConfigurations del set di scalabilità,</span><span class="sxs-lookup"><span data-stu-id="154ea-111">To use accelerated networking with scale sets, set enableAcceleratedNetworking to **true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="154ea-112">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="154ea-112">For example:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="154ea-113">Creare un set di scalabilità che faccia riferimento a un'istanza di Azure Load Balancer esistente</span><span class="sxs-lookup"><span data-stu-id="154ea-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="154ea-114">Quando viene creato un set di scalabilità usando il portale di Azure, viene creato un nuovo servizio di bilanciamento del carico per la maggior parte delle opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="154ea-114">When a scale set is created using the Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="154ea-115">Se si crea un set di scalabilità, che deve fare riferimento a un servizio di bilanciamento del carico esistente, è possibile farlo usando l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="154ea-115">If you create a scale set, which needs to reference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="154ea-116">Lo script di esempio seguente crea un servizio di bilanciamento del carico e quindi crea un set di scalabilità che vi fa riferimento:</span><span class="sxs-lookup"><span data-stu-id="154ea-116">The following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="154ea-117">Impostazioni DNS configurabili</span><span class="sxs-lookup"><span data-stu-id="154ea-117">Configurable DNS Settings</span></span>
<span data-ttu-id="154ea-118">Per impostazione predefinita, ai set di scalabilità vengono applicate le impostazioni DNS specifiche della rete virtuale e della subnet in cui sono state create.</span><span class="sxs-lookup"><span data-stu-id="154ea-118">By default, scale sets take on the specific DNS settings of the VNET and subnet they were created in.</span></span> <span data-ttu-id="154ea-119">È tuttavia possibile configurare direttamente le impostazioni DNS per un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="154ea-119">You can however, configure the DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="154ea-120">Creazione di un set di scalabilità con server DNS configurabili</span><span class="sxs-lookup"><span data-stu-id="154ea-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="154ea-121">Per creare un set di scalabilità con una configurazione DNS personalizzata usando l'interfaccia della riga di comando 2.0, aggiungere l'argomento **--dns-servers** al comando **vmss create**, seguito dagli indirizzi IP dei server separati da spazi,</span><span class="sxs-lookup"><span data-stu-id="154ea-121">To create a scale set with a custom DNS configuration using CLI 2.0, add the **--dns-servers** argument to the **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="154ea-122">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="154ea-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="154ea-123">Per configurare server DNS personalizzati in un modello di Azure, aggiungere una proprietà dnsSettings alla sezione networkInterfaceConfigurations del set di scalabilità,</span><span class="sxs-lookup"><span data-stu-id="154ea-123">To configure custom DNS servers in an Azure template, add a dnsSettings property to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="154ea-124">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="154ea-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="154ea-125">Creazione di un set di scalabilità con nomi di dominio di macchine virtuali configurabili</span><span class="sxs-lookup"><span data-stu-id="154ea-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="154ea-126">Per creare un set di scalabilità con un nome DNS personalizzato per le macchine virtuali usando l'interfaccia della riga di comando 2.0, aggiungere l'argomento **--vm-domain-name** al comando **vmss create**, seguito da una stringa che rappresenta il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="154ea-126">To create a scale set with a custom DNS name for virtual machines using CLI 2.0, add the **--vm-domain-name** argument to the **vmss create** command, followed by a string representing the domain name.</span></span>

<span data-ttu-id="154ea-127">Per impostare il nome di dominio in un modello di Azure, aggiungere una proprietà **dnsSettings** alla sezione **networkInterfaceConfigurations** del set di scalabilità,</span><span class="sxs-lookup"><span data-stu-id="154ea-127">To set the domain name in an Azure template, add a **dnsSettings** property to the scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="154ea-128">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="154ea-128">For example:</span></span>

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

<span data-ttu-id="154ea-129">L'output, per un singolo nome DNS di macchina virtuale, avrà il formato seguente:</span><span class="sxs-lookup"><span data-stu-id="154ea-129">The output, for an individual virtual machine dns name would be in the following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="154ea-130">IPv4 pubblico per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="154ea-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="154ea-131">Per le macchine virtuali di un set di scalabilità di Azure in genere non sono necessari indirizzi IP pubblici specifici.</span><span class="sxs-lookup"><span data-stu-id="154ea-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="154ea-132">Per la maggior parte degli scenari, risulta più economico e sicuro associare un indirizzo IP pubblico a un servizio di bilanciamento del carico o a una singola macchina virtuale (jumpbox), che quindi instrada le connessioni in ingresso alle macchine virtuali del set di scalabilità in base alle esigenze (ad esempio, tramite regole NAT in ingresso).</span><span class="sxs-lookup"><span data-stu-id="154ea-132">For most scenarios, it is more economical and secure to associate a public IP address to a load balancer or to an individual virtual machine (aka a jumpbox), which then routes incoming connections to scale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="154ea-133">Alcuni scenari tuttavia richiedono che le macchine virtuali del set di scalabilità abbiano i propri indirizzi IP pubblici,</span><span class="sxs-lookup"><span data-stu-id="154ea-133">However, some scenarios do require scale set virtual machines to have their own public IP addresses.</span></span> <span data-ttu-id="154ea-134">ad esempio i giochi, in cui una console deve stabilire una connessione diretta a una macchina virtuale cloud, che esegue l'elaborazione fisica del gioco.</span><span class="sxs-lookup"><span data-stu-id="154ea-134">An example is gaming, where a console needs to make a direct connection to a cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="154ea-135">Un altro esempio è quello in cui le macchine virtuali devono stabilire connessioni esterne reciproche tra aree in un database distribuito.</span><span class="sxs-lookup"><span data-stu-id="154ea-135">Another example is where virtual machines need to make external connections to one another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="154ea-136">Creazione di un set di scalabilità con un IP pubblico per ogni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="154ea-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="154ea-137">Per creare un set di scalabilità che assegni un indirizzo IP pubblico a ogni macchina virtuale con l'interfaccia della riga di comando 2.0, aggiungere il parametro **--public-ip-per-vm** al comando **vmss create**.</span><span class="sxs-lookup"><span data-stu-id="154ea-137">To create a scale set that assigns a public IP address to each virtual machine with CLI 2.0, add the **--public-ip-per-vm** parameter to the **vmss create** command.</span></span> 

<span data-ttu-id="154ea-138">Per creare un set di scalabilità usando un modello di Azure, verificare che la versione API della risorsa Microsoft.Compute/virtualMachineScaleSets sia almeno **2017-03-30** e aggiungere una proprietà JSON **publicIpAddressConfiguration** alla sezione ipConfigurations del set di scalabilità,</span><span class="sxs-lookup"><span data-stu-id="154ea-138">To create a scale set using an Azure template, make sure the API version of the Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property to the scale set ipConfigurations section.</span></span> <span data-ttu-id="154ea-139">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="154ea-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="154ea-140">Modello di esempio: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="154ea-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-the-public-ip-addresses-of-the-virtual-machines-in-a-scale-set"></a><span data-ttu-id="154ea-141">Query degli indirizzi IP pubblici delle macchine virtuali in un set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="154ea-141">Querying the public IP addresses of the virtual machines in a scale set</span></span>
<span data-ttu-id="154ea-142">Per elencare gli indirizzi IP pubblici assegnati alle macchine virtuali del set di scalabilità usando l'interfaccia della riga di comando 2.0, eseguire il comando **az vmss list-instance-public-ips**.</span><span class="sxs-lookup"><span data-stu-id="154ea-142">To list the public IP addresses assigned to scale set virtual machines using CLI 2.0, use the **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="154ea-143">Per elencare gli indirizzi IP pubblici del set di scalabilità usando PowerShell, eseguire il comando _Get-AzureRmPublicIpAddress_,</span><span class="sxs-lookup"><span data-stu-id="154ea-143">To list scale set public IP addresses using PowerShell, use the _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="154ea-144">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="154ea-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="154ea-145">È anche possibile eseguire una query degli indirizzi IP pubblici facendo direttamente riferimento all'ID risorsa della configurazione degli indirizzi IP pubblici,</span><span class="sxs-lookup"><span data-stu-id="154ea-145">You can also query the public IP addresses by referencing the resource id of the public IP address configuration directly.</span></span> <span data-ttu-id="154ea-146">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="154ea-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="154ea-147">Per eseguire una query degli indirizzi IP pubblici assegnati alle macchine virtuali del set di scalabilità, usare [Azure Resource Explorer](https://resources.azure.com) o l'API REST di Azure con versione **2017-03-30** o successiva.</span><span class="sxs-lookup"><span data-stu-id="154ea-147">To query the public IP addresses assigned to scale set virtual machines using the [Azure Resource Explorer](https://resources.azure.com), or the Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="154ea-148">Per visualizzare gli indirizzi IP pubblici per un set di scalabilità usando Resource Explorer, esaminare la sezione **publicipaddresses** sotto il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="154ea-148">To view public IP addresses for a scale set using the Resource Explorer, look at the **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="154ea-149">Ad esempio: https://resources.azure.com/subscriptions/_ID_sottoscrizione_/resourceGroups/_gruppo_di_risorse_/providers/Microsoft.Compute/virtualMachineScaleSets/_set_di_scalabilità_di_macchine_virtuali_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="154ea-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="154ea-150">Output di esempio:</span><span class="sxs-lookup"><span data-stu-id="154ea-150">Example output:</span></span>
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="154ea-151">Più indirizzi IP per ogni scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="154ea-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="154ea-152">Ogni scheda di interfaccia di rete collegata a una macchina virtuale in un set di scalabilità può avere una o più configurazioni IP associate.</span><span class="sxs-lookup"><span data-stu-id="154ea-152">Every NIC attached to a VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="154ea-153">A ogni configurazione viene assegnato un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="154ea-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="154ea-154">Ogni configurazione può anche avere una risorsa di indirizzo IP pubblico associata.</span><span class="sxs-lookup"><span data-stu-id="154ea-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="154ea-155">Per sapere quanti indirizzi IP possono essere assegnati a una scheda di interfaccia di rete e quanti indirizzi IP pubblici è possibile usare in una sottoscrizione di Azure, vedere [Limiti di Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="154ea-155">To understand how many IP addresses can be assigned to a NIC, and how many public IP addresses you can use in an Azure subscription, refer to [Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="154ea-156">Più schede di interfaccia di rete per ogni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="154ea-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="154ea-157">È possibile avere fino a 8 schede di interfaccia di rete per ogni macchina virtuale, a seconda delle dimensioni del computer.</span><span class="sxs-lookup"><span data-stu-id="154ea-157">You can have up to 8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="154ea-158">Il numero massimo di schede di interfaccia di rete per computer è disponibile nell'[articolo sulle dimensioni per le VM](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="154ea-158">The maximum number of NICs per machine is available in the [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="154ea-159">L'esempio seguente è un profilo di rete del set di scalabilità che mostra più voci di schede di interfaccia di rete e più IP pubblici per ogni macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="154ea-159">The following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a><span data-ttu-id="154ea-160">Gruppi di sicurezza di rete per ogni set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="154ea-160">NSG per scale set</span></span>
<span data-ttu-id="154ea-161">I gruppi di sicurezza di rete possono essere applicati direttamente a un set di scalabilità, aggiungendo un riferimento alla sezione della configurazione dell'interfaccia di rete delle proprietà delle macchine virtuali del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="154ea-161">Network Security Groups can be applied directly to a scale set, by adding a reference to the network interface configuration section of the scale set virtual machine properties.</span></span>

<span data-ttu-id="154ea-162">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="154ea-162">For example:</span></span> 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="154ea-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="154ea-163">Next steps</span></span>
<span data-ttu-id="154ea-164">Per altre informazioni sulle reti virtuali di Azure, vedere [questa documentazione](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="154ea-164">For more information about Azure virtual networks, refer to [this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
