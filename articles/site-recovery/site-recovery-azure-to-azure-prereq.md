---
title: aaaPrerequisites per la replica tooAzure tramite Azure Site Recovery | Documenti Microsoft
description: In questo articolo vengono riepilogati i prerequisiti per la replica delle macchine virtuali e i computer fisici tooAzure tramite il servizio di Azure Site Recovery hello.
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a>Prerequisiti per la replica delle macchine virtuali di Azure tooanother area tramite Azure Site Recovery

> [!div class="op_single_selector"]
> * [La replica da Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [La replica da locale tooAzure](site-recovery-prereq.md)

servizio Azure Site Recovery Hello favorisce la continuità aziendale tooyour e strategia di ripristino di emergenza gestendo:
* Replica delle macchine virtuali di Azure tooanother area di Azure.
* Replica delle sedi fisiche server e macchine virtuali tooAzure o tooa Data Center secondario. 

Quando si verificano interruzioni nella propria posizione primaria, è possibile eseguire il failover tooa posizione secondaria tookeep App e carichi di lavoro disponibili. È possibile eseguire il percorso primario tooyour indietro quando vengono restituite le operazioni di toonormal. Per altre informazioni su Site Recovery, vedere [Che cos'è Site Recovery?](site-recovery-overview.md).

In questo articolo riepiloga hello prerequisiti necessari toobegin la replica di ripristino del sito da tooAzure locale.

Inviare eventuali commenti nella parte inferiore di hello dell'articolo hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="azure-requirements"></a>Requisiti di Azure

**Requisito** | **Dettagli**
--- | ---
**Account di Azure** | Account [Microsoft Azure](http://azure.microsoft.com/) .<br/><br/> È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
**Servizio Site Recovery** | Per altre informazioni sui prezzi di Site Recovery, vedere [Prezzi di Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). È consigliabile creare un insieme di credenziali di servizi di ripristino nella destinazione hello regione di Azure che si desidera toouse come un percorso di ripristino di emergenza. Ad esempio, le macchine virtuali di origine sono in esecuzione negli Stati Uniti orientali, se si desidera tooreplicate tooCentral, è consigliabile creare archivi hello negli Stati Uniti centrali.|
**Capacità di Azure** | Per la destinazione di hello regione di Azure che si vuole toouse come la posizione di ripristino di emergenza, è necessario toohave una sottoscrizione con una capacità sufficiente per le macchine virtuali, gli account di archiviazione e i componenti di rete. È possibile contattare il supporto tooadd più capacità.
**Indicazioni per l'archiviazione** | Assicurarsi di seguire hello [informazioni aggiuntive sull'archiviazione](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) per l'origine virtuali di Azure macchine tooavoid eventuali problemi di prestazioni. Se si seguono le impostazioni predefinite di hello, Site Recovery crea gli account di archiviazione hello necessarie in base alla configurazione di origine hello. Se si personalizza e selezionare le proprie impostazioni, assicurarsi di seguire hello [obiettivi di scalabilità per i dischi di macchina virtuale](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Indicazioni per la rete** | È necessaria la connettività in uscita di hello toowhitelist dalla macchina virtuale di Azure per intervalli specifici URL o IP. Per ulteriori informazioni, vedere toohello [rete linee guida per la replica delle macchine virtuali di Azure](site-recovery-azure-to-azure-networking-guidance.md) articolo.
**Macchina virtuale di Azure** | Verificare che tutti i certificati radice più recenti hello siano presenti nel Windows hello o VM Linux. Se non sono presenti i certificati radice più recenti di hello, hello macchina virtuale non può essere registrato tooSite ripristino a causa di vincoli toosecurity.

>[!NOTE]
>Per altre informazioni sul supporto per configurazioni specifiche, leggere hello [matrice del supporto](site-recovery-support-matrix-azure-to-azure.md).

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni, vedere [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) (Indicazioni sulla rete per la replica di macchine virtuali di Azure).
- Iniziare a proteggere i carichi di lavoro [eseguendo la replica di macchine virtuali di Azure](site-recovery-azure-to-azure.md).
