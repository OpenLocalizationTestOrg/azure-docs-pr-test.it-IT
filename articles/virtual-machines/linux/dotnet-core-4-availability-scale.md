---
title: "Disponibilità e scalabilità nei modelli di Azure Resource Manager | Microsoft Docs"
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0250b8152ed31b9a5d8b42ae139c9b38da0984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="fc208-103">Disponibilità e scalabilità nei modelli di Azure Resource Manager per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="fc208-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="fc208-104">La disponibilità e la scalabilità sono correlate al tempo di attività e alla possibilità di soddisfare la domanda.</span><span class="sxs-lookup"><span data-stu-id="fc208-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="fc208-105">Se un'applicazione deve essere attiva durante il 99,9% del tempo, deve avere un'architettura che consente l'esecuzione di più risorse di calcolo simultanee.</span><span class="sxs-lookup"><span data-stu-id="fc208-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="fc208-106">Ad esempio, anziché avere un singolo sito Web, una configurazione con un livello di disponibilità più elevato include più istanze dello stesso sito, con tecnologia di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="fc208-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="fc208-107">In questa configurazione, una singola istanza dell'applicazione può essere arrestata per manutenzione, mentre le altre continuano a funzionare.</span><span class="sxs-lookup"><span data-stu-id="fc208-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="fc208-108">La scalabilità fa riferimento alla capacità delle applicazioni di soddisfare la domanda.</span><span class="sxs-lookup"><span data-stu-id="fc208-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="fc208-109">Nel caso di un'applicazione con carico bilanciato, l'aggiunta o la rimozione di istanze dal pool consente a un'applicazione di ridimensionare le risorse in base alla domanda.</span><span class="sxs-lookup"><span data-stu-id="fc208-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="fc208-110">Questo documento descrive in che modo è configurata la distribuzione di esempio di Music Store per la disponibilità e la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="fc208-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="fc208-111">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="fc208-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="fc208-112">Per ottenere risultati ottimali, pre-distribuire un'istanza della soluzione alla propria sottoscrizione di Azure ed esercitarsi con il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc208-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="fc208-113">Il modello completo è disponibile in [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)(Distribuzione di Music Store in Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="fc208-113">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="fc208-114">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="fc208-114">Availability Set</span></span>
<span data-ttu-id="fc208-115">Un set di disponibilità si estende logicamente sulle macchine virtuali di Azure attraverso host fisici e altri componenti dell'infrastruttura, ad esempio alimentatori e hardware di rete fisica.</span><span class="sxs-lookup"><span data-stu-id="fc208-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="fc208-116">I set di disponibilità assicurano che non tutte le macchine virtuali siano interessate da attività di manutenzione, errori dei dispositivi o altri tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="fc208-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="fc208-117">È possibile aggiungere un set di disponibilità a un modello di Azure Resource Manager usando la procedura guidata Aggiungi nuova risorsa di Visual Studio o inserendo una risorsa JSON valida nel modello.</span><span class="sxs-lookup"><span data-stu-id="fc208-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="fc208-118">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Set di disponibilità](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="fc208-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

<span data-ttu-id="fc208-119">Un set di disponibilità viene dichiarato come proprietà di una risorsa di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc208-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="fc208-120">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Associazione del set di disponibilità con la macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="fc208-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="fc208-121">Di seguito è illustrato il set di disponibilità come visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc208-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="fc208-122">Nell'immagine sono riportate le singole macchine virtuali con i relativi dettagli di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fc208-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![Set di disponibilità](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="fc208-124">Per informazioni approfondite sui set di disponibilità, vedere [Gestione della disponibilità delle macchine virtuali](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc208-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="fc208-125">Servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fc208-125">Network Load Balancer</span></span>
<span data-ttu-id="fc208-126">Se da un lato un set di disponibilità garantisce la tolleranza di errore dell'applicazione, dall'altro un servizio di bilanciamento del carico rende disponibili numerose istanze dell'applicazione su un singolo indirizzo di rete.</span><span class="sxs-lookup"><span data-stu-id="fc208-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="fc208-127">Più istanze di un'applicazione possono essere ospitate su numerose macchine virtuali, ciascuna connessa a un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="fc208-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="fc208-128">Quando viene inviata una richiesta di accesso all'applicazione, il servizio di bilanciamento del carico instrada la richiesta in ingresso attraverso i membri collegati.</span><span class="sxs-lookup"><span data-stu-id="fc208-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="fc208-129">È possibile aggiungere un servizio di bilanciamento del carico usando la procedura guidata Aggiungi nuova risorsa di Visual Studio o inserendo una risorsa JSON formattata correttamente nel modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc208-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="fc208-130">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Servizio di bilanciamento del carico di rete](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="fc208-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

<span data-ttu-id="fc208-131">Poiché l'applicazione di esempio viene esposta a Internet con un indirizzo IP pubblico, questo indirizzo è associato al servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="fc208-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="fc208-132">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Associazione del servizio di bilanciamento del carico con l'indirizzo IP pubblico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="fc208-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="fc208-133">Nel portale di Azure le informazioni generali sul servizio di bilanciamento del carico di rete mostrano l'associazione con l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="fc208-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![Servizio di bilanciamento del carico](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="fc208-135">Regola del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fc208-135">Load Balancer Rule</span></span>
<span data-ttu-id="fc208-136">Quando si usa un servizio di bilanciamento del carico, sono configurate delle regole che controllano il modo in cui il traffico viene bilanciato tra le risorse previste.</span><span class="sxs-lookup"><span data-stu-id="fc208-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="fc208-137">Nel caso dell'applicazione Music Store di esempio, il traffico arriva sulla porta 80 dell'indirizzo IP pubblico e viene distribuito attraverso la porta 80 di tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fc208-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="fc208-138">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Regola del servizio di bilanciamento del carico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="fc208-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

<span data-ttu-id="fc208-139">Di seguito è illustrata la regola del servizio di bilanciamento del carico di rete come visualizzata nel portale.</span><span class="sxs-lookup"><span data-stu-id="fc208-139">A view of the network load balancer rule from the portal.</span></span>

![Regola del servizio di bilanciamento del carico di rete](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="fc208-141">Probe del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fc208-141">Load Balancer Probe</span></span>
<span data-ttu-id="fc208-142">Il servizio di bilanciamento del carico deve anche monitorare ogni macchina virtuale in modo da soddisfare solo le richieste dei sistemi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fc208-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="fc208-143">Questo monitoraggio avviene tramite l'esecuzione costante del probe su una porta predefinita.</span><span class="sxs-lookup"><span data-stu-id="fc208-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="fc208-144">La distribuzione di Music Store è configurata in modo da eseguire il probe sulla porta 80 di tutte le macchine virtuali incluse.</span><span class="sxs-lookup"><span data-stu-id="fc208-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="fc208-145">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Probe del servizio di bilanciamento del carico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="fc208-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

<span data-ttu-id="fc208-146">Di seguito è illustrato il probe del servizio di bilanciamento del carico come visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc208-146">The load balancer probe seen from the Azure portal.</span></span>

![Probe del servizio di bilanciamento del carico di rete](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="fc208-148">Regole NAT in ingresso</span><span class="sxs-lookup"><span data-stu-id="fc208-148">Inbound NAT Rules</span></span>
<span data-ttu-id="fc208-149">Quando si usa un servizio di bilanciamento del carico, devono essere configurate delle regole che consentono l'accesso senza carico bilanciato a ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc208-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="fc208-150">Ad esempio, quando si crea una connessione SSH con ogni macchina virtuale, il carico del traffico non deve essere bilanciato, ma è necessario che sia configurato un percorso predeterminato.</span><span class="sxs-lookup"><span data-stu-id="fc208-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="fc208-151">I percorsi di questo tipo vengono configurati mediante una risorsa di regola NAT in ingresso.</span><span class="sxs-lookup"><span data-stu-id="fc208-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="fc208-152">Usando questa risorsa, le comunicazioni in ingresso possono essere mappate alle singole macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fc208-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="fc208-153">Nel caso dell'applicazione Music Store, una porta identificata da un numero a partire da 5000 viene mappata alla porta 22 di ogni macchina virtuale per l'accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="fc208-153">With the Music Store application, a port starting at 5000 is mapped to port 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="fc208-154">Per incrementare il numero della porta in ingresso viene usata la funzione `copyindex()` , in modo che la seconda macchina virtuale riceva una porta in ingresso 5001, la terza una 5002 e così via.</span><span class="sxs-lookup"><span data-stu-id="fc208-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span> 

<span data-ttu-id="fc208-155">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Regole NAT in ingresso](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="fc208-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="fc208-156">Di seguito è illustrato un esempio di regola NAT in ingresso come visualizzata nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc208-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="fc208-157">Per ogni macchina virtuale nella distribuzione viene creata una regola NAT SSH.</span><span class="sxs-lookup"><span data-stu-id="fc208-157">An SSH NAT rule is created for each virtual machine in the deployment.</span></span>

![Regola NAT in ingresso](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="fc208-159">Per informazioni approfondite sul servizio di bilanciamento del carico di rete di Azure, vedere [Bilanciamento del carico per i servizi di infrastruttura di Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc208-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="fc208-160">Distribuire più macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="fc208-160">Deploy multiple VMs</span></span>
<span data-ttu-id="fc208-161">Per il funzionamento efficiente di un set di disponibilità o di un servizio di bilanciamento del carico, sono necessarie più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fc208-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="fc208-162">Più macchine virtuali possono essere distribuite tramite la funzione copy del modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc208-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="fc208-163">Usando la funzione copy, non è necessario definire un numero finito di macchine virtuali, ma questo valore può essere fornito in modo dinamico in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fc208-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="fc208-164">La funzione copy utilizza il numero di istanze create e gestisce la distribuzione del numero appropriato di macchine virtuali e di risorse associate.</span><span class="sxs-lookup"><span data-stu-id="fc208-164">The copy function consumes the number of instances to created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="fc208-165">Nel modello di esempio di Music Store è definito un parametro che accetta un determinato numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="fc208-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="fc208-166">Questo numero viene usato nell'intero modello durante la creazione delle macchine virtuali e delle risorse associate.</span><span class="sxs-lookup"><span data-stu-id="fc208-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
}
```

<span data-ttu-id="fc208-167">Sulla risorsa della macchina virtuale, al ciclo copy vengono assegnati un nome e il valore del parametro relativo al numero di istanze usato per controllare il numero di copie risultanti.</span><span class="sxs-lookup"><span data-stu-id="fc208-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="fc208-168">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Funzione copy delle macchine virtuali](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="fc208-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

<span data-ttu-id="fc208-169">L'iterazione corrente della funzione copy è accessibile con la funzione `copyIndex()` .</span><span class="sxs-lookup"><span data-stu-id="fc208-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="fc208-170">Il valore della funzione copyIndex può essere usato per assegnare un nome alle macchine virtuali e ad altre risorse.</span><span class="sxs-lookup"><span data-stu-id="fc208-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="fc208-171">Ad esempio, se vengono distribuite due istanze di una macchina virtuale, queste devono avere nomi diversi.</span><span class="sxs-lookup"><span data-stu-id="fc208-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="fc208-172">La funzione `copyIndex()` può essere usata come parte del nome della macchina virtuale per creare un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="fc208-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="fc208-173">Un esempio d'uso della funzione `copyindex()` a scopo di denominazione è visibile nella risorsa della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc208-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="fc208-174">In questo caso, il nome del computer è il risultato di una concatenazione del parametro `vmName` e della funzione `copyIndex()`.</span><span class="sxs-lookup"><span data-stu-id="fc208-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="fc208-175">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Funzione copyIndex](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="fc208-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

<span data-ttu-id="fc208-176">La funzione `copyIndex` viene usata più volte nel modello di esempio di Music Store.</span><span class="sxs-lookup"><span data-stu-id="fc208-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="fc208-177">Le risorse e le funzioni che usano `copyIndex` includono dati specifici di una singola istanza della macchina virtuale, come l'interfaccia di rete, le regole del servizio di bilanciamento del carico e altri elementi, a seconda della funzione.</span><span class="sxs-lookup"><span data-stu-id="fc208-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="fc208-178">Per altre informazioni sulla funzione copy, vedere [Creare più istanze di risorse in Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="fc208-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="fc208-179">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="fc208-179">Next step</span></span>
<hr>

[<span data-ttu-id="fc208-180">Passaggio 4: Distribuzione di applicazioni con i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fc208-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

