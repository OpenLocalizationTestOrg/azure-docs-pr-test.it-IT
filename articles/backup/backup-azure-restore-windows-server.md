---
title: dati aaaRestore tooa Azure Windows Server o computer Windows | Documenti Microsoft
description: Informazioni su come i dati toorestore archiviati in Azure tooa Windows Server o computer Windows.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a>Ripristinare i file tooa Windows server o computer client Windows utilizzando il modello di distribuzione di gestione risorse
> [!div class="op_single_selector"]
> * [Portale di Azure](backup-azure-restore-windows-server.md)
> * [Portale classico](backup-azure-restore-windows-server-classic.md)
>
>

Questo articolo viene illustrato come toorestore dati da un insieme di credenziali di backup. dati toorestore, guidata hello Ripristina dati nell'agente di Microsoft Azure Recovery Services (MARS) hello. Quando si ripristinano dati, è possibile:

* Ripristino dati toohello stesso computer dai quali backup hello sono stati eseguiti.
* Ripristinare dati tooan alternativo macchina.

Gennaio January 2017, Microsoft ha rilasciato un agente di anteprima aggiornamento toohello MARS. Insieme a correzioni di bug, questo aggiornamento consente a ripristinare immediata, che consente di toomount uno snapshot del punto di ripristino scrivibile come volume di ripristino. È quindi possibile esplorare hello ripristino volume e copia i file tooa computer locale in modo selettivo il ripristino dei file.

> [!NOTE]
> Hello [gennaio January 2017 aggiornamento di Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) è obbligatorio se si desidera toouse ripristino immediato toorestore dati. Dati di backup hello devono inoltre essere protetti in insiemi di credenziali in impostazioni locali elencate nell'articolo di supporto tecnico hello. Consultare hello [gennaio January 2017 aggiornamento di Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) per l'elenco più recente di hello delle impostazioni locali che supportano il ripristino immediato. Il ripristino istantaneo **non** è attualmente disponibile in tutte le impostazioni locali.
>

Ripristino immediato è disponibile per l'uso di insiemi di credenziali di servizi di ripristino in hello portale di Azure e gli insiemi di credenziali di Backup nel portale classico hello. Se si desidera ripristinare immediata toouse, scaricare l'aggiornamento di MARS hello e seguire le procedure hello che menzionano il ripristino immediato.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

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
    > Se non si sceglie Smonta, hello ripristino Volume rimarrà montata per 6 ore dall'ora di hello quando è stato montato. Tuttavia, il tempo di montaggio hello è estesa fino a un massimo di 24 ore in caso di una copia di file in corso. Nessuna operazione di backup verranno eseguito mentre hello volume montato. Toorun qualsiasi operazione di backup pianificato durante la fase di hello quando hello volume montato, verrà eseguito dopo il volume di ripristino hello viene disinstallato.
    >


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
    > Se non si sceglie Smonta, hello ripristino Volume rimarrà montata per 6 ore dall'ora di hello quando è stato montato. Tuttavia, il tempo di montaggio hello è estesa fino a un massimo di 24 ore in caso di una copia di file in corso. Nessuna operazione di backup verranno eseguito mentre hello volume montato. Toorun qualsiasi operazione di backup pianificato durante la fase di hello quando hello volume montato, verrà eseguito dopo il volume di ripristino hello viene disinstallato.
    >

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se Azure Backup non correttamente montare il volume di ripristino hello anche dopo diversi minuti di facendo clic su **montare** o volume di ripristino ha esito negativo toomount hello con uno o più errori, seguire i passaggi di hello sotto toobegin ripristino normalmente.

1.  Annullare il processo di installazione in corso hello nel caso in cui è in esecuzione per diversi minuti.

2.  Verificare che trovino in più recente dell'agente di Backup di Azure hello hello. toofind le informazioni sulla versione di hello di Azure Backup agent, fare clic su **su Microsoft Azure Recovery Services Agent** su hello **azioni** riquadro di Microsoft Azure Backup console e verificare che hello  **Versione** numero è uguale tooor superiore indicato nella versione di hello [questo articolo](https://go.microsoft.com/fwlink/?linkid=229525). È possibile scaricare una versione più recente di hello dal [qui](https://go.microsoft.com/fwLink/?LinkID=288905)

3.  Andare troppo**Gestione dispositivi** -> **i controller di archiviazione** e assicurarsi che sia possibile individuare **iniziatore iSCSI Microsoft**. Se si desidera trovare, passare direttamente toostep 7 seguente. 

4.  Se è possibile individuare servizio iniziatore iSCSI Microsoft, come indicato nel passaggio 3, controllare toosee se è possibile trovare una voce nella sezione **Gestione dispositivi** -> **i controller di archiviazione** chiamato  **Dispositivo sconosciuto** con l'ID Hardware **ROOT\ISCSIPRT**.

5.  Fare clic con il pulsante destro del mouse su **Dispositivo sconosciuto** e scegliere **Aggiornamento software driver**.

6.  Aggiorna driver hello selezionando l'opzione hello troppo **cerca automaticamente un driver aggiornato**. Completamento dell'aggiornamento hello debba modificare **dispositivo sconosciuto** troppo**iniziatore iSCSI Microsoft** come illustrato di seguito. 

    ![Crittografia](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  Andare troppo**Task Manager** -> **servizi (locale)** -> **servizio iniziatore iSCSI Microsoft**. 

    ![Crittografia](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  Riavviare servizio iniziatore iSCSI Microsoft di hello facendo clic sul servizio hello, facendo clic su **arrestare** e ulteriormente destro del mouse facendo clic su Nuovo e facendo clic su **avviare**.

9.  Riprovare il ripristino istantaneo. 

Se non riesce ripristino hello, riavviare il server e client. Se non è auspicabile il riavvio o recupero hello persistono anche dopo il riavvio hello server, riprovare il ripristino da un computer alternativo e contattare il supporto di Azure passando troppo[portale Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e l'invio di una richiesta di supporto.

## <a name="next-steps"></a>Passaggi successivi
* Dopo aver ripristinato i file e le cartelle, è possibile [gestire i backup](backup-azure-manage-windows-server.md).
