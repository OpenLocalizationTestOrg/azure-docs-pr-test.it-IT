---
title: iniziare la replica delle macchine virtuali di Azure tooanother area aaaBefore | Microsoft documenti
description: "Vengono riepilogati i passaggi di hello tootake è necessario prima di replicare macchine virtuali di Azure tra le aree di Azure, tramite il servizio di Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a>Passaggio 2: Prima di iniziare

Dopo aver esaminato hello [architettura](azure-to-azure-walkthrough-architecture.md) per la replica delle macchine virtuali di Azure (VM) tra le aree di Azure con [Azure Site Recovery](site-recovery-overview.md), utilizzare i prerequisiti di tooverify questo articolo. 

- Dopo aver articolo hello, è necessario un oggetto, deselezionare la comprensione di cosa è necessario distribuzione hello toomake di lavoro e aver completato i passaggi precedenti richiesti hello.
- Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>
> La replica di macchine virtuali di Azure è attualmente in anteprima.



## <a name="support-recommendations"></a>Consigli per il supporto

Revisione hello nella tabella riportata di seguito.

**Componente** | **Requisito**
--- | ---
**Insieme di credenziali dei servizi di ripristino** | È consigliabile creare un insieme di credenziali di servizi di ripristino nella destinazione hello regione di Azure che si vuole toouse per il ripristino di emergenza. Se si desidera tooreplicate origine, le macchine virtuali in Stati Uniti orientali tooCentral Stati Uniti, ad esempio, creare credenziali hello negli Stati Uniti centrali.
**Sottoscrizione di Azure** | La sottoscrizione di Azure deve essere abilitato toocreate di macchine virtuali, nel percorso di destinazione hello che si desidera toouse come area di ripristino di emergenza hello. Contattare il supporto tecnico tooenable hello quota obbligatorio.
**Capacità dell'area di destinazione** | Sottoscrizione hello destinazione hello regione di Azure, deve avere una capacità sufficiente per le macchine virtuali, gli account di archiviazione e i componenti di rete.
**Archiviazione** | Hello utilizzare [informazioni aggiuntive sull'archiviazione](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) per le macchine virtuali di Azure, i problemi di prestazioni tooavoid di origine.<br/><br/> Gli account di archiviazione devono essere in hello stessa area dell'insieme di credenziali di hello.<br/><br/> Non è possibile replicare gli account toopremium centrale e meridionale.<br/><br/> Se si distribuisce la replica con le impostazioni predefinite di hello, Site Recovery crea gli account di archiviazione hello necessarie in base alla configurazione di origine hello. Se si personalizza le impostazioni, seguire hello [obiettivi di scalabilità per i dischi di macchina virtuale](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Rete** | Tooallow connettività in uscita da macchine virtuali di Azure, è necessario per determinati intervalli di URL/IP.<br/><br/> Gli account di rete devono essere in hello stessa area dell'insieme di credenziali di hello. 
**Macchina virtuale di Azure** | Assicurarsi che tutti i certificati radice più recenti di hello presenti hello macchina virtuale di Azure di Windows/Linux. Se non lo sono, non sarà in grado di tooregister hello VM in Site Recovery, a causa di vincoli di sicurezza.
**Account utente Azure** | L'account utente di Azure deve toohave determinati [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica della macchina virtuale di Azure.

Ottenere un elenco completo dei requisiti di supporto in hello [matrice del supporto](site-recovery-support-matrix-azure-to-azure.md)


## <a name="set-permissions-on-hello-account"></a>Impostare autorizzazioni per l'account di hello

1. Conoscenza hello [autorizzazioni](site-recovery-role-based-linked-access-control.md) è necessario per la replica.
2. Attenersi alla seguente [istruzioni](../active-directory/role-based-access-control-configure.md#add-access) tooadd autorizzazioni.


## <a name="verify-target-resources"></a>Verificare le risorse di destinazione

1. Attivare la sottoscrizione di Azure di tooallow si toocreate macchine virtuali in hello area toouse per il ripristino di emergenza che si desidera toouse come area di ripristino di emergenza hello di destinazione. Contattare il supporto tecnico tooenable hello quota obbligatorio.
2. Verificare che la sottoscrizione sia sufficiente tooenable risorse macchine virtuali con le dimensioni che corrispondono all'origine di macchine virtuali. Per impostazione predefinita, quando configurare la replica, il ripristino del sito prelievi hello hello stesse dimensioni macchina virtuale di destinazione o hello dimensioni possibili più vicina. Ulteriori informazioni sulla [risoluzione dei problemi](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) relativi alle risorse di destinazione.

## <a name="verify-azure-vm-certificates"></a>Verificare i certificati della macchina virtuale di Azure

1. Verificare che tutti i certificati radice più recenti hello sono presenti in Windows hello o le macchine virtuali Linux desiderato tooreplicate. Se non sono presenti i certificati radice più recenti di hello, hello macchina virtuale non può essere registrato tooSite ripristino a causa di vincoli toosecurity.
2. Per macchine virtuali di Windows hello seguenti:

    - Installare gli aggiornamenti di Windows più recenti di hello in hello macchina virtuale in modo che tutti i certificati radice attendibile hello sono computer hello.
    - In un ambiente disconnesso, seguire hello processo standard di Windows Update processo/certificato aggiornamento nell'organizzazione, i certificati radice più recenti di tooget hello e CRL aggiornato, nelle macchine virtuali hello.
3. Per le macchine virtuali Linux, attenersi alla Guida hello fornita dal hello più recente elenco certificati revocati in hello VM Linux distributore tooget hello più recenti certificati radice attendibili. Ulteriori informazioni sulla [risoluzione dei problemi](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) relativi alle radici attendibili.


## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 3: pianificare la rete](azure-to-azure-walkthrough-network.md) tooset della connettività in uscita.
