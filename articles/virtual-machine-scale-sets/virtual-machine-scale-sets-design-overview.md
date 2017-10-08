---
title: "Considerazioni per il set di scalabilità macchina virtuale di Azure aaaDesign | Documenti Microsoft"
description: "Considerazioni sulla progettazione per i set di scalabilità di macchine virtuali di Azure"
keywords: "macchina virtuale linux,set di scalabilità macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>Considerazioni sulla progettazione per i set di scalabilità
Questo argomento descrive una serie di considerazioni di progettazione per i set di scalabilità di macchine virtuali. Per informazioni sui set di scalabilità di macchine virtuali, vedere troppo[Panoramica set di scalabilità della macchina virtuale](virtual-machine-scale-sets-overview.md).

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>Quando la scala toouse imposta anziché le macchine virtuali?
I set di scalabilità sono in genere utili per distribuire un'infrastruttura a disponibilità elevata che include un set di computer con una configurazione simile. Tuttavia, alcune funzionalità sono disponibili soltanto nei set di scalabilità, mentre altre sono disponibili solo nelle macchine virtuali. Ordinare toomake una decisione consapevole su quando toouse ogni tecnologia, occorre prima verranno descritte alcune delle funzionalità di hello comunemente utilizzato che sono disponibili in set di scalabilità ma non le macchine virtuali:

### <a name="scale-set-specific-features"></a>Funzionalità specifiche dei set di scalabilità

- Dopo aver specificato una configurazione di set di scalabilità hello, è possibile limitarsi ad aggiornare hello "capacità" proprietà toodeploy più macchine virtuali in parallelo. Questo è molto più semplice rispetto alla scrittura di un tooorchestrate script distribuzione molti singole macchine virtuali in parallelo.
- È possibile [tooautomatically di scalabilità automatica di Azure usare ridimensionare un set di scalabilità](./virtual-machine-scale-sets-autoscale-overview.md) ma non per le singole macchine virtuali.
- È possibile [ricreare l'immagine delle macchine virtuali del set di scalabilità](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm) ma [non delle singole macchine virtuali](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- È possibile [eseguire il provisioning eccessivo](./virtual-machine-scale-sets-design-overview.md) delle macchine virtuali del set di scalabilità per una maggiore affidabilità e tempi di distribuzione più rapidi. Non è possibile farlo con singole macchine virtuali, a meno che non si scrive codice personalizzato toodo questo.
- È possibile specificare un [l'aggiornamento di criteri](./virtual-machine-scale-sets-upgrade-scale-set.md) toomake è facile tooroll di aggiornamenti tra le macchine virtuali nel set di scalabilità. Con le singole macchine virtuali, è necessario orchestrare gli aggiornamenti manualmente.

### <a name="vm-specific-features"></a>Funzionalità specifiche delle macchine virtuali

In hello invece, alcune funzionalità sono disponibili solo in macchine virtuali (almeno per hello momento):

- È possibile collegare dati dischi toospecific singole macchine virtuali, ma i dischi dati collegati sono configurati per tutte le macchine virtuali in un set di scalabilità.
- È possibile collegare i dischi di dati non vuoto tooindividual macchine virtuali ma non le macchine virtuali in un set di scalabilità.
- È possibile acquisire uno snapshot di una singola macchina virtuale, ma non di una macchina virtuale in un set di scalabilità.
- È possibile acquisire un'immagine da una singola macchina virtuale, ma non da una macchina virtuale in un set di scalabilità.
- È possibile eseguire la migrazione di una macchina virtuale di singoli dai dischi toomanaged dischi nativi, ma non per le macchine virtuali in un set di scalabilità.
- È possibile assegnare gli indirizzi IP pubblici IPv6 NIC VM tooindividual ma non è possibile farlo per le macchine virtuali in un set di scalabilità. Si noti che è possibile assegnare gli indirizzi IP pubblici IPv6 bilanciamento del carico tooload davanti entrambe singole macchine virtuali o set di scalabilità di macchine virtuali.

## <a name="storage"></a>Archiviazione

### <a name="scale-sets-with-azure-managed-disks"></a>Set di scalabilità con Azure Managed Disks
Invece che con i tradizionali account di archiviazione di Azure, i set di scalabilità possono essere creati con [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md). I dischi gestiti forniscono hello seguenti vantaggi:
- Non è toopre-creare un set di account di archiviazione di Azure per le macchine virtuali del set di scalabilità di hello.
- È possibile definire [i dischi dati collegati](virtual-machine-scale-sets-attached-disks.md) impostato per la scala Ciao macchine virtuali.
- Set di scalabilità può essere configurato troppo[supportano backup too1, 000 macchine virtuali in un set di](virtual-machine-scale-sets-placement-groups.md). 

Se si dispone di un modello esistente, è anche possibile [aggiornare hello modello toouse dischi gestiti](virtual-machine-scale-sets-convert-template-to-md.md).

### <a name="user-managed-storage"></a>Archiviazione gestita dall'utente
Un set di scalabilità non è definito con dischi gestiti di Azure si basa sui dischi del sistema operativo hello delle toostore di account di archiviazione creati dall'utente di hello macchine virtuali nel set di hello. È consigliabile un rapporto di 20 macchine virtuali per ogni account di archiviazione o meno i/o massimo tooachieve nonché sfruttare _overprovisioning_ (vedere sotto). È inoltre consigliabile che la distribuzione caratteri inizio hello di nomi di account di archiviazione hello tra alfabeto hello. Questo consente di suddividere il carico tra diversi sistemi interni. 


## <a name="overprovisioning"></a>Provisioning eccessivo
Attualmente scala imposta predefinito troppo "overprovisioning" le macchine virtuali. Con provisioning eccessivo attivata, scala hello effettivamente rotazioni di più macchine virtuali che è richiesto per imposta, quindi Elimina hello ulteriori macchine virtuali, una volta hello richiesto numero di macchine virtuali sono correttamente il provisioning. Il provisioning eccessivo migliora le percentuali di riuscita del provisioning e riduce i tempi di distribuzione. La fatturazione per hello ulteriori macchine virtuali e non vengono conteggiati per i limiti di quota.

L'overprovisioning migliorare provisioning percentuali di successo, può causare confusione per un'applicazione che viene progettato non toohandle ulteriori macchine virtuali visualizzato e quindi scomparire. tooturn overprovisioning off, verificare di aver hello successivi nel modello di stringa: `"overprovision": "false"`. Ulteriori informazioni, vedere hello [documentazione dell'API REST di impostare la scala](/rest/api/virtualmachinescalesets/create-or-update-a-set).

Se il set di scalabilità utilizza l'archiviazione gestita dall'utente, e si disattiva overprovisioning, è possibile avere più di 20 macchine virtuali per ogni account di archiviazione, ma non è consigliabile toogo sopra 40 per motivi di prestazioni dei / o. 

## <a name="limits"></a>Limiti
Un set di scalabilità basata su un'immagine del Marketplace (noto anche come un'immagine della piattaforma) e configurato toouse che dischi gestiti di Azure supporta una capacità di backup too1, 000 macchine virtuali. Se si configurano il toosupport di set di scalabilità di macchine virtuali di più di 100, non tutte le operazioni scenari hello stesso (ad esempio il bilanciamento del carico). Per altre informazioni, vedere [Uso di set di scalabilità di macchine virtuali di grandi dimensioni](virtual-machine-scale-sets-placement-groups.md). 

Una scala imposta configurata con account di archiviazione gestita dall'utente è attualmente limitata too100 VM e 5 account di archiviazione sono consigliate per la scala.

Un set di scalabilità basato su un'immagine personalizzata (uno creato dall'utente) può avere una capacità di backup di macchine virtuali too100 quando configurate con dischi gestito di Azure. Se il set di scalabilità di hello è configurato con account di archiviazione gestita dall'utente, è necessario creare tutti i file VHD di dischi del sistema operativo all'interno di un account di archiviazione. Di conseguenza, massimo hello numero consigliato di macchine virtuali in un set di scalabilità basato su un'immagine personalizzata e l'archiviazione gestita dall'utente è 20. Se si disattiva overprovisioning, è possibile passare i too40.

Per altre macchine virtuali superiore a quello consentono questi limiti, è necessario toodeploy scala più imposta come illustrato nella [questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale).

