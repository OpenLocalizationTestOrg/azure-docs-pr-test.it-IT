---
title: aaaAccess e la sicurezza in modelli di Azure per le macchine virtuali di Windows | Documenti Microsoft
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="3ea14-103">Accesso e sicurezza nei modelli di Azure Resource Manager per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="3ea14-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="3ea14-104">Applicazioni ospitate in Azure è probabilmente necessario toobe accesso su hello internet o una VPN o connessione Express Route con Azure.</span><span class="sxs-lookup"><span data-stu-id="3ea14-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="3ea14-105">Hello negozio applicazione di esempio viene reso disponibile nel sito web hello hello internet con un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="3ea14-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="3ea14-106">Con l'accesso è stata stabilita, devono essere protette connessioni toohello accesso alle applicazioni e toohello risorse della macchina virtuale se stessi.</span><span class="sxs-lookup"><span data-stu-id="3ea14-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="3ea14-107">La sicurezza dell'accesso è garantita da un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="3ea14-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="3ea14-108">Questo documento illustra in dettaglio come hello applicazione negozio viene protetto nel modello di gestione risorse di Azure di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="3ea14-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="3ea14-109">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="3ea14-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="3ea14-110">Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3ea14-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="3ea14-111">è disponibili qui: modello completa Hello [musica archivio distribuzione in Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="3ea14-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="3ea14-112">Indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="3ea14-112">Public IP Address</span></span>
<span data-ttu-id="3ea14-113">tooprovide accesso pubblico tooan risorse di Azure, una risorsa di indirizzo IP pubblica può essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="3ea14-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="3ea14-114">L'indirizzo IP pubblico può essere configurato con un indirizzo IP statico o dinamico.</span><span class="sxs-lookup"><span data-stu-id="3ea14-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="3ea14-115">Se viene utilizzato un indirizzo dinamico e macchina virtuale hello viene arrestata e deallocata, gli indirizzi di hello viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="3ea14-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="3ea14-116">Quando viene riavviato macchina hello, può essere assegnato un indirizzo IP pubblico diverso.</span><span class="sxs-lookup"><span data-stu-id="3ea14-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="3ea14-117">modifica degli indirizzi tooprevent un IP, un indirizzo IP riservato può essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="3ea14-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="3ea14-118">Un indirizzo IP pubblico possono essere aggiunti a un modello di Azure Resource Manager tooan utilizzando Visual Studio aggiungere Creazione guidata nuova risorsa, hello o mediante l'inserimento di un oggetto JSON valido in un modello.</span><span class="sxs-lookup"><span data-stu-id="3ea14-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="3ea14-119">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [indirizzo IP pubblico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span><span class="sxs-lookup"><span data-stu-id="3ea14-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="3ea14-120">Un indirizzo IP pubblico può essere associato a una scheda di rete virtuale o a un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="3ea14-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="3ea14-121">In questo esempio, poiché hello sito Web di negozio viene bilanciato tra più macchine virtuali, hello indirizzo IP pubblico è collegato toohello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="3ea14-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="3ea14-122">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [associazione indirizzo IP pubblico con bilanciamento del carico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="3ea14-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="3ea14-123">Hello indirizzo IP pubblico come rilevato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ea14-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="3ea14-124">Si noti che l'indirizzo IP pubblico hello è servizio di bilanciamento del carico tooa associati e non una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ea14-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="3ea14-125">Bilanciamento del carico di rete descritti nel documento successivo di hello di questa serie.</span><span class="sxs-lookup"><span data-stu-id="3ea14-125">Network load balancers are detailed in hello next document of this series.</span></span>

![Indirizzo IP pubblico](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="3ea14-127">Per altre informazioni sugli indirizzi IP pubblici di Azure, vedere [Indirizzi IP in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="3ea14-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="3ea14-128">Gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="3ea14-128">Network Security Group</span></span>
<span data-ttu-id="3ea14-129">Dopo l'accesso è stato stabilito tooAzure risorse, l'accesso deve essere limitato.</span><span class="sxs-lookup"><span data-stu-id="3ea14-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="3ea14-130">Per le macchine virtuali di Azure, la sicurezza dell'accesso è garantita da un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="3ea14-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="3ea14-131">Hello negozio applicazione di esempio tutte le macchine virtuali toohello di accesso è limitato, ad eccezione di sulla porta 80 per l'accesso http e la porta 3389 per l'accesso RDP.</span><span class="sxs-lookup"><span data-stu-id="3ea14-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="3ea14-132">Un gruppo di sicurezza di rete può essere aggiunto il modello di Azure Resource Manager tooan utilizzando Visual Studio aggiungere Creazione guidata nuova risorsa, hello o mediante l'inserimento di un oggetto JSON valido in un modello.</span><span class="sxs-lookup"><span data-stu-id="3ea14-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="3ea14-133">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span><span class="sxs-lookup"><span data-stu-id="3ea14-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

<span data-ttu-id="3ea14-134">In questo esempio, gruppo di sicurezza di rete hello è associato l'oggetto di subnet hello dichiarato nella risorsa di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3ea14-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="3ea14-135">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [associazione gruppo di sicurezza di rete con rete virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span><span class="sxs-lookup"><span data-stu-id="3ea14-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

<span data-ttu-id="3ea14-136">Ecco il gruppo di sicurezza di rete hello simile da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ea14-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="3ea14-137">Si noti che un gruppo di sicurezza di rete può essere associato a una subnet e/o a un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="3ea14-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="3ea14-138">In questo caso, hello NSG è subnet tooa associato.</span><span class="sxs-lookup"><span data-stu-id="3ea14-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="3ea14-139">In questa configurazione, hello in ingresso regole si applica tooall macchine virtuali connesse toohello subnet.</span><span class="sxs-lookup"><span data-stu-id="3ea14-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![Gruppo di sicurezza di rete](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="3ea14-141">Per informazioni approfondite sui gruppi di sicurezza di rete, vedere [Che cos'è un gruppo di sicurezza di rete](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="3ea14-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="3ea14-142">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="3ea14-142">Next step</span></span>
<hr>

[<span data-ttu-id="3ea14-143">Passaggio 3: Disponibilità e scalabilità nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3ea14-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

