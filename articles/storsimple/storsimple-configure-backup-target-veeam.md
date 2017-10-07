---
title: serie 8000 aaaStorSimple come destinazione di backup con Veeam | Documenti Microsoft
description: Descrive una configurazione di destinazione di backup di StorSimple hello con Veeam.
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
ms.date: 12/06/2016
ms.author: hkanna
ms.openlocfilehash: 74a4af307fab430942f94b3e28f514a9abce227b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a>StorSimple come destinazione di backup con Veeam

## <a name="overview"></a>Panoramica

Azure StorSimple è una soluzione di archiviazione cloud ibrida di Microsoft. StorSimple indirizzi complessità hello di crescita esponenziale dei dati utilizzando un account di archiviazione di Azure come estensione di una soluzione locale hello e automaticamente suddivisione in livelli i dati tra l'archiviazione locale e l'archiviazione cloud.

Questo articolo illustra l'integrazione di StorSimple con Veeam e le procedure consigliate per l'integrazione di entrambe le soluzioni. Rendiamo inoltre indicazioni sulla modalità di integrazione tooset backup Veeam toobest con StorSimple. Si rinvia tooVeeam procedure consigliate, backup architetti e amministratori per hello migliore modo tooset Veeam toomeet singoli requisiti per il backup e i contratti di servizio (SLA).

Anche se illustra i concetti chiave e i passaggi di configurazione, questo articolo non costituisce in alcun modo una guida dettagliata per la configurazione o l'installazione. Si presuppone che l'infrastruttura e dei componenti di base hello siano funzioni correttamente e pronto toosupport concetti hello descritti.

### <a name="who-should-read-this"></a>A chi è rivolto questo articolo?

informazioni di Hello in questo articolo sarà utile più toobackup amministratori, agli amministratori di sistema e architetti di archiviazione che hanno conoscenze di archiviazione, Windows Server 2012 R2, Ethernet, servizi cloud e Veeam.

### <a name="supported-versions"></a>Versioni supportate

-   Veeam 9 e versioni successive
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
![Diagramma della suddivisione in livelli di StorSimple](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)

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

| Capacità di archiviazione | 8100 | 8600 |
|---|---|---|
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

![Diagramma logico con StorSimple come destinazione primaria di backup](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Passaggi logici per il backup nella destinazione primaria

1.  contattato dal server di backup Hello hello agente backup di destinazione e l'agente di backup hello trasmette i server di backup di dati toohello.
2.  server di backup Hello scrive dati volumi a livelli di toohello StorSimple.
3.  server di backup Hello aggiorna il database di catalogo hello e quindi Termina processo di backup hello.
4.  Uno script di snapshot attiva hello cloud gestione snapshot StorSimple (iniziale o eliminazione).
5.  server di backup Hello Elimina i backup scaduti in base a criteri di conservazione.

### <a name="primary-target-restore-logical-steps"></a>Passaggi logici per il ripristino dalla destinazione primaria

1.  server di backup Hello Avvia ripristino hello appropriato da archivio hello.
2.  l'agente di backup Hello riceve dati hello dal server di backup hello.
3.  server di backup Hello termina il processo di ripristino hello.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple come destinazione secondaria di backup

In questo scenario i volumi StorSimple vengono usati principalmente per la conservazione o l'archiviazione a lungo termine.

Hello figura riportata di seguito è illustrata un'architettura di backup iniziale e di ripristinare il volume di destinazione ad alte prestazioni. Questi backup vengono copiati e archiviato tooa StorSimple a livelli a volume su una pianificazione impostata.

Si è importante toosize il volume ad alte prestazioni in modo che possa gestire i requisiti di capacità e prestazioni criteri conservazione.

![Diagramma logico con StorSimple come destinazione secondaria di backup](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Passaggi logici per il backup nella destinazione secondaria

1.  contattato dal server di backup Hello hello agente backup di destinazione e l'agente di backup hello trasmette i server di backup di dati toohello.
2.  server di backup Hello scrive l'archiviazione dei dati delle prestazioni di toohigh.
3.  server di backup Hello aggiorna il database di catalogo hello e quindi Termina processo di backup hello.
4.  server di backup Hello copia tooStorSimple i backup in base a criteri di conservazione.
5.  Uno script di snapshot attiva hello cloud gestione snapshot StorSimple (iniziale o eliminazione).
6.  server di backup Hello Elimina i backup scaduti in base a criteri di conservazione.

### <a name="secondary-target-restore-logical-steps"></a>Passaggi logici per il ripristino dalla destinazione secondaria

1.  server di backup Hello Avvia ripristino hello appropriato da archivio hello.
2.  l'agente di backup Hello riceve dati hello dal server di backup hello.
3.  server di backup Hello termina il processo di ripristino hello.

## <a name="deploy-hello-solution"></a>Distribuire la soluzione hello

La distribuzione di soluzioni hello richiede tre passaggi:

1. Preparare l'infrastruttura di rete hello.
2. Distribuire il dispositivo StorSimple come destinazione dei backup.
3. Distribuire Veeam.

Ogni passaggio è descritto in dettaglio nelle sezioni che seguono hello.

### <a name="set-up-hello-network"></a>Configurare una rete hello

StorSimple è una soluzione integrata con hello cloud di Azure, StorSimple richiede un cloud di Azure di toohello connessione attiva e funzionante. Questa connessione viene utilizzata per operazioni come snapshot nel cloud, gestione dei dati e il trasferimento di metadati e tootier nell'archivio cloud tooAzure dati precedenti, meno frequentemente.

Per tooperform soluzione hello è ottimale, consigliabile seguire queste procedure consigliate di rete:

-   collegamento Hello che si connette il tooAzure di suddivisione in livelli di StorSimple deve soddisfare i requisiti di larghezza di banda. A tale scopo l'applicazione hello necessarie Quality of Service (QoS) tooyour livello infrastruttura commutatori toomatch il RPO e il ripristino ora obiettivo i contratti di servizio.
-   Le latenze massime di accesso all'archiviazione BLOB di Azure devono essere di circa 80 ms.

### <a name="deploy-storsimple"></a>Distribuire StorSimple

Per una guida dettagliata alla distribuzione di StorSimple, vedere [Distribuire un dispositivo StorSimple locale](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-veeam"></a>Distribuire Veeam

Per Veeam ottimali per l'installazione, vedere [Veeam Backup & Replication Best Practices](https://bp.veeam.expert/), e leggere in Guida dell'utente hello [centro assistenza Veeam (documentazione tecnica)](https://www.veeam.com/documentation-guides-datasheets.html).

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

- Non usare i volumi con spanning, creati tramite il servizio di gestione dischi di Windows. I volumi con spanning non sono supportati.
- Formattare i volumi tramite NTFS con una dimensione dell'unità di allocazione di 64 KB.
- Eseguire il mapping di volumi StorSimple hello direttamente toohello Veeam server.
    - Usare iSCSI per i server fisici.


## <a name="best-practices-for-storsimple-and-veeam"></a>Procedure consigliate per StorSimple e Veeam

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

### <a name="veeam-best-practices"></a>Procedure consigliate di Veeam

-   database Veeam Hello deve essere locale toohello server e non risiede su un volume StorSimple.
-   Ripristino di emergenza, eseguire il backup database Veeam hello in un volume StorSimple.
-   Per questa soluzione sono supportati i backup Veeam completi e incrementali. Si consiglia di non usare backup sintetici e differenziali.
-   File di dati di backup devono contenere solo dati hello per un processo specifico. Non è ad esempio consentito alcun supporto di aggiunta tra diversi processi.
-   Disattivare la verifica dei processi. Se necessario, la verifica deve essere pianificata dopo il processo di backup più recente di hello. È importante toounderstand che questo processo determina la finestra di backup.
-   Disattivare la preallocazione dei supporti di memorizzazione.
-   Assicurarsi che l'elaborazione parallela sia attivata.
-   Disattivare la compressione.
-   Disattivare la deduplicazione sul processo di backup hello.
-   Impostare ottimizzazione troppo**LAN destinazione**.
-   Attivare **Create active full backup** (Crea backup completo attivo) ogni 2 settimane.
-   Sull'archivio di backup hello, configurare **utilizzare file di backup per ogni VM**.
-   Impostare **usare più flussi di caricamento per ogni processo** troppo**8** (è consentito un massimo di 16). Modificare questo numero verso l'alto o verso il basso in base a utilizzo della CPU nel dispositivo StorSimple hello.

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

## <a name="set-up-veeam-storage"></a>Configurare l'archiviazione Veeam

### <a name="tooset-up-veeam-storage"></a>tooset Veeam archiviazione

1.  Nella console di replica e hello Veeam Backup in **Repository strumenti**, andare troppo**infrastruttura Backup**. Fare clic con il pulsante destro del mouse su **Backup Repositories** (Archivi di backup) e selezionare **Add Backup Repository** (Aggiungi archivio di backup).

    ![Console di gestione di Veeam, pagina dell'archivio di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  In hello **nuovo Repository Backup** finestra di dialogo immettere un nome e una descrizione per il repository hello. Selezionare **Avanti**.

    ![Console di gestione di Veeam, pagina di nome e descrizione](./media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  Tipo di hello selezionare **Microsoft Windows server**. Selezionare server Veeam hello. Selezionare **Avanti**.

    ![Console di gestione Veeam, selezionare il tipo di repository di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  toospecify **percorso**, individuare e selezionare il volume di hello. Seleziona hello **limitare le attività simultanee massime:** casella di controllo e set hello valore troppo**4**. In questo modo si garantisce che vengano elaborati contemporaneamente solo quattro dischi virtuali durante l'elaborazione di ciascuna macchina virtuale (VM). Seleziona hello **avanzate** pulsante.

    ![Console di gestione Veeam, selezionare il volume](./media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  In hello **le impostazioni di compatibilità di archiviazione** la finestra di dialogo, seleziona hello **utilizzare file di backup per ogni VM** casella di controllo.

    ![Console di gestione Veeam, impostazioni di compatibilità di archiviazione](./media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  In hello **nuovo Repository Backup** la finestra di dialogo, seleziona hello **abilitare vPower NFS servizio nel server di montaggio hello (scelta consigliata)** casella di controllo. Selezionare **Avanti**.

    ![Console di gestione di Veeam, pagina dell'archivio di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  Esaminare le impostazioni di hello, quindi fare clic **Avanti**.

    ![Console di gestione di Veeam, pagina dell'archivio di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    Un repository viene aggiunto toohello Veeam server.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurare StorSimple come destinazione di backup primaria

> [!IMPORTANT]
> Ripristino dei dati da un backup è stato cloud toohello a più livelli si verifica a velocità cloud.

Hello nella figura seguente è illustrato hello mapping di un processo di backup tooa volume tipico. In questo caso, tutti i backup settimanali hello mappare toohello sabato completa del disco e i backup incrementali hello mappare dischi incrementale tooMonday venerdì. Tutti i backup di hello e ripristini provengono da un StorSimple a livelli a volume.

![Diagramma logico di configurazione della destinazione primaria di backup](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Esempio di pianificazione GFS con StorSimple come destinazione primaria di backup

Di seguito è riportato un esempio di una pianificazione a rotazione GFS per quattro settimane, mensile e annuale:

| Frequenza/Tipo di backup | Completa | Incrementale (giorni 1-5)  |   
|---|---|---|
| Settimanale (settimane 1-4) | Sabato | Lunedì-venerdì |
| Mensile  | Sabato  |   |
| Annuale | Sabato  |   |   |


### <a name="assign-storsimple-volumes-tooa-veeam-backup-job"></a>Assegnare processo backup Veeam tooa volumi StorSimple

Per lo scenario di destinazione del backup primario, creare un processo giornaliero con il volume StorSimple primario di Veeam. Per uno scenario di destinazione del backup secondario, creare un processo giornaliero mediante archiviazione DAS (Direct Attached Storage), NAS (Network Attached Storage) o JBOD (Just a Bunch of Disks).

#### <a name="tooassign-storsimple-volumes-tooa-veeam-backup-job"></a>tooassign StorSimple volumi tooa Veeam processo di backup

1.  Nella console di replica e hello Veeam Backup, selezionare **Backup & replica**. Fare clic con il pulsante destro del mouse su **Backup** e selezionare **VMware** o **Hyper-V** in base all'ambiente.

    ![Console di gestione Veeam, nuovo processo di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  In hello **nuovo processo di Backup** finestra di dialogo immettere un nome e una descrizione per il processo di backup giornaliero di hello.

    ![Console di gestione di Veeam, pagina del nuovo processo di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  Selezionare un massimo di tooback una macchina virtuale.

    ![Console di gestione di Veeam, pagina del nuovo processo di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  Selezionare i valori hello desiderati per **Backup proxy** e **repository Backup**. Selezionare un valore per **tookeep punti di ripristino su disco** in base toohello RPO e RTO le definizioni per l'ambiente in locale (NAS). Selezionare **Advanced** (Avanzate).

    ![Console di gestione di Veeam, pagina del nuovo processo di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. In hello **impostazioni avanzate** della finestra di dialogo hello **Backup** , selezionare **incrementale**. Assicurarsi che hello **creare periodicamente i backup completi sintetici** casella di controllo è deselezionata. Seleziona hello **creare periodicamente i backup completi active** casella di controllo. In **backup completo Active**selezionare hello **settimanale nei giorni selezionati** casella di controllo per sabato.

    ![Console di gestione di Veeam, pagina delle impostazioni avanzate nuovo processo di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. In hello **archiviazione** scheda, assicurarsi che tale hello **abilitare la deduplicazione dei dati inline** casella di controllo è deselezionata. Seleziona hello **blocchi di file di swapping Exclude** casella di controllo e seleziona hello **Exclude eliminato blocchi di file** casella di controllo. Impostare **livello di compressione** troppo**Nessuno**. Bilanciato delle prestazioni e la deduplicazione, impostare **ottimizzazione dell'archiviazione** troppo**destinazione LAN**. Selezionare **OK**.

    ![Console di gestione di Veeam, pagina delle impostazioni avanzate nuovo processo di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    Per informazioni sulle impostazioni di deduplicazione e compressione di Veeam, vedere [Deduplicazione e compressione dei dati](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).

7.  In hello **Modifica processo di Backup** nella finestra di dialogo è possibile selezionare hello **consentono l'elaborazione compatibile con l'applicazione** casella di controllo (facoltativo).

    ![Console di gestione di Veeam, pagina dell'elaborazione guest di un nuovo processo di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  Impostare hello pianificazione toorun una volta al giorno, che è possibile specificare contemporaneamente.

    ![Console di gestione di Veeam, pagina di pianificazione nuovo processo di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurare StorSimple come destinazione secondaria di backup

> [!NOTE]
> Ripristina dati da un backup è stato cloud a livelli toohello verificarsi velocità cloud.

In questo modello, è necessario disporre di un tooserve media (diverso da StorSimple) di archiviazione come una cache temporanea. Ad esempio, è possibile utilizzare redundant array of independent disks (RAID) volume tooaccommodate spazio, input/output (i/o) e della larghezza di banda. È consigliabile usare RAID 5, 50 e 10.

Hello seguente illustrazione mostra tipico volumi di locale (toohello server) di conservazione a breve termine e volumi di archiviazione di memorizzazione a lungo termine. In questo scenario, tutti i backup eseguiti hello locale (server toohello) volume RAID. Questi backup vengono periodicamente duplicati e archiviati tooan volume di archiviazione. Si è importante toosize (toohello server) locale volume RAID, in modo che possa gestire i requisiti di capacità e prestazioni conservazione a breve termine.

![Diagramma logico con StorSimple come destinazione secondaria di backup](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>Esempio GFS con StorSimple come destinazione secondaria di backup

tabella Hello seguente viene illustrato tooset backup toorun i backup su dischi di StorSimple e locali di hello. Include i requisiti di capacità totale e individuali.

| Tipo di backup e conservazione | Archiviazione configurata | Dimensioni (TiB) | Moltiplicatore GFS | Capacità totale\* (TiB) |
|---|---|---|---|---|
| Settimana 1 (completo e incrementale) |Disco locale (breve termine)| 1 | 1 | 1 |
| StorSimple settimane 2-4 |Disco StorSimple (lungo termine) | 1 | 4 | 4 |
| Completo mensile |Disco StorSimple (lungo termine) | 1 | 12 | 12 |
| Completo annuale |Disco StorSimple (lungo termine) | 1 | 1 | 1 |
|Requisiti di dimensione dei volumi GFS |  |  |  | 18*|
\* La capacità totale include 17 TiB dei dischi StorSimple e 1 TiB del volume RAID locale.


### <a name="gfs-example-schedule"></a>Pianificazione di esempio GFS

Pianificazione della rotazione GFS settimanale, mensile e annuale

| Settimana | Completa | Incrementale Giorno 1 | Incrementale Giorno 2 | Incrementale Giorno 3 | Incrementale Giorno 4 | Incrementale Giorno 5 |
|---|---|---|---|---|---|---|
| Settimana 1 | Volume RAID locale  | Volume RAID locale | Volume RAID locale | Volume RAID locale | Volume RAID locale | Volume RAID locale |
| Settimana 2 | StorSimple settimane 2-4 |   |   |   |   |   |
| Settimana 3 | StorSimple settimane 2-4 |   |   |   |   |   |
| Settimana 4 | StorSimple settimane 2-4 |   |   |   |   |   |
| Mensile | StorSimple Mensile |   |   |   |   |   |
| Annuale | StorSimple Annuale  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-tooa-veeam-copy-job"></a>Assegnare processo di copia Veeam tooa volumi StorSimple

#### <a name="tooassign-storsimple-volumes-tooa-veeam-copy-job"></a>processo di copia Veeam tooa volumi StorSimple tooassign

1.  Nella console di replica e hello Veeam Backup, selezionare **Backup & replica**. Fare clic con il pulsante destro del mouse su **Backup** e selezionare **VMware** o **Hyper-V** in base all'ambiente.

    ![Console di gestione di Veeam, pagina del processo di copia di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  In hello **nuovo processo di copia di Backup** finestra di dialogo immettere un nome e una descrizione per il processo di hello.

    ![Console di gestione di Veeam, pagina del processo di copia di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  Selezionare le macchine virtuali hello desiderato tooprocess. Selezionare dal backup, quindi il backup giornaliero hello creato in precedenza.

    ![Console di gestione di Veeam, pagina del processo di copia di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  Escludere gli oggetti dal processo di copia di backup hello, se necessario.

5.  Selezionare l'archivio di backup e impostare un valore per **punti di ripristino tookeep**. Essere certi hello tooselect **seguente hello Mantieni punti di ripristino per scopi di archiviazione** casella di controllo. Definire la frequenza di backup hello e quindi selezionare **avanzate**.

    ![Console di gestione di Veeam, pagina del processo di copia di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  Specificare le impostazioni avanzate seguenti hello:

    * In hello **manutenzione** scheda, disattivare la protezione il danneggiamento a livello di archiviazione.

    ![Console di gestione di Veeam, pagina delle impostazioni avanzate nuovo processo di copia di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * In hello **archiviazione** scheda, assicurarsi che la deduplicazione e compressione sono disattivate.

    ![Console di gestione di Veeam, pagina delle impostazioni avanzate nuovo processo di copia di backup](./media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  Specificare che il trasferimento dei dati hello è diretto.

8.  Definire una pianificazione della finestra hello copia di backup in base alle esigenze tooyour e quindi completare la procedura guidata hello.

Per altre informazioni, vedere [Creare processi di copia di backup](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).

## <a name="storsimple-cloud-snapshots"></a>Snapshot cloud StorSimple

Gli snapshot cloud StorSimple proteggono i dati di hello che risiede nel dispositivo StorSimple. Creazione di uno snapshot nel cloud è equivalente tooshipping nastri di backup locale tooan fuori sede. Se si utilizza l'archiviazione con ridondanza geografica di Azure, la creazione di uno snapshot nel cloud è siti toomultiple di tooshipping equivalente nastri di backup. Se è necessario toorestore un dispositivo dopo un'emergenza, che potrebbe portare un altro dispositivo di StorSimple online ed eseguire un failover. Dopo il failover hello, sarà in grado di tooaccess hello dati (cloud velocità) da uno snapshot nel cloud più recente hello.

Hello seguente sezione viene descritto come toocreate toostart un breve script e delete StorSimple snapshot cloud durante post-l'elaborazione backup.

> [!NOTE]
> Gli snapshot creati manualmente o a livello di codice non seguono i criteri di scadenza hello StorSimple snapshot. Devono essere eliminati manualmente o a livello di codice.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Avviare ed eliminare gli snapshot cloud mediante uno script

> [!NOTE]
> Valutare attentamente conformità hello e ripercussioni di conservazione dei dati prima di eliminare uno snapshot StorSimple. Per ulteriori informazioni su come toorun uno script di post-backup, vedere la documentazione di Veeam hello.


### <a name="backup-lifecycle"></a>Ciclo di vita del backup

![Diagramma del ciclo di vita del backup](./media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a>Requisiti

-   server di Hello che esegue script hello deve avere accesso alle risorse di cloud tooAzure.
-   account di utente di Hello deve disporre delle autorizzazioni necessarie hello.
-   Un criterio di backup di StorSimple con hello associati StorSimple volumi devono essere configurati ma non è attivati.
-   È necessario hello Nome risorsa di StorSimple, chiave di registrazione, nome del dispositivo e ID del criterio di backup.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart o eliminare uno snapshot nel cloud

1. [Installare Azure PowerShell](/powershell/azure/overview).
2. [Scaricare e importare le impostazioni di pubblicazione e le informazioni sulla sottoscrizione](https://msdn.microsoft.com/library/dn385850.aspx).
3. Nel portale di Azure classico hello, ottenere il nome di risorsa hello e [chiave di registrazione per il servizio StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4. Nel server di hello che esegue script hello, eseguire PowerShell come amministratore. Digitare il comando seguente:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    ID del criterio di backup. hello nota
5. Nel blocco note, creare un nuovo script di PowerShell utilizzando hello seguente codice.

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
6. backup di tooyour tooadd hello script del processo, modificare il processo di Veeam opzioni avanzate.

    ![Scheda script di impostazioni avanzate per il backup Veeam](./media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

È consigliabile eseguire il criterio di backup snapshot cloud StorSimple come script post-elaborazione alla fine di hello del processo di backup giornaliero. Per ulteriori informazioni su come tooback backup e ripristino toohelp di ambiente l'applicazione di backup soddisfare l'obiettivo RPO e RTO, consultare l'architetto di backup.

## <a name="storsimple-as-a-restore-source"></a>StorSimple come origine di ripristino

I ripristini da StorSimple funzionano in modo analogo ai ripristini da qualsiasi dispositivo di archiviazione a blocchi. Ripristino di dati a più livelli toohello cloud si verifica a velocità cloud. Per dati locali, le operazioni di ripristino si verificano alla velocità di hello disco locale del dispositivo hello.

Con Veeam, ripristino rapido, granulare a livello di file sono disponibili tramite StorSimple tramite i visualizzatori predefiniti hello nella console Veeam hello. Utilizzare i Veeam Explorers toorecover singoli elementi, quali messaggi di posta elettronica, gli oggetti di Active Directory e gli elementi di SharePoint dai backup. ripristino di Hello può essere eseguito senza interruzioni di macchina virtuale locale. È inoltre possibile eseguire il ripristino temporizzato per il database SQL di Azure e i database Oracle. Veeam e StorSimple rendere il processo di hello del ripristino a livello di elemento da Azure facile e veloce. Per informazioni su come tooperform un ripristino, vedere la documentazione di Veeam hello:

- Per [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)
- Per [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)
- Per [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)
- Per [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)
- Per [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)


## <a name="storsimple-failover-and-disaster-recovery"></a>Failover e ripristino di emergenza per StorSimple

> [!NOTE]
> Per scenari di destinazione di backup, StorSimple Cloud Appliance non è supportato come destinazione di ripristino.

Una situazione di emergenza può essere causata da numerosi fattori. Hello nella tabella seguente sono elencati i comuni scenari di ripristino di emergenza.

| Scenario | Impatto | Come toorecover | Note |
|---|---|---|---|
| Errore del dispositivo StorSimple | Le operazioni di backup e ripristino vengono interrotte. | Sostituire il dispositivo non riuscito di hello ed eseguire [StorSimple failover e ripristino di emergenza](storsimple-device-failover-disaster-recovery.md). | Se è necessario un ripristino dopo il ripristino dispositivo tooperform, working set di dati completo vengono recuperati dal nuovo dispositivo toohello cloud hello. Tutte le operazioni saranno eseguite alle velocità del cloud. indice di Hello e catalogo processo di analisi potrebbe tutti i set di backup toobe, analizzati e il pull da hello livello toohello dispositivo locale livello cloud, che potrebbe richiedere molto tempo. |
| Errore del server di Veeam | Le operazioni di backup e ripristino vengono interrotte. | Server backup hello ricompilare ed eseguire il ripristino di database come descritto in dettaglio nella [centro assistenza Veeam (documentazione tecnica)](https://www.veeam.com/documentation-guides-datasheets.html).  | È necessario ricompilare o ripristinare hello Veeam server nel sito di ripristino di emergenza hello. Hello database toohello più recente punto di ripristino. Se hello database Veeam ripristinato non sono sincronizzati con i processi di backup più recenti, la catalogazione e l'indicizzazione è obbligatorio. Questo indice e catalogo processo di analisi potrebbe tutti i set di backup toobe, analizzati e dal livello di dispositivo locale toohello livello cloud hello. In questo modo il tempo sarà un fattore ancora più importante. |
| Errore del sito che comporta la perdita di hello del server di backup hello e StorSimple | Le operazioni di backup e ripristino vengono interrotte. | Ripristinare innanzitutto StorSimple e quindi Veeam. | Ripristinare innanzitutto StorSimple e quindi Veeam. Se è necessario un ripristino dopo il ripristino dispositivo tooperform, working set di dati completo hello vengono recuperati dal nuovo dispositivo toohello cloud hello. Tutte le operazioni saranno eseguite alle velocità del cloud. |


## <a name="references"></a>Riferimenti

Hello seguenti documenti citata in questo articolo:

- [Configurazione di Multipath I/O per StorSimple](storsimple-configure-mpio-windows-server.md)
- [Scenari di archiviazione: thin provisioning](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Uso di unità GPT](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Configurare le copie shadow di cartelle condivise](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Passaggi successivi

- Per ulteriori informazioni su troppo[ripristino da un set di backup](storsimple-restore-from-backup-set-u2.md).
- Per ulteriori informazioni su tooperform [dispositivo failover e ripristino di emergenza](storsimple-device-failover-disaster-recovery.md).
