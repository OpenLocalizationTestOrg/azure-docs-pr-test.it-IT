---
title: aaaSet backup hello origine e di destinazione per il sito secondario di Hyper-V replica tooa con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come tooset up origine hello e di destinazione quando la replica delle macchine virtuali Hyper-V toosecondary VMM del sito con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>Passaggio 6: Configurare hello replica origine e destinazione


Dopo la creazione di servizi di ripristino di un insieme di credenziali per Hyper-V replica tooa VMM sito secondario con [Azure Site Recovery](site-recovery-overview.md), utilizzare questo tooset articolo codice sorgente hello e percorsi di replica di destinazione. 

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

Installare il Provider di Azure Site Recovery hello nei server VMM, individuare e registrare i server nell'insieme di credenziali hello.

1. Fare clic su **Passaggio 1: Preparare l'infrastruttura** > **Origine**.

    ![Impostare l'origine](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. In **origine Prepare**, fare clic su **+ VMM** tooadd un server VMM.

    ![Impostare l'origine](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. In **Aggiungi Server**, verificare che **server System Center VMM** viene visualizzato **tipo Server** e tale server VMM hello soddisfa hello [prerequisiti](#prerequisites).
4. Scaricare i file di installazione di Provider di Azure Site Recovery hello.
5. Scaricare la chiave di registrazione hello. che sarà necessaria durante l'installazione. chiave di Hello è valida per cinque giorni dopo la generazione è.

    ![Impostare l'origine](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Installare hello Provider di Azure Site Recovery nel server VMM hello. Non è necessario tooexplicitly installa alcun componente nel server host Hyper-V.


## <a name="install-hello-azure-site-recovery-provider"></a>Installare il Provider di Azure Site Recovery hello

1. Eseguire i file di installazione di Provider di hello in ogni server VMM. Se VMM è distribuito in un cluster, eseguire hello seguente hello prima fase di che installazione:
    -  Installare il provider di hello in un nodo attivo e fine server VMM nell'insieme di credenziali hello hello installazione tooregister hello.
    - Quindi, installare Provider hello in hello altri nodi. I nodi del cluster devono tutti eseguire hello stessa versione di hello Provider.
2. Il programma di installazione esegue alcuni controlli dei prerequisiti e le richieste di servizio VMM hello toostop di autorizzazione. Hello servizio VMM verrà riavviato automaticamente al completamento dell'installazione. Se si installa in un cluster VMM, si è il ruolo Cluster hello toostop richiesta.
3. In **Microsoft Update**, è possibile acconsentire esplicitamente toospecify che rispetti i criteri di Microsoft Update sono installati gli aggiornamenti di provider.
4. In **installazione**, accettare o modificare il percorso di installazione predefinito hello e fare clic su **installare**.

    ![Percorso di installazione](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. Al termine dell'installazione, fare clic su **registrare** server hello tooregister nell'insieme di credenziali hello.

    ![Percorso di installazione](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. In **nome insieme di credenziali**, verificare il nome di hello dell'insieme di credenziali hello in cui hello server verrà registrato. Fare clic su *Avanti*.

    ![Server registration](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. In **connessione Internet**, specificare la modalità di connessione tooAzure provider hello in esecuzione nel server VMM hello.

    ![Internet Settings](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - È possibile specificare tale provider hello devono connettersi direttamente toohello internet, o tramite un proxy.
   - Se necessario, specificare le impostazioni proxy.
   - Se si usa un proxy, un account RunAs VMM (DRAProxyAccount) viene creato automaticamente tramite hello specificato le credenziali del proxy. Configurare il server proxy hello in modo che questo account può autenticare correttamente. Hello impostazioni dell'account RunAs possono essere modificate nella console VMM hello > **impostazioni** > **sicurezza** > **account RunAs**. Riavviare le modifiche tooupdate di servizio VMM hello.
8. In **chiave di registrazione**selezionare chiave hello quello scaricato da Azure Site Recovery e copiato toohello server VMM.
9. impostazione di crittografia Hello viene utilizzato solo quando si esegue la replica di macchine virtuali Hyper-V in VMM cloud tooAzure. Se si esegue la replica del sito secondario tooa non utilizzato.
10. In **nome Server**, specificare un server di nome descrittivo tooidentify hello VMM nell'insieme di credenziali hello. In una configurazione cluster specificare il nome del ruolo cluster VMM hello.
11. In **Sincronizza metadati cloud**, selezionare se si desidera toosynchronize metadati per tutti i cloud nel server VMM hello con insieme di credenziali hello. Questa azione deve solo toohappen una volta in ogni server. Se non si desidera toosynchronize tutti i cloud, è possibile lasciare deselezionata questa opzione e sincronizzare ogni cloud singolarmente nelle proprietà del cloud nella console VMM hello hello.
12. Fare clic su **Avanti** processo hello toocomplete. Dopo la registrazione, i metadati dal server VMM hello vengono recuperati da Azure Site Recovery. server Hello viene visualizzato nella hello **server VMM** scheda hello **server** pagina nell'insieme di credenziali hello.

    ![Server](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Dopo che il server di hello è disponibile nella console di Site Recovery, hello in **origine** > **origine Prepare** selezionare hello VMM server e cloud selezionare hello in cui hello Hyper-V host si trova. Fare quindi clic su **OK**.

È anche possibile installare il provider di hello dalla riga di comando hello:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configurare un ambiente di destinazione hello

Selezionare i cloud e il server VMM di destinazione hello:

1. Fare clic su **Prepare infrastruttura** > **destinazione**e si desidera toouse server VMM di destinazione selezionare hello.
2. Verranno visualizzati i cloud nel server di hello sincronizzati con il ripristino del sito. Selezionare il cloud di destinazione hello.

   ![Destinazione](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 7: configurare il mapping di rete](vmm-to-vmm-walkthrough-network-mapping.md).
