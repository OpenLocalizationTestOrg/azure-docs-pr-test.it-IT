---
title: Esempio di script di Azure PowerShell - Aprire una porta dell'applicazione nel servizio di bilanciamento del carico | Microsoft Docs
description: Esempio di script di Azure PowerShell - Aprire una porta nel servizio di bilanciamento del carico di Azure per un'applicazione Service Fabric.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 2958bdef0889076249918608c04c66678fa80b97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="open-an-application-port-in-the-azure-load-balancer"></a><span data-ttu-id="bb879-103">Aprire una porta dell'applicazione nel servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="bb879-103">Open an application port in the Azure load balancer</span></span>

<span data-ttu-id="bb879-104">Il servizio di bilanciamento del carico di Azure è supportato da un'applicazione Service Fabric eseguita in Azure.</span><span class="sxs-lookup"><span data-stu-id="bb879-104">A Service Fabric application running in Azure sits behind the Azure load balancer.</span></span> <span data-ttu-id="bb879-105">Questo script di esempio apre una porta in un servizio di bilanciamento del carico di Azure in modo che un'applicazione Service Fabric possa comunicare con client esterni.</span><span class="sxs-lookup"><span data-stu-id="bb879-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="bb879-106">Personalizzare i parametri in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="bb879-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="bb879-107">Se necessario, installare il modulo PowerShell in Service Fabric con il [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bb879-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bb879-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="bb879-108">Sample script</span></span>

<span data-ttu-id="bb879-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Aprire una porta nel servizio di bilanciamento del carico")]</span><span class="sxs-lookup"><span data-stu-id="bb879-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="bb879-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="bb879-110">Script explanation</span></span>

<span data-ttu-id="bb879-111">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="bb879-111">This script uses the following commands.</span></span> <span data-ttu-id="bb879-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="bb879-112">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="bb879-113">Comando</span><span class="sxs-lookup"><span data-stu-id="bb879-113">Command</span></span> | <span data-ttu-id="bb879-114">Note</span><span class="sxs-lookup"><span data-stu-id="bb879-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bb879-115">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="bb879-115">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="bb879-116">Ottiene una risorsa di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb879-116">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="bb879-117">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="bb879-117">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="bb879-118">Ottiene il servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb879-118">Gets the Azure load balancer.</span></span> |
| [<span data-ttu-id="bb879-119">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="bb879-119">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="bb879-120">Aggiunge la configurazione di una porta probe per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bb879-120">Adds a probe configuration to a load balancer.</span></span>|
| [<span data-ttu-id="bb879-121">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="bb879-121">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="bb879-122">Ottiene la configurazione di un probe per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bb879-122">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="bb879-123">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="bb879-123">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="bb879-124">Aggiunge la configurazione di una regola a un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bb879-124">Adds a rule configuration to a load balancer.</span></span> |
| [<span data-ttu-id="bb879-125">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="bb879-125">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="bb879-126">Imposta lo stato dell'obiettivo per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="bb879-126">Sets the goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bb879-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb879-127">Next steps</span></span>

<span data-ttu-id="bb879-128">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bb879-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="bb879-129">Altri esempi di PowerShell per Azure Service Fabric sono disponibili in [Esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bb879-129">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
