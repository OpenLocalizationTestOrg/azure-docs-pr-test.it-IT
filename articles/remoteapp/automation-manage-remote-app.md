---
title: aaaManage RemoteApp di Azure utilizzando l'automazione di Azure | Documenti Microsoft
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage Azure RemoteApp."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="efdff-103">Gestione di Azure RemoteApp usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="efdff-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="efdff-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="efdff-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="efdff-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="efdff-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="efdff-106">Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="efdff-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="efdff-107">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="efdff-107">What is Azure Automation?</span></span>
<span data-ttu-id="efdff-108">[Automazione di Azure](../automation/automation-intro.md) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="efdff-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="efdff-109">Attività manuali ripetute di frequente, con esecuzione prolungata e soggetta a errori utilizzando l'automazione di Azure, può essere automatizzata tooincrease affidabilità, efficienza e toovalue tempo per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="efdff-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="efdff-110">Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="efdff-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="efdff-111">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="efdff-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="efdff-112">Liberare e ridurre i costi operativi IT e DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="efdff-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="efdff-113">Come può Automazione di Azure aiutare nella gestione di Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="efdff-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="efdff-114">RemoteApp possono essere gestiti in automazione di Azure tramite i cmdlet di PowerShell hello disponibili in hello [gli strumenti di Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="efdff-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="efdff-115">Automazione di Azure offre questi cmdlet PowerShell di RemoteApp disponibili predefinito hello, in modo che sia possibile eseguire tutte le attività di gestione RemoteApp nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="efdff-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="efdff-116">È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="efdff-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efdff-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="efdff-117">Next steps</span></span>
<span data-ttu-id="efdff-118">Dopo aver appreso hello nozioni di base automazione di Azure e come può essere utilizzato toomanage Azure RemoteApp, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="efdff-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="efdff-119">Vedere hello automazione di Azure [esercitazione introduttiva](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="efdff-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

