---
title: aaaSet backup hello origine e di destinazione per tooAzure di replica Hyper-V (con System Center VMM) con Azure Site Recovery | Documenti Microsoft
description: Riepiloga hello passaggi tooset le impostazioni di origine e di destinazione per la replica delle macchine virtuali Hyper-V nel servizio di archiviazione VMM cloud tooAzure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>Passaggio 8: Impostare hello origine e di destinazione per tooAzure di replica Hyper-V (con VMM)

Dopo aver [la creazione di un insieme di credenziali](vmm-to-azure-walkthrough-create-vault.md) e che specifica ciò che si desidera tooreplicate, usare questa origine tooconfigure articolo e le impostazioni di destinazione durante la replica delle macchine virtuali di Hyper-V in locale in System Center Virtual Machine Manager (VMM) cloud tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

S1. Fare clic su **Preparare l'infrastruttura** > **Origine**.

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. In **origine Prepare**, fare clic su **+ VMM** tooadd un server VMM.

    ![Impostare l'origine](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. In **Aggiungi Server**, verificare che **server System Center VMM** viene visualizzato **tipo Server** e tale server VMM hello soddisfa hello [prerequisiti e l'URL requisiti](#prerequisites).
4. Scaricare i file di installazione di Provider di Azure Site Recovery hello.
5. Scaricare la chiave di registrazione hello. che sarà necessaria durante l'installazione. chiave di Hello è valida per cinque giorni dopo la generazione è.

    ![Impostare l'origine](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Installare hello Provider nel server VMM hello

1. Eseguire i file di installazione di Provider di hello nel server VMM hello.
2. In **Microsoft Update** è possibile acconsentire esplicitamente agli aggiornamenti in modo che gli aggiornamenti del provider vengano installati in base ai criteri di Microsoft Update.
3. In **installazione**, accettare o modificare percorso di installazione di Provider predefinito hello e fare clic su **installare**.

    ![Percorso di installazione](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. Al termine dell'installazione, fare clic su **registrare** server VMM di hello tooregister nell'insieme di credenziali hello.
5. In hello **impostazioni insieme di credenziali** pagina, fare clic su **Sfoglia** tooselect file di chiave dell'insieme di credenziali hello. Specificare una sottoscrizione di Azure Site Recovery hello e il nome dell'insieme di credenziali hello.

    ![Server registration](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. In **connessione Internet**, specificare la modalità Provider in esecuzione nel server VMM hello si connetterà tooSite ripristino su hello hello internet.

   * Se si desidera hello Provider tooconnect direttamente, selezionare **connettersi direttamente tooAzure il ripristino del sito senza un proxy**.
   * Se il proxy esistente richiede l'autenticazione, o si desidera toouse un proxy personalizzato, selezionare **connettersi tooAzure ripristino del sito utilizzando un server proxy**.
   * Se si utilizza un proxy personalizzato, specificare le credenziali, porta e indirizzo hello.
   * Se si utilizza un proxy, è necessario avere già hello URL consentiti descritto in [prerequisiti](#on-premises-prerequisites).
   * Se si utilizza un proxy personalizzato, un account RunAs VMM (DRAProxyAccount) verrà creato automaticamente tramite hello specificato le credenziali del proxy. Configurare il server proxy hello in modo che questo account può autenticare correttamente. le impostazioni dell'account RunAs VMM Hello possono essere modificate nella console VMM hello. In **impostazioni**, espandere **sicurezza** > **account RunAs**e quindi modificare la password di hello di DRAProxyAccount. Servizio VMM toorestart hello è necessario in modo che questa impostazione ha effetto.

     ![Internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. Accettare o modificare il percorso di hello di un certificato SSL generato automaticamente per la crittografia dei dati. Questo certificato viene usato se si abilita la crittografia dei dati per un cloud protetto da Azure nel portale di Azure Site Recovery hello. Conservare il certificato in una posizione sicura, Quando si esegue un failover tooAzure necessario toodecrypt, se è abilitata la crittografia dei dati.
8. In **nome Server**, specificare un server di nome descrittivo tooidentify hello VMM nell'insieme di credenziali hello. In una configurazione cluster, specificare il nome del ruolo cluster VMM hello.
9. Abilitare **Sincronizza metadati cloud**, se si desidera toosynchronize metadati per tutti i cloud nel server VMM hello con insieme di credenziali hello. Questa azione deve solo toohappen una volta in ogni server. Se non si desidera toosynchronize tutti i cloud, è possibile lasciare deselezionata questa opzione e sincronizzare ogni cloud singolarmente nelle proprietà del cloud nella console VMM hello hello. Fare clic su **registrare** processo hello toocomplete.

    ![Server registration](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. Verrà avviata la registrazione. Al termine della registrazione, il server di hello viene visualizzato nel **infrastruttura di Site Recovery** > **server VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Installare l'agente di servizi di ripristino di Azure hello in host Hyper-V

1. Dopo aver configurato la hello Provider, file di installazione toodownload hello è necessario per l'agente di servizi di ripristino di Azure hello. Eseguire l'installazione in ogni server Hyper-V hello cloud VMM.

    ![Siti Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. In **Controllo dei prerequisiti** fare clic su **Avanti**. Gli eventuali prerequisiti mancanti verranno installati automaticamente.

    ![Prerequisiti per l'agente di Servizi di ripristino di Azure](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. In **le impostazioni di installazione**, accettare o modificare il percorso di installazione di hello e percorso della cache di hello. È possibile configurare cache di hello in un'unità con almeno 5 GB di spazio di archiviazione disponibile, ma è consigliabile un'unità di cache con più di 600 GB di spazio libero. Fare clic su **Installa**.
4. Al termine dell'installazione, fare clic su **Chiudi** toofinish.

    ![Registrare l'Agente di Servizi di ripristino di Microsoft Azure](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>Installazione dalla riga di comando
È possibile installare agente servizi di ripristino di Microsoft Azure hello dalla riga di comando utilizzando hello comando seguente:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Configurare internet proxy accesso tooSite ripristino dagli host Hyper-V

agente di servizi di ripristino Hello in esecuzione in host Hyper-V deve tooAzure accesso internet per la replica di macchina virtuale. Se si accede hello internet tramite un proxy, configurarlo come indicato di seguito:

1. Aprire hello Microsoft Azure Backup snap-in MMC in host Hyper-V hello. Per impostazione predefinita, un collegamento per il Backup di Microsoft Azure è disponibile sul desktop hello o in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Hello nello snap-in, fare clic su **Modifica proprietà**.
3. In hello **configurazione Proxy** , specificare le informazioni sul server proxy.

    ![Registrare l'Agente di Servizi di ripristino di Microsoft Azure](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. Verificare che l'agente di hello possibile raggiungere l'URL di hello descritto in hello [prerequisiti](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Configurare un ambiente di destinazione hello
Specificare hello toobe di account di archiviazione di Azure utilizzata per la replica si connetterà hello Azure rete toowhich macchine virtuali di Azure dopo il failover.

1. Fare clic su **Prepare infrastruttura** > **destinazione**, selezionare la sottoscrizione hello e hello gruppo di risorse in cui si desidera hello toocreate eseguito il failover delle macchine virtuali. Scegliere modello di distribuzione hello che si desidera toouse in Azure (classica o risorsa di gestione) per il failover le macchine virtuali hello.

    ![Archiviazione](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.

    ![Archiviazione](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. Se ancora stato creato un account di archiviazione e si desidera toocreate uno usando Gestione risorse, fare clic su **+ account di archiviazione** toodo tale inline.  In hello **creare account di archiviazione** pannello specificare un nome dell'account, tipo, sottoscrizione e posizione. Hello account deve essere hello stesso percorso hello insieme di credenziali di servizi di ripristino.

   ![Archiviazione](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * Se si desidera toocreate un account di archiviazione utilizzando il modello classico hello, eseguire questa operazione in hello portale di Azure. [Altre informazioni](../storage/common/storage-create-storage-account.md)
   * Se si utilizza un account di archiviazione premium per i dati replicati, impostare un account di archiviazione standard aggiuntiva, i log di replica toostore che acquisiscono dati locali tooon le modifiche in corso.
5. Se non è stata creata una rete di Azure e si desidera toocreate uno usando Gestione risorse, fare clic su **+ rete** toodo tale inline. In hello **crea rete virtuale** pannello specificare un nome di rete, intervallo di indirizzi, i dettagli di subnet, sottoscrizione e posizione. rete Hello devono trovarsi in hello stesso percorso hello insieme di credenziali di servizi di ripristino.

   ![Rete](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   Se si desidera toocreate una rete usando il modello classico di hello, eseguire questa operazione in hello portale di Azure. [Altre informazioni](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)





## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 9: configurare il mapping di rete](vmm-to-azure-walkthrough-network-mapping.md)
