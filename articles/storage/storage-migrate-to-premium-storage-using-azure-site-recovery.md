---
title: aaaMigrating tooAzure archiviazione Premium con Azure Site Recovery | Documenti Microsoft
description: Eseguire la migrazione del tooAzure macchine virtuali esistenti di archiviazione Premium utilizzando il ripristino del sito. Archiviazione Premium offre prestazioni elevate e supporto per dischi a bassa latenza per carichi di lavoro con I/O intensivo in esecuzione su Macchine virtuali di Azure.
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: luywang
ms.openlocfilehash: cb71c06e4a1a73d484e226a573d1ade48c87664d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery"></a>Migrazione tooPremium archiviazione usando Azure Site Recovery

[Archiviazione Premium di Azure](storage-premium-storage.md) offre prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali (VM) che eseguono carichi di lavoro con I/O intensivo. scopo di Hello di questa guida è toohelp utenti eseguire la migrazione dei dischi di macchina virtuale da un tooa di account di archiviazione Standard account di archiviazione Premium con [Azure Site Recovery](../site-recovery/site-recovery-overview.md).

Il ripristino del sito è un servizio di Azure che contribuisce tooyour continuità aziendale e hello di strategia di ripristino di emergenza gestendo la replica dei server fisici locali e macchine virtuali toohello cloud (Azure) o Data Center secondario tooa. Quando si verificano interruzioni nella propria posizione primaria, è possibile failover applicazioni tookeep di toohello posizione secondaria e i carichi di lavoro disponibili. Non si posizione primaria tooyour indietro al momento della restituzione toonormal operazione. Site Recovery fornisce esercitazioni di ripristino di emergenza toosupport i test failover senza influire su ambienti di produzione. È possibile eseguire failover con perdite di dati minime (a seconda della frequenza di replica) per emergenze impreviste. In uno scenario di hello di migrazione tooPremium archiviazione, è possibile utilizzare hello [il Failover di Site Recovery](../site-recovery/site-recovery-failover.md) in Azure Site Recovery toomigrate destinazione dischi tooa account di archiviazione Premium.

È consigliabile eseguire la migrazione tooPremium archiviazione tramite il ripristino del sito, perché questa opzione offre tempi di inattività minimi ed evita l'esecuzione manuale di hello di copia dei dischi e la creazione di nuove macchine virtuali. Site Recovery copierà in modo sistematico i dischi e creerà le nuove VM durante il failover. Site Recovery supporta diversi tipi di failover con un tempo di inattività minimo o inesistente. tooplan i tempi di inattività e stima la perdita di dati, vedere hello [tipi di failover](../site-recovery/site-recovery-failover.md) tabella in Site Recovery. Se si [preparare tooconnect tooAzure VM dopo il failover](../site-recovery/site-recovery-vmware-to-azure.md), dovrebbe essere in grado di tooconnect toohello macchina virtuale di Azure utilizzano il protocollo RDP dopo il failover.

![][1]

## <a name="azure-site-recovery-components"></a>Componenti di Azure Site Recovery

Questi sono i componenti di Site Recovery hello che sono rilevanti toothis uno scenario di migrazione.

* Un **Server di configurazione** è una VM di Azure che coordina le comunicazioni e gestisce i processi di ripristino e replica dei dati. In questa macchina virtuale verrà eseguito un server di configurazione di hello tooinstall di file di installazione a file singolo e un componente aggiuntivo, chiamata di un server di elaborazione, come un gateway di replica. Vedere le informazioni sui [prerequisiti del server di configurazione](../site-recovery/site-recovery-vmware-to-azure.md). Server di configurazione solo deve toobe configurati una volta e può essere utilizzato per tutte le migrazioni toohello stessa area.

* **Server di elaborazione** è Ottimizza hello dati con la memorizzazione nella cache, la compressione e crittografia, un gateway di replica che riceve i dati di replica da macchine virtuali di origine e lo invia tooa account di archiviazione. Inoltre, gestisce l'installazione push del toosource servizio di mobilità hello macchine virtuali e consente di eseguire l'individuazione automatica delle macchine virtuali di origine. server di elaborazione predefinita Hello è installato nel server di configurazione hello. È possibile distribuire autonomi aggiuntivi processo server tooscale la distribuzione. Vedere le informazioni sulle [procedure consigliate per la distribuzione del server di elaborazione](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) e sulla [distribuzione di server di elaborazione aggiuntivi](../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). Server di elaborazione è solo necessario toobe configurati una volta e può essere utilizzato per tutte le migrazioni toohello stessa area.

* **Servizio di mobilità** è un componente che viene distribuito in ogni VM standard desiderato tooreplicate. Vengono illustrate le operazioni di scrittura dati hello standard per VM e li inoltra toohello server di elaborazione. Vedere le informazioni sui [prerequisiti dei computer replicati](../site-recovery/site-recovery-vmware-to-azure.md).

Il grafico seguente mostra l'interazione tra questi componenti.

![][15]

> [!NOTE]
> Il ripristino del sito non supporta la migrazione di hello di dischi di spazi di archiviazione.

Per i componenti aggiuntivi per altri scenari, vedere troppo[architettura dello Scenario](../site-recovery/site-recovery-vmware-to-azure.md).

## <a name="azure-essentials"></a>Informazioni di base su Azure

Questi sono hello Azure requisiti per questo scenario di migrazione.

* Una sottoscrizione di Azure.
* Un toostore di account di archiviazione Premium di Azure i dati replicati.
* Un toowhich di rete virtuale di Azure (VNet), le macchine virtuali si connetterà quando vengono creati in caso di failover. Hello rete virtuale di Azure deve essere hello stessa area come hello uno in cui hello viene eseguito il ripristino del sito
* Un account di archiviazione Azure Standard in cui toostore i log di replica. Può trattarsi di hello stesso account di archiviazione come dischi di VM hello viene eseguita la migrazione

## <a name="prerequisites"></a>Prerequisiti

* Comprendere i componenti di scenario di migrazione rilevanti hello nella precedente sezione hello
* Pianificare il tempo di inattività da learning relativi hello [il Failover di Site Recovery](../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Passaggi di configurazione e migrazione

È possibile utilizzare il ripristino del sito toomigrate le macchine virtuali IaaS di Azure tra le aree o stessa area. Hello istruzioni seguenti sono state adattate per questo scenario di migrazione dall'articolo hello [replicare le macchine virtuali VMware o i server fisici tooAzure](../site-recovery/site-recovery-vmware-to-azure.md). Seguire i collegamenti di hello per i passaggi dettagliati in istruzioni toohello aggiuntivi in questo articolo.

1. **Creare un insieme di credenziali di Servizi di ripristino**. Creare e gestire l'insieme di credenziali di Site Recovery hello tramite hello [portale di Azure](https://portal.azure.com). Fare clic su **Nuovo** > **Gestione** > **Backup** e **Site Recovery (OMS)**. In alternativa, è possibile fare clic su **Sfoglia** > **Insieme di credenziali dei servizi di ripristino** > **Aggiungi**. Macchine virtuali saranno replicate toohello area specificati in questo passaggio. Ai fini di hello della migrazione in hello stessa area, hello selezionare area geografica in cui le macchine virtuali di origine e di un account di archiviazione di origine. Si noti che gli account di archiviazione di migrazione tooPremium è supportato solo in hello [portale di Azure](https://portal.azure.com), non hello [portale classico](https://manage.windowsazure.com).

2. Hello passaggi seguenti consentono di **scegliere gli obiettivi di protezione**.

    2a. Nella macchina virtuale in cui si desidera che server di configurazione hello tooinstall hello, aprire hello [portale di Azure](https://portal.azure.com). Andare troppo**insiemi di credenziali di servizi di ripristino** > **impostazioni**. In **Impostazioni** selezionare **Site Recovery**. In **Site Recovery** selezionare **Passaggio 1: Preparare l'infrastruttura**. In **Preparare l'infrastruttura** selezionare **Obiettivo di protezione**.

    ![][2]

    2b. In **obiettivi della protezione dati**in hello primo elenco a discesa, selezionare **tooAzure**. Nell'elenco a discesa secondo hello, selezionare **non virtualizzato / altri**, quindi fare clic su **OK**.

    ![][3]

3. Hello passaggi seguenti consentono di **configurare un ambiente di origine hello (server di configurazione)**.

    3a. Scaricare hello **installazione unificata di Azure Site Recovery** hello e **chiave di registrazione dell'insieme di credenziali** da passare toohello **Prepare infrastruttura**  >  **Origine Prepare** > **Aggiungi Server** blade. Sarà necessario hello impostazione hello unificata toorun chiave di registrazione dell'insieme di credenziali. chiave Hello è valido per 5 giorni dopo la generazione è.

    ![][4]

    3b. Aggiungere il Server di configurazione in hello **Aggiungi Server** blade.

    ![][5]

    3c. Nella macchina virtuale in uso come server di configurazione hello hello, eseguire il programma di installazione unificata tooinstall hello configurazione server e server di elaborazione hello. È possibile scorrere hello schermate [qui](../site-recovery/site-recovery-vmware-to-azure.md) installazione hello toocomplete. È possibile fare riferimento toohello seguente schermate per i passaggi specificati per questo scenario di migrazione.

    In **prima di iniziare**selezionare **installare server di configurazione hello e server di elaborazione**.

    ![][6]

    3d. In **registrazione**, individuare e selezionare la chiave di registrazione hello scaricato dall'insieme di credenziali hello.

    ![][7]

    3e. In **dettagli sull'ambiente**selezionare se si ha intenzione di macchine virtuali VMware tooreplicate. Per questo scenario di migrazione, scegliere **No**.

    ![][8]

    3f. Al termine dell'installazione di hello, verrà visualizzato hello **Microsoft Azure Site Recovery configurazione Server** finestra. Utilizzare hello **Gestisci account** scheda account hello toocreate che il ripristino del sito è possibile utilizzare per l'individuazione automatica. (In uno scenario di hello sulla protezione di computer fisici, impostazione hello account non è rilevante, ma è necessario almeno un tooenable account uno di hello alla procedura seguente. In questo caso, è possibile assegnare un nome account hello e una password come qualsiasi.) Hello utilizzare **registrazione insieme credenziali** file delle credenziali dell'insieme di credenziali hello tooupload scheda.

    ![][9]

4. **Configurare un ambiente di destinazione hello**. Fare clic su **Prepare infrastruttura** > **destinazione**e specificare il modello di distribuzione hello desiderato toouse per le macchine virtuali dopo il failover. È possibile scegliere **Classica** o **Resource Manager**, a seconda dello scenario.

    ![][10]

    Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili. Si noti che se si utilizza un account di archiviazione Premium per i dati replicati, è necessario tooset la replica di toostore account un ulteriore spazio di archiviazione Standard registri.

5. **Configurare le impostazioni di replica**. Seguire [configurare le impostazioni di replica](../site-recovery/site-recovery-vmware-to-azure.md) tooverify che il server di configurazione è correttamente associato al criterio di replica hello creato.

6. **Pianificazione della capacità**. Hello utilizzare [strumento capacity planner](../site-recovery/site-recovery-capacity-planner.md) tooaccurately di stima di larghezza di banda, archiviazione e altri requisiti toomeet richiede la replica. Al termine scegliere **Sì** in **È stata completata la pianificazione della capacità?**

    ![][11]

7. Hello passaggi seguenti consentono di **installare il servizio di mobilità e abilitare la replica**.

    7a. È possibile scegliere troppo[l'installazione push](../site-recovery/site-recovery-vmware-to-azure.md) tooyour origine macchine virtuali o troppo[installare manualmente il servizio mobility](../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) in macchine virtuali di origine. È possibile trovare il requisito di hello dell'installazione push e il percorso di hello del programma di installazione manuale di hello in hello collegamento fornito. Se si sta eseguendo un'installazione manuale, si potrebbe essere necessario toouse IP indirizzo toofind hello configurazione server interno.

    ![][12]

    Hello failover macchina virtuale avrà due dischi temporanei: uno dal hello primario macchina virtuale e hello altri creato durante il provisioning della macchina virtuale nell'area di ripristino hello hello. disco temporaneo di hello tooexclude prima che la replica, installare il servizio di mobilità hello prima di abilitare la replica. toolearn ulteriori informazioni su come tooexclude hello disco temporaneo, vedere troppo[Escludi dischi dalla replica](../site-recovery/site-recovery-vmware-to-azure.md).

    7b. Per abilitare la replica, procedere come descritto di seguito.
      * Fare clic su **Eseguire la replica dell'applicazione** > **Origine**. Dopo aver abilitato la replica per hello prima volta, fare clic su + replica nella replica di tooenable hello insieme di credenziali per le macchine aggiuntive.
      * Nel passaggio 1 configurare l'origine come server di elaborazione.
      * Nel passaggio 2, specificare modello di distribuzione dopo il failover hello, un toomigrate di account di archiviazione Premium a, un log toosave dell'account di archiviazione Standard e toofail una rete virtuale per.
      * Nel passaggio 3, aggiungere macchine virtuali protette in base all'indirizzo IP (potrebbe essere necessario un toofind di indirizzo IP interno li).
      * Nel passaggio 4, configurare le proprietà di hello selezionando hello account impostati in precedenza nel server di elaborazione hello.
      * Nel passaggio 5, scegliere il criterio di replica hello creato in precedenza, configurare le impostazioni di replica.
      Fare clic su **OK** e abilitare la replica.

    > [!NOTE]
    > Quando una macchina virtuale di Azure viene deallocata e avviata di nuovo, non c'è garanzia che riceverà hello stesso indirizzo IP. Se l'indirizzo IP di hello del server di server o il processo di configurazione hello o hello protetto modifica di macchine virtuali di Azure, la replica di hello in questo scenario potrebbe non funzionare correttamente.

    ![][13]

    Quando si progetta l'ambiente di Archiviazione di Azure, è consigliabile usare account di archiviazione distinti per ogni VM in un set di disponibilità. È consigliabile seguire hello consigliata per il livello di archiviazione hello troppo[utilizzare più account di archiviazione per ogni set di disponibilità](../virtual-machines/windows/manage-availability.md). Distribuire gli account di archiviazione toomultiple dischi di macchina virtuale consente la disponibilità di archiviazione tooimprove e distribuisce i/o hello attraverso l'infrastruttura di archiviazione di Azure hello. Se le macchine virtuali si trovano in un set di disponibilità, anziché replicare i dischi di tutte le macchine virtuali in un account di archiviazione, è consigliabile eseguire la migrazione di più macchine virtuali più volte, in modo che le macchine virtuali hello in hello stesso set di disponibilità non condividono un singolo account di archiviazione. Hello utilizzare **Abilita replica** tooset blade di un account di archiviazione di destinazione per ogni macchina virtuale, uno alla volta. È possibile scegliere un modello di distribuzione dopo il failover in base tooyour necessità. Se si sceglie il gestore di risorse (RM) come il modello di distribuzione dopo il failover, è possibile eseguire il failover tooan una VM RM VM RM oppure è possibile eseguire il failover un classico tooan VM RM VM.

8. **Eseguire un failover di test**. Se la replica è stata completata, fare clic sul ripristino del sito e quindi fare clic su toocheck **impostazioni** > **elementi replicati**. Verrà visualizzato lo stato di hello e la percentuale del processo di replica. Dopo la replica iniziale è toovalidate di Failover di Test completo, eseguire la strategia di replica. Per informazioni dettagliate di failover di test, fare riferimento troppo[eseguire un failover di test in Site Recovery](../site-recovery/site-recovery-vmware-to-azure.md). È possibile visualizzare lo stato di hello di failover di test in **impostazioni** > **processi** > **YOUR_FAILOVER_PLAN_NAME**. Nel Pannello di hello, verrà visualizzato un riepilogo dei passaggi di hello e i risultati di esito positivo o negativo. Se il failover di test hello non riesce in qualsiasi fase, fare clic su messaggio di errore hello toocheck hello passaggio. Verificare che le macchine virtuali e la strategia di replica requisiti hello prima di eseguire un failover. Lettura [tooAzure di Failover di Test in Site Recovery](../site-recovery/site-recovery-test-failover-to-azure.md) per ulteriori informazioni e istruzioni di failover di test.

9. **Eseguire un failover**. Dopo aver completato il failover di test hello, eseguire un failover toomigrate l'archiviazione di tooPremium dischi e replicare le istanze di VM hello. Seguire hello dettagliate passaggi [eseguire un failover](../site-recovery/site-recovery-failover.md#run-a-failover). Assicurarsi di selezionare **arrestare le macchine virtuali e sincronizzare i dati più recenti di hello** toospecify che il ripristino del sito deve provare tooshut verso il basso le macchine virtuali protetta hello e sincronizzare i dati di hello in modo che hello versione più recente dei dati hello verrà eseguito il failover. Se non si seleziona questa opzione o hello tentativo non riesce hello failover sarà dal punto di ripristino disponibile più recente di hello per hello macchina virtuale. Il ripristino del sito verrà creata un'istanza di macchina virtuale il cui tipo è hello uguale o simile tooa VM con supporto archiviazione Premium. È possibile controllare le prestazioni di hello e il prezzo di diverse istanze di macchina virtuale passando troppo[dei prezzi delle macchine virtuali Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) o [dei prezzi delle macchine virtuali Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Passaggi post-migrazione

1. **Configurare la disponibilità di toohello macchine virtuali replicate impostare eventualmente**. Il ripristino del sito non supporta la migrazione macchine virtuali insieme ai set di disponibilità hello. A seconda della distribuzione di hello della macchina virtuale replicata, effettuare una delle seguenti hello:
  * Per una macchina virtuale creata utilizzando il modello di distribuzione classica hello: aggiungere hello VM toohello set di disponibilità in hello portale di Azure. Per informazioni dettagliate, visitare troppo[aggiungere un set di disponibilità tooan macchina virtuale esistente](../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Per il modello di distribuzione di gestione risorse hello: salvare la configurazione di hello macchina virtuale e quindi eliminare e ricreare le macchine virtuali hello in set di disponibilità hello. toodo in tal caso, utilizzare uno script di hello al [impostare Azure Resource Manager VM Set di disponibilità](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Controllare la limitazione di hello di questo script e pianificare i tempi di inattività prima di eseguire script hello.

2. **Eliminare le VM e i dischi precedenti**. Prima di eliminare queste, verificare che i dischi Premium hello siano coerenti con hello che Hello stessa funzione come origine hello macchine virtuali di eseguire nuove macchine virtuali e i dischi di origine. Nel modello di distribuzione di gestione risorse (RM) hello, eliminare hello VM ed eliminare dischi hello dagli account di archiviazione di origine in hello portale di Azure. Nel modello di distribuzione classica hello, è possibile eliminare hello VM e i dischi nel portale classico hello o il portale di Azure. Se si verifica un problema in cui hello disco non viene eliminato anche se è stata eliminata hello macchina virtuale, consultare [risolvere gli errori quando si eliminano i dischi rigidi virtuali](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Infrastruttura di Azure Site Recovery hello pulita**. Se il ripristino del sito non è più necessario, è possibile rimuovere l'infrastruttura eliminando gli elementi replicati, il server di configurazione di hello e hello criteri di recupero, e quindi eliminando l'insieme di credenziali di Azure Site Recovery hello.

## <a name="troubleshooting"></a>Risoluzione dei problemi

* [Monitorare e risolvere i problemi di protezione per le macchine virtuali e i server fisici](../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Forum di Microsoft Azure Site Recovery](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Passaggi successivi

Vedere hello risorse per scenari specifici per la migrazione di macchine virtuale seguenti:

* [Eseguire la migrazione di macchine virtuali di Azure tra account di archiviazione](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Creare e caricare tooAzure un disco rigido virtuale di Windows Server.](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Creazione e caricamento di un disco rigido virtuale contenente hello del sistema operativo Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migrazione di macchine virtuali da Amazon AWS tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Vedere anche hello seguenti risorse toolearn ulteriori informazioni sull'archiviazione di Azure e macchine virtuali di Azure:

* [Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
