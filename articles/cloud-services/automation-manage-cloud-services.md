---
title: Gestire Servizi cloud di Azure usando Automazione di Azure | Documentazione Microsoft
description: "Informazioni su come è possibile usare il servizio Automazione di Azure per gestire i Servizi cloud di Azure su vasta scala."
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
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="4bb97-103">Gestione dei Servizi cloud di Azure mediante Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4bb97-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="4bb97-104">Questa guida fornisce un'introduzione al servizio Automazione di Azure e ne illustra l'utilizzo per semplificare la gestione dei Servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bb97-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="4bb97-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4bb97-105">What is Azure Automation?</span></span>
<span data-ttu-id="4bb97-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="4bb97-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="4bb97-107">Usando Automazione di Azure, è possibile automatizzare attività a esecuzione prolungata, manuali, soggette a errori e ripetute frequentemente per migliorare l'affidabilità, l'efficienza e i tempi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4bb97-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="4bb97-108">Automazione di Azure offre un motore di esecuzione del flusso di lavoro a elevata disponibilità e affidabilità che garantisce la scalabilità necessaria per rispondere alle esigenze aziendali in base alla crescita dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="4bb97-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="4bb97-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="4bb97-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="4bb97-110">Il servizio permette di ridurre i costi operativi e di liberare risorse dello staff IT/DevOp consentendo loro di concentrarsi su attività a valore aggiunto grazie al trasferimento delle attività di gestione del cloud all'esecuzione automatica di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bb97-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="4bb97-111">Come può Automazione di Azure aiutare nella gestione dei Servizi cloud di Azure?</span><span class="sxs-lookup"><span data-stu-id="4bb97-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="4bb97-112">I Servizi cloud di Azure possono essere gestiti in Automazione di Azure usando i cmdlet di PowerShell disponibili negli [strumenti di Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="4bb97-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="4bb97-113">I cmdlet di PowerShell per i Servizi cloud sono predefiniti in Automazione di Azure, per consentire l'esecuzione di tutte le attività di gestione dei servizi cloud dall'interno del servizio.</span><span class="sxs-lookup"><span data-stu-id="4bb97-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="4bb97-114">È anche possibile abbinare tali cmdlet in Automazione di Azure ai cmdlet per altri servizi di Azure per automatizzare attività complesse in tutti i servizi di Azure e nei sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="4bb97-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="4bb97-115">Gli esempi che usano Automazione di Azure per gestire i Servizi cloud di Azure includono:</span><span class="sxs-lookup"><span data-stu-id="4bb97-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="4bb97-116">Distribuzione continua di un servizio cloud ogni volta che il file cscfg o cspkg viene aggiornato nell'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="4bb97-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="4bb97-117">Riavvio di istanze del servizio cloud in parallelo, un dominio di aggiornamento alla volta</span><span class="sxs-lookup"><span data-stu-id="4bb97-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="4bb97-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4bb97-118">Next Steps</span></span>
<span data-ttu-id="4bb97-119">A questo punto, dopo aver appreso le nozioni di base di Automazione di Azure e come può essere usato per gestire i Servizi cloud di Azure, seguire i collegamenti seguenti per altre informazioni su Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bb97-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="4bb97-120">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4bb97-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="4bb97-121">Il primo runbook</span><span class="sxs-lookup"><span data-stu-id="4bb97-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="4bb97-122">Mappa di apprendimento di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4bb97-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
