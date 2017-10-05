---
title: Gestire Azure RemoteApp usando Automazione di Azure | Documentazione Microsoft
description: "Informazioni su come è possibile usare il servizio Automazione di Azure per gestire Azure RemoteApp."
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
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="196ae-103">Gestione di Azure RemoteApp usando Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="196ae-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="196ae-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="196ae-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="196ae-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="196ae-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="196ae-106">Questa guida fornisce un'introduzione al servizio Automazione di Azure e ne illustra l'utilizzo per semplificare la gestione di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="196ae-106">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="196ae-107">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="196ae-107">What is Azure Automation?</span></span>
<span data-ttu-id="196ae-108">[Automazione di Azure](../automation/automation-intro.md) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="196ae-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="196ae-109">Usando Automazione di Azure, è possibile automatizzare attività manuali, ripetute frequentemente, a esecuzione prolungata e soggette a errori per migliorare l'affidabilità, l'efficienza e i tempi di esecuzione dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="196ae-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="196ae-110">Automazione di Azure offre un motore di esecuzione del flusso di lavoro a elevata disponibilità e affidabilità che garantisce la scalabilità necessaria per rispondere alle esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="196ae-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="196ae-111">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="196ae-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="196ae-112">Il servizio consente di ridurre i costi operativi e di liberare risorse dello staff IT e DevOp consentendo loro di concentrarsi su attività a valore aggiunto grazie al trasferimento delle attività di gestione del cloud all'esecuzione automatica di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="196ae-112">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="196ae-113">Come può Automazione di Azure aiutare nella gestione di Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="196ae-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="196ae-114">RemoteApp può essere gestito in Automazione di Azure usando i cmdlet di PowerShell disponibili negli [strumenti di Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="196ae-114">RemoteApp can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="196ae-115">I cmdlet di PowerShell per RemoteApp sono predefiniti in Automazione di Azure per consentire l'esecuzione di tutte le attività di gestione di RemoteApp dall'interno del servizio.</span><span class="sxs-lookup"><span data-stu-id="196ae-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of the box, so that you can perform all of your RemoteApp management tasks within the service.</span></span> <span data-ttu-id="196ae-116">È anche possibile abbinare tali cmdlet in Automazione di Azure ai cmdlet per altri servizi di Azure per automatizzare attività complesse in tutti i servizi di Azure e nei sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="196ae-116">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="196ae-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="196ae-117">Next steps</span></span>
<span data-ttu-id="196ae-118">A questo punto, dopo aver appreso le nozioni di base di Automazione di Azure e come può essere usato per gestire Azure RemoteApp, seguire i collegamenti seguenti per altre informazioni su Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="196ae-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure RemoteApp, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="196ae-119">Vedere l' [esercitazione introduttiva](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="196ae-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

