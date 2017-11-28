---
title: aaaManage archiviazione di Azure utilizzando l'automazione di Azure
description: "Informazioni su come hello servizio automazione di Azure può essere utilizzato toomanage di archiviazione di Azure su larga scala."
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
ms.openlocfilehash: 15e34128ffb0ba3315b5260442f628b5978c5197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="39049-103">Gestione di Archiviazione di Azure mediante Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="39049-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="39049-104">Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione BLOB, tabelle e code di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="39049-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="39049-105">Informazioni su Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="39049-105">What is Azure Automation?</span></span>
<span data-ttu-id="39049-106">[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="39049-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="39049-107">Utilizzando l'automazione di Azure, a esecuzione prolungata manuale, soggetta a errori e con una frequenza ripetuto attività possono essere automatizzati tooincrease affidabilità e l'efficienza e ridurre toovalue tempo per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="39049-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="39049-108">Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze, man mano che aumenta l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="39049-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="39049-109">In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.</span><span class="sxs-lookup"><span data-stu-id="39049-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="39049-110">Liberare e ridurre i costi operativi IT / DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="39049-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="39049-111">Come può Automazione di Azure aiutare nella gestione di Archiviazione di Azure?</span><span class="sxs-lookup"><span data-stu-id="39049-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="39049-112">Archiviazione di Azure può essere gestito in automazione di Azure tramite i cmdlet di PowerShell hello disponibili in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="39049-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="39049-113">Automazione di Azure offre questi cmdlet PowerShell di archiviazione disponibili predefinito hello, in modo che sia possibile eseguire tutti i blob, tabella e l'attività di gestione di coda all'interno del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="39049-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="39049-114">È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="39049-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="39049-115">Hello [raccolta di runbook di automazione di Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene un'ampia gamma di prodotti team e community runbook tooget avviato l'automazione della gestione di archiviazione di Azure, altri servizi di Azure e sistemi di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="39049-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="39049-116">I Runbook della raccolta includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="39049-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="39049-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service (Rimuovere i BLOB di archiviazione di Azure di un determinato numero di giorni usando il servizio di automazione)</span><span class="sxs-lookup"><span data-stu-id="39049-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="39049-118">Download a Blob from Azure Storage (Scaricare un BLOB da Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="39049-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="39049-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service (Eseguire il backup di tutti i dischi per una singola macchina virtuale di Azure o per tutte le macchine virtuali in un servizio cloud)</span><span class="sxs-lookup"><span data-stu-id="39049-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="39049-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39049-120">Next Steps</span></span>
<span data-ttu-id="39049-121">Dopo aver appreso hello nozioni di base automazione di Azure e come può essere utilizzato toomanage BLOB di archiviazione di Azure, tabelle e code, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="39049-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="39049-122">Vedere l'esercitazione di automazione di Azure hello [creazione o importazione di un runbook in automazione di Azure](../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="39049-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

