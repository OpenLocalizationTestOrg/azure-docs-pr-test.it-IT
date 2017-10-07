---
title: modello di distribuzione classica di hello aaaRestore tooa di dati di Windows Server o Client Windows dall'utilizzo di Azure | Documenti Microsoft
description: Informazioni su come toorestore da Windows Server o Client Windows.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a>Ripristinare i file tooa Windows server o computer client Windows utilizzando il modello di distribuzione classica hello
> [!div class="op_single_selector"]
> * [Portale classico](backup-azure-restore-windows-server-classic.md)
> * [Portale di Azure](backup-azure-restore-windows-server.md)
>
>

Questo articolo spiega come toorecover dati da un backup dell'insieme di credenziali e ripristino tooa server o computer. A partire da marzo 2017, è possibile creare non più insiemi di credenziali di backup nel portale classico hello.

> [!IMPORTANT]
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> **15 ottobre 2017**, non potrà più insiemi di credenziali Backup a toocreate toouse in grado di PowerShell. <br/> **A partire dal 1° novembre 2017**:
>- Gli insiemi di credenziali di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>

dati toorestore, guidata hello Ripristina dati nell'agente di Microsoft Azure Recovery Services (MARS) hello. Quando si ripristinano dati, è possibile:

* Ripristino dati toohello stesso computer dai quali backup hello sono stati eseguiti.
* Ripristinare dati tooan alternativo macchina.

Gennaio January 2017, Microsoft ha rilasciato un agente di anteprima aggiornamento toohello MARS. Insieme a correzioni di bug, questo aggiornamento consente a ripristinare immediata, che consente di toomount uno snapshot del punto di ripristino scrivibile come volume di ripristino. È quindi possibile esplorare hello ripristino volume e copia i file tooa computer locale in modo selettivo il ripristino dei file.

> [!NOTE]
> Hello [gennaio January 2017 aggiornamento di Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) è obbligatorio se si desidera toouse ripristino immediato toorestore dati. Dati di backup hello devono inoltre essere protetti in insiemi di credenziali in impostazioni locali elencate nell'articolo di supporto tecnico hello. Consultare hello [gennaio January 2017 aggiornamento di Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) per l'elenco più recente di hello delle impostazioni locali che supportano il ripristino immediato. Il ripristino istantaneo **non** è attualmente disponibile in tutte le impostazioni locali.
>

Ripristino immediato è disponibile per l'uso di insiemi di credenziali di servizi di ripristino in hello portale di Azure e gli insiemi di credenziali di Backup nel portale classico hello. Se si desidera ripristinare immediata toouse, scaricare l'aggiornamento di MARS hello e seguire le procedure hello che menzionano il ripristino immediato.


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a>Utilizzare il ripristino immediato toorecover dati toohello nello stesso computer

Se è stato eliminato accidentalmente un file e preferenze di toorestore è toohello stessa macchina (da cui hello backup viene eseguito), hello seguendo i passaggi consentono di ripristinare i dati di hello.

1. Aprire hello **Backup di Microsoft Azure** allineamento in. Se non si conosce in cui è stato installato hello snap-in, eseguire la ricerca computer hello o un server per **Microsoft Azure Backup**.

    app desktop Hello dovrebbe essere visualizzato nei risultati della ricerca hello.

2. Fare clic su **Ripristina dati** guidata hello toostart.

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

3. In hello **Introduzione** riquadro, toorestore hello dati toohello stesso server o computer, selezionare **server (`<server name>`)** e fare clic su **Avanti**.

    ![Scegliere questo toohello di dati server opzione toorestore hello nello stesso computer](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. In hello **selezionare la modalità di ripristino** riquadro scegliere **singoli file e cartelle** e quindi fare clic su **Avanti**.

    ![Ricerca dei file](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. In hello **seleziona Volume e data** riquadro, volume hello select che contiene i file hello e/o le cartelle da toorestore.

    Calendario hello, selezionare un punto di ripristino. È possibile ripristinare da qualsiasi punto di ripristino. Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino. Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa.

    ![Volume e dati](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. Dopo aver scelto toorestore punto di ripristino hello, fare clic su **montare**.

    Backup di Azure monta il punto di ripristino locali hello che viene utilizzato come un volume di ripristino.

7. In hello **Sfoglia e ripristinare i file** riquadro, fare clic su **Sfoglia** tooopen in Esplora risorse e individuare i file hello e le cartelle desiderate.

    ![Opzioni di ripristino](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. In Esplora risorse, la copia di file hello e/o le cartelle si toorestore e incollarlo tooany percorso locale toohello server o computer. È possibile aprire o flusso di file hello direttamente dal volume di ripristino hello e verificare hello corretto versioni vengono ripristinate.

    ![Copiare e incollare i file e cartelle dal percorso toolocal volume montato](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. Al termine il ripristino file hello e/o cartelle, hello **Sfoglia e i file di ripristino** riquadro, fare clic su **Smonta**. Quindi fare clic su **Sì** tooconfirm che si desidera volume hello toounmount.

    ![Smontare il volume di hello e verificare](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > Se non si sceglie Smonta, hello ripristino Volume rimarrà montata per sei ore dall'ora di hello quando è stato montato. Nessuna operazione di backup verranno eseguito mentre hello volume montato. Toorun qualsiasi operazione di backup pianificato durante la fase di hello quando hello volume montato, verrà eseguito dopo il volume di ripristino hello viene disinstallato.
    >


## <a name="recover-data-toohello-same-machine"></a>Ripristinare i dati toohello nello stesso computer
Se è stato eliminato accidentalmente un file e preferenze di toorestore è toohello stessa macchina (da cui hello backup viene eseguito), hello seguendo i passaggi consentono di ripristinare i dati di hello.

1. Aprire hello **Backup di Microsoft Azure** allineamento in.
2. Fare clic su **Ripristina dati** flusso di lavoro tooinitiate hello.

    ![Ripristina dati](./media/backup-azure-restore-windows-server-classic/recover.png)
3. Seleziona hello * *server (*yourmachinename*) * * hello toorestore opzione file di backup su hello stesso computer.

    ![Nello stesso computer](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. Scegliere troppo**Sfoglia file** o **Cerca file**.

    Lasciare opzione predefinita hello se si prevede di toorestore uno o più file il cui percorso è noto. Se si desidera toosearch per un file dubbi sulla struttura di cartelle hello, selezionare hello **Cerca file** opzione. A scopo di hello in questa sezione, si procederà con l'opzione predefinita di hello.

    ![Ricerca dei file](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. Selezionare il volume di hello da cui si desidera file hello toorestore.

    È possibile ripristinare da qualsiasi data. Date visualizzate in **grassetto** nel controllo di calendario hello indicare la disponibilità di hello di un punto di ripristino. Dopo aver selezionata una data, in base alla pianificazione di backup (e successo hello di un'operazione di backup), è possibile selezionare un punto nel tempo da hello **ora** elenco a discesa.

    ![Volume e dati](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. Selezionare toorecover elementi hello. È possibile selezioni più cartelle/file desiderato toorestore.

    ![Selezione dei file](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. Specificare parametri per il ripristino hello.

    ![Opzioni di ripristino](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * È disponibile un'opzione di ripristino nel percorso originale toohello (in cui hello file/cartella verrebbe sovrascritto) o una posizione tooanother in hello nello stesso computer.
   * Se hello file/cartella in cui è presente nel percorso di destinazione hello toorestore, è possibile creare copie (due versioni di hello stesso file), sovrascrivere i file nel percorso di destinazione hello hello o ignorare il ripristino del file hello che esistono nella destinazione hello hello.
   * Si consiglia di lasciare l'opzione predefinita hello ripristino hello ACL nel file hello che verrà eseguito il ripristino.
8. Una volta forniti i dati di input, fare clic su **Avanti**. Hello ripristino flusso di lavoro che ripristina hello file toothis macchina, verrà avviato.

## <a name="recover-tooan-alternate-machine"></a>Ripristinare tooan alternativo macchina
Se l'intero server viene perso, è comunque possibile ripristinare dati da computer diversi tooa di Backup di Azure. Hello alla procedura seguente viene illustrato del flusso di lavoro di hello.  

terminologia di Hello utilizzata in questa procedura include:

* *Computer di origine* : macchina originale di hello dal backup hello è stato eseguito e non è attualmente disponibile.
* *Computer di destinazione* : dati di hello macchina toowhich hello viene ripristinati.
* *Insieme di credenziali di esempio* : hello toowhich insieme di credenziali di hello Backup *macchina di origine* e *nel computer di destinazione* registrati. <br/>

> [!NOTE]
> Impossibile ripristinare i backup eseguiti da un computer in un computer in cui è in esecuzione una versione precedente del sistema operativo hello. Ad esempio, se i backup vengono eseguiti da un computer che esegue Windows 7, è possibile ripristinare i dati in un computer con Windows 8 o versione successiva. Tuttavia, hello viceversa non ha valore true.
>
>

1. Aprire hello **Backup di Microsoft Azure** allineamento in su hello *nel computer di destinazione*.
2. Verificare che hello *inviala* hello e *macchina di origine* sono registrato toohello stesso insieme di credenziali di backup.
3. Fare clic su **Ripristina dati** flusso di lavoro tooinitiate hello.

    ![Ripristina dati](./media/backup-azure-restore-windows-server-classic/recover.png)
4. Selezionare **Un altro server**

    ![Un altro server](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. Fornire file delle credenziali dell'insieme di credenziali hello corrispondente toohello *insieme di credenziali di esempio*. Se file di credenziali dell'insieme di credenziali hello (scaduti o non validi) scaricare un nuovo file delle credenziali dell'insieme di credenziali da hello *insieme di credenziali di esempio* nel portale di Azure classico hello. Una volta file delle credenziali dell'insieme di credenziali hello viene fornito, viene visualizzato insieme di credenziali backup hello su file delle credenziali dell'insieme di credenziali hello.
6. Seleziona hello *macchina di origine* dall'elenco di hello macchine visualizzato.

    ![Elenco di computer](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. Selezionare entrambi hello **Cerca file** o **Sfoglia file** opzione. A scopo di hello in questa sezione, si utilizzerà hello **Cerca file** opzione.

    ![Ricerca](./media/backup-azure-restore-windows-server-classic/search.png)
8. Selezionare il volume di hello e alla data nella schermata successiva hello. Ricerca per nome di cartella/file hello desiderato toorestore.

    ![Ricerca di elementi](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. Selezionare il percorso di hello in cui è necessario ripristinare toobe hello file.

    ![Percorso di ripristino](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. Fornire una passphrase di crittografia hello fornita durante *macchina di origine* registrazione troppo*insieme di credenziali di esempio*.

    ![Crittografia](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. Una volta hello input viene fornito, fare clic su **ripristinare**, che i trigger hello ripristino del backup del file di destinazione toohello fornito hello.

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a>Utilizzare il ripristino immediato toorestore dati tooan macchina alternativo
Se l'intero server viene perso, è comunque possibile ripristinare dati da computer diversi tooa di Backup di Azure. Hello alla procedura seguente viene illustrato del flusso di lavoro di hello.

terminologia di Hello utilizzata in questa procedura include:

* *Computer di origine* : macchina originale di hello dal backup hello è stato eseguito e non è attualmente disponibile.
* *Computer di destinazione* : dati di hello macchina toowhich hello viene ripristinati.
* *Insieme di credenziali di esempio* : hello toowhich insieme di credenziali per servizi di ripristino di hello *macchina di origine* e *nel computer di destinazione* registrati. <br/>

> [!NOTE]
> I backup non possono essere ripristinato tooa computer di destinazione esegue una versione precedente del sistema operativo hello. Ad esempio, un backup eseguito su un computer con Windows 7 può essere ripristinato in un computer con Windows 8 o versioni successive. Un backup eseguito da un computer Windows 8 non può essere ripristinato tooa Windows 7 computer.
>
>

1. Aprire hello **Backup di Microsoft Azure** allineamento in su hello *nel computer di destinazione*.

2. Assicurarsi di hello *nel computer di destinazione* hello e *macchina di origine* sono registrato toohello servizi di ripristino stesso insieme di credenziali.

3. Fare clic su **Ripristina dati** tooopen hello **procedura guidata Ripristina dati**.

    ![Ripristina dati](./media/backup-azure-restore-windows-server/recover.png)

4. In hello **Introduzione** riquadro, selezionare **un altro server**

    ![Un altro server](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. Fornire file delle credenziali dell'insieme di credenziali hello corrispondente toohello *insieme di credenziali di esempio*, fare clic su **Avanti**.

    Caso di file delle credenziali dell'insieme di credenziali hello (scaduti o non validi), è possibile scaricare un nuovo file delle credenziali dell'insieme di credenziali da hello *insieme di credenziali di esempio* in hello portale di Azure. Dopo aver specificato un insieme valido di credenziali, nome hello di hello corrispondente dell'insieme di credenziali di Backup.

6. In hello **selezione Server di Backup** riquadro, seleziona hello *macchina di origine* dall'elenco di hello macchine visualizzati e fornire la passphrase hello. Quindi fare clic su **Next**.

    ![Elenco di computer](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. In hello **selezionare la modalità di ripristino** riquadro **singoli file e cartelle** e fare clic su **Avanti**.

    ![Ricerca](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. In hello **seleziona Volume e data** riquadro, volume hello select che contiene i file hello e/o le cartelle da toorestore.

    Calendario hello, selezionare un punto di ripristino. È possibile ripristinare da qualsiasi punto di ripristino. Le date in **grassetto** indicare hello la disponibilità di almeno un punto di ripristino. Dopo aver selezionato una data, se sono disponibili più punti di ripristino, scegliere il punto di ripristino specifico di hello da hello **ora** dal menu a discesa.

    ![Ricerca di elementi](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. Fare clic su **montare** toolocally montaggio hello punto di ripristino come in un volume di ripristino del *nel computer di destinazione*.

10. In hello **Sfoglia e ripristinare i file** riquadro, fare clic su **Sfoglia** tooopen in Esplora risorse e individuare i file hello e le cartelle desiderate.

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. In Esplora risorse, copiare i file hello o le cartelle dal volume di ripristino hello e incollarli tooyour *inviala* percorso. È possibile aprire o flusso di file hello direttamente dal volume di ripristino hello e verificare hello corretto versioni vengono ripristinate.

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. Al termine il ripristino file hello e/o cartelle, hello **Sfoglia e i file di ripristino** riquadro, fare clic su **Smonta**. Quindi fare clic su **Sì** tooconfirm che si desidera volume hello toounmount.

    ![Crittografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > Se non si sceglie Smonta, hello ripristino Volume rimarrà montata per sei ore dall'ora di hello quando è stato montato. Nessuna operazione di backup verranno eseguito mentre hello volume montato. Toorun qualsiasi operazione di backup pianificato durante la fase di hello quando hello volume montato, verrà eseguito dopo il volume di ripristino hello viene disinstallato.
    >


## <a name="next-steps"></a>Passaggi successivi
* [Backup di Azure - Domande frequenti](backup-azure-backup-faq.md)
* Visitare hello [Forum di Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933).

## <a name="learn-more"></a>Altre informazioni
* [Panoramica di Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [Eseguire il backup di macchine virtuali di Azure](backup-azure-vms-introduction.md)
* [Eseguire il backup dei carichi di lavoro di Microsoft](backup-azure-dpm-introduction.md)
