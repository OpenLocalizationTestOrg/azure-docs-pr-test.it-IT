---
title: Servizi Cloud di Azure utilizzando l'automazione di Azure aaaManage | Documenti Microsoft
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage di servizi cloud di Azure su larga scala."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="94c75-103">Gestione dei Servizi cloud di Azure mediante Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="94c75-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="94c75-104">Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione dei servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="94c75-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="94c75-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="94c75-105">What is Azure Automation?</span></span>
<span data-ttu-id="94c75-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="94c75-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="94c75-107">Utilizzando l'automazione di Azure, le attività a esecuzione prolungata, manuale, soggetta a errori e ripetute spesso possono essere toovalue tempo per l'organizzazione, efficienza e affidabilità tooincrease automatizzati.</span><span class="sxs-lookup"><span data-stu-id="94c75-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="94c75-108">Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze, man mano che aumenta l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="94c75-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="94c75-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="94c75-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="94c75-110">Liberare e ridurre i costi operativi IT / DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="94c75-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="94c75-111">Come può Automazione di Azure aiutare nella gestione dei Servizi cloud di Azure?</span><span class="sxs-lookup"><span data-stu-id="94c75-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="94c75-112">Servizi cloud di Azure possono essere gestiti in automazione di Azure tramite i cmdlet di PowerShell hello disponibili in hello [gli strumenti di Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="94c75-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="94c75-113">Automazione di Azure offre disponibili i cmdlet PowerShell di servizio cloud viene fornita hello, in modo che è possibile eseguire tutte le attività di gestione del servizio cloud all'interno del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="94c75-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="94c75-114">È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="94c75-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="94c75-115">Alcuni esempi di utilizzo dei servizi Cloud di Azure includono toomanage di automazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="94c75-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="94c75-116">Distribuzione continua di un servizio cloud ogni volta che il file cscfg o cspkg viene aggiornato nell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="94c75-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="94c75-117">Riavvio di istanze del servizio cloud in parallelo, un dominio di aggiornamento alla volta</span><span class="sxs-lookup"><span data-stu-id="94c75-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="94c75-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94c75-118">Next Steps</span></span>
<span data-ttu-id="94c75-119">Dopo aver appreso hello nozioni di base automazione di Azure e come può essere utilizzato toomanage servizi cloud di Azure, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="94c75-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="94c75-120">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="94c75-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="94c75-121">Il primo runbook</span><span class="sxs-lookup"><span data-stu-id="94c75-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="94c75-122">Mappa di apprendimento di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="94c75-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
