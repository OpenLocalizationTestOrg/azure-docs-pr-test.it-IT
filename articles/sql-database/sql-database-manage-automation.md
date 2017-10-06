---
title: Database SQL di Azure utilizzando l'automazione di Azure aaaManage | Documenti Microsoft
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage di database SQL di Azure su larga scala."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="7e886-103">Gestire i database SQL usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7e886-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="7e886-104">Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione dei database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e886-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="7e886-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7e886-105">What is Azure Automation?</span></span>
<span data-ttu-id="7e886-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="7e886-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="7e886-107">Utilizzando l'automazione di Azure, le attività a esecuzione prolungata, manuale, soggetta a errori e ripetute spesso possono essere toovalue tempo per l'organizzazione, efficienza e affidabilità tooincrease automatizzati.</span><span class="sxs-lookup"><span data-stu-id="7e886-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="7e886-108">Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze, man mano che aumenta l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7e886-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="7e886-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="7e886-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="7e886-110">Liberare e ridurre i costi operativi IT / DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e886-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="7e886-111">Come può Automazione di Azure aiutare nella gestione dei database SQL?</span><span class="sxs-lookup"><span data-stu-id="7e886-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="7e886-112">Database SQL di Azure possono essere gestito in automazione di Azure con hello [i cmdlet di PowerShell per Azure SQL Database](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) che sono disponibili in hello [gli strumenti di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7e886-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="7e886-113">Automazione di Azure dispone di questi cmdlet di PowerShell per Azure SQL Database disponibili predefinito hello, che è possibile eseguire tutte le attività di gestione di database di SQL Server all'interno del servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="7e886-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="7e886-114">È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="7e886-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="7e886-115">Automazione di Azure dispone inoltre hello possibilità toocommunicate con istanze di SQL Server direttamente, eseguendo i comandi SQL con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e886-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="7e886-116">Hello [raccolta di runbook di automazione di Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene un'ampia gamma di prodotti team e community runbook tooget avviato l'automazione della gestione di database SQL di Azure, gli altri servizi di Azure e sistemi di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="7e886-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="7e886-117">I Runbook della raccolta includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="7e886-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="7e886-118">Eseguire query SQL su un database SQL Server</span><span class="sxs-lookup"><span data-stu-id="7e886-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="7e886-119">Scalabilità verticale (verso l’alto o il basso) di un database di SQL Azure in una pianificazione</span><span class="sxs-lookup"><span data-stu-id="7e886-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="7e886-120">Troncare una tabella SQL se il database si avvicina alla dimensione massima</span><span class="sxs-lookup"><span data-stu-id="7e886-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="7e886-121">Tabelle dell’indice in un database SQL di Azure se sono molto frammentati</span><span class="sxs-lookup"><span data-stu-id="7e886-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="7e886-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e886-122">Next steps</span></span>
<span data-ttu-id="7e886-123">Ora che si è appreso hello nozioni di base automazione di Azure e come può essere toomanage utilizzati database di SQL Azure, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e886-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="7e886-124">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7e886-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="7e886-125">Il primo runbook</span><span class="sxs-lookup"><span data-stu-id="7e886-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="7e886-126">Mappa di apprendimento di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7e886-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="7e886-127">Automazione di Azure: L'agente SQL in hello Cloud</span><span class="sxs-lookup"><span data-stu-id="7e886-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

