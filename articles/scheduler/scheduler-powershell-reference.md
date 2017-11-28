---
title: aaaScheduler riferimento di cmdlet di PowerShell
description: "Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a2b23bcd3e4493ffba1dbf21fbb87818be7c01e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="452e0-103">Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione</span><span class="sxs-lookup"><span data-stu-id="452e0-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="452e0-104">Hello nella tabella seguente vengono descritti e collega toohello pagina di riferimento dei cmdlet principali di hello nell'utilità di pianificazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="452e0-104">hello following table describes and links toohello reference page of each of hello major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="452e0-105">tooinstall Azure PowerShell e associarlo a una sottoscrizione di Azure, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="452e0-105">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="452e0-106">Per altre informazioni sui [cmdlet di Azure Resource Manager](/powershell/azure/overview) vedere [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="452e0-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="452e0-107">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="452e0-107">Cmdlet</span></span> | <span data-ttu-id="452e0-108">Descrizione del cmdlet</span><span class="sxs-lookup"><span data-stu-id="452e0-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="452e0-109">Disable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="452e0-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="452e0-110">Disabilita una raccolta di processi.</span><span class="sxs-lookup"><span data-stu-id="452e0-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="452e0-111">Enable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="452e0-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="452e0-112">Abilita una raccolta di processi.</span><span class="sxs-lookup"><span data-stu-id="452e0-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="452e0-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="452e0-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="452e0-114">Ottiene processi dell'Utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="452e0-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="452e0-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="452e0-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="452e0-116">Ottiene raccolte di processi.</span><span class="sxs-lookup"><span data-stu-id="452e0-116">Gets job collections.</span></span> |
| [<span data-ttu-id="452e0-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="452e0-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="452e0-118">Ottiene la cronologia processi.</span><span class="sxs-lookup"><span data-stu-id="452e0-118">Gets job history.</span></span> |
| [<span data-ttu-id="452e0-119">New-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="452e0-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="452e0-120">Crea un processo HTTP.</span><span class="sxs-lookup"><span data-stu-id="452e0-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="452e0-121">New-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="452e0-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="452e0-122">Crea una raccolta di processi.</span><span class="sxs-lookup"><span data-stu-id="452e0-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="452e0-123">New-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="452e0-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="452e0-124">Crea un processo di coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="452e0-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="452e0-125">New-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="452e0-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="452e0-126">Crea un processo di argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="452e0-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="452e0-127">New-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="452e0-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="452e0-128">Crea un processo di coda di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="452e0-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="452e0-129">Remove-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="452e0-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="452e0-130">Elimina un processo dell'Utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="452e0-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="452e0-131">Remove-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="452e0-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="452e0-132">Rimuove una raccolta di processi.</span><span class="sxs-lookup"><span data-stu-id="452e0-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="452e0-133">Set-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="452e0-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="452e0-134">Modifica un processo HTTP dell'Utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="452e0-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="452e0-135">Set-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="452e0-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="452e0-136">Modifica una raccolta di processi.</span><span class="sxs-lookup"><span data-stu-id="452e0-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="452e0-137">Set-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="452e0-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="452e0-138">Modifica un processo di coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="452e0-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="452e0-139">Set-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="452e0-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="452e0-140">Modifica un processo di argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="452e0-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="452e0-141">Set-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="452e0-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="452e0-142">Modifica un processo di coda di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="452e0-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="452e0-143">Per informazioni più dettagliate, è possibile eseguire i seguenti cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="452e0-143">For more detailed information, you can run any of hello following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="452e0-144">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="452e0-144">See Also</span></span>
 [<span data-ttu-id="452e0-145">Che cos'è l'Utilità di pianificazione?</span><span class="sxs-lookup"><span data-stu-id="452e0-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="452e0-146">Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="452e0-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="452e0-147">Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="452e0-147">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="452e0-148">Piani e fatturazione nell'utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="452e0-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="452e0-149">Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="452e0-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="452e0-150">Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="452e0-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="452e0-151">Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="452e0-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="452e0-152">Autenticazione in uscita dell'Utilità di pianificazione di Azure</span><span class="sxs-lookup"><span data-stu-id="452e0-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

