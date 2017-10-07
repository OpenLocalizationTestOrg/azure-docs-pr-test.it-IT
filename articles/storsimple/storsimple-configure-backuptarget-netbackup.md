---
title: serie 8000 aaaStorSimple come destinazione di backup con NetBackup | Documenti Microsoft
description: Descrive una configurazione di destinazione di backup di StorSimple hello con Veritas NetBackup.
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: hkanna
ms.openlocfilehash: 7d032bbcf6e40e7609e51437e290fc92b232a48f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a>StorSimple come destinazione di backup con NetBackup

## <a name="overview"></a>Panoramica

Azure StorSimple è una soluzione di archiviazione cloud ibrida di Microsoft. StorSimple indirizzi complessità hello di crescita esponenziale dei dati utilizzando un account di archiviazione di Azure come estensione di una soluzione locale hello e automaticamente suddivisione in livelli i dati tra l'archiviazione locale e l'archiviazione cloud.

Questo articolo illustra l'integrazione di StorSimple con Veritas NetBackup e le procedure consigliate per l'integrazione di entrambe le soluzioni. Rendiamo inoltre indicazioni sulla modalità di integrazione tooset backup Veritas NetBackup toobest con StorSimple. Si rinvia tooVeritas procedure consigliate, backup architetti e amministratori per tooset modo migliore di hello Veritas NetBackup toomeet singoli requisiti per il backup e i contratti di servizio (SLA).

Anche se illustra i concetti chiave e i passaggi di configurazione, questo articolo non costituisce in alcun modo una guida dettagliata per la configurazione o l'installazione. Si presuppone che l'infrastruttura e dei componenti di base hello siano funzioni correttamente e pronto toosupport concetti hello descritti.

### <a name="who-should-read-this"></a>A chi è rivolto questo articolo?

informazioni di Hello in questo articolo sarà particolarmente utile per toobackup amministratori, agli amministratori di sistema e architetti di archiviazione che hanno conoscenze di Veritas NetBackup, Windows Server 2012 R2, Ethernet, servizi cloud e archiviazione.

### <a name="supported-versions"></a>Versioni supportate

-   NetBackup 7.7.x e versioni successive
-   [StorSimple Update 3 e versioni successive](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>Perché usare StorSimple come destinazione di backup?

StorSimple è un'ottima scelta come destinazione di backup perché:

-   Fornisce archiviazione standard, locali per le applicazioni di backup toouse come destinazione di backup rapido, senza alcuna modifica. È possibile usare StorSimple anche per il ripristino rapido dei backup recenti.
-   Il cloud più livelli è perfettamente integrato con un toouse di account di archiviazione cloud di Azure economica archiviazione di Azure.
-   Offre automaticamente archiviazione esterna per il ripristino di emergenza.

## <a name="key-concepts"></a>Concetti chiave

Come con qualsiasi soluzione di archiviazione, un'attenta valutazione delle prestazioni di archiviazione della soluzione hello, i contratti di servizio, frequenza di modifica e alle esigenze di capacità aumento delle dimensioni è toosuccess critici. Hello l'idea principale è che introducendo un livello di cloud, cloud toohello tempi di accesso e le velocità effettive svolge un ruolo fondamentale nella capacità di hello di StorSimple toodo il proprio lavoro.

StorSimple è progettato tooprovide archiviazione tooapplications che operano su un set ben definito di lavoro di dati (attivo). In questo modello, hello working set di dati viene archiviato nei livelli locale hello e hello rimanenti set non lavorativo/freddo/archiviazione di dati a più livelli toohello cloud. Questo modello è rappresentato nella seguente illustrazione hello. riga Hello quasi flat verde rappresenta dati hello archiviati nei livelli di locale hello del dispositivo StorSimple hello. Hello linea rossa rappresenta hello quantità totale di dati memorizzati nella soluzione StorSimple hello in tutti i livelli. spazio di Hello tra la riga hello flat verde e una curva esponenziale rosso hello rappresenta quantità totale di hello di dati archiviati nel cloud hello.

**Suddivisione in livelli di StorSimple**
![Diagramma della suddivisione in livelli di StorSimple](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)

Con questa architettura presente, si noterà che StorSimple è ideale toooperate come destinazione di backup. È possibile usare StorSimple per:
-   Eseguire il ripristino più frequente da hello locale working set di dati.
-   Usare hello del cloud per il ripristino di emergenza in un luogo e i dati precedenti, in cui i ripristini eseguiti sono meno frequenti.

## <a name="storsimple-benefits"></a>Vantaggi di StorSimple

StorSimple offre una soluzione locale che è perfettamente integrata con Microsoft Azure, sfruttando trasparente accedere tooon locale e l'archiviazione cloud.

StorSimple utilizza la suddivisione automatica in livelli tra il dispositivo locale hello, che dispone di SSD dispositivo (unità SSD) e seriale-attached storage SCSI (SAS) e di archiviazione di Azure. Mantiene suddivisione in livelli automatico si accede di frequente dati locali, nei livelli SSD e SAS hello. Sposta i dati di cui si accede raramente tooAzure archiviazione.

StorSimple offre i vantaggi seguenti:

-   Algoritmi di deduplicazione e compressione univoci che utilizzano livelli di hello cloud tooachieve deduplicazione precedenti
-   Disponibilità elevata
-   Replica geografica usando la replica geografica di Azure
-   Integrazione di Azure
-   Crittografia dei dati nel cloud hello
-   Miglioramento del ripristino di emergenza e della conformità

Sebbene StorSimple presenti due scenari di distribuzione principali (destinazione di backup primaria e secondaria), fondamentalmente si tratta di un normale dispositivo di archiviazione a blocchi. StorSimple hello la compressione e la deduplicazione. Invia facilmente e recupera i dati tra cloud hello e un'applicazione hello e file system.

Per altre informazioni su StorSimple, vedere [Serie 8000 StorSimple: una soluzione di archiviazione cloud ibrida](storsimple-overview.md). Inoltre, è possibile esaminare hello [specifiche tecniche di serie StorSimple 8000](storsimple-technical-specifications-and-compliance.md).

> [!IMPORTANT]
> L'uso di un dispositivo StorSimple come destinazione di backup è supportato solo per StorSimple 8000 Update 3 e versioni successive.

## <a name="architecture-overview"></a>Panoramica dell'architettura

Hello tabelle seguenti illustrano istruzioni iniziali per architettura del modello di dispositivo hello.

**Capacità di StorSimple per l'archiviazione locale e cloud**

| Capacità di archiviazione       | 8100          | 8600            |
|------------------------|---------------|-----------------|
| Capacità di archiviazione locale | &lt; 10 TiB\*  | &lt; 20 TiB\*  |
| Capacità di archiviazione cloud | &gt; 200 TiB\* | &gt; 500 TiB\* |
\* Le dimensioni di archiviazione si intendono senza alcuna deduplicazione o compressione.

**Capacità di StorSimple per il backup primario e secondario**

| Scenario di backup  | Capacità di archiviazione locale  | Capacità di archiviazione cloud  |
|---|---|---|
| Backup primario  | Backup recenti archiviati nell'archiviazione locale per l'obiettivo del punto di ripristino rapido toomeet ripristino (RPO) | La cronologia dei backup (RPO) rientra nella capacità del cloud |
| Backup secondario | La copia secondaria dei dati di backup può essere archiviata nella capacità del cloud  | N/D  |

## <a name="storsimple-as-a-primary-backup-target"></a>StorSimple come destinazione di backup primaria

In questo scenario, i volumi StorSimple vengono presentati toohello l'applicazione di backup come unico repository di hello per i backup. Hello nella figura seguente mostra un'architettura della soluzione in cui tutti i backup da utilizzare StorSimple a più livelli di volumi per il backup e ripristini.

![Diagramma logico con StorSimple come destinazione primaria di backup](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Passaggi logici per il backup nella destinazione primaria

1.  contattato dal server di backup Hello hello agente backup di destinazione e l'agente di backup hello trasmette i server di backup di dati toohello.
2.  server di backup Hello scrive dati volumi a livelli di toohello StorSimple.
3.  server di backup Hello aggiorna il database di catalogo hello e quindi Termina processo di backup hello.
4.  Uno script di snapshot attiva hello StorSimple snapshot manager (iniziale o eliminazione).
5.  server di backup Hello Elimina i backup scaduti in base a criteri di conservazione.

### <a name="primary-target-restore-logical-steps"></a>Passaggi logici per il ripristino dalla destinazione primaria

1.  server di backup Hello Avvia ripristino hello appropriato da archivio hello.
2.  l'agente di backup Hello riceve dati hello dal server di backup hello.
3.  server di backup Hello termina il processo di ripristino hello.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple come destinazione secondaria di backup

In questo scenario i volumi StorSimple vengono usati principalmente per la conservazione o l'archiviazione a lungo termine.

Hello figura riportata di seguito è illustrata un'architettura di backup iniziale e di ripristinare il volume di destinazione ad alte prestazioni. Questi backup vengono copiati e archiviato tooa StorSimple a livelli a volume su una pianificazione impostata.

È importante toosize il volume ad alte prestazioni in modo che possa gestire i requisiti di capacità e prestazioni criteri conservazione.

![Diagramma logico con StorSimple come destinazione secondaria di backup](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Passaggi logici per il backup nella destinazione secondaria

1.  contattato dal server di backup Hello hello agente backup di destinazione e l'agente di backup hello trasmette i server di backup di dati toohello.
2.  server di backup Hello scrive l'archiviazione dei dati delle prestazioni di toohigh.
3.  server di backup Hello aggiorna il database di catalogo hello e quindi Termina processo di backup hello.
4.  server di backup Hello copia tooStorSimple i backup in base a criteri di conservazione.
5.  Uno script di snapshot attiva hello StorSimple snapshot manager (iniziale o eliminazione).
6.  Hello backup server Elimina hello scaduti in base a criteri di conservazione dei backup.

### <a name="secondary-target-restore-logical-steps"></a>Passaggi logici per il ripristino dalla destinazione secondaria

1.  server di backup Hello Avvia ripristino hello appropriato da archivio hello.
2.  l'agente di backup Hello riceve dati hello dal server di backup hello.
3.  server di backup Hello termina il processo di ripristino hello.

## <a name="deploy-hello-solution"></a>Distribuire la soluzione hello

La distribuzione della soluzione richiede tre passaggi:
1. Preparare l'infrastruttura di rete hello.
2. Distribuire il dispositivo StorSimple come destinazione dei backup.
3. Distribuire Veritas NetBackup.

Ogni passaggio è descritto in dettaglio nelle sezioni che seguono hello.

### <a name="set-up-hello-network"></a>Configurare una rete hello

StorSimple è una soluzione integrata con hello cloud di Azure, StorSimple richiede un cloud di Azure di toohello connessione attiva e funzionante. Questa connessione viene utilizzata per operazioni come snapshot nel cloud, gestione dei dati e il trasferimento di metadati e tootier nell'archivio cloud tooAzure dati precedenti, meno frequentemente.

Per tooperform soluzione hello è ottimale, consigliabile seguire queste procedure consigliate di rete:

-   collegamento Hello che si connette hello StorSimple suddivisione in livelli tooAzure deve soddisfare i requisiti di larghezza di banda. tooachieve, applicare hello corretto Quality of Service (QoS) tooyour livello infrastruttura commutatori toomatch il RPO e il ripristino ora obiettivo i contratti di servizio.

-   Le latenze massime di accesso all'archiviazione BLOB di Azure devono essere di circa 80 ms.

### <a name="deploy-storsimple"></a>Distribuire StorSimple

Per una guida dettagliata alla distribuzione di StorSimple, vedere [Distribuire un dispositivo StorSimple locale](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-netbackup"></a>Distribuire NetBackup

Per istruzioni dettagliate NetBackup 7.7.x distribuzione, vedere hello [NetBackup 7.7.x documentazione](http://www.veritas.com/docs/000094423).

## <a name="set-up-hello-solution"></a>Configurare la soluzione hello

In questa sezione vengono descritti alcuni esempi di configurazione. Hello esempi e le indicazioni seguenti viene illustrata hello più fondamentali e base implementazione. Questa implementazione potrebbe non essere applicabili direttamente tooyour specifici requisiti di backup.

### <a name="set-up-storsimple"></a>Configurare StorSimple

| Attività di distribuzione di StorSimple  | Commenti aggiuntivi |
|---|---|
| Distribuire un dispositivo StorSimple locale. | Versioni supportate: Update 3 e versioni successive. |
| Attivare la destinazione del backup hello. | Utilizzare queste tooturn comandi su o disattivare la modalità di destinazione di backup e lo stato di tooget. Per ulteriori informazioni, vedere [connettersi in remoto il dispositivo di StorSimple tooa](storsimple-remote-connect.md).</br> tooturn in modalità di backup: `Set-HCSBackupApplianceMode -enable`. </br> tooturn la modalità di backup: `Set-HCSBackupApplianceMode -disable`. </br> stato corrente di hello tooget delle impostazioni di modalità di backup: `Get-HCSBackupApplianceMode`. |
| Creare un contenitore del volume per il volume che archivia i dati di backup hello comuni. Tutti i dati contenuti in un contenitore di volumi vengono deduplicati. | I contenitori di volumi StorSimple definiscono i domini di deduplicazione.  |
| Creare i volumi di StorSimple. | Creare volumi con dimensioni come toohello Chiudi previsto utilizzo possibile, perché dimensioni del volume influisce sul tempo di durata per gli snapshot cloud. Per informazioni su come toosize un volume, fare riferimento [criteri di conservazione](#retention-policies).</br> </br> Utilizzare StorSimple a livelli, volumi e seleziona hello **usare questo volume per i dati dell'archivio si accede di frequente** casella di controllo. </br> L'uso di soli volumi aggiunti in locale non è supportato. |
| Creare un criterio di backup di StorSimple univoco per tutti i volumi di destinazione di backup hello. | Un criterio di backup di StorSimple definisce gruppo la coerenza di hello volumi. |
| Disabilitare la pianificazione hello poiché gli snapshot hello scadono. | Gli snapshot vengono attivati come operazione di post-elaborazione. |

### <a name="set-up-hello-host-backup-server-storage"></a>Impostare l'archiviazione di backup di server host hello

Impostare l'archiviazione di backup di server host hello in base a linee guida toothese:  

- Non usare volumi con spanning, creati mediante il servizio di gestione dischi di Windows, in quanto non sono supportati.
- Formattare i volumi tramite NTFS con una dimensione di allocazione di 64 KB.
- Eseguire il mapping di volumi StorSimple hello direttamente toohello NetBackup server.
    - Usare iSCSI per i server fisici.
    - Usare dischi pass-through per i server virtuali.


## <a name="best-practices-for-storsimple-and-netbackup"></a>Procedure consigliate per StorSimple e NetBackup

Configurazione della soluzione in base alle linee guida toohello dell'hello alcune sezioni che seguono.

### <a name="operating-system-best-practices"></a>Procedure consigliate per il sistema operativo

-   Disabilitare la crittografia di Windows Server e la deduplicazione per file system NTFS hello.
-   Disabilitare la deframmentazione in linea di Windows Server nei volumi StorSimple hello.
-   Disabilitare l'indicizzazione in hello volumi StorSimple di Windows Server.
-   Eseguire una scansione antivirus all'host di origine hello (non in base volumi StorSimple hello).
-   Disattivare l'impostazione predefinita hello [manutenzione di Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Gestione attività. Eseguire questa operazione in uno dei seguenti modi hello:
    - Disattivare configurator manutenzione hello in utilità di pianificazione di Windows.
    - Scaricare [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) di Windows Sysinternals. Dopo aver scaricato PsExec, eseguire Windows PowerShell come amministratore e digitare:
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Procedure consigliate di StorSimple

-   Verificare che il dispositivo StorSimple hello viene aggiornato troppo[Update 3 o versione successiva](storsimple-install-update-3.md).
-   Isolare il traffico iSCSI e cloud. Utilizzare le connessioni iSCSI dedicato per il traffico tra server di backup di StorSimple e hello.
-   Assicurarsi che il dispositivo StorSimple sia una destinazione di backup dedicata. I carichi di lavoro misti non sono supportati in quanto influenzano RTO e RPO.

### <a name="netbackup-best-practices"></a>Procedure consigliate di NetBackup

-   database NetBackup Hello deve essere locale toohello server e non risiede su un volume StorSimple.
-   Ripristino di emergenza, eseguire il backup database NetBackup hello in un volume StorSimple.
-   Sostegno NetBackup backup (anche tooas cui differenziale backup incrementali in NetBackup) completi e incrementali per questa soluzione. Si consiglia di non usare backup sintetici e incrementali cumulativi.
-   File di dati di backup devono contenere solo dati hello per un processo specifico. Non è ad esempio consentito alcun supporto di aggiunta tra diversi processi.

Per hello impostazioni NetBackup più recenti e le procedure consigliate per l'implementazione di questi requisiti, vedere la documentazione di NetBackup hello in [www.veritas.com](https://www.veritas.com).


## <a name="retention-policies"></a>Criteri di conservazione

Uno dei tipi dei criteri di conservazione dei backup più comuni hello è un criterio nonno, padre e figlio (condivisione file di Groove). In un criterio GFS viene eseguito un backup incrementale ogni giorno e vengono eseguiti backup completi ogni settimana e ogni mese. Volumi a livelli di StorSimple sei i risultati dei criteri: un volume contiene hello settimanali, mensili e annuali completo di backup. Hello altri cinque volumi archiviano i backup incrementali giornalieri.

Nel seguente esempio di hello, utilizziamo una rotazione di condivisione file di Groove. esempio Hello presuppone seguente hello:

-   Vengono usati dati compressi o non deduplicati.
-   I backup completi hanno dimensione di 1 TiB ciascuno.
-   I backup incrementali giornalieri hanno dimensione di 500 GiB ciascuno.
-   Quattro backup settimanali sono conservati per un mese.
-   Dodici backup mensili sono conservati per un anno.
-   Un backup annuale è conservato per 10 anni.

In base hello precedente presupposti, creare un 26-TiB StorSimple a livelli a volume per i backup completi di mensili e annuali hello. Creare un TiB di 5 StorSimple a livelli a volume per ogni backup giornaliero incrementale hello.

| Conservazione per tipo di backup | Dimensioni (TiB) | Moltiplicatore GFS\* | Capacità totale (TiB)  |
|---|---|---|---|
| Completo settimanale | 1 | 4  | 4 |
| Incrementale giornaliero | 0,5 | 20 (il numero dei cicli è uguale al numero di settimane al mese) | 12 (2 per quota aggiuntiva) |
| Completo mensile | 1 | 12 | 12 |
| Completo annuale | 1  | 10 | 10 |
| Requisito GFS |   | 38 |   |
| Quota aggiuntiva  | 4  |   | 42 (requisito GFS totale)  |
\*Moltiplicatore di condivisione file di Groove Hello è hello numero di copie necessarie tooprotect e mantenere toomeet i requisiti dei criteri di backup.

## <a name="set-up-netbackup-storage"></a>Configurare l'archiviazione di NetBackup

### <a name="tooset-up-netbackup-storage"></a>tooset NetBackup archiviazione

1.  Nella Console di amministrazione NetBackup hello, selezionare **gestione dei dispositivi e supporti** > **dispositivi** > **pool di dischi**. In hello disco Pool configurazione guidata, selezionare tipo di server di archiviazione hello **AdvancedDisk**, quindi selezionare **Avanti**.

    ![Console di amministrazione di NetBackup, Configurazione guidata pool di dischi](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  Selezionare il server e fare clic su **Avanti**.

    ![Console di amministrazione NetBackup, server hello selezionare](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  Selezionare il volume StorSimple.

    ![Console di amministrazione NetBackup, disco del volume StorSimple hello selezionare](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  Immettere un nome per la destinazione di backup hello e quindi selezionare **Avanti** > **Avanti** guidata hello toofinish.

5.  Esaminare le impostazioni di hello, quindi fare clic **fine**.

6.  Alla fine hello ogni assegnazione di volume, modificare impostazioni dispositivo di hello archiviazione toomatch quelli consigliati in [procedure consigliate per StorSimple e NetBackup](#best-practices-for-storsimple-and-netbackup).

7. Ripetere i passaggi da 1 a 6 finché non si assegnano tutti i volumi StorSimple.

    ![Console di amministrazione di NetBackup, configurazione dei dischi](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurare StorSimple come destinazione di backup primaria

> [!NOTE]
> Ripristina dati da un backup è stato cloud a livelli toohello verificarsi velocità cloud.

Hello nella figura seguente è illustrato hello mapping di un processo di backup tooa volume tipico. In questo caso, tutti i backup settimanali hello mappare toohello sabato completa del disco e i backup incrementali hello mappare dischi incrementale tooMonday venerdì. Tutti i backup di hello e ripristini provengono da un StorSimple a livelli a volume.

![Diagramma logico di configurazione della destinazione primaria di backup ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Esempio di pianificazione GFS con StorSimple come destinazione primaria di backup

Di seguito è riportato un esempio di una pianificazione a rotazione GFS per quattro settimane, mensile e annuale:

| Frequenza/Tipo di backup | Completa | Incrementale (giorni 1-5)  |   
|---|---|---|
| Settimanale (settimane 1-4) | Sabato | Lunedì-venerdì |
| Mensile  | Sabato  |   |
| Annuale | Sabato  |   |   |

## <a name="assigning-storsimple-volumes-tooa-netbackup-backup-job"></a>L'assegnazione StorSimple volumi tooa NetBackup processo di backup

Hello seguente sequenza si presuppone che NetBackup e hello host di destinazione sono configurati in base alle linee guida di hello NetBackup agente.

### <a name="tooassign-storsimple-volumes-tooa-netbackup-backup-job"></a>tooassign StorSimple volumi tooa NetBackup processo di backup

1.  Nella Console di amministrazione NetBackup hello, selezionare **NetBackup gestione**, fare doppio clic su **criteri**, quindi selezionare **nuovi criteri**.

    ![Console di amministrazione di NetBackup, creare un nuovo criterio](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  In hello **aggiungere un nuovo criterio** nella finestra di dialogo immettere un nome per il criterio di hello e quindi selezionare hello **utilizza criteri di configurazione guidata** casella di controllo. Selezionare **OK**.

    ![Console di amministrazione di NetBackup, finestra di dialogo Add a New Policy (Aggiungi nuovo criterio)](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  In Criteri di configurazione guidata Backup hello, elezionare hello tipo di backup desiderato e quindi selezionare **Avanti**.

    ![Console di amministrazione di NetBackup, selezionare il tipo di backup](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  tooset hello tipo di criteri, seleziona **Standard**, quindi selezionare **Avanti**.

    ![Console di amministrazione di NetBackup, selezionare il tipo di criterio](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  Selezionare l'host, seleziona hello **rilevano il sistema operativo client** casella di controllo e quindi selezionare **Aggiungi**. Selezionare **Avanti**.

    ![Console di amministrazione di NetBackup, elencare i client in un nuovo criterio](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  Selezionare l'unità di hello da tooback backup.

    ![Console di amministrazione di NetBackup, selezioni relative al backup per un nuovo criterio](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  Selezionare la frequenza di hello e valori di memorizzazione che soddisfano i requisiti di rotazione dei backup.

    ![Console di amministrazione di NetBackup, frequenza e rotazione dei backup per un nuovo criterio](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  Selezionare **Next** (Avanti) > **Next** (Avanti) > **Finish** (Fine).  È possibile modificare la pianificazione hello dopo la creazione di criteri di hello.

9.  Selezionare i criteri di hello tooexpand appena creato, quindi **pianificazioni**.

    ![Console di amministrazione di NetBackup, pianificazioni per un nuovo criterio](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  Fare doppio clic su **differenziale Inc**selezionare **copiare toonew**, quindi selezionare **OK**.

    ![Console di amministrazione NetBackup, copia pianificazione tooa nuovo criterio](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  Pianificazione di hello appena creato e quindi scegliere **modifica**.

12.  In hello **attributi** scheda, seleziona hello **eseguire l'Override dei criteri archiviazione selezione** casella di controllo e quindi selezionare hello volume lunedì incrementali esiti.

    ![Console di amministrazione di NetBackup, modificare la pianificazione](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  In hello **avvia finestra** scheda, intervallo di tempo selezionare hello per le copie di backup.

    ![Console di amministrazione di NetBackup, modificare la finestra di avvio](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  Selezionare **OK**.

15.  Ripetere i passaggi da 10 a 14 per ogni backup incrementale. Seleziona volume appropriato hello e una pianificazione per ogni backup creati.

16.  Pulsante destro del mouse hello **differenziale Inc** pianificare e quindi eliminarlo.

17.  Modificare il toomeet pianificazione completa che richiede il backup.

    ![Console di amministrazione di NetBackup, modificare la pianificazione completa](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  Modificare la finestra di avvio hello.

    ![Console di amministrazione NetBackup, finestra di avvio hello modifica](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  pianificazione di Hello finale è simile al seguente:

    ![Console di amministrazione di NetBackup, pianificazione finale](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurare StorSimple come destinazione secondaria di backup

> [!NOTE]
>Ripristina dati da un backup è stato cloud a livelli toohello verificarsi velocità cloud.

In questo modello, è necessario disporre di un tooserve media (diverso da StorSimple) di archiviazione come una cache temporanea. Ad esempio, è possibile utilizzare redundant array of independent disks (RAID) volume tooaccommodate spazio, input/output (i/o) e della larghezza di banda. È consigliabile usare RAID 5, 50 e 10.

Hello seguente figura tipico a breve termine memorizzazione locale (server toohello) volumi gli archivi di volumi e conservazione a lungo termine. In questo scenario, tutti i backup eseguiti hello locale (server toohello) volume RAID. Questi backup vengono periodicamente duplicati e archiviati tooan gli archivi di volume. Si è importante toosize (toohello server) locale volume RAID, in modo che possa gestire i requisiti di capacità e prestazioni conservazione a breve termine.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>Esempio GFS con StorSimple come destinazione secondaria di backup

![Diagramma logico con StorSimple come destinazione secondaria di backup](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

tabella Hello seguente viene illustrato tooset backup toorun i backup su dischi di StorSimple e locali di hello. Include i requisiti di capacità totale e individuali.

### <a name="backup-configuration-and-capacity-requirements"></a>Configurazione di backup e requisiti di capacità

| Tipo di backup e conservazione | Archiviazione configurata | Dimensioni (TiB) | Moltiplicatore GFS | Capacità totale\* (TiB) |
|---|---|---|---|---|
| Settimana 1 (completo e incrementale) |Disco locale (breve termine)| 1 | 1 | 1 |
| StorSimple settimane 2-4 |Disco StorSimple (lungo termine) | 1 | 4 | 4 |
| Completo mensile |Disco StorSimple (lungo termine) | 1 | 12 | 12 |
| Completo annuale |Disco StorSimple (lungo termine) | 1 | 1 | 1 |
|Requisiti di dimensione dei volumi GFS |  |  |  | 18*|
\* La capacità totale include 17 TiB dei dischi StorSimple e 1 TiB del volume RAID locale.


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>Pianificazione di esempio GFS: rotazione GFS settimanale, mensile e annuale

| Settimana | Completa | Incrementale Giorno 1 | Incrementale Giorno 2 | Incrementale Giorno 3 | Incrementale Giorno 4 | Incrementale Giorno 5 |
|---|---|---|---|---|---|---|
| Settimana 1 | Volume RAID locale  | Volume RAID locale | Volume RAID locale | Volume RAID locale | Volume RAID locale | Volume RAID locale |
| Settimana 2 | StorSimple settimane 2-4 |   |   |   |   |   |
| Settimana 3 | StorSimple settimane 2-4 |   |   |   |   |   |
| Settimana 4 | StorSimple settimane 2-4 |   |   |   |   |   |
| Mensile | StorSimple Mensile |   |   |   |   |   |
| Annuale | StorSimple Annuale  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>Assegnare StorSimple volumi tooa NetBackup archivio e duplicazione del processo

Poiché NetBackup offre un'ampia gamma di opzioni per la gestione di archiviazione e i supporti, è consigliabile consultare con Veritas o il tooproperly architetto NetBackup valutare i requisiti di archiviazione del ciclo di vita dei criteri (SLP).

Dopo aver definito i pool di hello iniziale del disco, è necessario toodefine tre criteri del ciclo di vita ulteriore spazio di archiviazione, per un totale di quattro criteri:
* LocalRAIDVolume
* StorSimpleWeek2-4
* StorSimpleMonthlyFulls
* StorSimpleYearlyFulls

### <a name="tooassign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>tooassign StorSimple volumi tooa NetBackup archivio e duplicazione del processo

1.  Nella Console di amministrazione NetBackup hello, selezionare **archiviazione** > **criteri di archiviazione del ciclo di vita** > **nuovi criteri di archiviazione del ciclo di vita**.

    ![Console di amministrazione di NetBackup, nuovi criteri del ciclo di vita di archiviazione](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  Immettere un nome per snapshot hello e quindi selezionare **Aggiungi**.

3.  In hello **nuova operazione** della finestra di dialogo hello **proprietà** scheda per **operazione**selezionare **Backup**. Selezionare i valori hello desiderati per **archiviazione di destinazione**, **tipo memorizzazione**, e **periodo di memorizzazione**. Selezionare **OK**.

    ![Console di amministrazione di NetBackup, finestra di dialogo New Operation (Nuova operazione)](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    Per definire repository e l'operazione di backup prima di hello.

4.  Selezionare l'operazione precedente di hello toohighlight, quindi **Aggiungi**. In hello **l'operazione di archiviazione modifica** della finestra di dialogo valori hello selezionare desiderati per **archiviazione di destinazione**, **tipo memorizzazione**, e **periodo di memorizzazione** .

    ![Console di amministrazione NetBackup, finestra di dialogo Change Storage Operation (Modifica operazione di archiviazione)](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  Selezionare l'operazione precedente di hello toohighlight, quindi **Aggiungi**. In hello **nuovi criteri di archiviazione del ciclo di vita** finestra di dialogo, aggiungere i backup mensili per un anno.

    ![Console di amministrazione di NetBackup, nuovi criteri del ciclo di vita dell'archiviazione](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  Ripetere i passaggi 4-5 fino a creare hello completa SLP criteri di conservazione è necessario.

    ![Console di amministrazione NetBackup, Aggiungi criteri nella finestra di dialogo Nuovo criterio di archiviazione del ciclo di vita hello](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  Dopo aver terminato di definire i criteri di conservazione SLP in **criteri**, definire un criterio di backup seguendo i passaggi di hello descritti in dettaglio in [processo backup di StorSimple assegnazione volumi tooa NetBackup](#assigning-storsimple-volumes-to-a-netbackup-backup-job).

8.  In **pianificazioni**, in hello **Cambia pianificazione** la finestra di dialogo, fare doppio clic su **completo**e quindi selezionare **modifica**.

    ![Console di amministrazione di NetBackup, finestra di dialogo Modifica pianificazione](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  Seleziona hello **eseguire l'Override dei criteri archiviazione selezione** casella di controllo, quindi selezionare hello SLP criteri e conservazione creato nei passaggi da 1 a 6.

    ![Console di amministrazione NetBackup, Sostituisci selezione archiviazione criteri](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  Selezionare **OK**, quindi ripetere per pianificazione del backup incrementale hello.

    ![Console di amministrazione di NetBackup, finestra di dialogo Modifica pianificazione per i backup incrementali](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| Conservazione per tipo di backup | Dimensioni (TiB) | Moltiplicatore GFS\* | Capacità totale (TiB)  |
|---|---|---|---|
| Completo settimanale |  1  |  4 | 4  |
| Incrementale giornaliero  | 0,5  | 20 (cicli sono uguali toohello numero di settimane per mese) | 12 (2 per quota aggiuntiva) |
| Completo mensile  | 1 | 12 | 12 |
| Completo annuale | 1  | 10 | 10 |
| Requisito GFS  |     |     | 38 |
| Quota aggiuntiva  | 4  |    | 42 (requisito GFS totale) |
\*Moltiplicatore di condivisione file di Groove Hello è hello numero di copie necessarie tooprotect e mantenere toomeet i requisiti dei criteri di backup.

## <a name="storsimple-cloud-snapshots"></a>Snapshot cloud StorSimple

Gli snapshot cloud StorSimple proteggono i dati di hello che risiede nel dispositivo StorSimple. Creazione di uno snapshot nel cloud è equivalente tooshipping nastri di backup locale tooan fuori sede. Se si utilizza l'archiviazione con ridondanza geografica di Azure, la creazione di uno snapshot nel cloud è siti toomultiple di tooshipping equivalente nastri di backup. Se è necessario toorestore un dispositivo dopo un'emergenza, che potrebbe portare un altro dispositivo di StorSimple online ed eseguire un failover. Dopo il failover hello, sarà in grado di tooaccess hello dati (cloud velocità) da uno snapshot nel cloud più recente hello.

Hello seguente sezione viene descritto come toocreate toostart un breve script e delete StorSimple snapshot cloud durante post-l'elaborazione backup.

> [!NOTE]
> Gli snapshot creati manualmente o a livello di codice non seguono i criteri di scadenza hello StorSimple snapshot. Devono essere eliminati manualmente o a livello di codice.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Avviare ed eliminare gli snapshot cloud mediante uno script

> [!NOTE]
> Valutare attentamente conformità hello e ripercussioni di conservazione dei dati prima di eliminare uno snapshot StorSimple. Per ulteriori informazioni su come toorun uno script di post-backup, vedere hello [NetBackup documentazione](http://www.veritas.com/docs/000094423).

### <a name="backup-lifecycle"></a>Ciclo di vita del backup

![Diagramma del ciclo di vita del backup](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a>Requisiti

-   server di Hello che esegue script hello deve avere accesso alle risorse di cloud tooAzure.
-   account di utente di Hello deve disporre delle autorizzazioni necessarie hello.
-   Un criterio di backup di StorSimple con hello associati StorSimple volumi devono essere configurati ma non è attivati.
-   È necessario hello Nome risorsa di StorSimple, chiave di registrazione, nome del dispositivo e ID del criterio di backup.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart o eliminare uno snapshot nel cloud

1.  [Installare Azure PowerShell](/powershell/azure/overview).
2.  [Scaricare e importare le impostazioni di pubblicazione e le informazioni sulla sottoscrizione](https://msdn.microsoft.com/library/dn385850.aspx).
3.  Nel portale di Azure classico hello, ottenere il nome di risorsa hello e [chiave di registrazione per il servizio StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4.  Nel server di hello che esegue script hello, eseguire PowerShell come amministratore. Digitare il comando seguente:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    ID del criterio di backup. hello nota
5.  Nel blocco note, creare un nuovo script di PowerShell utilizzando hello seguente codice.

    Copiare e incollare questo frammento di codice:
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      Salva hello PowerShell script toohello le impostazioni di pubblicazione stesso percorso in cui è stato salvato di Azure. Ad esempio, salvare il file come C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.
6.  Componente aggiuntivo di processo di backup di hello script tooyour NetBackup. toodo, questa modifica il NetBackup processi opzioni di pre-elaborazione e i comandi di post-elaborazione.

> [!NOTE]
> È consigliabile eseguire il criterio di backup snapshot cloud StorSimple come script post-elaborazione alla fine di hello del processo di backup giornaliero. Per ulteriori informazioni su come tooback backup e ripristino toohelp di ambiente l'applicazione di backup soddisfare l'obiettivo RPO e RTO, consultare l'architetto di backup.

## <a name="storsimple-as-a-restore-source"></a>StorSimple come origine di ripristino

I ripristini da StorSimple funzionano in modo analogo ai ripristini da qualsiasi dispositivo di archiviazione a blocchi. Ripristino di dati a più livelli toohello cloud si verifica a velocità cloud. Per dati locali, le operazioni di ripristino si verificano alla velocità di hello disco locale del dispositivo hello. Per informazioni su come tooperform un ripristino, vedere hello [NetBackup documentazione](http://www.veritas.com/docs/000094423). È consigliabile conformi tooNetBackup ripristino procedure consigliate.

## <a name="storsimple-failover-and-disaster-recovery"></a>Failover e ripristino di emergenza per StorSimple

> [!NOTE]
> Per scenari di destinazione di backup, StorSimple Cloud Appliance non è supportato come destinazione di ripristino.

Una situazione di emergenza può essere causata da numerosi fattori. Hello nella tabella seguente sono elencati i comuni scenari di ripristino di emergenza.

| Scenario | Impatto | Come toorecover | Note |
|---|---|---|---|
| Errore del dispositivo StorSimple | Le operazioni di backup e ripristino vengono interrotte. | Sostituire il dispositivo non riuscito di hello ed eseguire [StorSimple failover e ripristino di emergenza](storsimple-device-failover-disaster-recovery.md). | Se è necessario un ripristino dopo il ripristino dispositivo tooperform, working set di dati completo vengono recuperati dal nuovo dispositivo toohello cloud hello. Tutte le operazioni saranno eseguite alle velocità del cloud. indice di Hello e catalogo processo di analisi potrebbe tutti i set di backup toobe, analizzati e il pull da hello livello toohello dispositivo locale livello cloud, che potrebbe richiedere molto tempo. |
| Errore del server di NetBackup | Le operazioni di backup e ripristino vengono interrotte. | Server backup hello ricompilare ed eseguire il ripristino di database. | È necessario ricompilare o ripristinare hello NetBackup server nel sito di ripristino di emergenza hello. Hello database toohello più recente punto di ripristino. Se hello database NetBackup ripristinato non sono sincronizzati con i processi di backup più recenti, la catalogazione e l'indicizzazione è obbligatorio. Questo indice e catalogo processo di analisi potrebbe tutti i set di backup toobe, analizzati e dal livello di dispositivo locale toohello livello cloud hello. In questo modo il tempo sarà un fattore ancora più importante. |
| Errore del sito che comporta la perdita di hello del server di backup hello e StorSimple | Le operazioni di backup e ripristino vengono interrotte. | Ripristinare innanzitutto StorSimple e quindi NetBackup. | Ripristinare innanzitutto StorSimple e quindi NetBackup. Se è necessario un ripristino dopo il ripristino dispositivo tooperform, working set di dati completo hello vengono recuperati dal nuovo dispositivo toohello cloud hello. Tutte le operazioni saranno eseguite alle velocità del cloud. |

## <a name="references"></a>Riferimenti

Hello seguenti documenti citata in questo articolo:

- [Configurazione di Multipath I/O per StorSimple](storsimple-configure-mpio-windows-server.md)
- [Scenari di archiviazione: thin provisioning](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Uso di unità GPT](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Configurare le copie shadow di cartelle condivise](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Passaggi successivi

- Per ulteriori informazioni su troppo[ripristino da un set di backup](storsimple-restore-from-backup-set-u2.md).
- Per ulteriori informazioni su tooperform [dispositivo failover e ripristino di emergenza](storsimple-device-failover-disaster-recovery.md).
