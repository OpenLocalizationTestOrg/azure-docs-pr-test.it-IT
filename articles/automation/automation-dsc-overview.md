---
title: Panoramica di DSC di automazione aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="02a3c-104">Panoramica della piattaforma DSC di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="02a3c-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="02a3c-105">DSC di automazione di Azure è un servizio di Azure che consente di toowrite, gestire e compilare PowerShell DSC Desired State Configuration () [configurazioni](https://msdn.microsoft.com/powershell/dsc/configurations), importare [risorse DSC](https://msdn.microsoft.com/powershell/dsc/resources)e assegnare configurazioni tootarget nodi, tutti i cloud hello.</span><span class="sxs-lookup"><span data-stu-id="02a3c-105">Azure Automation DSC is an Azure service that allows you toowrite, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations tootarget nodes, all in hello cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="02a3c-106">Perché usare Automation DSC per Azure</span><span class="sxs-lookup"><span data-stu-id="02a3c-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="02a3c-107">Automation DSC per Azure offre diversi vantaggi rispetto all'uso di DSC al di fuori di Azure.</span><span class="sxs-lookup"><span data-stu-id="02a3c-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="02a3c-108">Server di pull predefinito</span><span class="sxs-lookup"><span data-stu-id="02a3c-108">Built-in pull server</span></span>

<span data-ttu-id="02a3c-109">Automazione di Azure fornisce un [server di pull DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) in modo che i nodi di destinazione ricevano automaticamente le configurazioni, stato toohello desiderato è conforme e segnalare la conformità.</span><span class="sxs-lookup"><span data-stu-id="02a3c-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform toohello desired state, and report back on their compliance.</span></span>
<span data-ttu-id="02a3c-110">server di pull predefinite Hello in automazione di Azure Elimina hello necessità tooset backup e gestire il proprio server di pull.</span><span class="sxs-lookup"><span data-stu-id="02a3c-110">hello built-in pull server in Azure Automation eliminates hello need tooset up and maintain your own pull server.</span></span>
<span data-ttu-id="02a3c-111">Automazione di Azure può far riferimento a computer virtuali o fisici Windows o Linux, in locale o cloud hello.</span><span class="sxs-lookup"><span data-stu-id="02a3c-111">Azure Automation can target virtual or physical Windows or Linux machines, in hello cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="02a3c-112">Gestione di tutti gli elementi DSC</span><span class="sxs-lookup"><span data-stu-id="02a3c-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="02a3c-113">DSC di automazione di Azure offre hello stesso livello di gestione troppo[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) come l'automazione di Azure offre per lo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02a3c-113">Azure Automation DSC brings hello same management layer too[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="02a3c-114">Dal portale di Azure hello o da PowerShell, è possibile gestire tutti i DSC le configurazioni, risorse e nodi di destinazione.</span><span class="sxs-lookup"><span data-stu-id="02a3c-114">From hello Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Cattura di schermata del Pannello di automazione di Azure hello](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="02a3c-116">Importare i dati dei report in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="02a3c-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="02a3c-117">Nodi gestiti con Automation DSC per Azure trasmissione dettagliata stato dati toohello pull predefinite server di report.</span><span class="sxs-lookup"><span data-stu-id="02a3c-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data toohello built-in pull server.</span></span>
<span data-ttu-id="02a3c-118">È possibile configurare automazione di Azure DSC toosend questa area di lavoro di dati tooyour Analitica di Log di Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="02a3c-118">You can configure Azure Automation DSC toosend this data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="02a3c-119">toolearn toosend DSC stato dati tooyour area di lavoro Analitica di Log, vedere [rollforward Automation DSC per Azure reporting dati tooOMS Analitica Log](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="02a3c-119">toolearn how toosend DSC status data tooyour Log Analytics workspace, see [Forward Azure Automation DSC reporting data tooOMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="02a3c-120">Video introduttivo</span><span class="sxs-lookup"><span data-stu-id="02a3c-120">Introduction video</span></span>

<span data-ttu-id="02a3c-121">Se si preferisce guardare il video tooreading,</span><span class="sxs-lookup"><span data-stu-id="02a3c-121">Prefer watching tooreading?</span></span> <span data-ttu-id="02a3c-122">Sono esaminati hello seguente video da maggio 2015, quando cui è stato annunciato Automation DSC per Azure.</span><span class="sxs-lookup"><span data-stu-id="02a3c-122">Have a look at hello following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="02a3c-123">Mentre i concetti di hello e ciclo di vita descritti in questo video sono corrette, DSC di automazione di Azure è molto avanzato poiché in questo video è stato registrato.</span><span class="sxs-lookup"><span data-stu-id="02a3c-123">While hello concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="02a3c-124">È ora disponibile in genere, è un'interfaccia molto più ampia utente nel portale di Azure hello e supporta numerose funzionalità aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="02a3c-124">It is now generally available, has a much more extensive UI in hello Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="02a3c-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02a3c-125">Next steps</span></span>

* <span data-ttu-id="02a3c-126">toolearn come tooonboard toobe di nodi gestiti con DSC di automazione di Azure, vedere [macchine di caricamento per la gestione da Automation DSC per Azure](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="02a3c-126">toolearn how tooonboard nodes toobe managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="02a3c-127">tooget avviato tramite DSC di automazione di Azure, vedere [Introduzione a DSC di automazione di Azure](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="02a3c-127">tooget started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="02a3c-128">toolearn sulla compilazione di configurazioni DSC in modo che è possibile assegnarli tootarget nodi, vedere [compilazione delle configurazioni in automazione di Azure DSC](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="02a3c-128">toolearn about compiling DSC configurations so that you can assign them tootarget nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="02a3c-129">Per informazioni di riferimento sui cmdlet di PowerShell per Automation DSC per Azure, vedere [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation) (Cmdlet di Automation DSC per Azure)</span><span class="sxs-lookup"><span data-stu-id="02a3c-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="02a3c-130">Per informazioni sui prezzi, vedere [Prezzi di Automation DSC per Azure](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="02a3c-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="02a3c-131">vedere un esempio di utilizzo di Automation DSC per Azure in una pipeline di distribuzione continua, toosee [tooIaaS distribuzione continua DSC di automazione di Azure utilizzando macchine virtuali e Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="02a3c-131">toosee an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment tooIaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>
