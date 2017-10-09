---
title: aaaManage gestione API di Azure utilizzando l'automazione di Azure
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage gestione API di Azure."
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 05b8e3cad786fa701feb88f7b6d9629f16686d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="fdd7a-103">Gestione di Gestione API di Azure usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="fdd7a-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="fdd7a-104">Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione di gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd7a-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="fdd7a-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="fdd7a-105">What is Azure Automation?</span></span>
<span data-ttu-id="fdd7a-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="fdd7a-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="fdd7a-107">Attività manuali ripetute, con esecuzione prolungata e soggetta a errori utilizzando l'automazione di Azure, può essere automatizzata tooincrease affidabilità, efficienza e toovalue tempo per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="fdd7a-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="fdd7a-108">Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="fdd7a-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="fdd7a-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="fdd7a-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="fdd7a-110">Liberare e ridurre i costi operativi IT e DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd7a-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="fdd7a-111">In che modo Gestione API di Azure può essere gestito con Automazione di Azure?</span><span class="sxs-lookup"><span data-stu-id="fdd7a-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="fdd7a-112">Gestione API possono essere gestiti in automazione di Azure con hello [cmdlet Windows PowerShell per Azure API Gestione](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="fdd7a-112">API Management can be managed in Azure Automation by using hello [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="fdd7a-113">All'interno di automazione di Azure è possibile scrivere tooperform script del flusso di lavoro di PowerShell molte delle attività di gestione di API utilizzando i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="fdd7a-113">Within Azure Automation you can write PowerShell workflow scripts tooperform many of your API Management tasks using hello cmdlets.</span></span> <span data-ttu-id="fdd7a-114">È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="fdd7a-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="fdd7a-115">Di seguito sono riportati alcuni esempi di utilizzo di Gestione API con Automazione:</span><span class="sxs-lookup"><span data-stu-id="fdd7a-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="fdd7a-116">Gestione API di Azure: utilizzo di PowerShell per il backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="fdd7a-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="fdd7a-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdd7a-117">Next Steps</span></span>
<span data-ttu-id="fdd7a-118">Dopo aver appreso hello nozioni di base automazione di Azure e come può essere utilizzato toomanage gestione API di Azure, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="fdd7a-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure API Management, follow these links toolearn more.</span></span>

* <span data-ttu-id="fdd7a-119">Vedere hello automazione di Azure [esercitazione introduttiva](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="fdd7a-119">See hello Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

