---
title: Gestire Archiviazione di Azure usando Automazione di Azure
description: "Informazioni su come è possibile usare il servizio Automazione di Azure per gestire l'Archiviazione di Azure su vasta scala."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 4649e42a628307e15f8b067503e4e8e13f16f1af
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="af501-103">Gestione di Archiviazione di Azure mediante Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="af501-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="af501-104">Questa guida fornisce un'introduzione al servizio Automazione di Azure e ne illustra l'utilizzo per semplificare la gestione di BLOB, tabelle e code di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="af501-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="af501-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="af501-105">What is Azure Automation?</span></span>
<span data-ttu-id="af501-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="af501-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="af501-107">Usando Automazione di Azure, è possibile automatizzare attività a esecuzione prolungata, manuali, soggette a errori e ripetute frequentemente per migliorare l'affidabilità e l'efficienza e ridurre i tempi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="af501-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span></span>

<span data-ttu-id="af501-108">Automazione di Azure offre un motore di esecuzione del flusso di lavoro a elevata disponibilità e affidabilità che garantisce la scalabilità necessaria per rispondere alle esigenze aziendali in base alla crescita dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="af501-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="af501-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="af501-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="af501-110">Il servizio permette di ridurre i costi operativi e di liberare risorse dello staff IT/DevOp consentendo loro di concentrarsi su attività a valore aggiunto grazie al trasferimento delle attività di gestione del cloud all'esecuzione automatica di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="af501-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="af501-111">Come può Automazione di Azure aiutare nella gestione di Archiviazione di Azure?</span><span class="sxs-lookup"><span data-stu-id="af501-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="af501-112">Archiviazione di Azure può essere gestito in Automazione di Azure usando i cmdlet di PowerShell disponibili in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="af501-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="af501-113">I cmdlet di PowerShell per l'Archiviazione sono predefiniti in Automazione di Azure, per consentire l'esecuzione di tutte le attività di gestione di BLOB, tabelle e code dall'interno del servizio.</span><span class="sxs-lookup"><span data-stu-id="af501-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span></span> <span data-ttu-id="af501-114">È anche possibile abbinare tali cmdlet in Automazione di Azure ai cmdlet per altri servizi di Azure per automatizzare attività complesse in tutti i servizi di Azure e nei sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="af501-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="af501-115">La [raccolta di Runbook di Automazione di Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene diversi Runbook del team di prodotto e della community per iniziare ad automatizzare la gestione di Archiviazione di Azure, altri servizi di Azure e sistemi di terze parti.</span><span class="sxs-lookup"><span data-stu-id="af501-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="af501-116">I Runbook della raccolta includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="af501-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="af501-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service (Rimuovere i BLOB di archiviazione di Azure di un determinato numero di giorni usando il servizio di automazione)</span><span class="sxs-lookup"><span data-stu-id="af501-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="af501-118">Download a Blob from Azure Storage (Scaricare un BLOB da Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="af501-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="af501-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service (Eseguire il backup di tutti i dischi per una singola macchina virtuale di Azure o per tutte le macchine virtuali in un servizio cloud)</span><span class="sxs-lookup"><span data-stu-id="af501-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="af501-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af501-120">Next Steps</span></span>
<span data-ttu-id="af501-121">A questo punto, dopo aver appreso le nozioni di base di Automazione di Azure e come può essere usato per gestire BLOB, tabelle e code di Azure, seguire i collegamenti seguenti per altre informazioni su Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="af501-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span></span>

<span data-ttu-id="af501-122">Vedere l'esercitazione di Automazione di Azure [Creazione e importazione di un runbook in Automazione di Azure](../../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="af501-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

