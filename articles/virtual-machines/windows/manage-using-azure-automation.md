---
title: macchine virtuali utilizzando l'automazione di Azure aaaManage | Documenti Microsoft
description: "Scopri come hello servizio automazione di Azure può essere utilizzato toomanage macchine virtuali di Azure su larga scala."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="af805-103">Gestione delle Macchine virtuali di Azure mediante Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="af805-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="af805-104">Questa guida verranno presentate le toohello servizio di automazione di Azure e come può essere usato toosimplify la gestione delle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="af805-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="af805-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="af805-105">What is Azure Automation?</span></span>
<span data-ttu-id="af805-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="af805-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="af805-107">Tramite l'automazione di Azure, le attività a esecuzione prolungata, manuale, soggetta a errori e ripetute spesso possono essere ora-valore per l'organizzazione, efficienza e affidabilità tooincrease automatizzati.</span><span class="sxs-lookup"><span data-stu-id="af805-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="af805-108">Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze, man mano che aumenta l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="af805-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="af805-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="af805-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="af805-110">È possibile ridurre i costi operativi e liberare IT e DevOps personale toofocus lavoro che aggiunge il valore di business eseguendo cloud di attività di gestione automaticamente con l'automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="af805-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="af805-111">Come può Automazione di Azure aiutare nella gestione delle macchine virtuali di Azure?</span><span class="sxs-lookup"><span data-stu-id="af805-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="af805-112">Le macchine virtuali possono essere gestite in Automazione di Azure tramite [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="af805-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="af805-113">Automazione di Azure include cmdlet di Azure PowerShell hello, pertanto non è possibile eseguire tutte le attività di gestione macchina virtuale all'interno del servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="af805-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="af805-114">È anche possibile coppia cmdlet hello in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e nei sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="af805-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af805-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af805-115">Next steps</span></span>
<span data-ttu-id="af805-116">Ora che si è appreso i concetti di base hello di automazione di Azure e come può essere utilizzato toomanage macchine virtuali di Azure, altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="af805-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="af805-117">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="af805-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="af805-118">Il primo runbook</span><span class="sxs-lookup"><span data-stu-id="af805-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="af805-119">Mappa di apprendimento di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="af805-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

