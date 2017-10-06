---
title: aaaAzure Backup per i carichi di lavoro di SQL Server tramite il Server di Backup di Azure | Documenti Microsoft
description: Toobacking un'introduzione dei database di SQL Server tramite il Server di Backup di Azure
services: backup
documentationcenter: 
author: pvrk
manager: Shivamg
editor: 
ms.assetid: c8b1f7ec-26b1-4ef0-a3f2-91aec959daea
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 3a94338e8aca3f9d8611a72bcd223397ffb96f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-with-azure-backup-server"></a>Eseguire il backup di SQL Server tooAzure con Server di Backup di Azure
In questo articolo vengono descritti i passaggi di configurazione hello per il backup dei database di SQL Server utilizzando Microsoft Azure Backup Server (MABS).

gestione di Hello tooAzure di backup del database di SQL Server e il ripristino da Azure prevede tre passaggi:

1. Creare un database tooAzure di criteri di backup tooprotect SQL Server.
2. Creare copie di backup su richiesta tooAzure.
3. Ripristinare il database di hello da Azure.

## <a name="before-you-start"></a>Prima di iniziare
Prima di iniziare, assicurarsi di aver [installati e preparati hello Azure Backup Server](backup-azure-microsoft-azure-backup.md).

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>Creare un database tooAzure di criteri di backup tooprotect SQL Server
1. Scegliere hello hello Azure Backup Server UI, **protezione** dell'area di lavoro.
2. Sulla barra multifunzione dello strumento di hello, fare clic su **New** toocreate un nuovo gruppo protezione dati.

    ![Creazione di un gruppo di protezione](./media/backup-azure-backup-sql/protection-group.png)
3. MABS Mostra una schermata iniziale di hello indicazioni hello sulla creazione di un **gruppo protezione dati**. Fare clic su **Avanti**.
4. Selezione dei **Server**.

    ![Selezione del tipo di gruppo di protezione "Server"](./media/backup-azure-backup-sql/pg-servers.png)
5. Espandere il computer di SQL Server hello in cui sono presenti toobe database hello eseguito il backup. MABS mostra diverse origini dati di cui è possibile eseguire il backup in quel server. Espandere hello **tutte le condivisioni SQL** e selezionare il database di hello (in questo caso è selezionato ReportServer$ MSDPM2012 e ReportServer$ MSDPM2012TempDB) toobe il backup. Fare clic su **Avanti**.

    ![Selezione del database SQL](./media/backup-azure-backup-sql/pg-databases.png)
6. Specificare un nome per il gruppo di protezione dati hello e selezionare hello **protezione dati online** casella di controllo.

    ![Metodo di protezione dei dati - disco a breve termine e online in Azure](./media/backup-azure-backup-sql/pg-name.png)
7. In hello **Specifica obiettivi a breve termine** schermata, includere hello input necessario toocreate punti backup toodisk.

    Qui è possibile vedere che **mantenimento** è troppo*5 giorni*, **frequenza di sincronizzazione** è impostato tooonce ogni *15 minuti* ovvero hello frequenza con cui viene creato il backup. **Backup completo rapido** è troppo*8:00 formato*.

    ![Obiettivi a breve termine](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > 8:00 PM (in base a input schermata toohello) viene creato un punto di backup ogni giorno trasferendo dati hello che sono stati modificati da hello punto di backup ore 8:00 del giorno precedente. Questo processo è detto **Backup completo rapido**. Mentre i log delle transazioni hello vengono sincronizzati ogni 15 minuti, se è presente un database di hello toorecover necessario al 21:00:00: hello punto viene creato mediante la riproduzione registri hello hello express ultimo punto di backup completo (alle 20.00 in questo caso).
   >
   >

8. Fare clic su **Avanti**

    Mostra MABS hello complessiva dello spazio di archiviazione disponibile e hello potenziali spazio su disco.

    ![Allocazione dei dischi](./media/backup-azure-backup-sql/pg-storage.png)

    Per impostazione predefinita, MABS crea un volume per ogni origine dati (database di SQL Server) che viene utilizzato per la copia di backup iniziale di hello. Questo approccio, hello disco Manager LOGICI limita origini di dati too300 protezione MABS (database di SQL Server). toowork risolvere questa limitazione, seleziona hello **Condividi percorso dati nel Pool di archiviazione DPM**, opzione. Se si utilizza questa opzione, MABS utilizza un singolo volume per più origini dati, che consente di tooprotect MABS dei database SQL too2000.

    Se **Espandi automaticamente i volumi di hello** opzione è selezionata, MABS può tenere conto per il volume di backup hello aumentato man mano che aumenta il dati di produzione hello. Se **Espandi automaticamente i volumi di hello** opzione non è selezionata, MABS limita hello origini dati toohello di archiviazione di backup utilizzata nel gruppo protezione dati hello.
9. Gli amministratori possibile scegliere di hello del trasferimento di questa congestione della larghezza di banda iniziale tooavoid backup manualmente (fuori rete) o tramite rete hello. È inoltre possibile configurare ora hello in cui hello può verificarsi trasferimento iniziale. Fare clic su **Avanti**.

    ![Metodo di replica iniziale](./media/backup-azure-backup-sql/pg-manual.png)

    copia di backup iniziale Hello è necessario trasferire hello intera origine dei dati (database di SQL Server) da tooMABS (computer di SQL Server) di server di produzione. Tali dati potrebbero essere elevati e trasferimento dei dati di hello in rete hello può superare la larghezza di banda. Per questo motivo, gli amministratori possono scegliere di backup iniziale di hello tootransfer: **manualmente** (utilizzando supporti rimovibili) tooavoid congestione di larghezza di banda, o **automaticamente tramite rete hello** (in un oggetto specificato ora).

    Al termine del backup iniziale hello, hello altri backup hello sono backup incrementali sulla copia di backup iniziale hello. I backup incrementali tendono toobe piccola e facilmente vengono trasferiti in rete di hello.
10. Scegliere quando si desidera toorun di controllo di coerenza hello e fare clic su **Avanti**.

    ![Verifica coerenza](./media/backup-azure-backup-sql/pg-consistent.png)

    MABS è possibile eseguire un integrità di hello toocheck controllo coerenza del punto di backup hello. Viene calcolato il checksum hello hello del file di backup nel server di produzione hello (computer di SQL Server in questo scenario) e i dati di backup hello per tale file in MABS. In caso di hello di un conflitto, si presuppone che hello in MABS file di backup è danneggiato. MABS corregge i dati di backup hello inviando blocchi hello corrispondente toohello mancata corrispondenza del checksum. Verifica di coerenza hello è un'operazione di prestazioni, gli amministratori hanno il possibilità di hello di pianificazione di coerenza hello o eseguirla automaticamente.
11. toospecify protezione di origini dati hello online, selezionare hello database toobe protetti tooAzure e fare clic su **Avanti**.

    ![Selezione delle origini dati](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. Gli amministratori possono scegliere le pianificazioni di backup e i criteri di conservazione adatti a soddisfare i criteri dell'organizzazione.

    ![Pianificazione e conservazione](./media/backup-azure-backup-sql/pg-schedule.png)

    In questo esempio, i backup vengono eseguiti una volta al giorno alle 12:00 e alle 20.00 (parte inferiore della schermata Ciao)

    > [!NOTE]
    > È una buona norma toohave alcuni punti di ripristino a breve termine su disco, per un ripristino veloce. Questi punti di ripristino vengono usati per il "ripristino operativo". Azure è una posizione esterna ottimale con contratti di servizio più elevati e disponibilità garantita.
    >
    >

    **Procedura consigliata**: assicurarsi che i backup di Azure vengono programmati dopo il completamento di hello del backup del disco locale utilizzando Data Protection Manager. In questo modo tooAzure toobe backup copiati su disco più recente di hello.

13. Scegliere la pianificazione dei criteri di conservazione hello. vengono forniti i dettagli di Hello sul funzionamento di criteri di conservazione hello in [tooreplace utilizzare Azure Backup l'articolo di infrastruttura nastro](backup-azure-backup-cloud-as-tape.md).

    ![Criteri di conservazione](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    Esempio:

    * I backup vengono eseguiti una volta al giorno alle 12:00 e alle 20.00 (parte inferiore della schermata Ciao) e vengono mantenuti per 180 giorni.
    * backup di Hello sabato alle ore 12:00. viene conservato per 104 settimane
    * backup di Hello ultimo sabato alle ore 12:00. viene conservato per 60 mesi
    * backup di Hello ultimo sabato di marzo alle ore 12:00. viene conservato per 10 anni
14. Fare clic su **Avanti** e selezionare hello opzione appropriata per il trasferimento di hello tooAzure di copia di backup iniziale. È possibile scegliere **automaticamente tramite rete hello** o **Backup Offline**.

    * **Automaticamente tramite rete hello** trasferimenti hello tooAzure dati di backup in base alla pianificazione di hello scelto per il backup.
    * Il funzionamento di **Backup offline** è descritto in [Flusso di lavoro di Backup offline in Backup di Azure](backup-azure-backup-import-export.md).

    Scegliere trasferimento rilevanti hello meccanismo toosend hello copia di backup iniziale tooAzure fare clic su **Avanti**.
15. Una volta è esaminare i dettagli di criteri hello in hello **riepilogo** schermata, fare clic su hello **Crea gruppo** flusso di lavoro hello toocomplete pulsante. È possibile fare clic su hello **Chiudi** pulsante e monitorare l'avanzamento del processo hello nell'area di lavoro di monitoraggio.

    ![Creazione di un gruppo di protezione in corso](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>Backup su richiesta di un database SQL Server
Anche se i passaggi precedenti hello creano un criterio di backup, viene creato un punto di ripristino"" solo quando si verifica il primo backup di hello. Anziché attendere che tookick dell'utilità di pianificazione hello in, i passaggi di hello di sotto di creazione di trigger hello del ripristino di un punto manualmente.

1. Attendere finché non viene visualizzato lo stato gruppo di protezione hello **OK** per database hello prima di creare il punto di ripristino hello.

    ![Membri del gruppo di protezione](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Fare clic sul database hello e selezionare **Crea punto di ripristino**.

    ![Creazione di un punto di ripristino online](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. Scegliere **Online Protection** nel menu di scelta rapida hello e fare clic su **OK**. Verrà avviata la creazione di hello di un punto di ripristino in Azure.

    ![Crea punto di ripristino](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. È possibile visualizzare lo stato del processo hello in hello **monitoraggio** dell'area di lavoro in cui è disponibile un in corso del processo come hello uno illustrata nella figura che segue hello.

    ![Console di monitoraggio](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>Ripristinare un database SQL Server da Azure
Hello passaggi seguenti sono necessari toorecover un'entità protetta (database di SQL Server) da Azure.

1. Aprire il server DPM hello Console di gestione. Passare troppo**ripristino** dell'area di lavoro in cui è possibile visualizzare i server hello backup da Data Protection Manager. Esplorare database richiesti di hello (in questo caso ReportServer$ MSDPM2012). In **Ripristino da** selezionare un orario che termina con **Online**.

    ![Selezione di un punto di ripristino](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Nome del database hello destro e fare clic su **ripristinare**.

    ![Ripristino da Azure](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. DPM vengono visualizzati i dettagli di hello hello del punto di ripristino. Fare clic su **Avanti**. database hello toooverwrite, il tipo di ripristino selezionare hello **Ripristina toooriginal istanza di SQL Server**. Fare clic su **Avanti**.

    ![Ripristinare tooOriginal percorso](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    In questo esempio, DPM consente un ripristino dell'istanza di SQL Server tooanother hello database o una cartella di rete tooa autonomo.
4. In hello **opzioni di ripristino specificare** schermata, è possibile selezionare opzioni di ripristino hello come l'utilizzo della larghezza di banda di rete della limitazione della larghezza di banda di hello toothrottle utilizzata da un ripristino. Fare clic su **Avanti**.
5. In hello **riepilogo** dello schermo, vedrai tutte le configurazioni di ripristino hello fornite finora. Fare clic su **Ripristina**.

    Hello dello stato di ripristino Mostra database hello da recuperare. È possibile fare clic su **Chiudi** tooclose hello procedura guidata e visualizzare hello lo stato di avanzamento in hello **monitoraggio** dell'area di lavoro.

    ![Avvio del processo di ripristino](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Una volta completato il ripristino di hello, il database ripristinato hello è coerenti con l'applicazione.

### <a name="next-steps"></a>Passaggi successivi:
[Domande frequenti su Backup di Azure](backup-azure-backup-faq.md)
