---
title: Gestire i database SQL usando Automazione di Azure | Documentazione Microsoft
description: "Informazioni su come è possibile usare il servizio Automazione di Azure per gestire database SQL su vasta scala."
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
ms.openlocfilehash: 7f45b8b654691063823c13bee61e9bb874a6a13a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="22659-103">Gestire i database SQL usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="22659-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="22659-104">Questa guida fornisce un'introduzione al servizio Automazione di Azure e ne illustra l'utilizzo per semplificare la gestione dei database SQL.</span><span class="sxs-lookup"><span data-stu-id="22659-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="22659-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="22659-105">What is Azure Automation?</span></span>
<span data-ttu-id="22659-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="22659-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="22659-107">Usando Automazione di Azure, è possibile automatizzare attività a esecuzione prolungata, manuali, soggette a errori e ripetute frequentemente per migliorare l'affidabilità, l'efficienza e i tempi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="22659-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="22659-108">Automazione di Azure offre un motore di esecuzione del flusso di lavoro a elevata disponibilità e affidabilità che garantisce la scalabilità necessaria per rispondere alle esigenze aziendali in base alla crescita dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="22659-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="22659-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="22659-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="22659-110">Il servizio permette di ridurre i costi operativi e di liberare risorse dello staff IT/DevOp consentendo loro di concentrarsi su attività a valore aggiunto grazie al trasferimento delle attività di gestione del cloud all'esecuzione automatica di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="22659-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="22659-111">Come può Automazione di Azure aiutare nella gestione dei database SQL?</span><span class="sxs-lookup"><span data-stu-id="22659-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="22659-112">Il database SQL di Azure può essere gestito in Automazione di Azure usando i [cmdlet di PowerShell del database SQL di Azure](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) disponibili negli [strumenti di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22659-112">Azure SQL Database can be managed in Azure Automation by using the [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in the [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="22659-113">I cmdlet di PowerShell per database SQL di Azure sono predefiniti in Automazione di Azure, per consentire l'esecuzione di tutte le attività di gestione dei database SQL dall'interno del servizio.</span><span class="sxs-lookup"><span data-stu-id="22659-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of the box, so that you can perform all of your SQL DB management tasks within the service.</span></span> <span data-ttu-id="22659-114">È anche possibile abbinare tali cmdlet in Automazione di Azure ai cmdlet per altri servizi di Azure per automatizzare attività complesse in tutti i servizi di Azure e nei sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="22659-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="22659-115">Automazione di Azure è in grado di comunicare direttamente con i server SQL tramite l'invio di comandi SQL da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22659-115">Azure Automation also has the ability to communicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="22659-116">La [raccolta di Runbook di Automazione di Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene diversi Runbook del team di prodotto e della community per iniziare ad automatizzare la gestione dei database SQL di Azure, altri servizi di Azure e sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="22659-116">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="22659-117">I Runbook della raccolta includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="22659-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="22659-118">Eseguire query SQL su un database SQL Server</span><span class="sxs-lookup"><span data-stu-id="22659-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="22659-119">Scalabilità verticale (verso l’alto o il basso) di un database di SQL Azure in una pianificazione</span><span class="sxs-lookup"><span data-stu-id="22659-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="22659-120">Troncare una tabella SQL se il database si avvicina alla dimensione massima</span><span class="sxs-lookup"><span data-stu-id="22659-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="22659-121">Tabelle dell’indice in un database SQL di Azure se sono molto frammentati</span><span class="sxs-lookup"><span data-stu-id="22659-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="22659-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22659-122">Next steps</span></span>
<span data-ttu-id="22659-123">A questo punto, dopo aver appreso le nozioni di base di Automazione di Azure e come può essere usato per gestire i database SQL di Azure, seguire i collegamenti seguenti per altre informazioni su Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="22659-123">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure SQL databases, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="22659-124">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="22659-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="22659-125">Il primo runbook</span><span class="sxs-lookup"><span data-stu-id="22659-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="22659-126">Mappa di apprendimento di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="22659-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="22659-127">Automazione di Azure: SQL Agent nel cloud</span><span class="sxs-lookup"><span data-stu-id="22659-127">Azure Automation: Your SQL Agent in the Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

