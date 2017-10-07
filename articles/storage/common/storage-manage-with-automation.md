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
ms.openlocfilehash: 5edfba1a9ce1f9c81b5bd0889de19099f3d86fc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a>Gestione di Archiviazione di Azure mediante Automazione di Azure
Questa Guida verrà presentate toohello servizio di automazione di Azure e come può essere utilizzato toosimplify gestione BLOB, tabelle e code di archiviazione di Azure.

## <a name="what-is-azure-automation"></a>Informazioni su Automazione di Azure
[Automazione di Azure](https://azure.microsoft.com/services/automation/) è un servizio di Azure che consente di semplificare la gestione del cloud tramite l'automazione dei processi. Utilizzando l'automazione di Azure, a esecuzione prolungata manuale, soggetta a errori e con una frequenza ripetuto attività possono essere automatizzati tooincrease affidabilità e l'efficienza e ridurre toovalue tempo per l'organizzazione.

Automazione di Azure fornisce un motore di esecuzione del flusso di lavoro altamente affidabile e a disponibilità elevata che viene ridimensionata toomeet le proprie esigenze, man mano che aumenta l'organizzazione. In Automazione di Azure i processi possono essere attivati manualmente, da sistemi di terze parti o a intervalli pianificati in modo che le attività abbiano luogo esattamente quando necessario.

Liberare e ridurre i costi operativi IT / DevOps personale toofocus lavoro che aggiunge il valore di business spostando il toobe di attività di gestione cloud eseguiti automaticamente da automazione di Azure.

## <a name="how-can-azure-automation-help-manage-azure-storage"></a>Come può Automazione di Azure aiutare nella gestione di Archiviazione di Azure?
Archiviazione di Azure può essere gestito in automazione di Azure tramite i cmdlet di PowerShell hello disponibili in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx). Automazione di Azure offre questi cmdlet PowerShell di archiviazione disponibili predefinito hello, in modo che sia possibile eseguire tutti i blob, tabella e l'attività di gestione di coda all'interno del servizio hello. È anche possibile coppia questi cmdlet in automazione di Azure con i cmdlet di hello per altri servizi di Azure, l'attività complesse tooautomate in servizi di Azure e sistemi di terze parti 3rd.

Hello [raccolta di runbook di automazione di Azure](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contiene un'ampia gamma di prodotti team e community runbook tooget avviato l'automazione della gestione di archiviazione di Azure, altri servizi di Azure e sistemi di terze parti 3rd. I Runbook della raccolta includono i seguenti:

* [Remove Azure Storage Blobs that are Certain Days Old Using Automation Service (Rimuovere i BLOB di archiviazione di Azure di un determinato numero di giorni usando il servizio di automazione)](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [Download a Blob from Azure Storage (Scaricare un BLOB da Archiviazione di Azure)](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [Backup all disks for a single Azure VM or for all VMs in a Cloud Service (Eseguire il backup di tutti i dischi per una singola macchina virtuale di Azure o per tutte le macchine virtuali in un servizio cloud)](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a>Passaggi successivi
Dopo aver appreso hello nozioni di base automazione di Azure e come può essere utilizzato toomanage BLOB di archiviazione di Azure, tabelle e code, seguire questi toolearn collegamenti ulteriori informazioni sull'automazione di Azure.

Vedere l'esercitazione di automazione di Azure hello [creazione o importazione di un runbook in automazione di Azure](../../automation/automation-creating-importing-runbook.md).

