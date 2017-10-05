---
title: Gestire Gestione API di Azure usando Automazione di Azure
description: "Informazioni su come è possibile usare il servizio Automazione di Azure per gestire Gestione API di Azure."
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
ms.openlocfilehash: 73a1135482b88ea7c228bc8b228d47c57b2e70a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="e347a-103">Gestione di Gestione API di Azure usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e347a-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="e347a-104">Questa guida fornisce un'introduzione al servizio Automazione di Azure e ne illustra l'uso per semplificare la gestione di Gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="e347a-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="e347a-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e347a-105">What is Azure Automation?</span></span>
<span data-ttu-id="e347a-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="e347a-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="e347a-107">Usando Automazione di Azure, è possibile automatizzare attività manuali, ripetute, a esecuzione prolungata e soggette a errori per migliorare l'affidabilità, l'efficienza e i tempi di esecuzione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="e347a-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="e347a-108">Automazione di Azure offre un motore di esecuzione del flusso di lavoro a elevata disponibilità e affidabilità che garantisce la scalabilità necessaria per rispondere alle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="e347a-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="e347a-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="e347a-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="e347a-110">Il servizio consente di ridurre i costi operativi e di liberare risorse dello staff IT e DevOp consentendo loro di concentrarsi su attività a valore aggiunto grazie al trasferimento delle attività di gestione del cloud all'esecuzione automatica di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e347a-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="e347a-111">In che modo Gestione API di Azure può essere gestito con Automazione di Azure?</span><span class="sxs-lookup"><span data-stu-id="e347a-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="e347a-112">Gestione API può essere gestito in Automazione di Azure tramite l' [API cmdlet di Windows PowerShell per Gestione API di Azure](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="e347a-112">API Management can be managed in Azure Automation by using the [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="e347a-113">All'interno di Automazione di Azure è possibile scrivere gli script dei flussi di lavoro di PowerShell per eseguire molte delle attività di Gestione API mediante i cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e347a-113">Within Azure Automation you can write PowerShell workflow scripts to perform many of your API Management tasks using the cmdlets.</span></span> <span data-ttu-id="e347a-114">È anche possibile abbinare tali cmdlet in Automazione di Azure ai cmdlet per altri servizi di Azure per automatizzare attività complesse in tutti i servizi di Azure e nei sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="e347a-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="e347a-115">Di seguito sono riportati alcuni esempi di utilizzo di Gestione API con Automazione:</span><span class="sxs-lookup"><span data-stu-id="e347a-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="e347a-116">Gestione API di Azure: utilizzo di PowerShell per il backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="e347a-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="e347a-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e347a-117">Next Steps</span></span>
<span data-ttu-id="e347a-118">A questo punto, dopo aver appreso le nozioni di base di Automazione di Azure e del modo in cui può essere usato per gestire Gestione API di Azure, usare i collegamenti seguenti per altre informazioni su Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e347a-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure API Management, follow these links to learn more.</span></span>

* <span data-ttu-id="e347a-119">Vedere l' [esercitazione iniziale](../automation/automation-first-runbook-graphical.md)di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e347a-119">See the Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

