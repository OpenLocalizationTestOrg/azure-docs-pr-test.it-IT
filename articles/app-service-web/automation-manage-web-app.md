---
title: aaaManage App Web di Azure utilizzando l'automazione di Azure | Documenti Microsoft
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage App Web di Azure."
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="588a6-103">Gestire App Web di Azure usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="588a6-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="588a6-104">Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione di App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="588a6-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="588a6-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="588a6-105">What is Azure Automation?</span></span>
<span data-ttu-id="588a6-106">[Automazione di Azure](../automation/automation-intro.md) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="588a6-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="588a6-107">Attività manuali ripetute, con esecuzione prolungata e soggetta a errori utilizzando l'automazione di Azure, può essere automatizzata tooincrease affidabilità, efficienza e toovalue tempo per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="588a6-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="588a6-108">Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="588a6-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="588a6-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="588a6-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="588a6-110">Liberare e ridurre i costi operativi IT e DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="588a6-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="588a6-111">In che modo Automazione di Azure può rappresentare un aiuto nella gestione di App Web di Azure?</span><span class="sxs-lookup"><span data-stu-id="588a6-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="588a6-112">App Web possono essere gestiti in automazione di Azure tramite i cmdlet di PowerShell hello disponibili in hello [moduli di Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="588a6-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="588a6-113">È possibile [installare questi cmdlet PowerShell di App Web in automazione di Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), in modo che è possibile eseguire tutte le attività di gestione di App Web nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="588a6-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="588a6-114">Si possono essere anche questi cmdlet in automazione di Azure con i cmdlet di hello attività complesse di tooautomate altri servizi di Azure in servizi di Azure e sistemi di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="588a6-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="588a6-115">Di seguito sono riportati alcuni esempi di gestione dei servizi app con Automazione:</span><span class="sxs-lookup"><span data-stu-id="588a6-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="588a6-116">Script per la gestione di app Web</span><span class="sxs-lookup"><span data-stu-id="588a6-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="588a6-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="588a6-117">Next steps</span></span>
<span data-ttu-id="588a6-118">Dopo aver appreso hello nozioni di base automazione di Azure e come può essere utilizzato toomanage App Web di Azure, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="588a6-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="588a6-119">Vedere hello automazione di Azure [esercitazione introduttiva](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="588a6-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

