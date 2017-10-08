---
title: Esempio di Script di PowerShell - porta dell'applicazione aperte nel servizio di bilanciamento del carico aaaAzure | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - aprire una porta nel servizio di bilanciamento carico di Azure hello per un'applicazione di Service Fabric.
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
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a><span data-ttu-id="9e2d4-103">Aprire una porta dell'applicazione nel servizio di bilanciamento del carico di Azure hello</span><span class="sxs-lookup"><span data-stu-id="9e2d4-103">Open an application port in hello Azure load balancer</span></span>

<span data-ttu-id="9e2d4-104">Un'applicazione di Service Fabric in esecuzione in Azure si trova dietro il bilanciamento del carico di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-104">A Service Fabric application running in Azure sits behind hello Azure load balancer.</span></span> <span data-ttu-id="9e2d4-105">Questo script di esempio apre una porta in un servizio di bilanciamento del carico di Azure in modo che un'applicazione Service Fabric possa comunicare con client esterni.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="9e2d4-106">Personalizzare i parametri di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="9e2d4-107">Se necessario, installare il modulo di PowerShell di Service Fabric hello con hello [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9e2d4-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9e2d4-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9e2d4-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a><span data-ttu-id="9e2d4-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="9e2d4-109">Script explanation</span></span>

<span data-ttu-id="9e2d4-110">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-110">This script uses hello following commands.</span></span> <span data-ttu-id="9e2d4-111">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-111">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="9e2d4-112">Comando</span><span class="sxs-lookup"><span data-stu-id="9e2d4-112">Command</span></span> | <span data-ttu-id="9e2d4-113">Note</span><span class="sxs-lookup"><span data-stu-id="9e2d4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e2d4-114">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="9e2d4-114">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="9e2d4-115">Ottiene una risorsa di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-115">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="9e2d4-116">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="9e2d4-116">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="9e2d4-117">Ottiene i servizio di bilanciamento del carico di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-117">Gets hello Azure load balancer.</span></span> |
| [<span data-ttu-id="9e2d4-118">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="9e2d4-118">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="9e2d4-119">Aggiunge un bilanciamento del carico di tooa configurazione probe.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-119">Adds a probe configuration tooa load balancer.</span></span>|
| [<span data-ttu-id="9e2d4-120">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="9e2d4-120">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="9e2d4-121">Ottiene la configurazione di un probe per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-121">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9e2d4-122">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9e2d4-122">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="9e2d4-123">Aggiunge un bilanciamento del carico di tooa configurazione regola.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-123">Adds a rule configuration tooa load balancer.</span></span> |
| [<span data-ttu-id="9e2d4-124">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="9e2d4-124">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="9e2d4-125">Set di hello stato obiettivo per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9e2d4-125">Sets hello goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9e2d4-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e2d4-126">Next steps</span></span>

<span data-ttu-id="9e2d4-127">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e2d4-127">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9e2d4-128">Ulteriori esempi di Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9e2d4-128">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
