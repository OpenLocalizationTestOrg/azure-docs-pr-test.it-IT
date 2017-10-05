---
title: Accesso e sicurezza nei modelli di Azure per le macchine virtuali di Windows | Documentazione Microsoft
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
ms.openlocfilehash: ad1b5c4763cf56f681a50bb1bccc825311bbfdf5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="2f944-103">Accesso e sicurezza nei modelli di Azure Resource Manager per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="2f944-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="2f944-104">Le applicazioni ospitate in Azure devono in genere essere accessibili attraverso Internet o una connessione VPN/Express Route con Azure.</span><span class="sxs-lookup"><span data-stu-id="2f944-104">Applications hosted in Azure likely need to be access over the internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="2f944-105">Nel caso dell'applicazione Music Store di esempio, il sito Web è reso disponibile su Internet con un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="2f944-105">With the Music Store application sample, the web site is made available on the internet with a public IP address.</span></span> <span data-ttu-id="2f944-106">Una volta stabilito l'accesso, le connessioni all'applicazione e l'accesso alle risorse delle macchine virtuali deve essere protetto.</span><span class="sxs-lookup"><span data-stu-id="2f944-106">With access established, connections to the application and access to the virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="2f944-107">La sicurezza dell'accesso è garantita da un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="2f944-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="2f944-108">Questo documento descrive in che modo è protetta l'applicazione Music Store nel modello di esempio di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2f944-108">This document details how the Music Store application is secured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="2f944-109">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="2f944-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="2f944-110">Per ottenere risultati ottimali, pre-distribuire un'istanza della soluzione alla propria sottoscrizione di Azure ed esercitarsi con il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2f944-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="2f944-111">Il modello completo è disponibile in [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows) (Distribuzione di Music Store in Windows).</span><span class="sxs-lookup"><span data-stu-id="2f944-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="2f944-112">Indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="2f944-112">Public IP Address</span></span>
<span data-ttu-id="2f944-113">Per consentire l'accesso pubblico a una risorsa di Azure, è possibile usare una risorsa di indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="2f944-113">To provide public access to an Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="2f944-114">L'indirizzo IP pubblico può essere configurato con un indirizzo IP statico o dinamico.</span><span class="sxs-lookup"><span data-stu-id="2f944-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="2f944-115">Se viene usato un indirizzo dinamico e la macchina virtuale viene arrestata e deallocata, l'indirizzo viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="2f944-115">If a dynamic address is used, and the virtual machine is stopped and deallocated, the addresses is removed.</span></span> <span data-ttu-id="2f944-116">Al riavvio della macchina, è possibile che venga assegnato un indirizzo IP pubblico diverso.</span><span class="sxs-lookup"><span data-stu-id="2f944-116">When the machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="2f944-117">Per impedire l'assegnazione di un altro indirizzo IP, è possibile usare un indirizzo IP riservato.</span><span class="sxs-lookup"><span data-stu-id="2f944-117">To prevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="2f944-118">È possibile aggiungere un indirizzo IP pubblico a un modello di Azure Resource Manager usando la procedura guidata Aggiungi nuova risorsa di Visual Studio o inserendo una risorsa JSON valida nel modello.</span><span class="sxs-lookup"><span data-stu-id="2f944-118">A Public IP Address can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="2f944-119">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Indirizzo IP pubblico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span><span class="sxs-lookup"><span data-stu-id="2f944-119">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

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

<span data-ttu-id="2f944-120">Un indirizzo IP pubblico può essere associato a una scheda di rete virtuale o a un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2f944-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="2f944-121">In questo esempio, il carico del sito Web di Music Store è bilanciato tra più macchine virtuali e quindi l'indirizzo IP pubblico è associato al servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="2f944-121">In this example, because the Music Store website is load balanced across several virtual machines, the Public IP Address is attached to the Load Balancer.</span></span>

<span data-ttu-id="2f944-122">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Associazione dell'indirizzo IP pubblico con il servizio di bilanciamento del carico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="2f944-122">Follow this link to see the JSON sample within the Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

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

<span data-ttu-id="2f944-123">Di seguito è illustrato l'indirizzo IP pubblico come visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f944-123">The public IP Address as seen from the Azure portal.</span></span> <span data-ttu-id="2f944-124">Si noti che l'indirizzo IP pubblico è associato a un servizio di bilanciamento del carico e non a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2f944-124">Notice that the public IP address is associated to a load balancer and not a virtual machine.</span></span> <span data-ttu-id="2f944-125">I servizi di bilanciamento del carico di rete sono descritti in dettaglio nel documento successivo di questa serie.</span><span class="sxs-lookup"><span data-stu-id="2f944-125">Network load balancers are detailed in the next document of this series.</span></span>

![Indirizzo IP pubblico](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="2f944-127">Per altre informazioni sugli indirizzi IP pubblici di Azure, vedere [Indirizzi IP in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2f944-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="2f944-128">Gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="2f944-128">Network Security Group</span></span>
<span data-ttu-id="2f944-129">Una volta stabilito l'accesso alle risorse di Azure, è necessario imporre alcune limitazioni.</span><span class="sxs-lookup"><span data-stu-id="2f944-129">Once access has been established to Azure resources, this access should be limited.</span></span> <span data-ttu-id="2f944-130">Per le macchine virtuali di Azure, la sicurezza dell'accesso è garantita da un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="2f944-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="2f944-131">Nel caso dell'applicazione Music Store di esempio, qualsiasi accesso alla macchina virtuale è limitato, ad eccezione della porta 80 per l'accesso HTTP e della porta 3389 per l'accesso RDP.</span><span class="sxs-lookup"><span data-stu-id="2f944-131">With the Music Store application sample, all access to the virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="2f944-132">È possibile aggiungere un gruppo di sicurezza di rete a un modello di Azure Resource Manager usando la procedura guidata Aggiungi nuova risorsa di Visual Studio o inserendo una risorsa JSON valida nel modello.</span><span class="sxs-lookup"><span data-stu-id="2f944-132">A Network Security Group can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="2f944-133">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Gruppo di sicurezza di rete](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span><span class="sxs-lookup"><span data-stu-id="2f944-133">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

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

<span data-ttu-id="2f944-134">In questo esempio il gruppo di sicurezza di rete è associato all'oggetto subnet dichiarato nella risorsa della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2f944-134">In this example, the network security group is associate with the subnet object declared in the Virtual Network resource.</span></span> 

<span data-ttu-id="2f944-135">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Associazione del gruppo di sicurezza di rete con la rete virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span><span class="sxs-lookup"><span data-stu-id="2f944-135">Follow this link to see the JSON sample within the Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

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

<span data-ttu-id="2f944-136">Di seguito è illustrato il gruppo di sicurezza di rete come visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f944-136">Here is what the network security group looks like from the Azure portal.</span></span> <span data-ttu-id="2f944-137">Si noti che un gruppo di sicurezza di rete può essere associato a una subnet e/o a un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="2f944-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="2f944-138">In questo caso, il gruppo di sicurezza di rete è associato a una subnet.</span><span class="sxs-lookup"><span data-stu-id="2f944-138">In this case, the NSG is associated to a subnet.</span></span> <span data-ttu-id="2f944-139">In questa configurazione, le regole in ingresso si applicano a tutte le macchine virtuali connesse alla subnet.</span><span class="sxs-lookup"><span data-stu-id="2f944-139">In this configuration, the inbound rules apply to all virtual machines connected to the subnet.</span></span>

![Gruppo di sicurezza di rete](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="2f944-141">Per informazioni approfondite sui gruppi di sicurezza di rete, vedere [Che cos'è un gruppo di sicurezza di rete](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="2f944-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="2f944-142">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="2f944-142">Next step</span></span>
<hr>

[<span data-ttu-id="2f944-143">Passaggio 3: Disponibilità e scalabilità nei modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2f944-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

