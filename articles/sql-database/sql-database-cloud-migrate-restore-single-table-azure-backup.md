---
title: aaaRestore una singola tabella da un backup di Database SQL di Azure | Documenti Microsoft
description: Informazioni su come toorestore una singola tabella da un backup di Database SQL di Azure.
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>Come toorestore una singola tabella da un backup di Database SQL di Azure
Può verificarsi una situazione in cui è stato accidentalmente modificati alcuni dati in un database SQL e si desidera ora toorecover hello singola interessati tabella. In questo articolo viene descritto come toorestore una singola tabella in un database da uno dei Database SQL di hello [backup automatici](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>Passaggi di preparazione: rinominare la tabella hello e ripristinare una copia del database hello
1. Identificare hello tabella nel database SQL di Azure che si desidera tooreplace con copia hello ripristinato. Utilizzare tabella hello toorename di Microsoft SQL Management Studio. Ad esempio, rinominare la tabella hello come &lt;nome tabella&gt;old.
   
   > [!NOTE]
   > tooavoid bloccate, assicurarsi che non è presente alcuna attività in esecuzione in una tabella di hello che si sta rinominando. In caso di problemi, accertarsi di eseguire questa procedura durante una finestra di manutenzione.
   >

2. Ripristinare un backup del punto di tooa database nel tempo che si desidera hello toousing toorecover [In_Timeconpunto di ripristino](sql-database-recovery-using-backups.md#point-in-time-restore) passaggi.
   
   > [!NOTE]
   > nome Hello del database ripristinato hello sarà nel formato DBName + TimeStamp hello. ad esempio, **Adventureworks2012_2016-01-01T22-12Z**. Questo passaggio non sovrascriverà nome del database nel server di hello esistente hello. Si tratta di una misura di sicurezza e ha lo scopo tooallow tooverify hello database ripristinato prima di eliminare il database corrente e rinominare il database ripristinato hello per la produzione.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Copia della tabella hello da hello database ripristinato usando lo strumento di migrazione del Database SQL di hello

1. Scaricare e installare hello [migrazione guidata Database SQL](https://sqlazuremw.codeplex.com).
2. Aprire hello migrazione guidata Database SQL, in hello **Select Process** selezionare **Database di analisi/migrazione**e quindi fare clic su **Avanti**.

   ![SQL Database Migration wizard - Select Process](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. In hello **connettersi tooServer** finestra di dialogo casella, applicare hello seguenti impostazioni:

   * Server name (Nome server): **server SQL**
   * Authentication: (Autenticazione): **autenticazione di SQL Server**
   * Login (Account di accesso): **account di accesso**
   * Password: **password**
   * Database: **Master DB (List all databases)** (Database master - Elenca tutti i database)
   
   > [!NOTE]
   > Per impostazione predefinita la procedura guidata hello Salva le informazioni di accesso. Per modificare tale impostazione, selezionare **Forget Login Information**(Ignora informazioni di accesso).
   >
   
     ![SQL Database Migration wizard - Select Source - step 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. In hello **Seleziona origine** la finestra di dialogo, il nome del database selezionare hello ripristinato da hello **preparativi** sezione come origine e quindi fare clic su **Avanti**.
   
    ![SQL Database Migration wizard - Select Source - step 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. In hello **Seleziona oggetti** la finestra di dialogo, seleziona hello **selezionare oggetti di database specifici** opzione e quindi selezionare table(or tables) hello che si desidera toomigrate toohello server di destinazione.
   ![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. In hello **riepilogo generazione guidata Script** pagina, fare clic su **Sì** quando verrà richiesto se si è pronti toogenerate uno script SQL. È inoltre possibile hello toosave hello opzione Script TSQL per un uso successivo.
   ![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. In hello **riepilogo dei risultati** pagina, fare clic su **Avanti**.
   ![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. In hello **connessione al Server di destinazione installazione** pagina, fare clic su **connettersi tooServer**, quindi immettere i dettagli di hello come indicato di seguito:
   
   * **Server Name**(Nome server): istanza del server di destinazione.
   * **Autenticazione**: **autenticazione di SQL Server**. Immettere le credenziali di accesso.
   * **Database**: **Master DB (List all databases)** (Database master (Elenca tutti i database)). Questa opzione vengono elencati tutti i database nel server di destinazione hello hello.
     
     ![SQL Database Migration wizard - Setup Target Server Connection](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Fare clic su **Connetti**, selezionare i database di destinazione hello che si desidera toomove hello tabella e quindi fare clic su **Avanti**. Questo dovrebbe terminare l'esecuzione dello script generato in precedenza hello e dovrebbe essere hello appena spostato i database della tabella di destinazione toohello copiato.

## <a name="verification-step"></a>Passaggio di verifica

- Eseguire una query e test toomake tabella hello appena copiato che dati hello sia intatti. Dopo la conferma, è possibile eliminare il formato di tabella hello rinominato **preparativi** sezione. Ad esempio, &lt;nome tabella&gt;_old.

## <a name="next-steps"></a>Passaggi successivi
[Backup automatici del database SQL](sql-database-automated-backups.md)

