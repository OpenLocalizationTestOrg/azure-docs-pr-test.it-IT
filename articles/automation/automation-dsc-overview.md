---
title: Panoramica di Automation DSC per Azure | Documentazione Microsoft
description: Panoramica della piattaforma DSC (Desired State Configuration) di Automazione di Azure, dei termini a essa relativi e dei problemi noti
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powershell dsc, configurazione dello stato desiderato, powershell dsc azure
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="52747-104">Panoramica della piattaforma DSC di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="52747-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="52747-105">Automation DSC per Azure è un servizio di Azure che consente di scrivere, gestire e compilare [configurazioni](https://msdn.microsoft.com/powershell/dsc/configurations) PowerShell DSC (Desired State Configuration), importare [risorse DSC](https://msdn.microsoft.com/powershell/dsc/resources) e assegnare configurazioni ai nodi di destinazione, il tutto nel cloud.</span><span class="sxs-lookup"><span data-stu-id="52747-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="52747-106">Perché usare Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="52747-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="52747-107">Automation DSC per Azure offre diversi vantaggi rispetto all'uso di DSC al di fuori di Azure.</span><span class="sxs-lookup"><span data-stu-id="52747-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="52747-108">Server di pull predefinito</span><span class="sxs-lookup"><span data-stu-id="52747-108">Built-in pull server</span></span>

<span data-ttu-id="52747-109">Automazione di Azure fornisce un [server di pull DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) in modo che i nodi di destinazione ricevano automaticamente le configurazioni, conformemente allo stato desiderato, e segnalino la propria conformità.</span><span class="sxs-lookup"><span data-stu-id="52747-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="52747-110">Il server di pull predefinito in Automazione di Azure elimina la necessità di configurare e gestire un proprio server di pull.</span><span class="sxs-lookup"><span data-stu-id="52747-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="52747-111">Automazione di Azure può avere come destinazione macchine virtuali o computer fisici Windows o Linux, nel cloud o locali.</span><span class="sxs-lookup"><span data-stu-id="52747-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="52747-112">Gestione di tutti gli elementi DSC</span><span class="sxs-lookup"><span data-stu-id="52747-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="52747-113">Automation DSC per Azure introduce infatti in [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) lo stesso livello di gestione offerto da Automazione di Azure per gli script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52747-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="52747-114">Dal portale di Azure o da PowerShell è possibile gestire tutte le configurazioni, le risorse e i nodi di destinazione DSC.</span><span class="sxs-lookup"><span data-stu-id="52747-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Screenshot del pannello Automazione di Azure](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="52747-116">Importare i dati dei report in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="52747-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="52747-117">I nodi gestiti con Automation DSC per Azure inviano dati dettagliati sullo stato dei report al server di pull predefinito.</span><span class="sxs-lookup"><span data-stu-id="52747-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="52747-118">È possibile configurare Automation DSC per Azure per inviare questi dati all'area di lavoro Log Analytics di Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="52747-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="52747-119">Per informazioni su come inviare i dati sullo stato di DSC all'area di lavoro Log Analytics, vedere [Inoltrare i dati dei report di Automation DSC per Azure a Log Analytics di OMS](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="52747-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="52747-120">Video introduttivo</span><span class="sxs-lookup"><span data-stu-id="52747-120">Introduction video</span></span>

<span data-ttu-id="52747-121">Si preferisce guardare che leggere?</span><span class="sxs-lookup"><span data-stu-id="52747-121">Prefer watching to reading?</span></span> <span data-ttu-id="52747-122">Guardare il video di seguito del maggio 2015, quando Azure Automation DSC è stato annunciato per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="52747-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="52747-123">Anche se i concetti e il ciclo di vita descritti in questo video sono corretti, Automation DSC per Azure ha fatto molti progressi dalla registrazione del video.</span><span class="sxs-lookup"><span data-stu-id="52747-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="52747-124">È ora disponibile a livello generale, ha un'interfaccia utente molto più estesa nel portale di Azure e supporta molte funzionalità aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="52747-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="52747-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52747-125">Next steps</span></span>

* <span data-ttu-id="52747-126">Per informazioni su come caricare i nodi da gestire con Automation DSC per Azure, vedere [Onboarding di computer per la gestione con Automation DSC per Azure](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="52747-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="52747-127">Per iniziare a usare Automation DSC per Azure, vedere [Introduzione ad Automation DSC per Azure](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="52747-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="52747-128">Per informazioni sulla compilazione di configurazioni DSC da assegnare ai nodi di destinazione, vedere [Compilazione di configurazioni in Automation DSC per Azure](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="52747-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="52747-129">Per informazioni di riferimento sui cmdlet di PowerShell per Automation DSC per Azure, vedere [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation) (Cmdlet di Automation DSC per Azure)</span><span class="sxs-lookup"><span data-stu-id="52747-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="52747-130">Per informazioni sui prezzi, vedere [Prezzi di Automation DSC per Azure](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="52747-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="52747-131">Per un esempio di utilizzo di Automation DSC per Azure in una pipeline di distribuzione continua, vedere [distribuzione continua per IaaS macchine virtuali utilizzando Automation DSC per Azure e Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="52747-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>