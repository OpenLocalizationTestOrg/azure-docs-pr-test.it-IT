---
title: Gestire app Web di Azure usando Automazione di Azure | Documentazione Microsoft
description: "Informazioni su come è possibile usare il servizio Automazione di Azure per gestire App Web di Azure."
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
ms.openlocfilehash: a96332346747114620ee6ebd2a2d0c4417d4a213
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="c70ef-103">Gestire App Web di Azure usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c70ef-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="c70ef-104">Questa guida fornisce un'introduzione al servizio Automazione di Azure e ne illustra l'uso per semplificare la gestione di App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c70ef-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="c70ef-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c70ef-105">What is Azure Automation?</span></span>
<span data-ttu-id="c70ef-106">[Automazione di Azure](../automation/automation-intro.md) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="c70ef-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="c70ef-107">Usando Automazione di Azure, è possibile automatizzare attività manuali, ripetute, a esecuzione prolungata e soggette a errori per migliorare l'affidabilità, l'efficienza e i tempi di esecuzione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c70ef-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="c70ef-108">Automazione di Azure offre un motore di esecuzione del flusso di lavoro a elevata disponibilità e affidabilità che garantisce la scalabilità necessaria per rispondere alle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="c70ef-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="c70ef-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="c70ef-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="c70ef-110">Il servizio consente di ridurre i costi operativi e di liberare risorse dello staff IT e DevOp consentendo loro di concentrarsi su attività a valore aggiunto grazie al trasferimento delle attività di gestione del cloud all'esecuzione automatica di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c70ef-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="c70ef-111">In che modo Automazione di Azure può rappresentare un aiuto nella gestione di App Web di Azure?</span><span class="sxs-lookup"><span data-stu-id="c70ef-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="c70ef-112">È possibile gestire le app Web in Automazione di Azure usando i cmdlet di PowerShell disponibili nei [moduli di Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="c70ef-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="c70ef-113">È possibile [installare questi cmdlet di PowerShell per app Web in Automazione di Azure](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/)per eseguire tutte le attività di gestione delle app Web dall'interno del servizio.</span><span class="sxs-lookup"><span data-stu-id="c70ef-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span></span> <span data-ttu-id="c70ef-114">È anche possibile abbinare tali cmdlet in Automazione di Azure ai cmdlet per altri servizi di Azure per automatizzare attività complesse in tutti i servizi di Azure e nei sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="c70ef-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="c70ef-115">Di seguito sono riportati alcuni esempi di gestione dei servizi app con Automazione:</span><span class="sxs-lookup"><span data-stu-id="c70ef-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="c70ef-116">Script per la gestione di app Web</span><span class="sxs-lookup"><span data-stu-id="c70ef-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="c70ef-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c70ef-117">Next steps</span></span>
<span data-ttu-id="c70ef-118">A questo punto, dopo aver appreso le nozioni di base di Automazione di Azure e come può essere usato per gestire App Web di Azure, consultare i seguenti collegamenti per altre informazioni su Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c70ef-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="c70ef-119">Vedere l' [esercitazione introduttiva](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="c70ef-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

