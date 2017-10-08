---
title: linee guida per le macchine virtuali aaaAzure | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per la distribuzione di macchine virtuali di Windows in Azure
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f932e65a-437b-48b0-8d70-f61ded8ce1c6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: d2c8043cd5829b54a5d57e56533122e42021797d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-guidelines-for-windows"></a>Linee guida sulle macchine virtuali di Azure per Windows
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Questo articolo è incentrato su hello comprensione necessari passaggi per la creazione e gestione delle macchine virtuali (VM) per la pianificazione all'interno dell'ambiente Azure.

## <a name="implementation-guidelines-for-vms"></a>Linee guida per l'implementazione di macchine virtuali
Decisioni:

* Qual è il numero di macchine virtuali necessario per i vari componenti e livelli di applicazione dell'infrastruttura?
* Le risorse di CPU e memoria ogni macchina virtuale necessita, e quali sono i requisiti di archiviazione hello?

Attività:

* Definire i carichi di lavoro di hello per le hello risorse hello e di applicazione di che richiedono macchine virtuali.
* Allinea hello richieste di risorse per ogni macchina virtuale con hello VM archiviazione e dimensioni del tipo appropriato.
* Definire i gruppi di risorse per i livelli diversi di hello e i componenti dell'infrastruttura.
* Definire la convenzione di denominazione della macchina virtuale.
* Creare le macchine virtuali utilizzando hello Azure PowerShell, web del portale, o con modelli di gestione risorse.

## <a name="virtual-machines"></a>Macchine virtuali
Una delle risorse principali di hello all'interno dell'ambiente Azure è probabilmente macchine virtuali. In questa risorsa vengono infatti eseguiti database, applicazioni, servizi di autenticazione e così via.

È importante toounderstand hello [diverse dimensioni VM](sizes.md) toocorrectly dimensioni dell'ambiente da una prospettiva di prestazioni e costi. Se le macchine virtuali non hanno una quantità sufficiente di core CPU o di memoria, le prestazioni dell'applicazione ne risentono indipendentemente da come la stessa è stata progettata e sviluppata. Hello revisione suggerito carichi di lavoro per ogni serie di macchina virtuale come punto di partenza per stabilire quali toouse VM di dimensioni per ogni componente dell'infrastruttura. È possibile [modificare hello dimensioni di una macchina virtuale](resize-vm.md) dopo la distribuzione.

L'archiviazione svolge un ruolo fondamentale nelle prestazioni della macchina virtuale. È possibile usare l'archiviazione Standard che usa dischi in rotazione normali oppure l'archiviazione Premium per carichi di lavoro I/O elevati e prestazioni massime che usano dischi SSD. Come con hello dimensioni delle macchine Virtuali, vi sono costi supporto di archiviazione hello tooselecting considerazioni. È possibile leggere hello [articolo linee guida di archiviazione infrastruttura](infrastructure-storage-solutions-guidelines.md) toounderstand come toodesign appropriata l'archiviazione per ottimizzare le prestazioni delle macchine virtuali.

## <a name="resource-groups"></a>Gruppi di risorse
Componenti come le VM vengono raggruppati logicamente per facilitare la gestione e la manutenzione usando i [gruppi di risorse di Azure](../../azure-resource-manager/resource-group-overview.md). Tramite i gruppi di risorse, è possibile creare, gestire e monitorare tutte le risorse di hello che costituiscono una determinata applicazione. È anche possibile implementare [i controlli di accesso basato sui ruoli](../../active-directory/role-based-access-control-what-is.md) toogrant accesso tooothers all'interno delle risorse di hello tooonly team richiedono. Richiedere tooplan ora i gruppi di risorse e le assegnazioni di ruolo. Esistono diversi approcci tooactually progettazione e implementare i gruppi di risorse, è necessario che tooread hello [articolo linee guida per i gruppi di risorse](infrastructure-resource-groups-guidelines.md) toounderstand toobuild ottimale out le macchine virtuali.

## <a name="templates"></a>Modelli
È possibile compilare modelli, definito dal file JSON dichiarativi, toocreate le macchine virtuali. Modelli di compilazione in genere anche hello necessario archiviazione, rete, le interfacce di rete, gli indirizzi IP, e così via, insieme a macchine virtuali di hello. Utilizzare gli ambienti coerente e riproducibile toocreate di modelli per lo sviluppo e test tooeasily scopi replicare gli ambienti di produzione e viceversa. Ulteriori informazioni su [la creazione e utilizzo dei modelli](../../azure-resource-manager/resource-group-overview.md#template-deployment) toounderstand come è possibile utilizzare per creare e distribuire le macchine virtuali.

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

