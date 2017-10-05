---
title: Creare una regola di Azure Load Balancer per un cluster
description: Configurare un'istanza di Azure Load Balancer per aprire le porte per un cluster di Azure Service Fabric.
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
ms.openlocfilehash: c99c4d9f343ca97fd3cd363fb54feaf5507bb77c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a><span data-ttu-id="ee573-103">Aprire le porte per un cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ee573-103">Open ports for a Service Fabric cluster</span></span>

<span data-ttu-id="ee573-104">Il servizio di bilanciamento del carico distribuito con il cluster di Azure Service Fabric indirizza il traffico all'app eseguita in un nodo.</span><span class="sxs-lookup"><span data-stu-id="ee573-104">The load balancer deployed with your Azure Service Fabric cluster directs traffic to your app running on a node.</span></span> <span data-ttu-id="ee573-105">Se si modifica l'app per usare una porta diversa, è necessario esporre tale porta (o eseguire l'instradamento a un'altra porta) in Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="ee573-105">If you change your app to use a different port, you must expose that port (or route a different port) in the Azure Load Balancer.</span></span>

<span data-ttu-id="ee573-106">Al momento della distribuzione del cluster di Service Fabric in Azure, è stato creato automaticamente un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="ee573-106">When you deployed your service fabric cluster to Azure, a load balancer was automatically created for you.</span></span> <span data-ttu-id="ee573-107">Se non è disponibile un servizio di bilanciamento del carico, vedere l'articolo su come [configurare un servizio di bilanciamento del carico con connessione Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee573-107">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

## <a name="configure-service-fabric"></a><span data-ttu-id="ee573-108">Configurare Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ee573-108">Configure service fabric</span></span>

<span data-ttu-id="ee573-109">Il file di configurazione **ServiceManifest.xml** dell'applicazione di Service Fabric definisce gli endpoint che verranno usati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ee573-109">Your Service Fabric application **ServiceManifest.xml** config file defines the endpoints your application expects to use.</span></span> <span data-ttu-id="ee573-110">Dopo l'aggiornamento del file di configurazione per definire un endpoint, è necessario aggiornare il servizio di bilanciamento del carico per esporre tale porta o un'altra.</span><span class="sxs-lookup"><span data-stu-id="ee573-110">After the config file has been updated to define an endpoint, the load balancer must be updated to expose that (or a different) port.</span></span> <span data-ttu-id="ee573-111">Per altre informazioni sulla creazione dell'endpoint di Service Fabric, vedere l'articolo su come [configurare un endpoint](service-fabric-service-manifest-resources.md).</span><span class="sxs-lookup"><span data-stu-id="ee573-111">For more information on how to create the service fabric endpoint, see [Setup an Endpoint](service-fabric-service-manifest-resources.md).</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="ee573-112">Creare una regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="ee573-112">Create a load balancer rule</span></span>

<span data-ttu-id="ee573-113">Una regola di bilanciamento del carico apre una porta con connessione Internet e inoltra il traffico alla porta del nodo interno usata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ee573-113">A load balancer rule opens up an internet-facing port and forwards traffic to the internal node's port used by your application.</span></span> <span data-ttu-id="ee573-114">Se non è disponibile un servizio di bilanciamento del carico, vedere l'articolo su come [configurare un servizio di bilanciamento del carico con connessione Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee573-114">If you do not have a load balancer, see [Configure an Internet-facing load balancer](..\load-balancer\load-balancer-get-started-internet-portal.md).</span></span>

<span data-ttu-id="ee573-115">Per creare una regola di bilanciamento del carico, è necessario raccogliere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ee573-115">To create a load balancer rule, you need to collect the following information:</span></span>

- <span data-ttu-id="ee573-116">Nome del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="ee573-116">Load balancer name.</span></span>
- <span data-ttu-id="ee573-117">Gruppo di risorse del servizio di bilanciamento del carico e del cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ee573-117">Resource group of the load balancer and service fabric cluster.</span></span>
- <span data-ttu-id="ee573-118">Porta esterna.</span><span class="sxs-lookup"><span data-stu-id="ee573-118">External port.</span></span>
- <span data-ttu-id="ee573-119">Porta interna.</span><span class="sxs-lookup"><span data-stu-id="ee573-119">Internal port.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="ee573-120">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="ee573-120">Azure CLI</span></span>
>[!NOTE]
><span data-ttu-id="ee573-121">Se è necessario determinare il nome del servizio di bilanciamento del carico, usare questo comando per ottenere rapidamente un elenco di tutti i servizi di bilanciamento del carico e i gruppi di risorse associati.</span><span class="sxs-lookup"><span data-stu-id="ee573-121">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and the associated resource groups.</span></span>
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

<span data-ttu-id="ee573-122">Per creare una regola di bilanciamento del carico con l'**interfaccia della riga di comando di Azure** è sufficiente un solo comando.</span><span class="sxs-lookup"><span data-stu-id="ee573-122">It only takes a single command to create a load balancer rule with the **Azure CLI**.</span></span> <span data-ttu-id="ee573-123">Per creare una nuova regola è necessario sapere solo il nome del servizio di bilanciamento del carico e quello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ee573-123">You just need to know both the name of the load balancer and resource group to create a new rule.</span></span>

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

<span data-ttu-id="ee573-124">Il comando dell'interfaccia della riga di comando di Azure include alcuni parametri descritti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="ee573-124">The Azure CLI command has a few parameters that are described in the following table:</span></span>

| <span data-ttu-id="ee573-125">.</span><span class="sxs-lookup"><span data-stu-id="ee573-125">Parameter</span></span> | <span data-ttu-id="ee573-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ee573-126">Description</span></span> |
| --------- | ----------- |
| `--backend-port`  | <span data-ttu-id="ee573-127">Porta su cui è in ascolto l'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ee573-127">The port the service fabric application is listening to.</span></span> |
| `--frontend-port` | <span data-ttu-id="ee573-128">Porta esposta dal servizio di bilanciamento del carico per le connessioni esterne.</span><span class="sxs-lookup"><span data-stu-id="ee573-128">The port the load balancer exposes for external connections.</span></span> |
| `-lb-name` | <span data-ttu-id="ee573-129">Nome del servizio di bilanciamento del carico da modificare.</span><span class="sxs-lookup"><span data-stu-id="ee573-129">The name of the load balancer to change.</span></span> |
| `-g`       | <span data-ttu-id="ee573-130">Gruppo di risorse che include sia il servizio di bilanciamento del carico che il cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ee573-130">The resource group that has both the load balancer and service fabric cluster.</span></span> |
| `-n`       | <span data-ttu-id="ee573-131">Nome scelto per la regola.</span><span class="sxs-lookup"><span data-stu-id="ee573-131">The chosen name of the rule.</span></span> |


>[!NOTE]
><span data-ttu-id="ee573-132">Per altre informazioni in merito, vedere l'articolo su come [creare un servizio di bilanciamento del carico con l'interfaccia della riga di comando di Azure](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ee573-132">For more information on how to create a load balancer with the Azure CLI, see [Create a load balancer with the Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="ee573-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee573-133">PowerShell</span></span>

>[!NOTE]
><span data-ttu-id="ee573-134">Se è necessario determinare il nome del servizio di bilanciamento del carico, usare questo comando per ottenere rapidamente un elenco di tutti i servizi di bilanciamento del carico e i gruppi di risorse associati.</span><span class="sxs-lookup"><span data-stu-id="ee573-134">If you need to determine the name of the load balancer, use this command to quickly get a list of all load balancers and associated resource groups.</span></span>
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

<span data-ttu-id="ee573-135">PowerShell è un po' più complesso rispetto all'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee573-135">PowerShell is a little more complicated than the Azure CLI.</span></span> <span data-ttu-id="ee573-136">A livello concettuale, per creare una regola è necessario completare i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ee573-136">Conceptually, do the following steps to create a rule.</span></span>

1. <span data-ttu-id="ee573-137">Recuperare il servizio di bilanciamento del carico da Azure.</span><span class="sxs-lookup"><span data-stu-id="ee573-137">Get the load balancer from Azure.</span></span>
2. <span data-ttu-id="ee573-138">Creare una regola.</span><span class="sxs-lookup"><span data-stu-id="ee573-138">Create a rule.</span></span>
3. <span data-ttu-id="ee573-139">Aggiungere la regola al servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="ee573-139">Add the rule to the load balancer.</span></span>
4. <span data-ttu-id="ee573-140">Aggiornare il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="ee573-140">Update the load balancer.</span></span>

```powershell
# Get the load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create the rule based on information from the load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add the rule to the load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update the load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

<span data-ttu-id="ee573-141">Nel comando `New-AzureRmLoadBalancerRuleConfig`, `-FrontendPort` rappresenta la porta esposta dal servizio di bilanciamento del carico per le connessioni esterne, mentre `-BackendPort` rappresenta la porta su cui è in ascolto l'app di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ee573-141">Regarding the `New-AzureRmLoadBalancerRuleConfig` command, the `-FrontendPort` represents the port the load balancer exposes for external connections, and the `-BackendPort` represents the port the service fabric app is listening to.</span></span>

>[!NOTE]
><span data-ttu-id="ee573-142">Per altre informazioni in merito, vedere l'articolo su come [creare un servizio di bilanciamento del carico con PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ee573-142">For more information on how to create a load balancer with PowerShell, see [Create a load balancer with PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).</span></span>

