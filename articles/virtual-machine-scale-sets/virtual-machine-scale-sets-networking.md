---
title: "aaaNetworking per il set di scalabilità di macchine virtuali di Azure | Documenti Microsoft"
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
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="475f0-103">Rete per i set di scalabilità di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="475f0-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="475f0-104">Quando si distribuisce una macchina virtuale di Azure di scala impostato tramite il portale di hello, alcune proprietà di rete vengono impostate come predefinite, ad esempio un servizio di bilanciamento del carico di Azure con connessioni in entrata regole NAT.</span><span class="sxs-lookup"><span data-stu-id="475f0-104">When you deploy an Azure virtual machine scale set through hello portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="475f0-105">In questo articolo viene descritto come toouse alcune hello più avanzate funzionalità di rete che è possibile configurare con scala imposta.</span><span class="sxs-lookup"><span data-stu-id="475f0-105">This article describes how toouse some of hello more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="475f0-106">È possibile configurare le funzionalità hello trattate in questo articolo, utilizzando i modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="475f0-106">You can configure all of hello features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="475f0-107">Sono inclusi anche esempi dell'interfaccia della riga di comando di Azure e di PowerShell per le funzionalità selezionate.</span><span class="sxs-lookup"><span data-stu-id="475f0-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="475f0-108">Usare l'interfaccia della riga di comando 2.10 e PowerShell 4.2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="475f0-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="475f0-109">Rete accelerata</span><span class="sxs-lookup"><span data-stu-id="475f0-109">Accelerated Networking</span></span>
<span data-ttu-id="475f0-110">Azure [Accelerated rete](../virtual-network/virtual-network-create-vm-accelerated-networking.md) migliora le prestazioni di rete abilitando la macchina virtuale tooa di single root i/o virtualization (SR-IOV).</span><span class="sxs-lookup"><span data-stu-id="475f0-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) tooa virtual machine.</span></span> <span data-ttu-id="475f0-111">toouse accelerated con set di scalabilità di rete, impostare enableAcceleratedNetworking troppo**true** nelle impostazioni di configurazioni del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="475f0-111">toouse accelerated networking with scale sets, set enableAcceleratedNetworking too**true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="475f0-112">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="475f0-112">For example:</span></span>
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

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="475f0-113">Creare un set di scalabilità che faccia riferimento a un'istanza di Azure Load Balancer esistente</span><span class="sxs-lookup"><span data-stu-id="475f0-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="475f0-114">Quando viene creato un set di scalabilità mediante hello portale di Azure, viene creato un nuovo bilanciamento del carico per la maggior parte delle opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="475f0-114">When a scale set is created using hello Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="475f0-115">Se si crea un set di scalabilità, che deve tooreference un bilanciamento del carico esistente, è possibile farlo tramite CLI.</span><span class="sxs-lookup"><span data-stu-id="475f0-115">If you create a scale set, which needs tooreference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="475f0-116">Hello lo script di esempio seguente crea un bilanciamento del carico e quindi crea un set di scalabilità, che fa riferimento a essa:</span><span class="sxs-lookup"><span data-stu-id="475f0-116">hello following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="475f0-117">Impostazioni DNS configurabili</span><span class="sxs-lookup"><span data-stu-id="475f0-117">Configurable DNS Settings</span></span>
<span data-ttu-id="475f0-118">Per impostazione predefinita, set di scalabilità di intraprendere hello le impostazioni DNS specifiche di hello tra reti VIRTUALI e subnet che in cui sono stati creati.</span><span class="sxs-lookup"><span data-stu-id="475f0-118">By default, scale sets take on hello specific DNS settings of hello VNET and subnet they were created in.</span></span> <span data-ttu-id="475f0-119">È tuttavia possibile configurare le impostazioni DNS hello per una scala impostata direttamente.</span><span class="sxs-lookup"><span data-stu-id="475f0-119">You can however, configure hello DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="475f0-120">Creazione di un set di scalabilità con server DNS configurabili</span><span class="sxs-lookup"><span data-stu-id="475f0-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="475f0-121">toocreate una scala impostata con una configurazione DNS personalizzata utilizzando 2.0 CLI, aggiungere hello **-server - dns** argomento toohello **vmss creare** separati di comando, seguito da uno spazio indirizzi ip del server.</span><span class="sxs-lookup"><span data-stu-id="475f0-121">toocreate a scale set with a custom DNS configuration using CLI 2.0, add hello **--dns-servers** argument toohello **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="475f0-122">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="475f0-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="475f0-123">server DNS personalizzati tooconfigure in un modello di Azure, aggiungere configurazioni sezione del set di una scala di toohello proprietà dnsSettings.</span><span class="sxs-lookup"><span data-stu-id="475f0-123">tooconfigure custom DNS servers in an Azure template, add a dnsSettings property toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="475f0-124">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="475f0-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="475f0-125">Creazione di un set di scalabilità con nomi di dominio di macchine virtuali configurabili</span><span class="sxs-lookup"><span data-stu-id="475f0-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="475f0-126">toocreate una scala impostata con un nome DNS personalizzato per le macchine virtuali utilizzando 2.0 CLI, aggiungere hello **nome di dominio - vm** argomento toohello **vmss creare** comando, seguito da una stringa che rappresenta il nome di dominio di hello.</span><span class="sxs-lookup"><span data-stu-id="475f0-126">toocreate a scale set with a custom DNS name for virtual machines using CLI 2.0, add hello **--vm-domain-name** argument toohello **vmss create** command, followed by a string representing hello domain name.</span></span>

<span data-ttu-id="475f0-127">nome di dominio tooset hello in un modello di Azure, aggiungere un **dnsSettings** proprietà set di scalabilità toohello **configurazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="475f0-127">tooset hello domain name in an Azure template, add a **dnsSettings** property toohello scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="475f0-128">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="475f0-128">For example:</span></span>

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

<span data-ttu-id="475f0-129">output di Hello, per il nome dns di ogni macchina virtuale sarà in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="475f0-129">hello output, for an individual virtual machine dns name would be in hello following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="475f0-130">IPv4 pubblico per macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="475f0-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="475f0-131">Per le macchine virtuali di un set di scalabilità di Azure in genere non sono necessari indirizzi IP pubblici specifici.</span><span class="sxs-lookup"><span data-stu-id="475f0-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="475f0-132">Per la maggior parte degli scenari, è più economico e sicuro tooassociate un pubblica IP indirizzo tooa carico bilanciamento o tooan singola macchina virtuale (noto anche come jumpbox), che instrada le macchine virtuali set tooscale le connessioni in ingresso in base alle esigenze (ad esempio, tramite regole NAT in ingresso).</span><span class="sxs-lookup"><span data-stu-id="475f0-132">For most scenarios, it is more economical and secure tooassociate a public IP address tooa load balancer or tooan individual virtual machine (aka a jumpbox), which then routes incoming connections tooscale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="475f0-133">Tuttavia, alcuni scenari richiedono set di scalabilità di macchine virtuali toohave proprio indirizzo IP pubblico indirizzi.</span><span class="sxs-lookup"><span data-stu-id="475f0-133">However, some scenarios do require scale set virtual machines toohave their own public IP addresses.</span></span> <span data-ttu-id="475f0-134">Il gioco è riportato un esempio, in cui una console deve toomake una connessione diretta tooa cloud macchina virtuale, che esegue l'elaborazione di gioco fisica.</span><span class="sxs-lookup"><span data-stu-id="475f0-134">An example is gaming, where a console needs toomake a direct connection tooa cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="475f0-135">Un altro esempio è toomake connessioni esterne tooone necessario le macchine virtuali in un altro in aree geografiche in un database distribuito.</span><span class="sxs-lookup"><span data-stu-id="475f0-135">Another example is where virtual machines need toomake external connections tooone another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="475f0-136">Creazione di un set di scalabilità con un IP pubblico per ogni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="475f0-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="475f0-137">toocreate un set di scalabilità che assegna una pubblica macchina virtuale tooeach di indirizzi IP con 2.0 CLI, aggiungere hello **-public-ip per ogni vm** parametro toohello **vmss creare** comando.</span><span class="sxs-lookup"><span data-stu-id="475f0-137">toocreate a scale set that assigns a public IP address tooeach virtual machine with CLI 2.0, add hello **--public-ip-per-vm** parameter toohello **vmss create** command.</span></span> 

<span data-ttu-id="475f0-138">toocreate una scala impostata utilizzando un modello di Azure, assicurarsi hello API versione di hello risorsa Microsoft.Compute/virtualMachineScaleSets almeno **2017-03-30**e aggiungere un **publicIpAddressConfiguration**Set di scalabilità di toohello proprietà JSON della sezione di configurazione IP.</span><span class="sxs-lookup"><span data-stu-id="475f0-138">toocreate a scale set using an Azure template, make sure hello API version of hello Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="475f0-139">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="475f0-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="475f0-140">Modello di esempio: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="475f0-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a><span data-ttu-id="475f0-141">Esecuzione di query hello indirizzo IP pubblico del set di indirizzi di hello le macchine virtuali in una scala</span><span class="sxs-lookup"><span data-stu-id="475f0-141">Querying hello public IP addresses of hello virtual machines in a scale set</span></span>
<span data-ttu-id="475f0-142">gli indirizzi IP pubblici di toolist hello assegnato tooscale set le macchine virtuali utilizzando 2.0 CLI, utilizzare hello **az vmss elenco-istanza-public-IP** comando.</span><span class="sxs-lookup"><span data-stu-id="475f0-142">toolist hello public IP addresses assigned tooscale set virtual machines using CLI 2.0, use hello **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="475f0-143">scala toolist imposta gli indirizzi IP pubblici tramite PowerShell, utilizzare hello _Get AzureRmPublicIpAddress_ comando.</span><span class="sxs-lookup"><span data-stu-id="475f0-143">toolist scale set public IP addresses using PowerShell, use hello _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="475f0-144">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="475f0-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="475f0-145">È inoltre possibile gli indirizzi IP pubblici di query hello facendo riferimento direttamente all'id della configurazione degli indirizzi IP pubblica hello risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="475f0-145">You can also query hello public IP addresses by referencing hello resource id of hello public IP address configuration directly.</span></span> <span data-ttu-id="475f0-146">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="475f0-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="475f0-147">gli indirizzi IP pubblici di tooquery hello assegnato tooscale set le macchine virtuali utilizzando hello [Esplora inventario risorse di Azure](https://resources.azure.com), o hello API REST di Azure con la versione **2017-03-30** o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="475f0-147">tooquery hello public IP addresses assigned tooscale set virtual machines using hello [Azure Resource Explorer](https://resources.azure.com), or hello Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="475f0-148">indirizzi IP pubblici tooview per una scala impostata utilizzando hello Esplora inventario risorse, esaminare hello **publicipaddresses** sezione del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="475f0-148">tooview public IP addresses for a scale set using hello Resource Explorer, look at hello **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="475f0-149">Ad esempio: https://resources.azure.com/subscriptions/_ID_sottoscrizione_/resourceGroups/_gruppo_di_risorse_/providers/Microsoft.Compute/virtualMachineScaleSets/_set_di_scalabilità_di_macchine_virtuali_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="475f0-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="475f0-150">Output di esempio:</span><span class="sxs-lookup"><span data-stu-id="475f0-150">Example output:</span></span>
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

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="475f0-151">Più indirizzi IP per ogni scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="475f0-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="475f0-152">Tutte le schede NIC associata tooa che macchina virtuale in un set di scalabilità può avere uno o più configurazioni IP associate.</span><span class="sxs-lookup"><span data-stu-id="475f0-152">Every NIC attached tooa VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="475f0-153">A ogni configurazione viene assegnato un indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="475f0-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="475f0-154">Ogni configurazione può anche avere una risorsa di indirizzo IP pubblico associata.</span><span class="sxs-lookup"><span data-stu-id="475f0-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="475f0-155">toounderstand quanti indirizzi IP possono essere assegnato tooa NIC, e quanti indirizzi IP pubblici, è possibile utilizzare in una sottoscrizione di Azure, fare riferimento troppo[i limiti di Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="475f0-155">toounderstand how many IP addresses can be assigned tooa NIC, and how many public IP addresses you can use in an Azure subscription, refer too[Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="475f0-156">Più schede di interfaccia di rete per ogni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="475f0-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="475f0-157">È possibile disporre di schede NIC too8 per ogni macchina virtuale, a seconda delle dimensioni della macchina.</span><span class="sxs-lookup"><span data-stu-id="475f0-157">You can have up too8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="475f0-158">numero massimo di schede NIC Hello per ogni computer è disponibile in hello [articolo dimensioni VM](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="475f0-158">hello maximum number of NICs per machine is available in hello [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="475f0-159">Hello riportato di seguito è che una scala di imposta il profilo di rete con più voci di interfaccia di rete e più indirizzi IP pubblici per ogni macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="475f0-159">hello following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
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

## <a name="nsg-per-scale-set"></a><span data-ttu-id="475f0-160">Gruppi di sicurezza di rete per ogni set di scalabilità</span><span class="sxs-lookup"><span data-stu-id="475f0-160">NSG per scale set</span></span>
<span data-ttu-id="475f0-161">Gruppi di sicurezza di rete possono essere applicati direttamente il set di scalabilità tooa, aggiungendo una sezione di configurazione riferimento toohello rete interfaccia della scala hello imposta proprietà della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="475f0-161">Network Security Groups can be applied directly tooa scale set, by adding a reference toohello network interface configuration section of hello scale set virtual machine properties.</span></span>

<span data-ttu-id="475f0-162">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="475f0-162">For example:</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="475f0-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="475f0-163">Next steps</span></span>
<span data-ttu-id="475f0-164">Per ulteriori informazioni sulle reti virtuali di Azure, vedere troppo[questa documentazione](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="475f0-164">For more information about Azure virtual networks, refer too[this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
