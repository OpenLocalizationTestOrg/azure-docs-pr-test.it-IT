---
title: sito secondario aaaReplicate macchine virtuali Hyper-V tooa con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come tooreplicate macchine virtuali Hyper-V in VMM cloud tooa secondario VMM del sito utilizzando hello portale di Azure.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>Replicare le macchine virtuali Hyper-V in VMM cloud tooa VMM del sito secondario utilizzando hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmm-to-vmm.md)
> * [Portale classico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Gestione risorse](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

In questo articolo viene descritto come tooreplicate locale macchine virtuali Hyper-V gestite nei cloud di System Center Virtual Machine Manager (VMM), tooa sito secondario utilizzando [Azure Site Recovery](site-recovery-overview.md) in hello portale di Azure. Ulteriori informazioni sull'[architettura dello scenario](site-recovery-components.md).

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Prerequisiti

**Prerequisito** | **Dettagli**
--- | ---
**Azzurro** | È necessario un account [Microsoft Azure](http://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/). [Altre informazioni](https://azure.microsoft.com/pricing/details/site-recovery/) sui prezzi di Site Recovery.
**VMM locale** | È consigliabile che disporre di due server VMM, uno nel sito primario di hello e uno in hello secondario.<br/><br/> È possibile replicare tra cloud in un singolo server VMM.<br/><br/> Server VMM devono essere in esecuzione almeno System Center 2012 SP1 con gli aggiornamenti più recenti di hello.<br/><br/> I server VMM richiedono l'accesso a Internet.
**Cloud VMM** | Ogni server VMM deve essere in uno o più cloud e in tutte le aree è necessario impostare il profilo di capacità Hyper-V hello. <br/><br/>I cloud devono contenere uno o più gruppi host VMM.<br/><br/> Se si dispone solo di un server VMM, è necessario almeno due cloud, tooact come primario e secondario.
**Hyper-V** | Server Hyper-V deve essere in esecuzione almeno Windows Server 2012 con il ruolo Hyper-V hello, e hanno hello installati aggiornamenti più recenti.<br/><br/> Il server Hyper-V deve contenere una o più macchine virtuali.<br/><br/>  Server host Hyper-V devono essere distribuiti nei gruppi host nei cloud VMM primario e secondario di hello.<br/><br/> Se si esegue Hyper-V in un cluster in Windows Server 2012 R2 installare l'[aggiornamento 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Se si esegue Hyper-V in un cluster basato su indirizzi IP statici in Windows Server 2012, il broker del cluster non viene creato automaticamente. Configurare un gestore cluster hello manualmente. [Altre informazioni](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> I server Hyper-V richiedono l'accesso a Internet.
**URL** | Server VMM e host Hyper-V deve essere in grado di tooreach questi URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>Passaggi di distribuzione

È necessario eseguire queste operazioni:

1. Verificare i prerequisiti.
2. Preparare il server VMM hello e host Hyper-V.
3. Creare un insieme di credenziali dei servizi di ripristino. insieme di credenziali Hello contiene impostazioni di configurazione e Orchestra la replica.
4. Specificare origine, destinazione e impostazioni di replica.
5. Distribuzione di servizio di mobilità hello in macchine virtuali desiderate tooreplicate.
6. Preparare per la replica e abilitare la replica per le macchine virtuali Hyper-V.
7. Eseguire un toomake di failover di test che tutto funzioni come previsto.

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>Preparare i server VMM e gli host Hyper-V

tooprepare per la distribuzione:

1. Verificare che i server VMM hello e host Hyper-V conformarsi prerequisiti hello descritti in precedenza e può raggiungere URL hello necessario.
2. Configurare le reti VMM in modo che sia possibile configurare il [mapping di rete](#network-mapping-overview).

    - Assicurarsi che le macchine virtuali di origine hello server host Hyper-V siano connesso tooa rete VM di VMM. La rete deve essere collegato tooa la rete logica associata al cloud hello.
    Verificare che i cloud secondario hello utilizzati per il ripristino sia configurata una rete VM corrispondente. Rete VM deve essere collegato tooa la rete logica associata a cloud secondario hello.

3. Preparare un [singola distribuzione server](#single-vmm-server-deployment), se si desidera che le macchine virtuali tooreplicate tra cloud in hello stesso server VMM.

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo** > **Gestione** > **Servizi di ripristino**.
3. In **nome**, specificare un insieme di credenziali di nome descrittivo tooidentify hello. Se è disponibile più di una sottoscrizione, selezionarne una.
4. [Creare un gruppo di risorse](../azure-resource-manager/resource-group-template-deploy-portal.md)o selezionarne uno esistente. Specificare un'area di Azure. Le macchine vengono replicati toothis area. aree toocheck supportato vedere aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Insieme di credenziali di tooquickly accesso hello da hello Dashboard, fare clic su **Pin toodashboard** > **Crea insieme di credenziali**.

    ![Nuovo insieme di credenziali](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

viene visualizzata di nuovo insieme di credenziali Hello in hello **Dashboard**nella **tutte le risorse**e su hello principale **insiemi di credenziali di servizi di ripristino** blade.


## <a name="choose-a-protection-goal"></a>Scegliere un obiettivo di protezione

Selezionare gli elementi si desidera tooreplicate e in cui si desidera tooreplicate per.

2. Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Obiettivo di protezione**.
3. Selezionare **toorecovery sito**e selezionare **Sì, con Hyper-V**.
4. Selezionare **Sì** tooindicate si utilizza un host Hyper-V hello toomanage VMM.
5. Selezionare **Sì** se si dispone di un server VMM secondario. Se si distribuisce la replica tra cloud in un unico server VMM, fare clic su **No**. Fare quindi clic su **OK**.

    ![Scegliere gli obiettivi](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

Installare il Provider di Azure Site Recovery hello nei server VMM, individuare e registrare i server nell'insieme di credenziali hello.

1. Fare clic su **Passaggio 1: Preparare l'infrastruttura** > **Origine**.

    ![Impostare l'origine](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. In **origine Prepare**, fare clic su **+ VMM** tooadd un server VMM.

    ![Impostare l'origine](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. In **Aggiungi Server**, verificare che **server System Center VMM** viene visualizzato **tipo Server** e tale server VMM hello soddisfa hello [prerequisiti](#prerequisites).
4. Scaricare i file di installazione di Provider di Azure Site Recovery hello.
5. Scaricare la chiave di registrazione hello. che sarà necessaria durante l'installazione. chiave di Hello è valida per cinque giorni dopo la generazione è.

    ![Impostare l'origine](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. Installare hello Provider di Azure Site Recovery nel server VMM hello. Non è necessario tooexplicitly installa alcun componente nel server host Hyper-V.


### <a name="install-hello-azure-site-recovery-provider"></a>Installare il Provider di Azure Site Recovery hello

1. Eseguire i file di installazione di Provider di hello in ogni server VMM. Se VMM è distribuito in un cluster, eseguire hello seguente hello prima fase di che installazione:
    -  Installare il provider di hello in un nodo attivo e fine server VMM nell'insieme di credenziali hello hello installazione tooregister hello.
    - Quindi, installare Provider hello in hello altri nodi. I nodi del cluster devono tutti eseguire hello stessa versione di hello Provider.
2. Il programma di installazione esegue alcuni controlli dei prerequisiti e le richieste di servizio VMM hello toostop di autorizzazione. Hello servizio VMM verrà riavviato automaticamente al completamento dell'installazione. Se si installa in un cluster VMM, si è il ruolo Cluster hello toostop richiesta.
3. In **Microsoft Update**, è possibile acconsentire esplicitamente toospecify che rispetti i criteri di Microsoft Update sono installati gli aggiornamenti di provider.
4. In **installazione**, accettare o modificare il percorso di installazione predefinito hello e fare clic su **installare**.

    ![Percorso di installazione](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. Al termine dell'installazione, fare clic su **registrare** server hello tooregister nell'insieme di credenziali hello.

    ![Percorso di installazione](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. In **nome insieme di credenziali**, verificare il nome di hello dell'insieme di credenziali hello in cui hello server verrà registrato. Fare clic su *Avanti*.

    ![Server registration](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. In **connessione Internet**, specificare la modalità di connessione tooAzure provider hello in esecuzione nel server VMM hello.

    ![Internet Settings](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - È possibile specificare tale provider hello devono connettersi direttamente toohello internet, o tramite un proxy.
   - Se necessario, specificare le impostazioni proxy.
   - Se si usa un proxy, un account RunAs VMM (DRAProxyAccount) viene creato automaticamente tramite hello specificato le credenziali del proxy. Configurare il server proxy hello in modo che questo account può autenticare correttamente. Hello impostazioni dell'account RunAs possono essere modificate nella console VMM hello > **impostazioni** > **sicurezza** > **account RunAs**. Riavviare le modifiche tooupdate di servizio VMM hello.
8. In **chiave di registrazione**selezionare chiave hello quello scaricato da Azure Site Recovery e copiato toohello server VMM.
9. impostazione di crittografia Hello viene utilizzato solo quando si esegue la replica di macchine virtuali Hyper-V in VMM cloud tooAzure. Se si esegue la replica del sito secondario tooa non utilizzato.
10. In **nome Server**, specificare un server di nome descrittivo tooidentify hello VMM nell'insieme di credenziali hello. In una configurazione cluster specificare il nome del ruolo cluster VMM hello.
11. In **Sincronizza metadati cloud**, selezionare se si desidera toosynchronize metadati per tutti i cloud nel server VMM hello con insieme di credenziali hello. Questa azione deve solo toohappen una volta in ogni server. Se non si desidera toosynchronize tutti i cloud, è possibile lasciare deselezionata questa opzione e sincronizzare ogni cloud singolarmente nelle proprietà del cloud nella console VMM hello hello.
12. Fare clic su **Avanti** processo hello toocomplete. Dopo la registrazione, i metadati dal server VMM hello vengono recuperati da Azure Site Recovery. server Hello viene visualizzato nella hello **server VMM** scheda hello **server** pagina nell'insieme di credenziali hello.

    ![Server](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Dopo che il server di hello è disponibile nella console di Site Recovery, hello in **origine** > **origine Prepare** selezionare hello VMM server e cloud selezionare hello in cui hello Hyper-V host si trova. Fare quindi clic su **OK**.

È anche possibile installare il provider di hello dalla riga di comando hello:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configurare un ambiente di destinazione hello

Selezionare i cloud e il server VMM di destinazione hello.

1. Fare clic su **Prepare infrastruttura** > **destinazione**e si desidera toouse server VMM di destinazione selezionare hello.
2. Verranno visualizzati i cloud nel server di hello sincronizzati con il ripristino del sito. Selezionare il cloud di destinazione hello.

   ![Destinazione](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>Configurare le impostazioni di replica

- Quando si crea un criterio di replica, tutti gli host tramite criteri di hello devono avere hello stesso sistema operativo. Hello cloud VMM può contenere host Hyper-V che eseguono versioni diverse di Windows Server, ma in questo caso, è necessario più criteri di replica.
- È possibile eseguire hello la replica iniziale offline. [Altre informazioni](#prepare-for-initial-offline-replication)

1. Fare clic su un nuovo criterio di replica toocreate **Prepare infrastruttura** > **le impostazioni di replica** > **+ crea e associa**.

    ![Rete](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. In **Criteri di creazione e associazione**specificare il nome dei criteri. Hello tipo di origine e di destinazione deve essere **Hyper-V**.
3. In **versione dell'host Hyper-V**, selezionare il sistema operativo è in esecuzione nell'host di hello.
4. In **tipo di autenticazione** e **porta di autenticazione**, specificare come viene autenticato il traffico tra hello primario e i server host Hyper-V di ripristino. Selezionare **Certificato** a meno che non sia configurato un ambiente Kerberos funzionante. Azure Site Recovery configura automaticamente i certificati per l'autenticazione HTTPS. Non è necessario toodo nulla manualmente. Per impostazione predefinita, porte 8083 e 8084 (per i certificati) sono aperte in hello Windows Firewall nei server host Hyper-V di hello. Se si seleziona **Kerberos**, verrà usato un ticket Kerberos per l'autenticazione reciproca dei server host hello. Questa impostazione è rilevante solo per i server host Hyper-V in esecuzione su Windows Server 2012 R2.
5. In **frequenza di copia**, specificare la frequenza con cui si desidera dati delta tooreplicate dopo la replica iniziale hello (ogni 30 secondi, 5 o 15 minuti).
6. In **conservazione del punto di ripristino**, specificare in ore, per quanto tempo il periodo di memorizzazione hello verrà per ogni punto di ripristino. Macchine virtuali protette possono essere ripristinati tooany punto all'interno di una finestra.
7. In **Frequenza snapshot coerenti con l'app** specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione. Hyper-V usa due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale di hello e uno snapshot coerente dell'applicazione che accetta uno snapshot del punto nel tempo dei dati dell'applicazione hello macchina virtuale hello. Snapshot coerenti dell'applicazione usare tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot. Se si abilita snapshot coerenti dell'applicazione, influisce negativamente sulle prestazioni di hello delle applicazioni in esecuzione in macchine virtuali di origine. Verificare che il valore di hello impostato è minore hello numero di punti di ripristino aggiuntivi configurati.
8. In **Compressione trasferimento dati**specificare se i dati replicati che vengono trasferiti devono essere compressi.
9. Selezionare **Elimina replica VM**, toospecify che hello macchina virtuale di replica deve essere eliminata se si disabilita la protezione per la macchina virtuale di origine hello. Se si abilita questa impostazione, quando si disabilita la protezione per la macchina virtuale viene rimosso dalla console di Site Recovery hello di origine di hello, le impostazioni di Site Recovery per VMM hello vengono rimosse dalla console VMM hello e hello replica viene eliminata.
10. In **il metodo di replica iniziale**, se si esegue la replica in rete hello, specificare se toostart hello la replica iniziale o la pianificazione. larghezza di banda toosave, potrebbe essere necessario tooschedule è di fuori dell'orario di disponibilità. Fare quindi clic su **OK**.

     ![Criteri di replica](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. Quando si crea un nuovo criterio automaticamente associato hello cloud VMM. In **Criteri di replica** fare clic su **OK**. È possibile associare altri cloud VMM (e hello macchine virtuali in essi contenuti) con questo criterio di replica in **replica** > Nome criterio > **associare Cloud VMM**.

     ![Criteri di replica](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>Configurare il mapping di rete

- Leggere le informazioni sul [mapping di rete](#prepare-for-network-mapping) prima di iniziare.
- Verificare che le macchine virtuali nei server VMM siano connessi tooa rete VM.


1. In **Site Recovery Infrastructure** >  (Infrastruttura di Site Recovery) **Mapping di rete** > **Mapping di rete** fare clic su **+Mapping di rete**.

    ![Mapping di rete](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. In **aggiungere mapping di rete** , selezionare l'origine hello e i server VMM di destinazione. vengono recuperate le reti VM Hello associate al server VMM hello.
3. In **rete di origine**selezionare hello rete toouse elenco hello di reti VM associate al server VMM primario hello.
4. In **rete di destinazione**selezionare hello rete toouse nel server VMM secondario hello. Fare quindi clic su **OK**.

    ![Mapping di rete](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

Quando ha inizio il mapping di rete vengono eseguite le operazioni seguenti:

* Le macchine virtuali di replica esistente che corrispondono toohello rete VM di origine sarà connessa toohello rete VM di destinazione.
* Nuove macchine virtuali che sono connessi toohello rete VM di origine sarà connessa toohello rete mappata di destinazione dopo la replica.
* Se si modifica un mapping esistente con una nuova rete, macchine virtuali di replica verranno connesse usando le nuove impostazioni hello.
* Se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover. Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.

### <a name="configure-storage-mapping"></a>Configurare il mapping di archiviazione.

[Mapping di archiviazione](#prepare-for-storage-mapping) non è supportato nel nuovo portale di Azure hello. ma può essere abilitato tramite Powershell. [Altre informazioni](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping).

## <a name="step-5-capacity-planning"></a>Passaggio 5: Pianificazione della capacità

Dopo avere configurato l'infrastruttura di base, passare alla pianificazione della capacità e valutare se sono necessarie altre risorse.

- Scaricare ed eseguire hello [pianificazione della capacità di ripristino del sito Azure](site-recovery-capacity-planner.md), toogather informazioni sull'ambiente di replica, tra cui le macchine virtuali, dischi per ogni macchina virtuale e archiviazione per ogni disco.
- Dopo aver raccolto le informazioni di replica in tempo reale, è possibile modificare la larghezza di banda di hello NetQos criteri toocontrol replica per le macchine virtuali. Altre informazioni sulla [limitazione del traffico di replica di Hyper-V](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/) sono disponibili sul blog di Thomas Maurer. Ottenere altre informazioni su hello [cmdlet New-NetQosPolicy](https://technet.microsoft.com/library/hh967468.aspx.).

## <a name="enable-replication"></a>Abilitare la replica

1. Fare clic su **Passaggio 2: Eseguire la replica dell'applicazione** > **Origine**. Dopo aver abilitato la replica per hello prima volta, si fa clic su **+ replicare** nella replica di tooenable hello insieme di credenziali per le macchine aggiuntive.

    ![Abilitare la replica](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. In **origine**, selezionare il server VMM di hello e cloud in cui hello si trovano gli host Hyper-V da tooreplicate hello. Fare quindi clic su **OK**.

    ![Abilitare la replica](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. In **destinazione**, verificare il server VMM secondario di hello e cloud.
4. In **macchine virtuali**, selezionare le macchine virtuali hello desiderato tooprotect dall'elenco di hello.

    ![Abilitare la protezione delle macchine virtuali](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

È possibile monitorare lo stato di avanzamento di hello **Abilita protezione** azione in **processi** > **i processi di ripristino del sito**. Dopo aver hello **finalizzazione della protezione** completamento del processo, la macchina virtuale di hello è pronta per il failover.

Si noti che:

- È inoltre possibile abilitare la protezione per le macchine virtuali nella console VMM hello. Fare clic su **Abilita protezione** sulla barra degli strumenti hello in proprietà macchina virtuale hello > **Azure Site Recovery** scheda.
- Dopo avere abilitato la replica, è possibile visualizzare le proprietà per hello VM in **elementi replicati**. In hello **Essentials** dashboard, è possibile visualizzare informazioni sui criteri di replica hello per hello macchina virtuale e il relativo stato. Per altri dettagli, fare clic su **Proprietà** .

### <a name="onboard-existing-virtual-machines"></a>Caricare le macchine virtuali esistenti
Se in VMM sono presenti macchine virtuali replicate tramite la replica Hyper-V, è possibile caricarle per la replica in Azure Site Recovery nel modo seguente:

1. Assicurarsi che nel server hello Hyper-V ospita macchina virtuale esistente si trova nel cloud primario hello hello e tale server Hyper-V hello hosting hello macchina virtuale di replica si trova nel cloud secondario hello.
2. Verificare che sia configurato un criterio di replica per i cloud VMM primario hello.
3. Abilitare la replica per macchina virtuale primaria hello. Azure Site Recovery e VMM assicurarsi che hello stesso host di replica e la macchina virtuale viene rilevato, Azure Site Recovery riutilizzerà e ristabilire la replica hello utilizzando le impostazioni specificate.

## <a name="test-your-deployment"></a>Testare la distribuzione

tootest la distribuzione, è possibile eseguire un [failover di test](site-recovery-test-failover-vmm-to-vmm.md) per una singola macchina virtuale, o [creare un piano di ripristino](site-recovery-create-recovery-plans.md) che contiene uno o più macchine virtuali.



## <a name="prepare-for-offline-initial-replication"></a>Preparare la replica iniziale offline

È possibile eseguire la replica offline per la copia di dati iniziale hello. Per prepararla, procedere come segue:

* Nel server di origine hello, specificare il percorso dal quale hello esportazione dei dati avrà luogo. Assegnare il controllo completo per le autorizzazioni di condivisione e NTFS, il servizio VMM toohello nel percorso di esportazione hello. Nel server di destinazione hello, specificare il percorso da cui importare i dati di hello si verificherà. Assegnare hello delle stesse autorizzazioni su questo percorso di importazione.
* Se hello importare o percorso di esportazione è condiviso, assegnare l'appartenenza al gruppo Administrator, Power User, Print Operator o Server Operators per l'account del servizio VMM hello nel computer remoto hello in cui hello condiviso si trova.
* Se si utilizza qualsiasi host tooadd account RunAs, su hello importare ed esportare i percorsi, assegnare di lettura e delle autorizzazioni di scrittura toohello account RunAs in VMM.
* Hello importazione ed esportazione di condivisioni non deve trovarsi in qualsiasi computer utilizzato come server host Hyper-V, perché la configurazione di loopback non è supportata da Hyper-V.
* In Active Directory, in ogni server host Hyper-V che contiene le macchine virtuali da tooprotect, abilitare e configurare la delega vincolata tootrust hello computer remoti in cui hello importazione e l'esportazione percorsi si trovano, come indicato di seguito:
  1. Nel controller di dominio hello, aprire **Active Directory Users and Computers**.
  2. Nella console di hello, fare clic su **DomainName** > **computer**.
  3. Nome del server host Hyper-V hello rapida > **proprietà**.
  4. In hello **delega** scheda, fare clic su **computer attendibile per i servizi solo di delega toospecified**.
  5. Fare clic su **Usa un qualsiasi protocollo di autenticazione**.
  6. Fare clic su **Aggiungi** > **Utenti e computer**.
  7. Nome del computer di hello che ospita il percorso di esportazione hello hello di tipo > **OK**. Tenere premuto CTRL hello hello l'elenco dei servizi disponibili e fare clic su **cifs** > **OK**. Ripetere per il nome del computer hello hello tale percorso di importazione hello host. Ripetere l'operazione per eventuali altri server host Hyper-V.



## <a name="prepare-for-network-mapping"></a>Preparare il mapping di rete
Rete viene eseguito il mapping tra i server VMM primari e secondari di hello per le reti VM di VMM:

* Posizionare in modo ottimale le macchine virtuali di replica in host Hyper-V secondari dopo il failover.
* Connettere reti VM tooappropriate macchine virtuali di replica dopo il failover.

Si noti che:
- Mapping di rete può essere configurato tra reti VM nei due server VMM o in un singolo server VMM se due siti sono gestiti da hello stesso server.
- Quando il mapping è configurato correttamente e la replica è abilitata, una macchina virtuale nella posizione primaria hello sarà connessa tooa rete e la replica nel percorso di destinazione hello verrà connessa tooits eseguito il mapping di rete.
- Se le reti impostate correttamente in VMM, quando si seleziona una rete VM di destinazione durante il mapping di rete, cloud di origine VMM hello che utilizzano una rete VM di origine hello verrà visualizzato, insieme a reti VM di destinazione disponibili hello nei cloud di destinazione hello che vengono utilizzati per protezione dati.
- Se la rete di destinazione hello dispone di più subnet e una di queste subnet ha hello stesso nome come hello subnet in cui hello macchina virtuale di origine si trova quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover. Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.


Ecco un esempio tooillustrate questo meccanismo. Si prenda come esempio un’organizzazione con due sedi, New York e Chicago.

| **Posizione** | **Server VMM** | **Reti VM** | **Mappata a** |
| --- | --- | --- | --- |
| New York |VMM-NewYork |VMNetwork1-NewYork |Mappato tooVMNetwork1-Chicago |
| VMNetwork2-NewYork |Non mappata | | |
| Chicago |VMM-Chicago |VMNetwork1-Chicago |TooVMNetwork1-NewYork mappato |
| VMNetwork2-Chicago |Non mappata | | |

Con questo esempio:

* Creazione di una macchina virtuale di replica per ogni macchina virtuale che è connesso tooVMNetwork1-NewYork, verrà connesso tooVMNetwork1-Chicago.
* Quando una macchina virtuale di replica viene creata per VMNetwork2-NewYork o VMNetwork2-Chicago, non sarà connessa tooany rete.

Ecco come vengono impostati cloud VMM, organizzazione di esempio e le reti logiche di hello associate hello cloud.

### <a name="cloud-protection-settings"></a>Impostazioni di protezione del cloud
| **Cloud protetto** | **Protezione del cloud** | **Rete logica (New York)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>ND</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |
| SilverCloud2 |<p>ND</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |

### <a name="logical-and-vm-network-settings"></a>Impostazioni di rete VM e logica
| **Posizione** | **Rete logica** | **Rete VM associata** |
| --- | --- | --- |
| New York |LogicalNetwork1-NewYork |VMNetwork1-NewYork |
| Chicago |LogicalNetwork1-Chicago |VMNetwork1-Chicago |
| LogicalNetwork2Chicago |VMNetwork2-Chicago | |

### <a name="target-networks"></a>Reti di destinazione
In base a queste impostazioni, quando si seleziona una rete VM di destinazione hello, hello nella tabella seguente mostra le scelte di hello che saranno disponibili.

| **Select** | **Cloud protetto** | **Protezione del cloud** | **Rete di destinazione disponibili** |
| --- | --- | --- | --- |
| VMNetwork1-Chicago |SilverCloud1 |SilverCloud2 |Disponibile |
| GoldCloud1 |GoldCloud2 |Disponibile | |
| VMNetwork2-Chicago |SilverCloud1 |SilverCloud2 |Non disponibile |
| GoldCloud1 |GoldCloud2 |Disponibile | |


### <a name="failback"></a>Failback
toosee cosa accade nel caso di hello di failback (replica inversa), si supponga che VMNetwork1-NewYork è mappato tooVMNetwork1-Chicago, con le impostazioni seguenti hello.

| **Macchina virtuale** | **Rete tooVM connesso** |
| --- | --- |
| VM1 |VMNetwork1-Network |
| VM2 (replica di VM1) |VMNetwork1-Chicago |

Con queste impostazioni esaminare cosa accade in un paio di scenari possibili.

| **Scenario** | **Risultato** |
| --- | --- |
| Nessuna modifica apportata alle proprietà di rete hello di VM-2 dopo il failover. |VM-1 rimane connessa toohello rete di origine. |
| Le proprietà di rete di VM-2 cambiano dopo il failover e la macchina virtuale viene disconnessa  |VM-1 viene disconnessa |
| Le proprietà di rete di VM-2 vengono modificate dopo il failover e viene connesso tooVMNetwork2-Chicago. |Se non viene eseguito il mapping di VMNetwork2-Chicago, VM-1 verrà disconnessa |
| Il mapping di rete di VMNetwork1-Chicago viene modificato |VM-1 verrà connessa toohello rete ora mappato tooVMNetwork1-Chicago. |


## <a name="prepare-for-single-server-deployment"></a>Prepararsi per una distribuzione a server singolo


Se si dispone solo di un singolo server VMM, è possibile replicare le macchine virtuali in host Hyper-V nel cloud VMM hello troppo[Azure](site-recovery-vmm-to-azure.md) o cloud VMM secondario tooa. È consigliabile prima opzione hello perché la replica tra cloud non è trasparente. Se si desidera tooreplicate tra cloud, è possibile replicare un server VMM singolo autonomo o con un singolo server VMM distribuito in un cluster di Windows con estensione

### <a name="standalone-vmm-server"></a>Server VMM autonomo

In questo scenario, la distribuzione di server VMM singolo hello come una macchina virtuale nel sito primario di hello e replicare il sito secondario tooa VM utilizzando il ripristino del sito e Replica Hyper-V.

1. **Configurare VMM in una VM Hyper-V**. Si consiglia di condivisione percorso di istanza di SQL Server hello utilizzato da VMM in hello stessa macchina virtuale. Ciò consente di risparmiare tempo come solo una macchina virtuale ha toobe creato. Se si desidera toouse istanza remota di SQL Server e si verifica un'interruzione, è necessario toorecover quell'istanza prima di poter ripristinare VMM.
2. **Verificare che il server VMM hello disponga di almeno due cloud configurato**. Un cloud contiene macchine virtuali desiderate tooreplicate e hello altri cloud verranno utilizzata come posizione secondaria hello hello. Hello cloud che si desidera tooprotect devono essere conformi alle macchine virtuali di hello contiene [prerequisiti](#prerequisites).
3. Configurare Site Recovery come descritto in questo articolo. Creare e registrare il server VMM hello in un insieme di credenziali, impostare un criterio di replica e abilitare la replica. nomi di VMM di origine e destinazione Hello verrà essere hello stesso. Specificare che la replica iniziale viene effettuata tramite rete hello.
4. Quando si configura il mapping di rete eseguire il mapping di rete VM hello per rete VM di toohello hello cloud primario per il cloud secondario hello.
5. Nella console di gestione di Hyper-V hello, abilitare la Replica Hyper-V nell'host Hyper-V hello contenente hello VM di VMM e abilitare la replica in hello macchina virtuale. Assicurarsi che non si aggiungono tooclouds di macchina virtuale VMM hello che sono protetti mediante il ripristino del sito, tooensure che le impostazioni di Replica Hyper-V non sono sottoposto a override da Site Recovery.
6. Se si crea piani di ripristino per il failover che è utilizzare hello stesso server VMM di origine e di destinazione.
7. In caso di interruzione totale, eseguire il failover e il ripristino come riportato di seguito:

   1. Eseguire un failover non pianificato nella console di gestione di Hyper-V hello nel sito secondario di hello, toofail su hello VM di VMM toohello secondario del sito primario.
   2. Verificare che hello che VM di VMM sia attivo e in esecuzione e nell'insieme di credenziali hello eseguire toofail un failover non pianificato in macchine virtuali hello da cloud primario toosecondary. Eseguire il commit hello failover e selezionare un punto di ripristino alternativa, se necessario.
   3. Al termine hello failover non pianificato, tutte le risorse sono accessibili dal sito primario di hello nuovamente.
   4. Quando il sito primario di hello è disponibile anche nella console di gestione di Hyper-V hello nel sito secondario di hello, abilitare la replica inversa per hello VM di VMM. Verrà avviata la replica per hello VM da tooprimary secondario.
   5. Eseguire un failover pianificato nella console di gestione di Hyper-V hello nel sito secondario di hello, toofail su hello sito primario di toohello VM di VMM. Eseguire il commit hello failover. Abilitare la replica inversa, in modo che hello VM di VMM è nuovamente la replica da primario toosecondary.
   6. Nell'insieme di credenziali di hello servizi di ripristino, abilitare la replica inversa per carico di lavoro hello le macchine virtuali, toostart replicarle da tooprimary secondario.
   7. Nell'archivio di servizi di ripristino hello, eseguire un failover pianificato toofail hello indietro del carico di lavoro macchine virtuali toohello sito primario. Eseguire il commit toocomplete failover hello è. Quindi, abilitare la replica inversa toostart replica hello carico di lavoro macchine virtuali da toosecondary primario.

### <a name="stretched-vmm-cluster"></a>Cluster VMM esteso

Anziché distribuire un server VMM autonomo come una macchina virtuale che esegue la replica del sito secondario tooa, effettuabili VMM a disponibilità elevata mediante la distribuzione di una macchina virtuale in un cluster di failover di Windows. assicurando così flessibilità al carico di lavoro e protezione da errori hardware. toodeploy con hello Site Recovery VM di VMM devono essere distribuiti in un cluster di estensione in siti geograficamente separati. toodo questo:

1. Installazione di VMM in una macchina virtuale in un cluster di failover di Windows e selezionare hello opzione toorun hello server come a disponibilità elevata durante l'installazione.
2. istanza di SQL Server Hello che viene utilizzato da VMM deve essere replicato con gruppi di disponibilità AlwaysOn di SQL Server, in modo che vi sia una replica di database hello nel sito secondario hello.
3. Seguire le istruzioni hello questo toocreate articolo un insieme di credenziali, registrare il server di hello e impostare la protezione. È necessario tooregister ogni server VMM in hello cluster nel hello insieme di credenziali di servizi di ripristino. toodo, si installa hello Provider in un nodo attivo e registrare il server VMM hello. È quindi possibile installare Provider hello in altri nodi.
4. Quando si verifica un'interruzione, il server VMM hello e il database di SQL Server corrispondente sono il failover e accessibili dal sito secondario hello.



## <a name="prepare-for-storage-mapping"></a>Eseguire la preparazione per il mapping dell'archiviazione


È possibile impostare l'archiviazione mapping dal mapping classificazioni di archiviazione su un'origine e seguenti di hello toodo server VMM di destinazione:

  * **Identificare l'archiviazione di destinazione per le macchine virtuali di replica**: un disco rigido VM di origine verranno replicate archiviazione toohello specificato (condivisione SMB o cluster volumi condivisi (CSV)) nel percorso di destinazione hello.
  * **Posizionamento delle macchine virtuali di replica**: mapping di archiviazione è macchine virtuali di replica sul posto toooptimally utilizzato nei server host Hyper-V. Macchine virtuali di replica verrà essere posizionate in host che possono accedere hello mappato classificazione di archiviazione.
  * **Nessun mapping di archiviazione**, se non si configura il mapping di archiviazione, macchine virtuali saranno percorso di archiviazione replicata toohello predefinito specificato nel server host Hyper-V hello associata a una macchina virtuale di replica hello.

Si noti che:
- È possibile configurare il mapping tra due cloud VMM in un singolo server.
- Le classificazioni di archiviazione devono essere disponibile toohello gruppi di host presenti nei cloud di origine e di destinazione.
- Le classificazioni non devono toohave hello stesso tipo di archiviazione. Ad esempio, è possibile mappare una classificazione di origine che contiene la classificazione destinazione tooa di condivisioni SMB che contiene i volumi condivisi cluster.

### <a name="example"></a>Esempio
Se le classificazioni sono configurate correttamente in VMM quando si seleziona origine hello e il server VMM di destinazione durante il mapping di archiviazione, delle classificazioni di origine e destinazione hello verranno visualizzate. Di seguito è riportato un esempio di condivisioni di file di archiviazione e le classificazioni per un'organizzazione con due posizioni a New York e Chicago.

| **Posizione** | **Server VMM** | **Condivisione file (origine)** | **Classificazione (origine)** | **Mappata a** | **Condivisione file (destinazione)** |
| --- | --- | --- | --- | --- | --- |
| New York |VMM_Source |SourceShare1 |GOLD |GOLD_TARGET |TargetShare1 |
| SourceShare2 |SILVER |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRONZE |BRONZE_TARGET |TargetShare3 | | |
| Chicago |VMM_Target | |GOLD_TARGET |Non mappata | |
|  |SILVER_TARGET |Non mappata | | | |
|  |BRONZE_TARGET |Non mappata | | | |

Con questo esempio:

* Creazione di una macchina virtuale di replica per ogni macchina virtuale nell'archiviazione oro (SourceShare1), verrà replicata tooa GOLD_TARGET archiviazione (TargetShare1).
* Creazione di una macchina virtuale di replica per ogni macchina virtuale nell'archiviazione SILVER (SourceShare2), verrà è replicata tooa SILVER_TARGET (TargetShare2) di archiviazione e così via.

### <a name="multiple-storage-locations"></a>Posizioni di archiviazione multiple
Se la classificazione di destinazione hello viene assegnata alle condivisioni SMB toomultiple o volumi condivisi cluster, il percorso di archiviazione ottimale hello verrà selezionato automaticamente quando macchina virtuale hello è protetta. Se non è disponibile con archiviazione alcuna destinazione valida hello specificato classificazione, il valore predefinito di hello percorso di archiviazione specificato nell'host Hyper-V hello è usato tooplace hello replica i dischi rigidi virtuali.

Hello nella tabella seguente mostra come classificazione di archiviazione e volumi condivisi cluster sono configurati in questo esempio.

| **Posizione** | **Classificazione** | **Risorsa di archiviazione associata** |
| --- | --- | --- |
| New York |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| Chicago |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

Questa tabella riepiloga il comportamento di hello quando si abilita la protezione per le macchine virtuali (VM1 - VM5) in questo ambiente di esempio.

| **Macchina virtuale** | **Risorsa di archiviazione di origine** | **Classificazione di origine** | **Risorsa di archiviazione di destinazione mappata** |
| --- | --- | --- | --- |
| VM1 |C:\ClusterStorage\SourceVolume1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>Entrambi GOLD_TARGET</p> |
| VM2 |\\FileServer\SourceShare1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>Entrambi GOLD_TARGET</p> |
| VM3 |C:\ClusterStorage\SourceVolume2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| VM4 |\FileServer\SourceShare2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>Entrambi SILVER_TARGET</p> |
| VM5 |C:\ClusterStorage\SourceVolume3 |N/D |Nessun mapping, in modo hello posizione di archiviazione predefinita dell'host Hyper-V hello viene utilizzata |



### <a name="data-privacy-overview"></a>Panoramica sulla privacy dei dati

Questa tabella descrive come vengono riepilogati i dati in questo scenario:

- - -
| Azione | **Dettagli** | **Dati raccolti** | **Uso** | **Obbligatorio** |
| --- | --- | --- | --- | --- |
| **Registrazione** | Si registra un server VMM in un insieme di credenziali dei servizi di ripristino. Se in seguito si toounregister un server, è possibile farlo eliminando le informazioni sul server hello dal hello portale di Azure. | Dopo che un server VMM è registrato il ripristino del sito raccoglie, elabora e trasferisce i metadati relativi al server VMM hello e i nomi di hello dei cloud VMM hello rilevato da Site Recovery. | dati Hello tooidentify utilizzato e comunicano con il server VMM appropriato di hello e configurare le impostazioni per i cloud VMM appropriato. | Questa operazione è obbligatoria. Se non vuoi toosend questo tooSite informazioni ripristino è consigliabile utilizzare il servizio di Site Recovery hello. |
| **Abilitare la replica** | Hello Provider di Azure Site Recovery è installato nel server VMM hello ed è il canale hello per le comunicazioni con hello servizio Site Recovery. Hello Provider è una libreria di collegamento dinamico (DLL) ospitata nel processo VMM hello. Dopo aver hello che provider è installato, funzionalità "Datacenter Recovery" hello viene abilitata nella console di amministrazione VMM hello. Macchine virtuali nuove ed esistenti è possono abilitare questa protezione tooenable funzionalità per una macchina virtuale. |Questa proprietà è impostata, hello Provider invia hello nome e l'ID di hello VM tooSite ripristino.  La replica viene abilitata dalla tecnologia di replica Hyper-V disponibile in Windows Server 2012 o Windows Server 2012 R2. dati della macchina virtuale Hello vengono replicati da uno tooanother di host Hyper-V (in genere si trova in un data center di "ripristino" diverso). |Il ripristino del sito utilizza hello metadati toopopulate hello VM informazioni hello portale di Azure. | Questa funzionalità è una parte essenziale del servizio hello e non può essere disattivata. Se non si desiderano toosend queste informazioni, non abilitare la protezione di Site Recovery per le macchine virtuali. Si noti che tutti i dati inviati dal Provider di hello tooSite ripristino viene inviato su HTTPS. |
| **Piano di ripristino** | I piani di ripristino consentono di compilare un piano di orchestrazione del data center di ripristino hello. È possibile definire l'ordine di hello in cui le macchine virtuali o un gruppo di macchine virtuali deve essere avviato nel sito di ripristino hello. Inoltre, è possibile specificare qualsiasi toobe script automatizzati eseguire o toobe qualsiasi azione manuale al momento di hello del ripristino per ogni macchina virtuale. Il failover viene in genere attivato a livello di piano di ripristino di hello per un ripristino coordinato. | Il ripristino del sito raccoglie, elabora e trasmette i metadati per il piano di ripristino hello, inclusi i metadati della macchina virtuale e i metadati di qualsiasi script di automazione e note di azione manuale. |metadati Hello sono piano di ripristino utilizzato toobuild hello in hello portale di Azure. |Questa funzionalità è una parte essenziale del servizio hello e non può essere disattivata. Se non si desidera toosend questo tooSite informazioni ripristino, non creare piani di ripristino. |
| **Mapping di rete** | Esegue il mapping di rete le informazioni di hello data center toohello ripristino data center principale. Quando le macchine virtuali sono ripristinate presso il sito di ripristino di hello, mapping di rete consente di ristabilire la connettività di rete. |Il ripristino del sito raccoglie, elabora e trasmette i metadati di hello di reti logiche di hello per ogni sito (primario e Data Center). |metadati Hello sono toopopulate utilizzate le impostazioni di rete in modo che è possibile eseguire il mapping di informazioni di rete hello. | Questa funzionalità è una parte essenziale del servizio hello e non può essere disattivata. Se non si desidera toosend questo tooSite informazioni ripristino, non utilizzare il mapping di rete. |
| **Failover (pianificato/non pianificato/test)** | Il failover viene eseguito il failover le macchine virtuali da tooanother centro dati gestiti da VMM. azione di failover Hello viene attivata manualmente nel portale di Azure hello. |Hello Provider nel server VMM hello riceve una notifica di evento di failover hello tramite il ripristino del sito e viene eseguita un'azione di failover host Hyper-V hello tramite le interfacce VMM. Failover effettivo di una macchina virtuale si trova in uno tooanother di host Hyper-V e gestito da Windows Server 2012 o Windows Server 2012 R2 Hyper-V Replica. Il ripristino del sito posteriore utilizza le informazioni di hello inviate le informazioni sull'azione di failover hello stato hello toopopulate nel portale di Azure hello. | Questa funzionalità è una parte essenziale del servizio hello e non può essere disattivata. Se non si desidera toosend questo tooSite informazioni ripristino, non utilizzare il failover. |

## <a name="next-steps"></a>Passaggi successivi

Dopo aver testato distribuzione hello, ulteriori informazioni su altri tipi di [failover](site-recovery-failover.md)
