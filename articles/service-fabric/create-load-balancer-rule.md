---
title: aaaCreate una regola per un cluster di bilanciamento del carico di Azure
description: Configurare le porte tooopen un bilanciamento del carico di Azure per il cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="167c7-103">Aprire le porte per un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="167c7-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="167c7-104">bilanciamento del carico Hello distribuito con il cluster di Azure Service Fabric indirizza il traffico tooyour app in esecuzione in un nodo.</span><span class="sxs-lookup"><span data-stu-id="167c7-104">hello load balancer deployed with your Azure Service Fabric cluster directs traffic tooyour app running on a node.</span></span> <span data-ttu-id="167c7-105">Se si modifica il toouse app una porta diversa, è necessario esporre tale porta (o indirizzare una porta diversa) in hello bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="167c7-105">If you change your app toouse a different port, you must expose that port (or route a different port) in hello Azure Load Balancer.</span></span>

<span data-ttu-id="167c7-106">Quando è stato distribuito il tooAzure di servizio dell'infrastruttura cluster, è stato creato automaticamente un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="167c7-106">When you deployed your service fabric cluster tooAzure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="167c7-107">Se non è disponibile un servizio di bilanciamento del carico, vedere l'articolo su come [configurare un servizio di bilanciamento del carico con connessione Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="167c7-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="167c7-108">Configurare Service Fabric</span><span class="sxs-lookup"><span data-stu-id="167c7-108">Configure service fabric</span></span>

<span data-ttu-id="167c7-109">L'applicazione di Service Fabric **ServiceManifest.xml** file di configurazione definisce gli endpoint hello l'applicazione prevede toouse.</span><span class="sxs-lookup"><span data-stu-id="167c7-109">Your Service Fabric application **ServiceManifest.xml** config file defines hello endpoints your application expects toouse.</span></span> <span data-ttu-id="167c7-110">Al termine del file di configurazione hello è stata aggiornata toodefine un endpoint, bilanciamento del carico hello deve essere aggiornato tooexpose tale (o una diversa) porta.</span><span class="sxs-lookup"><span data-stu-id="167c7-110">After hello config file has been updated toodefine an endpoint, hello load balancer must be updated tooexpose that (or a different) port.</span></span> <span data-ttu-id="167c7-111">Per ulteriori informazioni su come toocreate hello endpoint dell'infrastruttura del servizio, vedere [un Endpoint del programma di installazione](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="167c7-111">For more information on how toocreate hello service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="167c7-112">Creare una regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="167c7-112">Create a load balancer rule</span></span>

<span data-ttu-id="167c7-113">Una regola di bilanciamento del carico viene aperta una porta con connessione internet e inoltra porta traffico toohello interno del nodo utilizzata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="167c7-113">A load balancer rule opens up an internet-facing port and forwards traffic toohello internal node's port used by your application.</span></span> <span data-ttu-id="167c7-114">Se non è disponibile un servizio di bilanciamento del carico, vedere l'articolo su come [configurare un servizio di bilanciamento del carico con connessione Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="167c7-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="167c7-115">regola toocreate un bilanciamento del carico, è necessario hello toocollect le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="167c7-115">toocreate a load balancer rule, you need toocollect hello following information:</span></span>

- <span data-ttu-id="167c7-116">Nome del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="167c7-116">Load balancer name.</span></span>
- <span data-ttu-id="167c7-117">Gruppo di risorse di hello bilanciamento del carico e cluster di service fabric.</span><span class="sxs-lookup"><span data-stu-id="167c7-117">Resource group of hello load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="167c7-118">Porta esterna.</span><span class="sxs-lookup"><span data-stu-id="167c7-118">External port.</span></span>
- <span data-ttu-id="167c7-119">Porta interna.</span><span class="sxs-lookup"><span data-stu-id="167c7-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="167c7-120">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="167c7-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="167c7-121">Se è necessario il nome hello toodetermine di bilanciamento del carico hello, utilizzare un elenco di tutti i servizi di bilanciamento del carico e i gruppi di risorse hello associata get di tooquickly questo comando.</span><span class="sxs-lookup"><span data-stu-id="167c7-121">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and hello associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="167c7-122">È sufficiente un singolo comando toocreate una regola di bilanciamento del carico con hello **CLI di Azure**.</span><span class="sxs-lookup"><span data-stu-id="167c7-122">It only takes a single command toocreate a load balancer rule with hello **Azure CLI**.</span></span> <span data-ttu-id="167c7-123">È sufficiente tooknow sia nome hello del carico hello bilanciamento e risorse toocreate gruppo una nuova regola.</span><span class="sxs-lookup"><span data-stu-id="167c7-123">You just need tooknow both hello name of hello load balancer and resource group toocreate a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="167c7-124">Hello comando CLI di Azure dispone di alcuni parametri descritti nella seguente tabella hello:</span><span class="sxs-lookup"><span data-stu-id="167c7-124">hello Azure CLI command has a few parameters that are described in hello following table:</span></span>

| <span data-ttu-id="167c7-125">.</span><span class="sxs-lookup"><span data-stu-id="167c7-125">Parameter</span></span> | <span data-ttu-id="167c7-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="167c7-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="167c7-127">applicazione di Hello porta hello service fabric è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="167c7-127">hello port hello service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="167c7-128">hello porta Hello caricare espone di bilanciamento del carico per le connessioni esterne.</span><span class="sxs-lookup"><span data-stu-id="167c7-128">hello port hello load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="167c7-129">nome Hello di hello caricare toochange di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="167c7-129">hello name of hello load balancer toochange.</span></span> |
| `-g`       | <span data-ttu-id="167c7-130">gruppo di risorse Hello con bilanciamento del carico hello sia cluster di service fabric.</span><span class="sxs-lookup"><span data-stu-id="167c7-130">hello resource group that has both hello load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="167c7-131">Hello scelto il nome della regola hello.</span><span class="sxs-lookup"><span data-stu-id="167c7-131">hello chosen name of hello rule.</span></span> |


>[!NOTE]
><span data-ttu-id="167c7-132">Per ulteriori informazioni su come toocreate un bilanciamento del carico con hello CLI di Azure, vedere [creare un servizio di bilanciamento del carico con hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="167c7-132">For more information on how toocreate a load balancer with hello Azure CLI, see [Create a load balancer with hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="167c7-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="167c7-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="167c7-134">Se è necessario il nome hello toodetermine di bilanciamento del carico hello, utilizzare un elenco di tutti i servizi di bilanciamento del carico e i gruppi di risorse associati get di tooquickly questo comando.</span><span class="sxs-lookup"><span data-stu-id="167c7-134">If you need toodetermine hello name of hello load balancer, use this command tooquickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="167c7-135">PowerShell è leggermente più complicato hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="167c7-135">PowerShell is a little more complicated than hello Azure CLI.</span></span> <span data-ttu-id="167c7-136">Concettualmente, eseguire hello seguendo i passaggi toocreate una regola.</span><span class="sxs-lookup"><span data-stu-id="167c7-136">Conceptually, do hello following steps toocreate a rule.</span></span>

1. <span data-ttu-id="167c7-137">Ottenere bilanciamento del carico hello da Azure.</span><span class="sxs-lookup"><span data-stu-id="167c7-137">Get hello load balancer from Azure.</span></span>
2. <span data-ttu-id="167c7-138">Creare una regola.</span><span class="sxs-lookup"><span data-stu-id="167c7-138">Create a rule.</span></span>
3. <span data-ttu-id="167c7-139">Aggiungere toohello hello regola il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="167c7-139">Add hello rule toohello load balancer.</span></span>
4. <span data-ttu-id="167c7-140">Aggiorna bilanciamento del carico di hello.</span><span class="sxs-lookup"><span data-stu-id="167c7-140">Update hello load balancer.</span></span>

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="167c7-141">Riguardanti hello `New-AzureRmLoadBalancerRuleConfig` comando hello `-FrontendPort` espone rappresenta hello porta hello bilanciamento del carico per le connessioni esterne e hello `-BackendPort` rappresenta hello porta hello service fabric app è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="167c7-141">Regarding hello `New-AzureRmLoadBalancerRuleConfig` command, hello `-FrontendPort` represents hello port hello load balancer exposes for external connections, and hello `-BackendPort` represents hello port hello service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="167c7-142">Per ulteriori informazioni su come toocreate un bilanciamento del carico con PowerShell, vedere [creare un servizio di bilanciamento del carico con PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="167c7-142">For more information on how toocreate a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

