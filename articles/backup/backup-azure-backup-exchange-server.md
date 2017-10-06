---
title: aaaBack backup un tooAzure di Exchange server Backup con System Center 2012 R2 DPM | Documenti Microsoft
description: Informazioni su come eseguire Backup tooback backup un tooAzure di Exchange server con System Center 2012 R2 DPM
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a>Eseguire il backup di un tooAzure di Exchange server Backup con System Center 2012 R2 DPM
Questo articolo viene descritto come tooconfigure un tooback server System Center 2012 R2 Data Protection Manager (DPM) di un server di Microsoft Exchange troppo Azure Backup.  

## <a name="updates"></a>Aggiornamenti
toosuccessfully registro hello DPM server con Backup di Azure, è necessario installare hello ultimo aggiornamento cumulativo per System Center 2012 R2 DPM e hello versione più recente di hello Azure Backup Agent. Ottenere l'aggiornamento cumulativo più recente di hello da hello [catalogo Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).

> [!NOTE]
> Per esempi di hello in questo articolo, è installata la versione 2.0.8719.0 di hello Azure Backup Agent e aggiornamento cumulativo 6 è installato System Center 2012 R2 DPM.
>
>

## <a name="prerequisites"></a>Prerequisiti
Prima di continuare, assicurarsi che tutti hello [prerequisiti](backup-azure-dpm-introduction.md#prerequisites) per l'utilizzo di Microsoft Azure Backup tooprotect i carichi di lavoro sono stati soddisfatti. Questi prerequisiti includono l'esempio hello:

* È stato creato un insieme di credenziali di backup nel sito di Azure hello.
* Le credenziali dell'agente e l'insieme di credenziali sono state server DPM toohello scaricato.
* Hello agente è installato nel server DPM hello.
* insieme di credenziali Hello erano server DPM di hello tooregister utilizzato.
* Se si desidera proteggere Exchange 2016, eseguire l'aggiornamento tooDPM 2012 R2 UR9 o versione successiva

## <a name="dpm-protection-agent"></a>Agente protezione DPM
agente di protezione di DPM tooinstall hello hello Exchange Server, seguire questi passaggi:

1. Assicurarsi che i firewall hello siano configurati correttamente. Vedere [configurare le eccezioni del firewall per l'agente di hello](https://technet.microsoft.com/library/Hh758204.aspx).
2. Installare l'agente di hello sul server Exchange hello facendo **gestione > agenti > installare** nella Console amministrazione DPM. Vedere [agente protezione DPM di installare hello](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) per i passaggi dettagliati.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Creare un gruppo protezione dati per il server di Exchange hello
1. Nella Console amministrazione DPM hello, fare clic su **protezione**e quindi fare clic su **New** su hello tooopen della barra multifunzione dello strumento di hello **Crea nuovo gruppo protezione dati** procedura guidata.
2. In hello **iniziale** schermata di hello guidata fare clic su **Avanti**.
3. In hello **Seleziona tipo di gruppo protezione dati** selezionare **server** e fare clic su **Avanti**.
4. Database del server Exchange hello selezionare tooprotect desiderati e fare clic su **Avanti**.

   > [!NOTE]
   > Se si desidera proteggere Exchange 2013, controllare hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).
   >
   >

    Nell'esempio seguente di hello, è selezionato il database di Exchange 2010 hello.

    ![Seleziona membri del gruppo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Selezionare il metodo di protezione dati hello.

    Nome gruppo di protezione dati hello e quindi selezionare entrambi hello le opzioni seguenti:

   * Protezione dati breve termine tramite: Disco.
   * Protezione dati online.
6. Fare clic su **Avanti**.
7. Seleziona hello **l'integrità dei dati di esecuzione di Eseutil toocheck** opzione se si desidera integrità hello toocheck dei database di Exchange Server hello.

    Dopo aver selezionato questa opzione, la verifica della coerenza del backup deve essere eseguita su hello DPM server tooavoid hello i/o il traffico generato eseguendo hello **eseutil** comando sul server Exchange hello.

   > [!NOTE]
   > toouse questa opzione, è necessario copiare hello Ese.dll ed Eseutil.exe directory C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin toohello dei file nel server DPM hello. In caso contrario, viene attivato hello errore seguente:  
   > ![Errore di Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. Fare clic su **Avanti**.
9. Database selezionare hello per **Backup di copia**, quindi fare clic su **Avanti**.

   > [!NOTE]
   > Se non si seleziona "Backup completo" per almeno una copia del gruppo di disponibilità dei database di un database, i registri non verranno troncati.
   >
   >
10. Configurare gli obiettivi di hello per **backup a breve termine**, quindi fare clic su **Avanti**.
11. Esaminare lo spazio disponibile su disco hello e quindi fare clic su **Avanti**.
12. Selezionare hello ora in cui DPM hello server Creazione replica iniziale hello e quindi fare clic su **Avanti**.
13. Selezionare opzioni di verifica coerenza hello e quindi fare clic su **Avanti**.
14. Scegliere hello database che desidera tooback backup tooAzure e quindi fare clic su **Avanti**. ad esempio:

    ![Specifica i dati da proteggere online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. Definire la pianificazione hello per **Azure Backup**, quindi fare clic su **Avanti**. ad esempio:

    ![Specificare la pianificazione dei backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > Tenere presente che i punti di ripristino online sono basati sui punti di ripristino di backup completo rapido. Pertanto, è necessario pianificare il punto di ripristino online hello dopo hello periodo di tempo specificato per hello express punto di recupero con registrazione completa.
    >
    >
16. Configurare i criteri di conservazione hello **Azure Backup**, quindi fare clic su **Avanti**.
17. Scegliere un'opzione di replica online e fare clic su **Avanti**.

    Se si dispone di un database di grandi dimensioni, potrebbero richiedere molto tempo per hello iniziale toobe backup creati tramite rete hello. tooavoid questo problema, è possibile creare un backup offline.  

    ![Specificare i criteri di mantenimento online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Confermare le impostazioni di hello e quindi fare clic su **Crea gruppo**.
19. Fare clic su **Close**.

## <a name="recover-hello-exchange-database"></a>Ripristinare il database di Exchange hello
1. Fare clic su un database di Exchange, toorecover **ripristino** nella Console amministrazione DPM hello.
2. Individuare il database di Exchange hello che si desidera toorecover.
3. Selezionare un punto di ripristino in linea da hello *tempo di recupero* elenco a discesa.
4. Fare clic su **ripristinare** toostart hello **ripristino guidato**.

Per i punti di ripristino online sono disponibili cinque tipi:

* **Ripristinare il percorso di Exchange Server toooriginal:** dati hello sarà ripristinato toohello originale Exchange server.
* **Ripristinare il database tooanother su un Server Exchange:** dati hello sarà ripristinato tooanother database in un altro server di Exchange.
* **Ripristinare i Database di ripristino tooa:** dati hello sarà ripristinato tooan Exchange ripristino Database (RDB).
* **Cartella di rete copia tooa:** dati hello sarà ripristinato tooa cartella di rete.
* **Copiare tootape:** se si dispone di una libreria di nastri o un'unità nastro autonoma hello collegato e configurato nel server DPM, il punto di ripristino hello saranno copiati tooa nastro.

    ![Scegliere la replica online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Passaggi successivi
* [Backup di Azure - Domande frequenti](backup-azure-backup-faq.md)
