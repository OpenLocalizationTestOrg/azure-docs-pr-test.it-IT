---
title: aaaBack backup un tooAzure di Exchange server Backup con il Server di Backup di Azure | Documenti Microsoft
description: Informazioni su come eseguire Backup tooback backup un tooAzure di Exchange server tramite il Server di Backup di Azure
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a>Eseguire il backup di un tooAzure di Exchange server con Server di Backup di Azure Backup
Questo articolo viene descritto come tooconfigure tooback di Microsoft Azure Backup Server (MABS) di un tooAzure di Microsoft Exchange server.  

## <a name="prerequisites"></a>Prerequisiti
Prima di continuare, assicurarsi che il Server di Backup di Azure sia [installato e pronto](backup-azure-microsoft-azure-backup.md).

## <a name="mabs-protection-agent"></a>Agente protezione MABS
agente di protezione MABS hello tooinstall hello Exchange Server, seguire questi passaggi:

1. Assicurarsi che i firewall hello siano configurati correttamente. Vedere [configurare le eccezioni del firewall per l'agente di hello](https://technet.microsoft.com/library/Hh758204.aspx).
2. Installare l'agente di hello sul server Exchange hello facendo **gestione > agenti > installare** nella Console di amministrazione di MABS. Vedere [agente protezione di installazione hello MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) per i passaggi dettagliati.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Creare un gruppo protezione dati per il server di Exchange hello
1. Nella Console di amministrazione MABS hello, fare clic su **protezione**, quindi fare clic su **New** su hello tooopen della barra multifunzione dello strumento di hello **Crea nuovo gruppo protezione dati** procedura guidata.
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

    Dopo aver selezionato questa opzione, la verifica della coerenza del backup verrà eseguita in MABS tooavoid hello i/o il traffico che viene generato eseguendo hello **eseutil** comando sul server Exchange hello.

   > [!NOTE]
   > toouse questa opzione, è necessario copiare hello Ese.dll ed Eseutil.exe directory C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin toohello dei file nel server MAB hello. In caso contrario, viene attivato hello errore seguente:  
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
12. Selezionare hello ora in cui hello MAB Server Creazione replica iniziale hello e quindi fare clic su **Avanti**.
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
1. Fare clic su un database di Exchange, toorecover **ripristino** nella Console di amministrazione MABS hello.
2. Individuare il database di Exchange hello che si desidera toorecover.
3. Selezionare un punto di ripristino in linea da hello *tempo di recupero* elenco a discesa.
4. Fare clic su **ripristinare** toostart hello **ripristino guidato**.

Per i punti di ripristino online sono disponibili cinque tipi:

* **Ripristinare il percorso di Exchange Server toooriginal:** dati hello sarà ripristinato toohello originale Exchange server.
* **Ripristinare il database tooanother su un Server Exchange:** dati hello sarà ripristinato tooanother database in un altro server di Exchange.
* **Ripristinare i Database di ripristino tooa:** dati hello sarà ripristinato tooan Exchange ripristino Database (RDB).
* **Cartella di rete copia tooa:** dati hello sarà ripristinato tooa cartella di rete.
* **Copiare tootape:** se si dispone di una libreria di nastri o un'unità nastro autonoma associata e configurato in MABS, il punto di ripristino hello saranno copiati tooa nastro.

    ![Scegliere la replica online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Passaggi successivi
* [Backup di Azure - Domande frequenti](backup-azure-backup-faq.md)
