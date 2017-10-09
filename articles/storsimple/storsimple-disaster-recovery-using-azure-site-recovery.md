---
title: condivisione file StorSimple aaaAutomate ripristino di emergenza con Azure Site Recovery | Documenti Microsoft
description: Descrive i passaggi di hello e procedure consigliate per la creazione di una soluzione di ripristino di emergenza per le condivisioni file ospitati in archiviazione di Microsoft Azure StorSimple.
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 23049a2c-055e-4d0e-b8f5-af2a87ecf53f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/09/2017
ms.author: vidarmsft
ms.openlocfilehash: fa3e8d4e77ca0f6a7b5f9bbb956a4de12547642e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-disaster-recovery-solution-using-azure-site-recovery-for-file-shares-hosted-on-storsimple"></a>Soluzione di ripristino di emergenza automatizzato usando Azure Site Recovery per le condivisioni file ospitate su StorSimple
## <a name="overview"></a>Panoramica
Microsoft Azure StorSimple è una soluzione di archiviazione cloud ibrida che indirizzi hello complessità dei dati non strutturati generalmente associati a condivisioni file. StorSimple utilizza l'archiviazione cloud come soluzione locale di un'estensione di hello e livelli automaticamente i dati tra l'archiviazione locale e l'archiviazione cloud. Integrati, protezione dei dati locali e gli snapshot nel cloud, evitando hello un'infrastruttura di archiviazione ha.

[Azure Site Recovery](../site-recovery/site-recovery-overview.md) è un servizio basato su Azure che fornisce funzionalità di ripristino di emergenza per il coordinamento di replica, failover e ripristino delle macchine virtuali. Azure Site Recovery supporta un numero di replicare tooconsistently tecnologie di replica, proteggere e facilmente il failover le macchine virtuali e le applicazioni cloud tooprivate/pubblico o ospitato.

Tramite Azure Site Recovery, la replica della macchina virtuale e funzionalità di snapshot cloud StorSimple, è possibile proteggere l'ambiente di server completo del file hello. In caso di hello di un'interruzione, è possibile utilizzare un solo clic toobring le condivisioni di file online in Azure in pochi minuti.

Questo documento illustra in dettaglio come creare una soluzione di ripristino di emergenza per le condivisioni file ospitate nell'archiviazione di StorSimple ed eseguire failover pianificati, non pianificati e di test usando un piano di ripristino con un solo clic. In pratica, viene illustrato come è possibile modificare il piano di ripristino hello il tooenable insieme di credenziali di Azure Site Recovery StorSimple failover durante gli scenari di emergenza. Inoltre, descrive le configurazioni supportate e i prerequisiti. Questo documento presuppone che si abbia familiarità con concetti di base di hello di architetture di Azure Site Recovery e StorSimple.

## <a name="supported-azure-site-recovery-deployment-options"></a>Opzioni di distribuzione di Azure Site Recovery
I clienti possono distribuire file server come server fisici o macchine virtuali (VM) in esecuzione in Hyper-V o VMware e quindi creare le condivisioni file da volumi ottenuti dall'archiviazione StorSimple. Azure Site Recovery può proteggere entrambi tooeither distribuzioni fisici e virtuali a un sito secondario o tooAzure. Questo documento vengono illustrati i dettagli di una soluzione di ripristino di emergenza con Azure come sito di ripristino hello per un macchina virtuale ospitata in Hyper-V di file server e condivisioni di file in archiviazione di StorSimple. Altri scenari in cui hello file server di che macchina virtuale si trova in una VM di VMware o da un computer fisico possono essere implementati in modo analogo.

## <a name="prerequisites"></a>Prerequisiti
Implementazione di una soluzione di ripristino di emergenza con un clic che utilizza Azure Site Recovery per le condivisioni file ospitate in StorSimple archiviazione ha hello seguenti prerequisiti:

* VM del file server Windows Server 2012 R2 locale ospitata in Hyper-V, VMware o in un computer fisico
* Dispositivo di archiviazione StorSimple locale registrato con Azure StorSimple Manager
* StorSimple Appliance di Cloud create in hello Azure StorSimple manager (questo può rimanere in stato di arresto)
* Condivisioni file ospitate in volumi hello configurati nel dispositivo di archiviazione StorSimple hello
* [insieme di credenziali dei servizi di Azure Site Recovery](../site-recovery/site-recovery-vmm-to-vmm.md) creato in una sottoscrizione di Microsoft Azure

Inoltre, se Azure è il sito di ripristino, eseguire hello [dello strumento di valutazione della macchina virtuale Azure](http://azure.microsoft.com/downloads/vm-readiness-assessment/) su tooensure macchine virtuali che siano compatibili con macchine virtuali di Azure e Azure Site Recovery services.

problemi di latenza tooavoid (cosa che può comportare costi più elevati), assicurarsi che si crea il dispositivo StorSimple per Cloud, account di automazione, e degli account di archiviazione nella stessa regione di hello.

## <a name="enable-dr-for-storsimple-file-shares"></a>Abilitare il ripristino di emergenza per le condivisioni file di StorSimple
Ogni componente di hello locale ambiente deve toobe protetti tooenable completare la replica e il ripristino. Questa sezione illustra come:

* Configurare la replica di Active Directory e DNS (facoltativo)
* Utilizzare la protezione di Azure Site Recovery tooenable hello del file server di VM
* Abilitare la protezione dei volumi StorSimple
* Configurare la rete hello

### <a name="set-up-active-directory-and-dns-replication-optional"></a>Configurare la replica di Active Directory e DNS (facoltativo)
Se si desidera hello tooprotect computer che eseguono Active Directory e DNS in modo che siano disponibili nel sito di ripristino di emergenza hello, è necessario tooexplicitly proteggerli (in modo che i server di file hello sono accessibili dopo il failover con l'autenticazione). Sono disponibili due opzioni consigliate in base hello complessità dell'ambiente locale del cliente hello.

#### <a name="option-1"></a>Opzione 1
Se il cliente hello dispone di un numero ridotto di applicazioni, un singolo controller di dominio per intero hello sito locale e sarà possibile failover hello dell'intero sito, quindi è consigliabile utilizzare macchina controller di dominio di Azure Site Recovery replica tooreplicate hello sito secondario tooa (questa opzione è disponibile per site-to-site e site in Azure).

#### <a name="option-2"></a>Opzione 2
Se hello cliente ha un numero elevato di applicazioni, è in esecuzione una foresta di Active Directory e sarà possibile failover alcune applicazioni alla volta, quindi è consigliabile configurare un controller di dominio nel sito di ripristino di emergenza hello (è possibile che un sito secondario o in Azure).

Consultare troppo[soluzione di ripristino di emergenza automatizzata per Active Directory e DNS usando Azure Site Recovery](../site-recovery/site-recovery-active-directory.md) per le istruzioni quando si rende disponibile un controller di dominio nel sito di ripristino di emergenza hello. Resto hello di questo documento, si suppone che un controller di dominio è disponibile nel sito di ripristino di emergenza hello.

### <a name="use-azure-site-recovery-tooenable-protection-of-hello-file-server-vm"></a>Utilizzare la protezione di Azure Site Recovery tooenable hello del file server di VM
Questo passaggio è necessario preparare l'ambiente hello locale file server, creare e preparare un insieme di credenziali di Azure Site Recovery e abilitare la protezione dei file di hello macchina virtuale.

#### <a name="tooprepare-hello-on-premises-file-server-environment"></a>ambiente tooprepare hello locale file server
1. Set hello **controllo dell'Account utente** troppo**non notificare mai**. Ciò è necessario in modo che è possibile utilizzare destinazioni iSCSI di automazione di Azure script tooconnect hello dopo carico da Azure Site Recovery.

   1. Premere tasto Windows hello + Q e cercare **UAC**.
   2. Selezionare **Modifica impostazioni di Controllo dell'account utente**.
   3. Hello trascinare barra inferiore toohello verso **non notificare mai**.
   4. Fare clic su **OK**, quindi selezionare **Sì** quando richiesto.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image1.png)
2. Installare hello agente VM in ciascuno dei server file hello macchine virtuali. Ciò è necessario in modo che sia possibile eseguire gli script di automazione di Azure su hello failover le macchine virtuali.

   1. [Scaricare l'agente di hello](http://aka.ms/vmagentwin) troppo`C:\\Users\\<username>\\Downloads`.
   2. Aprire Windows PowerShell in modalità amministratore (Esegui come amministratore) e quindi immettere hello comando toonavigate toohello download percorso seguente:

      `cd C:\\Users\\<username>\\Downloads\\WindowsAzureVmAgent.2.6.1198.718.rd\_art\_stable.150415-1739.fre.msi`

      > [!NOTE]
      > a seconda della versione di hello può modificare il nome di file Hello.
      >
      >
3. Fare clic su **Avanti**.
4. Accettare hello **termini del contratto** e quindi fare clic su **Avanti**.
5. Fare clic su **Finish**.
6. Creare condivisioni file usando volumi ottenuti dall'archiviazione StorSimple. Per ulteriori informazioni, vedere [utilizzare volumi toomanage servizio StorSimple Manager di hello](storsimple-manage-volumes.md).

   1. Le macchine virtuali in locale, premere tasto Windows hello + Q e cercare **iSCSI**.
   2. Selezionare **Iniziatore iSCSI**.
   3. Seleziona hello **configurazione** scheda e copia nome iniziatore hello.
   4. Accedi toohello [portale di Azure](https://portal.azure.com/).
   5. Seleziona hello **StorSimple** scheda e quindi selezionare hello servizio StorSimple Manager che contiene il dispositivo fisico di hello.
   6. Creare i contenitori di volumi e quindi creare i volumi (Questi volumi sono per condivisioni file hello hello in file server in macchine virtuali). Copia nome iniziatore hello e assegnare un nome appropriato per hello record di controllo di accesso quando si creano volumi hello.
   7. Seleziona hello **configura** scheda e annotare l'indirizzo IP di hello del dispositivo hello.
   8. Nelle macchine virtuali in locale, passare toohello **iniziatore iSCSI** nuovamente e immettere l'indirizzo IP di hello in hello sezione connessione rapida. Fare clic su **connessione rapida** (dispositivo hello dovrebbe ora essere connesso).
   9. Hello aprirlo portale di Azure e seleziona hello **volumi e dispositivi** scheda. Fare clic su **Configura automaticamente**. volume Hello appena creato dovrebbe essere visualizzato.
   10. Nel portale di hello selezionare hello **dispositivi** e quindi selezionare **crea un nuovo dispositivo virtuale.** (il dispositivo virtuale verrà usato se si verifica un failover). Questo nuovo dispositivo virtuale può essere mantenuto in un stato non in linea di tooavoid costi aggiuntivi. tootake hello dispositivo virtuale non in linea, andare toohello **macchine virtuali** sezione portale hello e arrestarlo.
   11. Tornare indietro toohello macchine virtuali in locale e aprire Gestione disco (premere tasto Windows hello + X e selezionare **Gestione disco**).
   12. Si noterà che alcuni dischi aggiuntivi (in base a numero hello di volumi creati). Fare clic su hello prima di selezionare **Inizializza disco**e selezionare **OK**. Pulsante destro del mouse hello **non allocata** selezionare **nuovo Volume semplice**, assegnarvi una lettera di unità e completare la procedura guidata hello.
   13. Ripetere il passaggio l per tutti i dischi di hello. È ora possibile visualizzare tutti i dischi di hello in **questo PC** in Esplora risorse di Windows hello.
   14. In questi volumi, utilizzare hello servizi File e archiviazione ruolo toocreate condivisioni file.

#### <a name="toocreate-and-prepare-an-azure-site-recovery-vault"></a>toocreate e preparare un insieme di credenziali di Azure Site Recovery
Fare riferimento toohello [documentazione di Azure Site Recovery](../site-recovery/site-recovery-hyper-v-site-to-azure.md) tooget iniziali di Azure Site Recovery prima di proteggere una macchina virtuale del server file hello.

#### <a name="tooenable-protection"></a>protezione tooenable
1. Disconnettere hello iSCSI target da hello locale macchine virtuali che si desidera tooprotect tramite Azure Site Recovery:

   1. Premere il tasto Windows + Q e cercare **iSCSI**.
   2. Selezionare **Configura iniziatore iSCSI**.
   3. Disconnettere i dispositivi StorSimple hello connessa in precedenza. In alternativa, è possibile disattivare server file hello per alcuni minuti durante l'abilitazione della protezione.

   > [!NOTE]
   > In questo modo hello toobe condivisioni di file temporaneamente non disponibile.
   >
   >
2. [Abilitare la protezione della macchina virtuale](../site-recovery/site-recovery-hyper-v-site-to-azure.md) del file server hello macchina virtuale dal portale di Azure Site Recovery hello.
3. Quando inizia la sincronizzazione iniziale di hello, è possibile riconnettersi destinazione hello nuovamente. Passare l'iniziatore iSCSI toohello, selezionare il dispositivo di StorSimple hello e fare clic su **Connetti**.
4. Quando è stata completata la sincronizzazione di hello e stato hello di hello VM è **Protected**selezionare hello macchina virtuale, selezionare hello **configura** scheda e aggiornare di conseguenza rete hello di hello VM (questa è la rete hello tale hello failover nelle macchine virtuali sarà parte). Rete hello non viene visualizzato, significa che la sincronizzazione hello continua.

### <a name="enable-protection-of-storsimple-volumes"></a>Abilitare la protezione dei volumi StorSimple
Se non è stato selezionato hello **abilitare un backup predefinito per questo volume** opzione per i volumi StorSimple hello, andare troppo**criteri di Backup** in hello servizio StorSimple Manager, quindi creare un backup adeguato criteri per tutti i volumi di hello. È consigliabile impostare la frequenza di hello dell'obiettivo del punto di backup toohello ripristino (RPO) che si desidera toosee per un'applicazione hello.

### <a name="configure-hello-network"></a>Configurare la rete hello
Per la macchina virtuale del server file hello, configurare le impostazioni di rete in Azure Site Recovery in modo che le reti VM hello siano collegati toohello corretto ripristino di emergenza rete dopo il failover.

È possibile selezionare hello VM hello **gli elementi replicati** scheda Impostazioni di rete hello tooconfigure, come illustrato nella seguente figura hello.

![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image2.png)

## <a name="create-a-recovery-plan"></a>Creare un piano di ripristino
È possibile creare un piano di ripristino nel processo di ripristino automatico di sistema tooautomate hello failover delle condivisioni file hello. Se si verifica un'interruzione, è possibile visualizzare le condivisioni file hello in pochi minuti con un semplice clic. tooenable l'automazione, è necessario un account di automazione di Azure.

#### <a name="toocreate-an-automation-account"></a>toocreate un account di automazione
1. Passare toohello portale di Azure &gt; **automazione** sezione.
2. Fare clic sul pulsante **+ Aggiungi** e viene aperto il pannello sotto.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image11.png)

   * Nome: immettere un nuovo account di automazione
   * Sottoscrizione: scegliere la sottoscrizione
   * Gruppo di risorse: creare un nuovo gruppo di risorse o sceglierne uno esistente
   * Posizione - Scegli percorso, mantenerla in hello stessa area geografica/area geografica in cui hello StorSimple Appliance di Cloud e account di archiviazione sono stati creati.
   * Creare un account RunAs di Azure: selezionare l'opzione **Sì**.

3. Account di automazione toohello, quindi scegliere **runbook** &gt; **Sfoglia raccolta** tooimport tutti hello necessari runbook nell'account di automazione hello.
4. Aggiungere hello seguente runbook individuando **il ripristino di emergenza** tag nella raccolta hello:

   * Eliminare i volumi StorSimple dopo il failover di test
   * Eseguire il failover dei contenitori dei volumi StorSimple
   * Montare i volumi nel dispositivo StorSimple dopo il failover
   * Disinstallare l'estensione script personalizzata in una VM di Azure
   * Avviare l'appliance virtuale StorSimple

     ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image3.png)

5. Pubblicare tutti gli script hello selezionando hello runbook nell'account di automazione hello e fare clic su **modifica** &gt; **pubblica** e quindi **Sì** toohello verifica Messaggio. Dopo questo passaggio, hello **runbook** scheda verrà visualizzata come indicato di seguito:

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image4.png)

6. Nell'account di automazione hello, selezionare hello **asset** scheda &gt; fare clic su **variabili** &gt; **aggiungere una variabile** e aggiungere hello seguenti variabili. È possibile scegliere tooencrypt queste risorse. Queste variabili sono specifiche del piano di ripristino. Se il ripristino prevede (che verrà creata nel passaggio successivo hello) è denominato piano di verifica, quindi le variabili devono essere StorSimRegKey di piano di verifica, piano di verifica AzureSubscriptionName e così via.

   * *RecoveryPlanName***- StorSimRegKey**: chiave di registrazione hello per hello servizio StorSimple Manager.
   * *RecoveryPlanName***- AzureSubscriptionName**: nome hello di hello sottoscrizione di Azure.
   * *RecoveryPlanName***- ResourceName**: nome hello di hello StorSimple di risorsa con il dispositivo di StorSimple hello.
   * *RecoveryPlanName***- DeviceName**: dispositivo hello che è stato eseguito il failover toobe.
   * *RecoveryPlanName***- VolumeContainers**: stringa dei contenitori di volumi delimitato da virgole è presente nel dispositivo hello toobe non riuscito; ad esempio, è necessario volcon1, volcon2, volcon3.
   * *RecoveryPlanName***- TargetDeviceName**: hello StorSimple Appliance di Cloud in cui hello contenitori sono toobe il failover.
   * *RecoveryPlanName***- TargetDeviceDnsName**: nome del servizio hello del dispositivo di destinazione hello (disponibile in hello **macchina virtuale** sezione: nome del servizio hello è hello stesso come hello Nome DNS).
   * *RecoveryPlanName***- StorageAccountName**: nome di account di archiviazione hello in quale script hello (quale toorun su hello failover della macchina virtuale) verrà archiviato. Può trattarsi di qualsiasi account di archiviazione che è temporaneamente alcuni script di hello toostore spazio.
   * *RecoveryPlanName***- StorageAccountKey**: chiave di accesso hello per hello di sopra di account di archiviazione.
   * *RecoveryPlanName***- ScriptContainer**: hello nome del contenitore di hello in cui hello script verranno archiviati nel cloud hello. Se il contenitore di hello non esiste, verrà creato.
   * *RecoveryPlanName***- VMGUIDS**: al momento di proteggere una macchina virtuale, Azure Site Recovery assegna ogni macchina virtuale un ID univoco che fornisce informazioni dettagliate di hello di hello failover macchina virtuale. hello tooobtain VMGUID, seleziona hello **servizi di ripristino** scheda e fare clic su **elemento protetto** &gt; **gruppi protezione dati** &gt; **Macchine** &gt; **proprietà**. Se si dispone di più macchine virtuali, quindi aggiungere hello GUID come una stringa delimitata da virgole.
   * *RecoveryPlanName***- AutomationAccountName** : hello nome dell'account di automazione hello in cui è stato aggiunto hello runbook e gli asset hello.

  Ad esempio, se hello Nome hello del piano di ripristino è fileServerpredayRP, è possibile che il **credenziali** & **variabili** schede compariranno come indicato di seguito dopo aver aggiunto tutte le risorse hello.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image5.png)

7. Passare toohello **servizi di ripristino** sezione e credenziali di Azure Site Recovery selezionare hello creato in precedenza.
8. Seleziona hello **piani di ripristino (ripristino del sito)** opzione **Gestisci** gruppo e creare un nuovo piano di ripristino come segue:

   a.  Fare clic sul pulsante **+ Piano di ripristino**. Verrà visualizzato il pannello seguente.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image6.png)

   b.  Immettere un nome del piano di ripristino e scegliere i valori di Origine, Destinazione e Modello di distribuzione.

   c.  Consente di selezionare le macchine virtuali hello hello gruppo di protezione che si desidera tooinclude nel piano di ripristino hello e fare clic su **OK** pulsante.

   d.  Selezionare il piano di ripristino creato in precedenza, fare clic su **Personalizza** pulsante visualizzazione di personalizzazione piano di ripristino di tooopen hello.

   e.  Fare clic con il pulsante destro su **Spegnimento di tutti i gruppi** e fare clic su **Aggiungi pre-azione**.

   f.  Consente di aprire Pannello di azione di inserimento, immettere un nome, selezionare **lato primario** opzione dove toorun opzione, selezionare account di automazione (in cui è stato aggiunto hello runbook) e quindi selezionare hello  **StorSimple di failover-contenitori di volumi** runbook.

   g.  Fare clic con il pulsante destro su **gruppo 1: avviare** e fare clic su **Aggiungi elementi protetti** opzione e quindi selezionare hello le macchine virtuali protette nel piano di ripristino hello e fare clic su toobe **Ok** pulsante. Facoltativo se le VM sono già selezionate.

   h.  Fare clic con il pulsante destro su **gruppo 1: avviare** e fare clic su **azione post-** opzione quindi aggiungere tutti hello seguenti script:

   * Runbook Start-StorSimple-Virtual-Appliance
   * Runbook Fail over-StorSimple-volume-containers
   * Runbook Mount-volumes-after-failover
   * Runbook Uninstall-custom-script-extension

   i.  Aggiungere un'azione manuale dopo hello sopra 4 script hello stesso **gruppo 1: post-passaggi** sezione. Questa azione è punto hello in corrispondenza del quale è possibile verificare che tutto funzioni correttamente. Questa azione deve toobe aggiunti solo come parte del failover di Test (hello pertanto solo seleziona **Failover di Test** casella di controllo).

   j.  Dopo l'azione manuale hello, aggiungere hello **pulizia** script utilizzando hello stessa procedura utilizzata per hello altri runbook. **Salvare** piano di ripristino hello.

    > [!NOTE]
    > Quando si esegue un failover di test, è necessario verificare tutti gli elementi al passaggio dell'azione manuale hello volumi StorSimple hello duplicati nel dispositivo di destinazione hello vengono eliminati come parte della pulizia hello al termine dell'azione manuale hello.
    >

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image7.png)

## <a name="perform-a-test-failover"></a>Eseguire un failover di test
Fare riferimento toohello [soluzione di ripristino di emergenza di Active Directory](../site-recovery/site-recovery-active-directory.md) guida complementare per considerazioni specifiche tooActive Directory durante il failover di test hello. il programma di installazione di Hello locale non verrà modificata affatto quando si verifica il failover di test hello. Hello volumi StorSimple di cui sono stati allegati toohello locale VM sono toohello clonato StorSimple Appliance di Cloud in Azure. Una macchina virtuale per scopi di test viene visualizzata in Azure e volumi clonati hello sono collegato toohello macchina virtuale.

#### <a name="tooperform-hello-test-failover"></a>failover di test hello tooperform
1. Nel portale di Azure hello, selezionare l'insieme di credenziali di site recovery.
2. Scegliere il piano di ripristino hello creato per la macchina virtuale del server file hello.
3. Fare clic su **Failover di test**.
4. Selezionare hello toowhich di rete virtuale di Azure che saranno connesse le macchine virtuali di Azure dopo il failover si verifica.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image8.png)
5. Fare clic su **OK** toobegin hello failover. È possibile monitorare i progressi facendo clic su hello VM tooopen le relative proprietà o in hello **il processo di failover di Test** nel nome dell'insieme di credenziali &gt; **processi** &gt; **iprocessidiripristinodelsito**.
6. Al termine del processo di failover di hello, inoltre deve essere in grado di replica hello toosee macchina di Azure vengono visualizzati nel portale di Azure hello &gt; **macchine virtuali**. È possibile eseguire le operazioni di convalida.
7. Al termine delle convalide hello, fare clic su **convalide completo**. Questo hello pulizia verrà hello volumi StorSimple e arresto del sistema StorSimple Appliance di Cloud.
8. Al termine, fare clic su **il failover di test di pulizia** nel piano di ripristino hello. Failover di test nel record di note e salvare eventuali commenti associati hello. Questa operazione eliminerà hello macchina virtuale in cui sono stati creati durante il failover di test.

## <a name="perform-a-planned-failover"></a>Eseguire un failover pianificato
   Durante un failover pianificato, hello locale del file server che macchina virtuale viene arrestato normalmente e un cloud di backup di volumi hello nel dispositivo StorSimple dello snapshot. i volumi StorSimple Hello vengono eseguiti il failover toohello dispositivo virtuale, una macchina virtuale viene portata in Azure, di replica e i volumi di hello sono collegato toohello macchina virtuale.

#### <a name="tooperform-a-planned-failover"></a>tooperform un failover pianificato
1. Nel portale di Azure hello, selezionare **servizi di ripristino** insieme di credenziali &gt; **i piani di ripristino (ripristino del sito)** &gt; **recoveryplan_name** creato per macchina virtuale del server file Hello.
2. Nel Pannello di piano di ripristino hello, fare clic su **più** &gt; **failover pianificato**.  

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image9.png)
3. In hello **conferma Failover pianificato** pannello, scegliere origine hello e i percorsi di destinazione e di rete di destinazione selezionare quindi il processo di failover hello hello controllo icona ✓ toostart.
4. Dopo la replica le macchine virtuali create sono in uno stato di attesa di commit. Fare clic su **Commit** toocommit hello failover.
5. Una volta completata la replica, le macchine virtuali hello avviate nella posizione secondaria hello.

## <a name="perform-a-failover"></a>Eseguire un failover
Durante un failover non pianificato, i volumi StorSimple hello vengono eseguiti il failover toohello dispositivo virtuale, una replica di verranno inseriti VM in Azure, e volumi hello sono collegato toohello macchina virtuale.

#### <a name="tooperform-a-failover"></a>tooperform un failover
1. Nel portale di Azure hello, selezionare **servizi di ripristino** insieme di credenziali &gt; **i piani di ripristino (ripristino del sito)** &gt; **recoveryplan_name** creato per macchina virtuale del server file Hello.
2. Nel Pannello di piano di ripristino hello, fare clic su **più** &gt; **Failover**.  
3. In hello **conferma Failover** pannello, scegliere l'origine hello e percorsi di destinazione.
4. Selezionare **arrestare le macchine virtuali e sincronizzare i dati più recenti di hello** toospecify che il ripristino del sito deve provare tooshut verso il basso macchina virtuale protetta hello e sincronizzare i dati di hello in modo che hello versione più recente dei dati hello eseguire il failover.
5. Dopo il failover hello, hello le macchine virtuali sono in uno stato in sospeso di commit. Fare clic su **Commit** toocommit hello failover.


## <a name="perform-a-failback"></a>Eseguire il failback
Durante un failback, i contenitori di volumi StorSimple stati eseguiti il failover dispositivo fisico toohello indietro dopo un backup.

#### <a name="tooperform-a-failback"></a>tooperform un failback
1. Nel portale di Azure hello, selezionare **servizi di ripristino** insieme di credenziali &gt; **i piani di ripristino (ripristino del sito)** &gt; **recoveryplan_name** creato per macchina virtuale del server file Hello.
2. Nel Pannello di piano di ripristino hello, fare clic su **più** &gt; **Failover pianificato**.  
3. Scegliere i percorsi di origine e destinazione di hello, la sincronizzazione dei dati appropriati selezionare hello e opzioni di creazione di VM.
4. Fare clic su **OK** pulsante toostart processo di failback hello.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image10.png)

## <a name="best-practices"></a>Procedure consigliate
### <a name="capacity-planning-and-readiness-assessment"></a>Pianificazione della capacità e valutazione della conformità
#### <a name="hyper-v-site"></a>Sito di Hyper-V
Hello utilizzare [dello strumento di pianificazione delle capacità utente](http://www.microsoft.com/download/details.aspx?id=39057) toodesign hello server, archiviazione e infrastruttura di rete per l'ambiente di replica Hyper-V.

#### <a name="azure"></a>Azure
È possibile eseguire hello [dello strumento di valutazione della macchina virtuale Azure](http://azure.microsoft.com/downloads/vm-readiness-assessment/) su tooensure macchine virtuali che siano compatibili con le macchine virtuali di Azure e servizi di Azure Site Recovery. Hello Readiness Assessment Tool controlla le configurazioni di macchina virtuale e visualizza un avviso quando le configurazioni sono compatibili con Azure. Ad esempio, genera un avviso se un'unità C: è maggiore di 127 GB.

La pianificazione della capacità prevede almeno due processi importanti:

* Mapping locale dimensioni delle macchine Virtuali di macchine virtuali Hyper-V tooAzure (ad esempio A6, A7, A8 e A9).
* Determinazione hello necessaria una larghezza di banda Internet.

## <a name="limitations"></a>Limitazioni
* Attualmente, failover può essere eseguito solo in 1 dispositivo StorSimple (tooa singola StorSimple Appliance di Cloud). scenario di Hello di un file server che si estende su più dispositivi StorSimple non è ancora supportato.
* Se si verifica un errore durante l'abilitazione della protezione per una macchina virtuale, assicurarsi che non è stato scollegato destinazioni iSCSI hello.
* Tutti i contenitori di volumi hello raggruppati insieme a causa dei criteri di backup che si estende su ai contenitori dei volumi verranno eseguiti il failover insieme.
* Tutti i volumi di hello in contenitori di volumi hello scelto verranno eseguiti il failover.
* Volumi che costituiscono toomore rispetto a 64 TB non è possibile eseguire il failover Poiché la capacità massima di hello di un singolo dispositivo Cloud StorSimple è 64 TB.
* Se si verifica un errore di failover pianificato o non pianificato hello e hello macchine virtuali vengono create in Azure, quindi eseguire la pulizia hello macchine virtuali. ma eseguire un failback. Se si eliminano le macchine virtuali hello quindi hello locale macchine virtuali non possono essere accesi nuovamente.
* Dopo un failover, se non si è in grado di toosee hello volumi, passare a macchine virtuali toohello, aprire Gestione disco, Ripeti analisi dischi hello e resi disponibili online.
* In alcuni casi, le lettere di unità hello nel sito di ripristino di emergenza hello potrebbero essere diverse da lettere hello in locale. In questo caso, è necessario problema hello corretto toomanually termine failover hello.
* Multi-factor authentication deve essere disabilitato per hello Azure credenziali immesso nell'account di automazione hello un asset. Se il processo di autenticazione non è disabilitato, gli script non potrà essere toorun automaticamente e il piano di ripristino hello avrà esito negativo.
* Timeout del processo di failover: hello StorSimple script scadrà se hello failover dei contenitori di volumi impiega più tempo del limite massimo di Azure Site Recovery hello per script (attualmente 120 minuti).
* Timeout del processo di backup: hello StorSimple script timeout se il backup dei volumi di hello richiede più tempo del limite massimo di Azure Site Recovery hello per script (attualmente 120 minuti).

  > [!IMPORTANT]
  > Eseguire backup hello manualmente dal portale di Azure hello e quindi eseguire di nuovo piano di ripristino hello.

* Timeout del processo di clonazione: hello StorSimple script timeout se hello la clonazione dei volumi richiede più tempo rispetto al limite massimo di Azure Site Recovery hello per script (attualmente 120 minuti).
* Errore di sincronizzazione di tempo: hello StorSimple script errori che informa che il backup di hello erano esito negativo anche se il backup di hello ha esito positivo nel portale di hello. Una possibile causa per questa potrebbe essere il che ora del dispositivo StorSimple che hello potrebbe essere sincronizzato con hello ora corrente nel fuso orario hello.

  > [!IMPORTANT]
  > Sincronizzazione hello ora dello strumento con hello ora corrente nel fuso orario hello.

* Errore di failover di dispositivo: hello StorSimple script potrebbe non riuscire se si verifica un failover del dispositivo durante il piano di ripristino hello è in esecuzione.

  > [!IMPORTANT]
  > Eseguire di nuovo piano di ripristino hello dopo il failover dell'apparecchiatura hello è stato completato.


## <a name="summary"></a>Riepilogo
Usando Azure Site Recovery è possibile creare un piano di ripristino di emergenza automatizzato completo per una VM del server file con condivisioni file ospitate nell'archiviazione StorSimple. È possibile avviare il failover hello entro pochi secondi da qualsiasi posizione in hello evento di interruzione e ottenere un'applicazione hello attivo e in esecuzione in pochi minuti.
