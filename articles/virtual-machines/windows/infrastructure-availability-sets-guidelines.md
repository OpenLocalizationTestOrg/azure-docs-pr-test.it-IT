---
title: aaaAvailability imposta per le macchine virtuali Windows in Azure | Documenti Microsoft
description: "Informazioni su hello progettazione e implementazione di linee guida fondamentali per la distribuzione di set di disponibilità in servizi di infrastruttura di Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f9449f58-664b-4d5d-82f6-84c5d083047f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cc35fd1e913434d9facb94116edb1b1c30447c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-windows-vms"></a>Linee guida per i set di disponibilità di Azure per macchine virtuali Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

In questo articolo è incentrata sulla comprensione hello necessario passaggi di pianificazione per la disponibilità delle applicazioni di tooensure imposta rimangono accessibili durante gli eventi pianificati o non pianificati.

## <a name="implementation-guidelines-for-availability-sets"></a>Linee guida di implementazione per i set di disponibilità
Decisioni:

* Il numero di set di disponibilità necessaria per hello diversi livelli e ruoli nell'infrastruttura di applicazioni?

Attività:

* Definire il numero di hello di macchine virtuali in ogni livello di applicazione, che è necessario.
* Determinare se è necessario numero hello tooadjust di toobe di domini di errore o di aggiornamento utilizzato per l'applicazione.
* Definire il set di disponibilità hello necessario utilizzando la convenzione di denominazione e le macchine virtuali in esse contenuti. Una macchina virtuale può risiedere soltanto in un set di disponibilità.

## <a name="availability-sets"></a>Set di disponibilità
In Azure, macchine virtuali (VM) può essere inserite raggruppamento logico di tooa chiamato set di disponibilità. Quando si creano le macchine virtuali all'interno di un set di disponibilità, hello piattaforma Azure distribuisce il posizionamento di hello di tali macchine virtuali tra hello infrastruttura sottostante. Deve esistere un toohello evento di manutenzione pianificata della piattaforma Azure o di un hardware sottostante o errore di infrastruttura, usare hello del set di disponibilità garantisce che almeno una macchina virtuale rimane in esecuzione.

La procedura consigliata prevede che le applicazioni non risiedano in una singola macchina virtuale. Un set di disponibilità che contiene una singola macchina virtuale non può ottenere alcuna protezione dagli eventi pianificati o all'interno di hello piattaforma Azure. Hello [SLA di Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines) richiede due o più macchine virtuali all'interno di una disponibilità set tooallow hello distribuzione di macchine virtuali tra hello infrastruttura sottostante. Se si utilizza [archiviazione Premium di Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello SLA di Azure si applica tooa singola macchina virtuale.

infrastruttura Hello in Azure è diviso in cluster hardware toomultiple. Ogni cluster hardware può supportare una gamma di dimensioni delle macchine virtuali. Un set di disponibilità può essere ospitato solo in un singolo cluster hardware in un determinato momento. Pertanto, hello intervallo di dimensioni delle macchine Virtuali che possono essere presenti in un unico set di disponibilità è limitato toohello intervallo di dimensioni delle macchine Virtuali dal cluster hardware hello è supportati. cluster hardware Hello per set di disponibilità hello è selezionato quando hello prima macchina virtuale nel set di disponibilità hello viene distribuito o avvio hello prima macchina virtuale in un set di disponibilità in cui tutte le macchine virtuali sono attualmente in stato di arresto-deallocazione hello. Hello comando PowerShell seguente può essere utilizzato toodetermine hello intervallo di dimensioni disponibili per un set di disponibilità: "Get-AzureRmVMSize - ResourceGroupName \<stringa\> - AvailabilitySetName \<stringa\> "

Ogni cluster hardware è suddivisa in domini di aggiornamento toomultiple e domini di errore. Tali domini sono definiti in base agli host che condividono un ciclo di aggiornamento comune o un'infrastruttura fisica simile, ad esempio quella di alimentazione e rete. Azure distribuisce automaticamente le macchine virtuali all'interno di un set tra domini toomaintain disponibilità e la tolleranza di disponibilità. A seconda delle dimensioni di hello dell'applicazione e il numero di hello di macchine virtuali all'interno di un set di disponibilità, è possibile modificare il numero di hello dei domini desiderato toouse. Altre informazioni su [gestione della disponibilità e uso dei domini di aggiornamento e di errore](manage-availability.md).

Quando si progetta l'infrastruttura dell'applicazione, pianificare i livelli di applicazione hello in uso. Macchine virtuali di gruppo che servono hello stesso scopo tooavailability set, ad esempio un set di disponibilità per le macchine virtuali front-end che esegue IIS. Creare un set di disponibilità distinto per le VM back-end che eseguono SQL Server. obiettivo di Hello è tooensure che ogni componente dell'applicazione è protetto da un set di disponibilità e almeno una volta istanza rimanga sempre in esecuzione.

Servizi di bilanciamento del carico possono essere utilizzate davanti a ogni toowork di livello applicazione insieme a un set di disponibilità e assicurarsi che il traffico può essere sempre indirizzato tooa esegue l'istanza. Senza un bilanciamento del carico, le macchine virtuali possono restare in esecuzione durante gli eventi pianificati e di manutenzione, ma l'utente finale potrebbe non essere in grado di tooresolve li se hello VM primaria non è disponibile.

Progettare l'applicazione per la disponibilità elevata a livello di archiviazione. procedura consigliata Hello è troppo[utilizzare dischi gestiti per le macchine virtuali in un Set di disponibilità](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Se i dischi non gestiti attualmente in uso, è consigliabile troppo[convertire le macchine virtuali nel Set di disponibilità di dischi gestiti di toouse](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]
