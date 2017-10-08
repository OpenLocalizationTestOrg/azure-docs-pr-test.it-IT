---
title: aaaAvailability e scala in modelli di gestione risorse di Azure | Documenti Microsoft
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
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="40749-103">Disponibilità e scalabilità nei modelli di Azure Resource Manager per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="40749-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="40749-104">Disponibilità e scalabilità vedere toouptime e hello richiesta toomeet possibilità.</span><span class="sxs-lookup"><span data-stu-id="40749-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="40749-105">Se un'applicazione deve essere del 99,9% di tempo hello, è necessario toohave un'architettura che consente di più risorse di calcolo simultanee.</span><span class="sxs-lookup"><span data-stu-id="40749-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="40749-106">Ad esempio, invece di un singolo sito Web, una configurazione con un livello più elevato di disponibilità include più istanze dello stesso sito, con bilanciamento del carico tecnologia li hello.</span><span class="sxs-lookup"><span data-stu-id="40749-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="40749-107">In questa configurazione, un'istanza di un'applicazione hello può essere disattivata per manutenzione, mentre hello rimanenti continua toofunction.</span><span class="sxs-lookup"><span data-stu-id="40749-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="40749-108">Scala in hello invece fa riferimento la domanda di tooserve tooan applicazioni possibilità.</span><span class="sxs-lookup"><span data-stu-id="40749-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="40749-109">Con un carico bilanciata applicazione, aggiungendo o rimuovendo istanze dal pool hello consente una richiesta di applicazione tooscale toomeet.</span><span class="sxs-lookup"><span data-stu-id="40749-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="40749-110">Questo documento illustra in dettaglio come distribuzione di esempio negozio hello è configurato per la disponibilità e scalabilità.</span><span class="sxs-lookup"><span data-stu-id="40749-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="40749-111">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="40749-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="40749-112">Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="40749-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="40749-113">è disponibili qui: modello completa Hello [distribuzione archivio musica in Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="40749-113">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="40749-114">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="40749-114">Availability Set</span></span>
<span data-ttu-id="40749-115">Un set di disponibilità si estende logicamente sulle macchine virtuali di Azure attraverso host fisici e altri componenti dell'infrastruttura, ad esempio alimentatori e hardware di rete fisica.</span><span class="sxs-lookup"><span data-stu-id="40749-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="40749-116">I set di disponibilità assicurano che non tutte le macchine virtuali siano interessate da attività di manutenzione, errori dei dispositivi o altri tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="40749-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="40749-117">Un Set di disponibilità può essere aggiunto tooan modello di gestione risorse di Azure utilizzando Visual Studio aggiungere Creazione guidata nuova risorsa hello o inserimento JSON valido in un modello.</span><span class="sxs-lookup"><span data-stu-id="40749-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="40749-118">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Set di disponibilità](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="40749-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

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

<span data-ttu-id="40749-119">Un set di disponibilità viene dichiarato come proprietà di una risorsa di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="40749-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="40749-120">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Set di disponibilità di associazione con la macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="40749-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="40749-121">disponibilità Hello impostata come illustrato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40749-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="40749-122">Ogni macchina virtuale e informazioni dettagliate sulla configurazione di hello sono illustrate di seguito.</span><span class="sxs-lookup"><span data-stu-id="40749-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![Set di disponibilità](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="40749-124">Per informazioni approfondite sui set di disponibilità, vedere [Gestione della disponibilità delle macchine virtuali](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40749-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="40749-125">Servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="40749-125">Network Load Balancer</span></span>
<span data-ttu-id="40749-126">Mentre un set di disponibilità garantisce tolleranza di errore di applicazione, un bilanciamento del carico rende disponibili molte istanze di un'applicazione hello in un unico indirizzo di rete.</span><span class="sxs-lookup"><span data-stu-id="40749-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="40749-127">Più istanze di un'applicazione possono essere ospitate nel numero di macchine virtuali, ciascuno di essi connessa tooa servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="40749-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="40749-128">Come si accede a un'applicazione hello, le route del servizio di bilanciamento carico di hello hello richiesta in ingresso tra i membri di hello associata.</span><span class="sxs-lookup"><span data-stu-id="40749-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="40749-129">Un servizio di bilanciamento del carico possono essere aggiunti utilizzando Visual Studio aggiungere Creazione guidata nuova risorsa hello o inserendo correttamente formattato risorse JSON nel modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="40749-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="40749-130">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [bilanciamento del carico di rete](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="40749-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

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

<span data-ttu-id="40749-131">Poiché l'applicazione di esempio hello è esposto toohello internet con un indirizzo IP pubblico, questo indirizzo è associato con bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="40749-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="40749-132">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [associazione di bilanciamento del carico di rete con indirizzo IP pubblico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="40749-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

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

<span data-ttu-id="40749-133">Dal portale di Azure hello, hello Panoramica di bilanciamento carico di rete Mostra associazione hello con indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="40749-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![Servizio di bilanciamento del carico](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="40749-135">Regola del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="40749-135">Load Balancer Rule</span></span>
<span data-ttu-id="40749-136">Quando si utilizza un bilanciamento del carico, vengono configurate le regole che controllano come il traffico viene bilanciato tra le risorse di hello previsto.</span><span class="sxs-lookup"><span data-stu-id="40749-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="40749-137">Con un'applicazione hello esempio Negozio, il traffico che arriva nella porta 80 dell'indirizzo IP pubblico hello e viene distribuito tra la porta 80 di tutte le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="40749-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="40749-138">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [regola di bilanciamento del carico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="40749-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

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

<span data-ttu-id="40749-139">Una vista della rete hello caricare regola di bilanciamento del carico dal portale di hello.</span><span class="sxs-lookup"><span data-stu-id="40749-139">A view of hello network load balancer rule from hello portal.</span></span>

![Regola del servizio di bilanciamento del carico di rete](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="40749-141">Probe del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="40749-141">Load Balancer Probe</span></span>
<span data-ttu-id="40749-142">servizio di bilanciamento del carico Hello deve inoltre toomonitor ogni macchina virtuale in modo che le richieste vengono soddisfatte solo i sistemi toorunning.</span><span class="sxs-lookup"><span data-stu-id="40749-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="40749-143">Questo monitoraggio avviene tramite l'esecuzione costante del probe su una porta predefinita.</span><span class="sxs-lookup"><span data-stu-id="40749-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="40749-144">distribuzione di negozio Hello è tooprobe configurata la porta 80 in tutti inclusa le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="40749-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="40749-145">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [Probe di bilanciamento del carico](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="40749-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

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

<span data-ttu-id="40749-146">probe di bilanciamento del carico Hello rilevato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40749-146">hello load balancer probe seen from hello Azure portal.</span></span>

![Probe del servizio di bilanciamento del carico di rete](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="40749-148">Regole NAT in ingresso</span><span class="sxs-lookup"><span data-stu-id="40749-148">Inbound NAT Rules</span></span>
<span data-ttu-id="40749-149">Quando si utilizza un bilanciamento del carico, è necessario toobe regole allocate che forniscono l'accesso non carico bilanciato tooeach macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="40749-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="40749-150">Ad esempio, quando si crea una connessione SSH con ogni macchina virtuale, il carico del traffico non deve essere bilanciato, ma è necessario che sia configurato un percorso predeterminato.</span><span class="sxs-lookup"><span data-stu-id="40749-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="40749-151">I percorsi di questo tipo vengono configurati mediante una risorsa di regola NAT in ingresso.</span><span class="sxs-lookup"><span data-stu-id="40749-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="40749-152">Utilizzare questa risorsa, comunicazioni in ingresso possono essere mappato tooindividual macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="40749-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="40749-153">Con l'applicazione di archiviazione di file musicali hello, una porta a partire da 5000 è mappato tooport 22 in ogni macchina virtuale per l'accesso SSH.</span><span class="sxs-lookup"><span data-stu-id="40749-153">With hello Music Store application, a port starting at 5000 is mapped tooport 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="40749-154">Hello `copyindex()` funzione è utilizzata tooincrement hello porta in ingresso, ad esempio che hello seconda macchina virtuale riceve una porta in ingresso di 5001, hello 5002 terzo e così via.</span><span class="sxs-lookup"><span data-stu-id="40749-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span> 

<span data-ttu-id="40749-155">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [le regole NAT in ingresso](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="40749-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

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

<span data-ttu-id="40749-156">Esempio di una regola NAT in ingresso come hello visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="40749-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="40749-157">Per ogni macchina virtuale nella distribuzione hello viene creata una regola di SSH NAT.</span><span class="sxs-lookup"><span data-stu-id="40749-157">An SSH NAT rule is created for each virtual machine in hello deployment.</span></span>

![Regola NAT in ingresso](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="40749-159">Per informazioni dettagliate su hello bilanciamento del carico di rete di Azure, vedere [bilanciamento del carico per servizi di infrastruttura di Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40749-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="40749-160">Distribuire più macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="40749-160">Deploy multiple VMs</span></span>
<span data-ttu-id="40749-161">Infine, per una funzione di tooeffectively Set di disponibilità o bilanciamento del carico, sono necessari più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="40749-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="40749-162">Più macchine virtuali possono essere distribuite tramite funzione di copia modello hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="40749-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="40749-163">Utilizza la funzione di copia hello, non è necessario toodefine un numero finito di macchine virtuali, invece questo valore può essere specificato in modo dinamico in fase di hello della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="40749-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="40749-164">funzione di copia Hello utilizza hello numerose istanze toocreated e gestisce la distribuzione di numero adeguato di hello di macchine virtuali e le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="40749-164">hello copy function consumes hello number of instances toocreated and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="40749-165">Nel modello di esempio di archivio musica hello è definito un parametro che accetta un numero di istanza.</span><span class="sxs-lookup"><span data-stu-id="40749-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="40749-166">Questo numero viene utilizzato in tutto il modello di hello durante la creazione di macchine virtuali e le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="40749-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

<span data-ttu-id="40749-167">In hello risorsa di macchina virtuale, il ciclo di copia hello viene assegnato un nome e numero hello del parametro di istanze usati toocontrol hello copie risultante.</span><span class="sxs-lookup"><span data-stu-id="40749-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="40749-168">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [funzione di copia macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="40749-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

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

<span data-ttu-id="40749-169">iterazione corrente di Hello della funzione di copia hello accessibili con hello `copyIndex()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="40749-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="40749-170">il valore di Hello della funzione di hello copia indice può essere utilizzato tooname le macchine virtuali e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="40749-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="40749-171">Ad esempio, se vengono distribuite due istanze di una macchina virtuale, queste devono avere nomi diversi.</span><span class="sxs-lookup"><span data-stu-id="40749-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="40749-172">Hello `copyIndex()` funzione può essere utilizzata come parte della macchina virtuale hello Nome toocreate un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="40749-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="40749-173">Un esempio di hello `copyindex()` funzione utilizzata per scopi di denominazione può essere visualizzati in hello risorsa di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="40749-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="40749-174">In questo caso, il nome di computer hello è una concatenazione di hello `vmName` parametro e hello `copyIndex()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="40749-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="40749-175">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [funzione indice copia](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="40749-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

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

<span data-ttu-id="40749-176">Hello `copyIndex` funzione viene utilizzata più volte nel modello di esempio hello Negozio.</span><span class="sxs-lookup"><span data-stu-id="40749-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="40749-177">Utilizzo di funzioni e risorse `copyIndex` includono tooa nulla specifica una singola istanza di macchina virtuale hello come interfaccia di rete, regole di bilanciamento del carico, e qualsiasi dipende da funzioni.</span><span class="sxs-lookup"><span data-stu-id="40749-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="40749-178">Per ulteriori informazioni sulla funzione di copia hello, vedere [creare più istanze delle risorse in Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="40749-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="40749-179">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="40749-179">Next step</span></span>
<hr>

[<span data-ttu-id="40749-180">Passaggio 4: Distribuzione di applicazioni con i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="40749-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

