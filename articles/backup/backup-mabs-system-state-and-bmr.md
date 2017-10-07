---
title: aaaAzure Backup Server protegge lo stato del sistema e ripristini metal toobare | Documenti Microsoft
description: Utilizzare il Server di Backup di Azure tooback dello stato del sistema e fornire protezione del ripristino bare metal (BMR).
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>Eseguire il backup dello stato del sistema e il ripristino metal toobare con Server di Backup di Azure

Il server di Backup di Azure esegue il backup dello stato del sistema e offre la protezione del ripristino bare metal.

*   **Backup dello stato del sistema**: il backup dei file del sistema operativo, pertanto è possibile ripristinare quando un computer viene avviato, ma il file system e Registro di sistema di hello vanno perdute. Un backup dello stato del sistema include:
    * Membro di dominio: file di avvio, database di registrazione della classe COM+, registro
    * Controller di dominio: file di avvio di Windows Server Active Directory (NTDS), database di registrazione della classe COM+, registro, volume di sistema (SYSVOL)
    * Computer che esegue servizi cluster: metadati del server di cluster
    * Computer che esegue servizi certificati: dati del certificato
* **Backup bare metal**: esegue il backup dei file del sistema operativo e di tutti i dati su volumi critici (tranne i dati utente). Per definizione, un backup bare metal include un backup dello stato del sistema. Fornisce una protezione quando non si avvia un computer e si dispone di toorecover tutto.

Hello nella tabella seguente sono riepilogati i quali è possibile eseguire il backup e ripristino. Per informazioni dettagliate sulle versioni delle app che è possibile proteggere con il ripristino dello stato del sistema e bare metal, vedere [Di quali elemento esegue il backup il server di Backup di Azure?](backup-mabs-protection-matrix.md).

|Backup|Problema|Ripristino dal backup del server di Backup di Azure|Ripristino dal backup dello stato del sistema|Ripristino bare metal|
|----------|---------|---------------------------|------------------------------------|-------|
|**Dati di file**<br /><br />Backup dei dati regolare<br /><br />Ripristino bare metal/backup dello stato del sistema|Dati di file persi|S|N|N|
|**Dati di file**<br /><br />Backup del server di Backup di Azure dei dati di file<br /><br />Ripristino bare metal/backup dello stato del sistema|Sistema operativo perso o danneggiato|N|S|S|
|**Dati di file**<br /><br />Backup del server di Backup di Azure dei dati di file<br /><br />Ripristino bare metal/backup dello stato del sistema|Server perso (volumi di dati intatti)|N|N|S|
|**Dati di file**<br /><br />Backup del server di Backup di Azure dei dati di file<br /><br />Ripristino bare metal/backup dello stato del sistema|Server perso (volumi di dati persi)|S|No|Sì (ripristino bare metal, seguito dal ripristino regolare dei dati di file di cui è stato eseguito il backup)|
|**Dati di SharePoint**:<br /><br />Backup del server di Backup di Azure dei dati della farm<br /><br />Ripristino bare metal/backup dello stato del sistema|Sito, elenchi, elementi elenco, documenti persi|S|N|N|
|**Dati di SharePoint**:<br /><br />Backup del server di Backup di Azure dei dati della farm<br /><br />Ripristino bare metal/backup dello stato del sistema|Sistema operativo perso o danneggiato|N|S|S|
|**Dati di SharePoint**:<br /><br />Backup del server di Backup di Azure dei dati della farm<br /><br />Ripristino bare metal/backup dello stato del sistema|Ripristino di emergenza|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Backup del server di Backup di Azure dell'host o guest Hyper-V<br /><br />Ripristino bare metal/backup dello stato del sistema di host|Macchine virtuali perse|S|N|N|
|Hyper-V<br /><br />Backup del server di Backup di Azure dell'host o guest Hyper-V<br /><br />Ripristino bare metal/backup dello stato del sistema di host|Sistema operativo perso o danneggiato|N|S|S|
|Hyper-V<br /><br />Backup del server di Backup di Azure dell'host o guest Hyper-V<br /><br />Ripristino bare metal/backup dello stato del sistema di host|Host Hyper-V perso (macchine virtuali intatte)|N|N|S|
|Hyper-V<br /><br />Backup del server di Backup di Azure dell'host o guest Hyper-V<br /><br />Ripristino bare metal/backup dello stato del sistema di host|Host Hyper-V perso (macchine virtuali perse)|N|N|S<br /><br />Ripristino bare metal, seguito da ripristino regolare del server di Backup di Azure|
|SQL Server/Exchange<br /><br />Backup dell'app del server di Backup di Azure<br /><br />Ripristino bare metal/backup dello stato del sistema|Dati di app persi|S|N|N|
|SQL Server/Exchange<br /><br />Backup dell'app del server di Backup di Azure<br /><br />Ripristino bare metal/backup dello stato del sistema|Sistema operativo perso o danneggiato|N|y|S|
|SQL Server/Exchange<br /><br />Backup dell'app del server di Backup di Azure<br /><br />Ripristino bare metal/backup dello stato del sistema|Server perso (database/log delle transazioni intatti)|N|N|S|
|SQL Server/Exchange<br /><br />Backup dell'app del server di Backup di Azure<br /><br />Ripristino bare metal/backup dello stato del sistema|Server perso (database/log delle transazioni persi)|N|N|S<br /><br />Ripristino bare metal, seguito da ripristino regolare del server di Backup di Azure|

## <a name="how-system-state-backup-works"></a>Funzionamento del backup dello stato del sistema

Quando viene eseguito un backup dello stato del sistema, Backup Server comunica con Windows Server Backup toorequest un backup dello stato del sistema del server hello. Per impostazione predefinita, Backup di Server e Windows Server Backup utilizzare unità hello con hello più spazio libero. Informazioni su questa unità viene salvate nel file PSDataSourceConfig.xml hello. Questo è l'unità di hello che utilizza Windows Server Backup per i backup.

È possibile personalizzare l'unità di hello utilizzata dal Server di Backup per backup dello stato del sistema hello. Nel server di hello protetto, passare tooC:\Program Files\Microsoft Manager\MABS\Datasources di protezione dati. Aprire il file PSDataSourceConfig.xml hello per la modifica. Hello modifica \<FilesToProtect\> valore per la lettera di unità hello. Salvare e chiudere il file hello. Se è presente che un gruppo protezione dati set tooprotect hello stato del sistema hello computer, eseguire una verifica coerenza. Se viene generato un avviso, selezionare **Modifica gruppo protezione dati** avviso hello e guidata hello quindi completato. Eseguire quindi un'altra verifica di coerenza.

Si noti che se il server di protezione hello in un cluster, è possibile che un'unità cluster venga selezionata come unità hello con hello maggiore spazio libero. Se la proprietà di tale unità sono stati disattivati tooanother nodo ed esegue un backup dello stato del sistema, non è disponibile unità hello e hello backup non riesce. In questo scenario, modificare l'unità di PSDataSourceConfig.xml toopoint tooa locale.

Successivamente, Windows Server Backup crea una cartella denominata WindowsImageBackup nella radice di hello della cartella di ripristino hello. Come Windows Server Backup crea backup hello, tutti i dati di hello viene inserito in questa cartella. Al termine dell'operazione backup hello, file hello è toohello trasferiti Backup Server. Si noti hello le seguenti informazioni:

* Questa cartella e il relativo contenuto non viene eliminati al termine di hello backup o il trasferimento. Hello toothink di modo migliore di ciò è che hello spazio viene riservato per hello successivo che viene completato un backup.
* Hello cartella viene creata ogni volta che viene eseguito un backup. Hello data e l'ora di riflettere hello ora dell'ultimo backup dello stato del sistema.

## <a name="bmr-backup"></a>Backup bare metal

Per il ripristino bare metal (incluso un backup dello stato del sistema), processo di backup hello verrà salvato direttamente tooa condivisione nel computer Server di Backup hello. Cartella tooa non viene salvata nel server protetto hello.

Server di backup chiama Windows Server Backup e condivide il volume di replica hello relativo al backup del ripristino bare metal. In questo caso, non indica a Windows Server Backup toouse hello unità con hello più spazio. Utilizza invece condivisione hello che è stato creato per il processo di hello.

Al termine dell'operazione backup hello, file hello è toohello trasferiti Backup Server. I log vengono archiviati in C:\Windows\Logs\WindowsServerBackup.

## <a name="prerequisites-and-limitations"></a>Prerequisiti e limitazioni

-   Il ripristino bare metal non è supportato per i computer con Windows Server 2003 o che eseguono un sistema operativo client.

-   Non è possibile proteggere il ripristino bare metal e stato di sistema per hello stesso computer in diversi gruppi protezione dati.

-   Un computer server di Backup non può proteggere sé stesso per il ripristino bare metal.

-   Tootape di protezione a breve termine (disco-a-nastro o D2T) non è supportata per il ripristino bare metal. A lungo termine tootape di archiviazione (disco-a-disco-a-nastro o D2D2T) è supportata.

-   Per la protezione ripristino bare metal, Windows Server Backup deve essere installato hello protetto.

-   Per la protezione ripristino bare metal, a differenza di per la protezione stato del sistema, Backup Server non ha requisiti di spazio sul computer protetto hello. Windows Server Backup trasferisce direttamente i computer del Server di Backup toohello backup. il processo di trasferimento di backup di Hello non viene visualizzato nel Server di Backup hello **processi** visualizzazione.

-   Backup Server riserva 30 GB di spazio sul volume di replica hello per il ripristino bare metal. È possibile modificare questo valore su hello **allocazione dei dischi** pagina nella procedura guidata Modifica gruppo protezione dati hello o utilizzando i cmdlet Get-DatasourceDiskAllocation e Set-DatasourceDiskAllocation PowerShell hello. Nel volume del punto di ripristino hello, protezione BMR richiede circa 6 GB per una conservazione di cinque giorni.
    * Si noti che non è possibile ridurre tooless di hello replica volume dimensione superiore a 15 GB.
    * Server di backup non Calcola dimensioni hello dell'origine dati di ripristino bare metal hello. Presume 30 GB per tutti i server. Modificare il valore di hello in base alle dimensioni di hello dei backup BMR previsti nell'ambiente in uso. dimensioni di Hello di un backup bare metal possono essere calcolata approssimativamente come somma hello di spazio utilizzato in tutti i volumi critici. Volumi critici = volume di avvio + volume di sistema + volume che ospita i dati dello stato del sistema, ad esempio Active Directory.

-   Se si modifica da protezione tooBMR protezione stato del sistema, protezione BMR richiede meno spazio sul hello *volume del punto di ripristino*. Tuttavia, hello spazio aggiuntivo sul volume hello non viene recuperato. È possibile compattare manualmente la dimensione del volume hello in hello **modifica allocazione dischi** pagina della procedura guidata Modifica gruppo protezione dati hello o utilizzando i cmdlet Get-DatasourceDiskAllocation e Set-DatasourceDiskAllocation PowerShell hello.

    Se si modifica da protezione tooBMR protezione stato del sistema, protezione BMR richiede più spazio sul hello *volume di replica*. volume Hello viene estesa automaticamente. Se si desidera allocazioni di spazio predefinite hello toochange, utilizzare i cmdlet di PowerShell Modify-DiskAllocation hello.

-   Se si modifica dalla protezione dello stato di ripristino bare metal protezione toosystem, è necessario più spazio sul volume del punto di ripristino hello. Backup Server potrebbe provare tooautomatically aumentare il volume di hello. Se è presente spazio insufficiente nel pool di archiviazione hello, si verifica un errore.

    Se si modifica dalla protezione dello stato di ripristino bare metal protezione toosystem, è necessario spazio sul computer protetto hello. In questo modo scrive innanzitutto computer locale di hello replica toohello protezione stato del sistema e quindi lo trasferisce toohello computer del Server di Backup.

## <a name="before-you-begin"></a>Prima di iniziare

1.  **Distribuire il server di Backup di Azure**. Verificare che il server di Backup sia distribuito correttamente. Per altre informazioni, vedere:
    * [Requisiti di sistema per il server di Backup di Azure](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)
    * [Matrice di protezione del server di Backup](backup-mabs-protection-matrix.md)

2.  **Configurare l'archiviazione**. È possibile archiviare i dati di backup su disco, su nastro e nel cloud hello con Azure. Per altre informazioni, vedere [Preparare l'archiviazione dei dati](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage).

3.  **Configurare l'agente protezione hello**. Installare l'agente protezione hello computer che si desidera ripristinare tooback hello. Per ulteriori informazioni, vedere [agente protezione DPM di hello Distribuisci](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent).

## <a name="back-up-system-state-and-bare-metal"></a>Backup dello stato del sistema e bare metal
Configurare un gruppo protezione dati come descritto in [Distribuire gruppi protezione dati](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups). Si noti che non è possibile proteggere il ripristino bare metal e stato di sistema per hello stesso computer in gruppi diversi. Inoltre, quando si seleziona il ripristino bare metal, lo stato del sistema viene abilitato automaticamente.


1.  le procedura guidata Crea nuovo gruppo protezione dati nella Console di amministrazione di Server di Backup, selezionare hello tooopen hello **protezione** > **azioni** > **Crea gruppo protezione dati Gruppo**.

2.  In hello **Selezione tipo di gruppo protezione dati** selezionare **server**e quindi selezionare **Avanti**.

3.  In hello **Seleziona membri del gruppo** pagina espandere hello computer e quindi selezionare **il ripristino bare metal** o **dello stato del sistema**.

    Tenere presente che non è possibile proteggere lo stato di ripristino bare metal e di sistema per hello stesso computer in gruppi diversi. Inoltre, quando si seleziona il ripristino bare metal, lo stato del sistema viene abilitato automaticamente. Per altre informazioni, vedere [Distribuire gruppi di protezione](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups).

4.  In hello **Selezione metodo protezione dati** pagina, selezionare la modalità di backup a breve termine e a lungo termine di toohandle. Backup a breve termine è sempre toodisk prima, con l'opzione hello di backup da disco di hello toohello Azure cloud con Azure Backup (a breve termine o a lungo termine). Un cloud di backup toohello termine toolong alternativo è tooset backup a lungo termine tooa backup autonomo dispositivo o un nastro libreria di nastri che è connesso tooBackup Server.

5.  In hello **Seleziona obiettivi a breve termine** pagina, selezionare la modalità tooback spazio di archiviazione tooshort termine su disco:
    1. Per **mantenimento**, selezionare la durata desiderata dati hello tookeep sul disco. 
    2. Per **frequenza di sincronizzazione**, selezionare la frequenza con cui si desidera toorun un toodisk backup incrementale. Se non si desidera tooset un intervallo di backup, è possibile controllare hello **immediatamente prima di un punto di ripristino** opzione. Il server di backup eseguirà un backup completo rapido appena prima di ogni punto di ripristino pianificato.

6.  Se si desidera toostore dati su nastro per l'archiviazione a lungo termine su hello **Specifica obiettivi a lungo termine** pagina, selezionare quanto tempo i dati del nastro tookeep (1-99 anni). 
    1. Per **frequenza di backup**, selezionare la frequenza di backup tootape deve essere eseguito. frequenza di Hello è basata sull'intervallo di conservazione hello selezionata:
        * Quando il periodo di conservazione hello è 1-99 anni, è possibile selezionare toooccur di backup giornaliera, settimanale, bisettimanale, mensile, trimestrale, semestrale o annuale.
        * Quando il periodo di conservazione hello è 1-11 mesi, è possibile selezionare toooccur di backup giornaliera, settimanale, bisettimanale o mensile.
        * Quando il periodo di conservazione hello è 1-4 settimane, è possibile selezionare toooccur di backup giornaliera o settimanale.

    2. In hello **selezione dettagli libreria e nastro** pagina, selezionare hello toouse libreria e nastro, e se i dati devono essere compressi e crittografati.

7.  In hello **Verifica allocazione dischi** verificare spazio su disco del pool di archiviazione hello allocata per il gruppo di protezione dati hello.

    1. **Totale dimensioni dati** hello dimensioni di dati di hello tooback da backup.
    2. **Toobe spazio su disco nel Server di Backup di Azure eseguito il provisioning** spazio hello del Server di Backup consigliata per gruppo protezione dati hello. Backup Server sceglie hello ideale volume di backup in base alle impostazioni di hello. Tuttavia, è possibile modificare le opzioni relative al volume di backup hello di **dettagli di allocazione del disco**. 
    3. Per i carichi di lavoro, nel menu a discesa hello, selezionare l'archiviazione hello preferito. Le modifiche modificano i valori di hello per **spazio di archiviazione totale** e **spazio di archiviazione** in hello **archiviazione su disco disponibile** riquadro. Lo spazio underprovisioned è quantità hello di archiviazione che il Server di Backup suggerisce che aggiungere volume toohello, tooensure smooth backup.

8.  In hello **Scegli metodo di creazione della Replica** pagina, selezionare la modalità di replica iniziale dei dati completo di toohandle hello. Se si sceglie tooreplicate rete hello, è consigliabile scegliere un orario. Per grandi quantità di dati o per le condizioni della rete che sono ottimali, prendere in considerazione la replica dei dati hello offline usando supporti rimovibili.

9. In hello **scegliere Opzioni di verifica coerenza** pagina, selezionare la modalità di tooautomate le verifiche di coerenza. È possibile scegliere un controllo toorun solo quando i dati di replica diventano incoerenti o in una pianificazione. Se non si desidera tooconfigure verifica di coerenza automatica, è possibile eseguire una verifica manuale in qualsiasi momento. una verifica manuale, in hello toorun **protezione** area di hello Console di amministrazione di Server di Backup, fare doppio clic su protezione hello gruppo e quindi seleziona **Esegui verifica coerenza**.

10. Se è stata selezionata tooback backup cloud toohello da Backup di Azure, in hello **specificare dati da proteggere Online** pagina, assicurarsi di selezionare i carichi di lavoro hello desiderato tooback backup tooAzure.

11. In hello **specificare la pianificazione dei Backup Online** pagina, selezionare la frequenza con cui incrementali tooAzure si verificherà. È possibile pianificare i backup toorun ogni giorno, settimana, mese e anno e selezionare Data e ora hello in corrispondenza del quale deve essere eseguito. I backup possono verificarsi backup tootwice al giorno. Ogni volta che viene eseguito un backup, un punto di ripristino di dati viene creato in Azure da copia hello hello dei dati di backup archiviati su disco di Backup Server hello.

12. In hello **specificare criteri di conservazione Online** selezionare come punti di ripristino hello che vengono creati dal backup giornaliero, settimanale, mensile e annuale di hello vengono mantenuti in Azure.

13. In hello **Scegli replica Online** selezionare modalità hello iniziale completa dei dati di replica. È possibile replicare in rete hello o eseguire un backup (seeding non in linea). Backup offline Usa funzionalità di importazione di Azure hello. Per altre informazioni, vedere [Flusso di lavoro del backup offline in Backup di Azure](backup-azure-backup-import-export.md).

14. In hello **riepilogo** pagina, rivedere le impostazioni. Dopo aver selezionato **Crea gruppo**, viene eseguita la replica iniziale dei dati di hello. Quando viene completata la replica dei dati, in hello **stato** pagina stato del gruppo protezione dati hello è **OK**. Il backup viene eseguito per la protezione hello quindi le impostazioni di gruppo.

## <a name="recover-system-state-or-bmr"></a>Ripristino dello stato del sistema o bare metal
È possibile ripristinare percorso di rete tooa lo stato del sistema o del ripristino bare metal. Se hai eseguito un backup bare metal, utilizzare il sistema di toostart ambiente ripristino Windows (WinRE) e connetterla toohello rete. Quindi, è possibile utilizzare Windows Server Backup toorecover dal percorso di rete hello. Se hai eseguito un backup dello stato del sistema, è sufficiente utilizzare Windows Server Backup toorecover dal percorso di rete hello.

### <a name="restore-bmr"></a>Ripristino bare metal
Eseguire il ripristino nel computer del Server di Backup hello:

1.  In hello **ripristino** riquadro, individuare i computer di hello toorecover desiderato e quindi selezionare **ripristino Bare Metal**.

2.  Punti di ripristino disponibili sono indicati in grassetto nel calendario hello. Hello selezionare Data e ora per il punto di ripristino hello che si desidera toouse.

3.  In hello **Selezione tipo di ripristino** selezionare **copia tooa cartella di rete.**

4.  In hello **specifica destinazione** pagina, selezionare in cui si desidera toocopy hello dati. Tenere presente che la destinazione selezionata hello deve toohave spazio sufficiente. È consigliabile creare una nuova cartella.

5.  In hello **Specifica opzioni di ripristino** pagina, tooapply le impostazioni di sicurezza selezionare hello. Quindi, selezionare se si desidera rete di toouse archiviazione (SAN)-basato su snapshot dell'hardware, per un ripristino più veloce. (Si tratta di un'opzione solo se si dispone di una SAN con questa funzionalità è disponibile e hello toocreate possibilità e divisa toomake un clone è accessibile in scrittura. Inoltre, hello computer protetto e il computer Server di Backup deve essere connesso toohello stessa rete.)

6.  Configurare le opzioni di notifica. In hello **conferma** selezionare **ripristinare**.

Impostare il percorso della condivisione hello:

1.  Nel percorso di ripristino hello, andare toohello cartella il cui backup hello.

2.  Condivisione cartella hello in un livello superiore rispetto a WindowsImageBackup in modo da radice della cartella condivisa hello hello è cartella WindowsImageBackup hello. Se non si esegue questa operazione, ripristino non trovare backup hello. tooconnect tramite ambiente ripristino Windows (WinRE), è necessario una condivisione accessibile in ambiente ripristino Windows con le credenziali e l'indirizzo IP corretto hello.

Ripristinare il sistema di hello:

1.  Avviare il computer di hello in cui si desidera che toorestore hello immagine usando il DVD di Windows hello per sistema hello da ripristinare.

2.  Sulla prima pagina hello, verificare le impostazioni di lingua e delle impostazioni locali. In hello **installare** selezionare **Ripristina il computer**.

3.  In hello **Opzioni ripristino di sistema** selezionare **ripristinare il computer utilizzando un'immagine del sistema creato in precedenza**.

4.  In hello **selezionare un backup dell'immagine del sistema** selezionare **selezionare un'immagine del sistema** > **avanzate** > **ricerca per un sistema immagine di rete hello**. Se viene visualizzato un avviso, selezionare **Sì**. Passare il percorso di condivisione toohello, immettere le credenziali di hello e quindi selezionare il punto di ripristino di hello. Viene avviata la ricerca di backup specifici disponibili nel punto di ripristino. Selezionare il punto di ripristino hello che si desidera toouse.

5.  In hello **scegliere come toorestore hello backup** selezionare **formatta e partiziona i dischi**. Nella pagina successiva di hello, verificare le impostazioni. 

6.  ripristino di hello toobegin, seleziona **fine**. È necessario un riavvio.

### <a name="restore-system-state"></a>Ripristino dello stato del sistema

Eseguire il ripristino nel server di Backup:

1.  In hello **ripristino** riquadro Trova hello computer che desidera toorecover e quindi selezionare **ripristino Bare Metal**.

2.  Punti di ripristino disponibili sono indicati in grassetto nel calendario hello. Hello selezionare Data e ora per il punto di ripristino hello che si desidera toouse.

3.  In hello **Selezione tipo di ripristino** selezionare **cartella di rete copia tooa**.

4.  In hello **specifica destinazione** pagina, selezionare il percorso dati hello toocopy. Tenere presente che la destinazione selezionata hello è necessario spazio sufficiente. È consigliabile creare una nuova cartella.

5.  In hello **Specifica opzioni di ripristino** pagina, tooapply le impostazioni di sicurezza selezionare hello. Selezionare quindi se si desidera che gli snapshot hardware basati su SAN toouse per un ripristino più veloce. (Si tratta di un'opzione solo se si dispone di una SAN con questa funzionalità e capacità toocreate hello e divisa toomake un clone è accessibile in scrittura. Inoltre, hello computer protetto e il Server di Backup deve essere connesso toohello stessa rete.)

6.  Configurare le opzioni di notifica. In hello **conferma** selezionare **ripristinare**.

Eseguire Windows Server Backup:

1.  Selezionare **Azioni** > **Ripristina** > **Questo server** > **Avanti**.

2.  Selezionare **un altro Server**selezionare hello **impostazione tipo di percorso** pagina e quindi selezionare **cartella condivisa remota**. Immettere hello toohello cartella che contiene il punto di ripristino hello.

3.  In hello **Selezione tipo di ripristino** selezionare **dello stato del sistema**. 

4. In hello **Selezione percorso per il ripristino dello stato del sistema** selezionare **nel percorso originale**.

5.  In hello **conferma** selezionare **ripristinare**. Dopo il ripristino di hello, riavviare il server di hello.

6.  È anche possibile eseguire hello ripristino dello stato del sistema a un prompt dei comandi. toodo, Windows Server Backup di start computer hello desiderato toorecover. Identificatore di versione hello tooget, al prompt dei comandi, immettere:```wbadmin get versions -backuptarget \<servername\sharename\>```

    Utilizzare hello versione identificatore toostart hello ripristino del sistema. Al prompt dei comandi di hello, immettere:```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    Confermare che si desidera ripristino hello toostart. È possibile visualizzare il processo di hello nella finestra del prompt dei comandi hello. Viene creato un registro di ripristino. Dopo il ripristino di hello, riavviare il server di hello.

