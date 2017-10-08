---
title: serie 8000 aaaStorSimple come destinazione di backup con Backup Exec | Documenti Microsoft
description: Descrive una configurazione di destinazione di backup di StorSimple hello con Veritas Backup Exec.
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
ms.date: 12/05/2016
ms.author: hkanna
ms.openlocfilehash: 270ad95e1f6b367e80048cad42beb936f205f69c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a>StorSimple come destinazione di backup con Backup Exec

## <a name="overview"></a>Panoramica

Azure StorSimple è una soluzione di archiviazione cloud ibrida di Microsoft. StorSimple indirizzi complessità hello di crescita esponenziale dei dati utilizzando un account di archiviazione di Azure come estensione di una soluzione locale hello e automaticamente suddivisione in livelli i dati tra l'archiviazione locale e l'archiviazione cloud.

Questo articolo illustra l'integrazione di StorSimple con Veritas Backup Exec e le procedure consigliate per l'integrazione di entrambe le soluzioni. Rendiamo inoltre indicazioni sulla modalità di integrazione tooset backup Backup Exec toobest con StorSimple. Si rinvia tooVeritas procedure consigliate, backup architetti e amministratori per tooset modo migliore di hello Backup Exec toomeet singoli requisiti per il backup e i contratti di servizio (SLA).

Anche se illustra i concetti chiave e i passaggi di configurazione, questo articolo non costituisce in alcun modo una guida dettagliata per la configurazione o l'installazione. Si presuppone che l'infrastruttura e dei componenti di base hello siano funzioni correttamente e pronto toosupport concetti hello descritti.

### <a name="who-should-read-this"></a>A chi è rivolto questo articolo?

informazioni di Hello in questo articolo sarà utile più toobackup amministratori, agli amministratori di sistema e architetti di archiviazione che hanno conoscenze di archiviazione, Windows Server 2012 R2, Ethernet, servizi cloud e Backup Exec.

## <a name="supported-versions"></a>Versioni supportate

-   [Backup Exec 16 e versioni successive](http://backupexec.com/compatibility)
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
![Diagramma della suddivisione in livelli di StorSimple](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)

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

![Diagramma logico con StorSimple come destinazione primaria di backup](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

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

![Diagramma logico con StorSimple come destinazione secondaria di backup](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

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
3. Distribuire Backup Exec.

Ogni passaggio è descritto in dettaglio nelle sezioni che seguono hello.

### <a name="set-up-hello-network"></a>Configurare una rete hello

StorSimple è una soluzione integrata con hello cloud di Azure, StorSimple richiede un cloud di Azure di toohello connessione attiva e funzionante. Questa connessione viene utilizzata per operazioni come snapshot nel cloud, gestione e il trasferimento di metadati e tootier nell'archivio cloud tooAzure dati precedenti, meno frequentemente.

Per tooperform soluzione hello è ottimale, consigliabile seguire queste procedure consigliate di rete:

-   collegamento Hello che si connette il tooAzure di suddivisione in livelli di StorSimple deve soddisfare i requisiti di larghezza di banda. tooachieve, applicare hello necessarie Quality of Service (QoS) tooyour livello infrastruttura commutatori toomatch il RPO e il ripristino ora obiettivo i contratti di servizio.
-   Le latenze massime di accesso all'archiviazione BLOB di Azure devono essere di circa 80 ms.

### <a name="deploy-storsimple"></a>Distribuire StorSimple

Per una guida dettagliata alla distribuzione di StorSimple, vedere [Distribuire un dispositivo StorSimple locale](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-backup-exec"></a>Distribuire Backup Exec

Per le procedure consigliate per l'installazione di Backup Exec, vedere [Best practices for Backup Exec installation](https://www.veritas.com/support/en_US/article.000068207) (Procedure consigliate per l'installazione di Backup Exec).

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

- Non usare i volumi con spanning, creati tramite il servizio di gestione dischi di Windows. I dischi con spanning non sono supportati.
- Formattare i volumi tramite NTFS con una dimensione di allocazione di 64 KB.
- Eseguire il mapping di volumi StorSimple hello toohello direttamente i server di Backup Exec.
    - Usare iSCSI per i server fisici.
    - Usare dischi pass-through per i server virtuali.

## <a name="best-practices-for-storsimple-and-backup-exec"></a>Procedure consigliate per StorSimple e Backup Exec

Configurazione della soluzione in base alle linee guida toohello dell'hello le sezioni seguenti.

### <a name="operating-system-best-practices"></a>Procedure consigliate per il sistema operativo

-   Disabilitare la crittografia di Windows Server e la deduplicazione per file system NTFS hello.
-   Disabilitare la deframmentazione in linea di Windows Server nei volumi StorSimple hello.
-   Disabilitare l'indicizzazione in hello volumi StorSimple di Windows Server.
-   Eseguire una scansione antivirus all'host di origine hello (non in base volumi StorSimple hello).
-   Disattivare l'impostazione predefinita hello [manutenzione di Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Gestione attività. Eseguire questa operazione in uno dei seguenti modi hello:
   - Disattivare configurator manutenzione hello in utilità di pianificazione di Windows.
   - Scaricare [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) di Windows Sysinternals. Dopo aver scaricato PsExec, eseguire Azure PowerShell come amministratore e digitare:
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Procedure consigliate di StorSimple

  -   Verificare che il dispositivo StorSimple hello viene aggiornato troppo[Update 3 o versione successiva](storsimple-install-update-3.md).
  -   Isolare il traffico iSCSI e cloud. Utilizzare le connessioni iSCSI dedicato per il traffico tra server di backup di StorSimple e hello.
  -   Assicurarsi che il dispositivo StorSimple sia una destinazione di backup dedicata. I carichi di lavoro misti non sono supportati in quanto influenzano RTO e RPO.

### <a name="backup-exec-best-practices"></a>Procedure consigliate di Backup Exec

-   Backup Exec deve essere installato in un'unità locale del server hello e non su un volume StorSimple.
-   Impostare l'archiviazione di Backup Exec hello **le operazioni di scrittura simultanee** toohello massimo consentito.
    -   Impostare l'archiviazione di Backup Exec hello **dimensioni di blocco e buffer** too512 KB.
    -   Attivare la **lettura e scrittura in buffering** dell'archiviazione di Backup Exec.
-   StorSimple supporta i backup completi e incrementali di Backup Exec. Si consiglia di non usare backup sintetici e differenziali.
-   I file dei dati di backup devono contenere solo i dati per un processo specifico. Non è ad esempio consentito alcun supporto di aggiunta tra diversi processi.
-   Disabilitare la verifica dei processi. Se necessario, la verifica deve essere pianificata dopo il processo di backup più recente di hello. È importante toounderstand che questo processo determina la finestra di backup.
-   Selezionare **Storage** (Archiviazione) > **Your disk** (Disco) > **Details** (Dettagli) > **Properties** (Proprietà). Disattivare **Pre-allocate disk space** (Prealloca spazio del disco).

Per le impostazioni di esecuzione di Backup più recente hello e procedure consigliate per l'implementazione di questi requisiti, vedere [sito Web Veritas hello](https://www.veritas.com).

## <a name="retention-policies"></a>Criteri di conservazione

Uno dei tipi dei criteri di conservazione dei backup più comuni hello è un criterio nonno, padre e figlio (condivisione file di Groove). In un criterio GFS viene eseguito un backup incrementale ogni giorno e vengono eseguiti backup completi ogni settimana e ogni mese. Questo criterio genera sei volumi StorSimple a livelli. Un volume contiene backup completi hello settimanali, mensili e annuali. Hello altri cinque volumi archiviano i backup incrementali giornalieri.

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

## <a name="set-up-backup-exec-storage"></a>Configurare l'archiviazione con Backup Exec

### <a name="tooset-up-backup-exec-storage"></a>tooset spazio di archiviazione di Backup Exec

1.  Nella console di gestione Backup Exec hello selezionare **archiviazione** > **configurare archiviazione** > **archiviazione basata su disco**  >   **Avanti**.

    ![Console di gestione di Backup Exec, pagina di configurazione dell'archiviazione](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  Selezionare **Disk Storage** (Archiviazione su disco) e quindi selezionare **Next** (Avanti).

    ![Console di gestione di Backup Exec, pagina di selezione dell'archiviazione](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  Inserire un nome rappresentativo, ad esempio **Saturday Full** (Sabato completo), e una descrizione. Selezionare **Avanti**.

    ![Console di gestione di Backup Exec, pagina del nome e descrizione](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  Disco hello SELECT in cui desidera dispositivo di archiviazione su disco hello toocreate e quindi selezionare **Avanti**.

    ![Console di gestione di Backup Exec, pagina di selezione del disco di archiviazione](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  Incrementa il numero di hello delle operazioni di scrittura troppo**16**, quindi selezionare **Avanti**.

    ![Console di gestione di Backup Exec, pagina delle impostazioni per le operazioni di scrittura simultanee](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  Esaminare le impostazioni di hello, quindi fare clic **fine**.

    ![Console di gestione di Backup Exec, pagina di riepilogo della configurazione di archiviazione](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  Alla fine hello ogni assegnazione di volume, modificare impostazioni dispositivo di hello archiviazione toomatch quelli consigliati in [procedure consigliate per StorSimple e Backup Exec](#best-practices-for-storsimple-and-backup-exec).

    ![Console di gestione di Backup Exec, pagina delle impostazioni del dispositivo di archiviazione](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  Ripetere i passaggi da 1 a 7 fino a quando non si desidera assegnare il tooBackup volumi StorSimple Exec.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurare StorSimple come destinazione di backup primaria

> [!NOTE]
> Ripristino dei dati da un backup è stato cloud toohello a più livelli si verifica a velocità cloud.

Hello nella figura seguente è illustrato hello mapping di un processo di backup tooa volume tipico. In questo caso, tutti i backup settimanali hello mappare toohello sabato completa del disco e i backup incrementali hello mappare dischi incrementale tooMonday venerdì. Tutti i backup di hello e ripristini provengono da un StorSimple a livelli a volume.

![Diagramma logico di configurazione della destinazione primaria di backup](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Esempio di pianificazione GFS con StorSimple come destinazione primaria di backup

Di seguito è riportato un esempio di una pianificazione a rotazione GFS per quattro settimane, mensile e annuale:

| Frequenza/Tipo di backup | Completa | Incrementale (giorni 1-5)  |   
|---|---|---|
| Settimanale (settimane 1-4) | Sabato | Lunedì-venerdì |
| Mensile  | Sabato  |   |
| Annuale | Sabato  |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-backup-job"></a>Assegnare processo backup Backup Exec tooa volumi StorSimple

Hello sequenza riportata di seguito si presuppone che tale host di destinazione di Backup Exec e hello configurati in base alle linee guida per l'agente di Backup Exec hello.

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-backup-job"></a>tooassign StorSimple volumi tooa Backup Exec processo di backup

1.  Nella console di gestione Backup Exec hello selezionare **Host** > **Backup** > **tooDisk Backup**.

    ![Console di gestione Exec di backup, selezionare l'host, backup e backup toodisk](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  In hello **Backup definizione proprietà** nella finestra di dialogo **Backup**selezionare **modifica**.

    ![Console di gestione di Backup Exec, finestra di dialogo Backup Definition Properties (Proprietà definizione backup)](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  Configurare i backup completi e incrementali in modo che soddisfano i requisiti RPO e RTO e conforme tooVeritas procedure consigliate.

4.  In hello **opzioni di Backup** nella finestra di dialogo **archiviazione**.

    ![Console di gestione di Backup Exec, finestra di dialogo Backup Options Storage (Opzioni di backup Archiviazione)](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  Assegnare i volumi StorSimple corrispondente tooyour una pianificazione backup.

    > [!NOTE]
    > **Compressione** e **tipo di crittografia** impostati troppo**Nessuno**.

6.  In **verificare**selezionare hello **non verificare i dati per questo processo** casella di controllo. L'opzione potrebbe influire sulla suddivisione in livelli di StorSimple.

    > [!NOTE]
    > Deframmentazione in linea, indicizzazione e verifica di background influire negativamente sulle suddivisione in livelli hello StorSimple.

    ![Console di gestione di Backup Exec, finestra di dialogo Backup Options Verify (Opzioni di backup Verifica)](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  Quando è stato configurato il resto di hello del toomeet opzioni di backup i requisiti, selezionare **OK** toofinish.

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurare StorSimple come destinazione secondaria di backup

> [!NOTE]
>Ripristina dati da un backup è stato cloud a livelli toohello verificarsi velocità cloud.

In questo modello, è necessario disporre di un tooserve media (diverso da StorSimple) di archiviazione come una cache temporanea. Ad esempio, è possibile utilizzare redundant array of independent disks (RAID) volume tooaccommodate spazio, input/output (i/o) e della larghezza di banda. È consigliabile usare RAID 5, 50 e 10.

Hello seguente figura tipico a breve termine memorizzazione locale (server toohello) volumi gli archivi di volumi e conservazione a lungo termine. In questo scenario, tutti i backup eseguiti hello locale (server toohello) volume RAID. Questi backup vengono periodicamente duplicati e archiviati tooan gli archivi di volume. Si è importante toosize (toohello server) locale volume RAID, in modo che possa gestire i requisiti di capacità e prestazioni conservazione a breve termine.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>Esempio GFS con StorSimple come destinazione secondaria di backup

![Diagramma logico con StorSimple come destinazione secondaria di backup](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

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


### <a name="assign-storsimple-volumes-tooa-backup-exec-archive-and-deduplication-job"></a>Assegnare StorSimple volumi tooa Backup Exec archivio e deduplicazione processo

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-archive-and-duplication-job"></a>tooassign StorSimple volumi tooa Backup Exec archivio e duplicazione del processo

1.  Nella console di gestione di Backup Exec hello, fare doppio clic su processo hello desidera tooarchive tooa StorSimple volume e quindi selezionare **Backup definizione proprietà** > **modifica**.

    ![Console di gestione di Backup Exec, scheda Backup Definition Properties (Proprietà definizione backup)](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  Selezionare **aggiungere fase** > **duplicato tooDisk** > **modifica**.

    ![Console di gestione di Backup Exec, aggiungere una fase](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  In hello **duplicato opzioni** della finestra di dialogo valori hello selezionare da toouse per **origine** e **pianificazione**.

    ![Console di gestione di Backup Exec, proprietà di definizione del backup e opzioni di duplicazione](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  In hello **archiviazione** elenco a discesa, volume StorSimple hello select in cui si desidera hello Archivia processo toostore hello dati.

    ![Console di gestione di Backup Exec, proprietà di definizione del backup e opzioni di duplicazione](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  Selezionare **verificare**, quindi selezionare hello **non verificare i dati per questo processo** casella di controllo.

    ![Console di gestione di Backup Exec, proprietà di definizione del backup e opzioni di duplicazione](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  Selezionare **OK**.

    ![Console di gestione di Backup Exec, proprietà di definizione del backup e opzioni di duplicazione](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  In hello **Backup** colonna, aggiungere una nuova fase. Per origine hello, utilizzare **incrementale**. Per la destinazione hello scegliere hello volume StorSimple in cui è archiviato il processo di backup incrementale di hello. Ripetere i passaggi da 1 a 6.

## <a name="storsimple-cloud-snapshots"></a>Snapshot cloud StorSimple

Gli snapshot cloud StorSimple proteggono i dati di hello che risiede nel dispositivo StorSimple. Creazione di uno snapshot nel cloud è equivalente tooshipping nastri di backup locale tooan fuori sede. Se si utilizza l'archiviazione con ridondanza geografica di Azure, la creazione di uno snapshot nel cloud è siti toomultiple di tooshipping equivalente nastri di backup. Se è necessario toorestore un dispositivo dopo un'emergenza, che potrebbe portare un altro dispositivo di StorSimple online ed eseguire un failover. Dopo il failover hello, sarà in grado di tooaccess hello dati (cloud velocità) da uno snapshot nel cloud più recente hello.

Hello seguente sezione viene descritto come toocreate toostart un breve script e delete StorSimple snapshot cloud durante post-l'elaborazione backup.

> [!NOTE]
> Gli snapshot creati manualmente o a livello di codice non seguono i criteri di scadenza hello StorSimple snapshot. Devono essere eliminati manualmente o a livello di codice.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Avviare ed eliminare gli snapshot cloud mediante uno script

> [!NOTE]
> Valutare attentamente conformità hello e ripercussioni di conservazione dei dati prima di eliminare uno snapshot StorSimple. Per ulteriori informazioni su come toorun uno script di post-backup, vedere hello [documentazione Backup Exec](https://www.veritas.com/support/en_US/15047.html).

### <a name="backup-lifecycle"></a>Ciclo di vita del backup

![Diagramma del ciclo di vita del backup](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

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
6.  Modificando la pre-elaborazione delle opzioni di processo Backup Exec e comandi di post-elaborazione, aggiungere il processo di backup tooyour script hello in Backup Exec.

    ![Console di Backup Exec, opzioni di backup, scheda dei comandi di pre-elaborazione e post-elaborazione](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> È consigliabile eseguire il criterio di backup snapshot cloud StorSimple come script post-elaborazione alla fine di hello del processo di backup giornaliero. Per ulteriori informazioni su come tooback backup e ripristino toohelp di ambiente l'applicazione di backup soddisfare l'obiettivo RPO e RTO, consultare l'architetto di backup.

## <a name="storsimple-as-a-restore-source"></a>StorSimple come origine di ripristino

I ripristini da StorSimple funzionano in modo analogo ai ripristini da qualsiasi dispositivo di archiviazione a blocchi. Ripristino di dati a più livelli toohello cloud si verifica a velocità cloud. Per dati locali, le operazioni di ripristino si verificano alla velocità di hello disco locale del dispositivo hello. Per informazioni su come tooperform un ripristino, vedere la documentazione di Backup Exec hello. È consigliabile conformi tooBackup Exec ripristino le procedure consigliate.

## <a name="storsimple-failover-and-disaster-recovery"></a>Failover e ripristino di emergenza per StorSimple

> [!NOTE]
> Per scenari di destinazione di backup, StorSimple Cloud Appliance non è supportato come destinazione di ripristino.

Una situazione di emergenza può essere causata da numerosi fattori. Hello nella tabella seguente sono elencati i comuni scenari di ripristino di emergenza.

| Scenario | Impatto | Come toorecover | Note |
|---|---|---|---|
| Errore del dispositivo StorSimple | Le operazioni di backup e ripristino vengono interrotte. | Sostituire il dispositivo non riuscito di hello ed eseguire [StorSimple failover e ripristino di emergenza](storsimple-device-failover-disaster-recovery.md). | Se è necessario un ripristino dopo il ripristino dispositivo tooperform, working set di dati completo vengono recuperati dal nuovo dispositivo toohello cloud hello. Tutte le operazioni saranno eseguite alle velocità del cloud. Hello catalogazione il processo di analisi e l'indicizzazione potrebbe tutti i set di backup toobe, analizzati e il pull da hello livello toohello dispositivo locale livello cloud, che potrebbe richiedere molto tempo. |
| Errore del server di Backup Exec | Le operazioni di backup e ripristino vengono interrotte. | Server backup hello ricompilare ed eseguire il ripristino di database come descritto in dettaglio nella [come un database di Backup e ripristino di Backup Exec (BEDB) manuale toodo](http://www.veritas.com/docs/000041083). | È necessario ricompilare o ripristinare il server di Backup Exec hello nel sito di ripristino di emergenza hello. Hello database toohello più recente punto di ripristino. Se hello ripristinato Exec Backup database non sono sincronizzato con i processi di backup più recente, la catalogazione e l'indicizzazione è obbligatorio. Questo indice e catalogo processo di analisi potrebbe tutti i set di backup toobe, analizzati e dal livello di dispositivo locale toohello livello cloud hello. In questo modo il tempo sarà un fattore ancora più importante. |
| Errore del sito che comporta la perdita di hello del server di backup hello e StorSimple | Le operazioni di backup e ripristino vengono interrotte. | Ripristinare innanzitutto StorSimple e quindi Backup Exec. | Ripristinare innanzitutto StorSimple e quindi Backup Exec. Se è necessario un ripristino dopo il ripristino dispositivo tooperform, working set di dati completo hello vengono recuperati dal nuovo dispositivo toohello cloud hello. Tutte le operazioni saranno eseguite alle velocità del cloud. |

## <a name="references"></a>Riferimenti

Hello seguenti documenti citata in questo articolo:

- [Configurazione di Multipath I/O per StorSimple](storsimple-configure-mpio-windows-server.md)
- [Scenari di archiviazione: thin provisioning](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Uso di unità GPT](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Configurare le copie shadow di cartelle condivise](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Passaggi successivi

- Per ulteriori informazioni su troppo[ripristino da un set di backup](storsimple-restore-from-backup-set-u2.md).
- Per ulteriori informazioni su tooperform [dispositivo failover e ripristino di emergenza](storsimple-device-failover-disaster-recovery.md).
