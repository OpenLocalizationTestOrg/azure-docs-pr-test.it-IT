---
title: aaaSet backup hello origine e di destinazione per tooAzure di replica Hyper-V (senza System Center VMM) con Azure Site Recovery | Documenti Microsoft
description: Riepiloga hello passaggi tooset le impostazioni di origine e di destinazione per la replica di archiviazione di macchine virtuali Hyper-V tooAzure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a>Passaggio 8: Impostare hello origine e di destinazione per Hyper-V replica tooAzure

In questo articolo viene descritto come le impostazioni di tooconfigure origine e di destinazione durante la replica locale tooAzure macchine virtuali (senza System Center VMM) di Hyper-V, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

Impostare il sito di hello Hyper-V, installare hello Provider di Azure Site Recovery e l'agente di servizi di ripristino di Azure di hello negli host Hyper-V e registrare sito hello nell'insieme di credenziali hello.

1. In **Preparare l'infrastruttura** fare clic su **Origine**. Fare clic su un nuovo sito Hyper-V come contenitore per l'host Hyper-V o cluster, tooadd **+ sito Hyper-V**.

    ![Impostare l'origine](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. In **sito Hyper-V creare**, specificare un nome per il sito hello. Fare quindi clic su **OK**. Ora, selezionare il sito di hello creata, quindi fare clic su **+ Server Hyper-V** tooadd un sito di toohello server.

    ![Impostare l'origine](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. In **Aggiungi server** > **Tipo di server** verificare che sia visualizzato **Server Hyper-V**.

    - Verificare che tale server hello Hyper-V da tooadd è conforme con hello [prerequisiti](#on-premises-prerequisites), ed è in grado di tooaccess hello URL specificati.
    - Scaricare i file di installazione di Provider di Azure Site Recovery hello. Eseguire questo hello tooinstall file Provider e hello agente servizi di ripristino in ogni host Hyper-V.

    ![Impostare l'origine](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Installare hello Provider e agente

1. Eseguire i file di installazione di Provider di hello in ogni host aggiunti al sito toohello Hyper-V. Se l'installazione viene eseguita in un cluster Hyper-V, eseguire il file di installazione in ogni nodo del cluster. L'installazione e la registrazione di ogni nodo del cluster Hyper-V garantisce che le macchine virtuali siano protette anche se ne viene eseguita la migrazione tra i nodi.
2. In **Microsoft Update** è possibile acconsentire esplicitamente agli aggiornamenti in modo che gli aggiornamenti del provider vengano installati in base ai criteri di Microsoft Update.
3. In **installazione**, accettare o modificare percorso di installazione di Provider predefinito hello e fare clic su **installare**.
4. In **impostazioni insieme di credenziali**, fare clic su **Sfoglia** tooselect hello insieme di credenziali chiave file scaricato. Specificare una sottoscrizione di Azure Site Recovery hello, nome di archivio, hello e hello Hyper-V del sito toowhich hello Hyper-V server appartiene.

    ![Server registration](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. In **le impostazioni del Proxy**, specificare la modalità Provider in esecuzione in host Hyper-V si connette tooAzure Site Recovery tramite hello hello internet.

    * Se si desidera selezionare direttamente hello Provider tooconnect **connettersi direttamente tooAzure il ripristino del sito senza un proxy**.
    * Se il proxy esistente richiede l'autenticazione, o si desidera toouse un proxy personalizzato per la connessione al Provider di hello, selezionare **connettersi tooAzure ripristino del sito utilizzando un server proxy**.
    * Se si usa un proxy:
        - Specificare le credenziali, porta e indirizzo hello
        - Rendono che URL hello descritto in hello [prerequisiti](#prerequisites) siano consentiti attraverso il proxy di hello.

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. Al termine dell'installazione, fare clic su **registrare** server hello tooregister nell'insieme di credenziali hello.

    ![Percorso di installazione](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. Al termine della registrazione, i metadati dal server hello Hyper-V vengono recuperati da Azure Site Recovery e hello server viene visualizzato nel **infrastruttura di Site Recovery** > **host Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Configurare un ambiente di destinazione hello

Specificare l'account di archiviazione di Azure hello per la replica e si connetterà hello Azure rete toowhich macchine virtuali di Azure dopo il failover.

1. Fare clic su **Preparare l'infrastruttura** > **Destinazione**.
2. Selezionare la sottoscrizione hello e gruppo di risorse hello in cui si desidera toocreate hello macchine virtuali di Azure dopo il failover. Scegliere hello distribuzione modello che si vuole toouse in Azure (classica o risorsa di gestione) per le macchine virtuali hello.

3. Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.

    - Se non si dispone di un account di archiviazione, fare clic su **+ archiviazione** toocreate inline un account basato su Gestione risorse. 
    - Se non si dispone di una rete di Azure, fare clic su **+ rete** toocreate un inline basate su Gestione risorse di rete.






## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 9: configurare un criterio di replica](hyper-v-site-walkthrough-replication.md)
