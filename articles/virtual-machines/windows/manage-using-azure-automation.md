---
title: Gestire le macchine virtuali con Automazione di Azure | Microsoft Docs
description: "Informazioni su come è possibile usare il servizio Automazione di Azure per gestire le macchine virtuali di Azure su vasta scala."
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
ms.openlocfilehash: 15653c5d653ae538bdb66eaf0daee12c35858b45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="b8b25-103">Gestione delle Macchine virtuali di Azure mediante Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b8b25-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="b8b25-104">Questa guida fornisce un'introduzione al servizio Automazione di Azure e ne illustra l'utilizzo per semplificare la gestione delle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8b25-104">This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b8b25-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b8b25-105">What is Azure Automation?</span></span>
<span data-ttu-id="b8b25-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="b8b25-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b8b25-107">Usando Automazione di Azure, è possibile automatizzare attività a esecuzione prolungata, manuali, soggette a errori e ripetute frequentemente per migliorare l'affidabilità, l'efficienza e i tempi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b8b25-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="b8b25-108">Automazione di Azure offre un motore di esecuzione del flusso di lavoro a elevata disponibilità e affidabilità che garantisce la scalabilità necessaria per rispondere alle esigenze aziendali in base alla crescita dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b8b25-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="b8b25-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="b8b25-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b8b25-110">È possibile ridurre i costi operativi e di liberare risorse dello staff IT e DevOp consentendo loro di concentrarsi su attività a valore aggiunto grazie all'esecuzione automatica delle attività di gestione del cloud con Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8b25-110">You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="b8b25-111">Come può Automazione di Azure aiutare nella gestione delle macchine virtuali di Azure?</span><span class="sxs-lookup"><span data-stu-id="b8b25-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="b8b25-112">Le macchine virtuali possono essere gestite in Automazione di Azure tramite [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8b25-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="b8b25-113">Automazione di Azure include i cmdlet di Azure PowerShell per consentire l'esecuzione di tutte le attività di gestione delle macchine virtuali dall'interno del servizio.</span><span class="sxs-lookup"><span data-stu-id="b8b25-113">Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service.</span></span> <span data-ttu-id="b8b25-114">È anche possibile abbinare i cmdlet in Automazione di Azure ai cmdlet per altri servizi di Azure per automatizzare attività complesse in tutti i servizi di Azure e nei sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="b8b25-114">You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8b25-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8b25-115">Next steps</span></span>
<span data-ttu-id="b8b25-116">A questo punto, dopo aver appreso le nozioni di base di Automazione di Azure e del modo in cui può essere usato per gestire le macchine virtuali di Azure, usare i collegamenti seguenti per altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="b8b25-116">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="b8b25-117">Panoramica di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b8b25-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="b8b25-118">Il primo runbook</span><span class="sxs-lookup"><span data-stu-id="b8b25-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="b8b25-119">Mappa di apprendimento di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b8b25-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

