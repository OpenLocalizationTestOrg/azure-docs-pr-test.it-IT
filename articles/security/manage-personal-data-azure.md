---
title: aaaManage dati personali in Microsoft Azure | Documenti Microsoft
description: informazioni aggiuntive su come toocorrect, aggiornare, eliminare ed esportare dati personali in Azure Active Directory e Database SQL di Azure
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a>Gestire i dati personali in Microsoft Azure

Questo articolo fornisce informazioni aggiuntive su come toocorrect, aggiornare, eliminare ed esportare dati personali in Azure Active Directory e Database SQL di Azure.

## <a name="scenario"></a>Scenario

Una società di Dublin fornisce un punto vendita per matrimoni di destinazione di fascia alta in Irlanda e tutto il mondo hello per entrambi una base per i clienti locali e internazionali. Hanno uffici, clienti, dipendenti e fornitori dislocati in località hello hello world toofully servizio che offrono.

Tra molti altri elementi, la società hello tiene traccia di inviate risposte che includono allergie food e le preferenze del. Gli utenti guest matrimonio può registrare per varie attività, ad esempio riding, percorso di navigazione, emergenza si basa e così via e anche interagire tra loro in una pagina web centrale mesi hello conducono toohello evento. società Hello raccoglie informazioni personali dai dipendenti, fornitori, clienti e utenti guest matrimonio. A causa di hello natura internazionale hello hello azienda deve conformarsi a più livelli del regolamento.

## <a name="problem-statement"></a>Presentazione del problema

- Gli amministratori di dati devono essere toocorrect in grado di corrette personale informazioni e aggiornamento incomplete o la modifica delle informazioni personali.

- Necessità di amministratori di dati deve essere in grado di toodelete informazioni personali su richiesta hello di un oggetto dati.

- Gli amministratori di dati necessario tooexport dati e forniscono tooa soggetto di dati in un formato comune e strutturato sulla propria richiesta.

## <a name="company-goals"></a>Obiettivi dell'azienda

- I dati personali errati di clienti, ospiti, dipendenti e fornitori devono essere corretti e aggiornati in Azure Active Directory e nel database SQL di Azure.

- Informazioni personali dell'utente devono essere eliminate in Azure Active Directory e Database SQL di Azure su richiesta hello di un oggetto dati.

- Dati personali devono essere esportati in un formato comune e strutturato su richiesta hello di un oggetto dati.

## <a name="solutions"></a>Soluzioni

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a>Azure Active Directory: rettificare/correggere i dati personali errati o incompleti e cancellare/eliminare i profili utente/dati personali

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) è un servizio Microsoft per la gestione delle identità e delle directory multi-tenant, basato sul cloud.
È possibile correggere, aggiornare o eliminare i profili utente di clienti e dipendenti e le informazioni utente lavoro che contengono dati personali, ad esempio nome, il titolo di lavoro, indirizzo o il numero di telefono, un utente nel [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) ambiente utilizzando hello [portale di Azure](https://portal.azure.com/).

È necessario accedere con un account che sia un amministratore globale per la directory di hello.

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a>Come si correggono o si aggiornano le informazioni del profilo e di lavoro degli utenti in Azure Active Directory?

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.

2. Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.

    ![supporto/image1.png](media/manage-personal-data-azure/image001.png)

3. In hello **utenti e gruppi** pannello seleziona **utenti**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. In hello **utenti e gruppi di utenti -** pannello selezionare un utente dall'elenco di hello, quindi, nel Pannello di hello per l'utente selezionato hello, **profilo** tooview hello informazioni del profilo utente che deve toobe corretto o aggiornati.

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. Correggere o aggiornare le informazioni di hello e quindi nella barra dei comandi di hello, selezionare **salvare.**

6.  Nel Pannello di hello per l'utente selezionato hello, selezionare **Info lavoro** informazioni sul lavoro tooview utente che deve toobe corretto o è stato aggiornato.

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. Correggere o aggiornare le informazioni lavoro hello e quindi nella barra dei comandi di hello, selezionare **salvare.**

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a>Come si elimina un profilo utente in Azure Active Directory?

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.

2. Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.

    ![](media/manage-personal-data-azure/image001.png)

3. In hello **utenti e gruppi** pannello seleziona **utenti**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. In hello **utenti e gruppi di utenti -** pannello, selezionare un utente dall'elenco di hello.

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. Nel Pannello di hello per l'utente selezionato hello, selezionare **Panoramica**, quindi nella barra dei comandi di hello, selezionare **eliminare**.

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a>Database SQL: rettificare/correggere i dati personali errati o incompleti, cancellare/eliminare di dati personali ed esportare i dati personali 

Il [database SQL di Microsoft Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) è un database che consente agli sviluppatori di compilare e gestire le applicazioni.

I dati personali possono essere aggiornati nel [database SQL di Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) usando le query SQL standard e possono anche essere eliminati. Inoltre, è possibile esportare i dati personali da Database SQL tramite una vasta gamma di metodi, incluso hello importazione Server SQL Azure e l'esportazione guidata in un'ampia gamma di formati, tra cui un file BACPAC.

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a>Come si correggono, aggiornano o cancellano i dati personali nel database SQL?

toolearn come toocorrect o aggiornamento dati personali in Database SQL, visitare hello [aggiornamento (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [aggiornare testo](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [aggiornare con l'espressione di tabella comune](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), o [ Aggiornamento del testo scrivere](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentazione.

toolearn come toodelete dati personali in Database SQL, visitare hello [eliminare (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentazione.

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a>Come esportare file BACPAC di tooa dati personali in Database SQL?

Un file BACPAC include i metadati e dati del Database SQL hello e un file zip con estensione BACPAC. Questa operazione può essere eseguita utilizzando hello [portale di Azure](https://portal.azure.com/), hello SQLPackage utilità della riga di comando, SQL Server Management Studio (SSMS) o PowerShell.

toolearn come file BACPAC tooa di tooexport dati, visitare hello [esportare un file BACPAC di SQL Azure database tooa](https://docs.microsoft.com/azure/sql-database/sql-database-export) pagina, che include istruzioni dettagliate per ogni metodo elencate in precedenza.

Come esportare i dati personali da Database SQL con SQL Server Import hello / esportazione guidata?

Questa procedura guidata consente di copiare i dati da una destinazione tooa di origine. Per una procedura guidata toohello introduzione, incluso come tooget, le informazioni sulle autorizzazioni e informazioni tooget con lo strumento di hello, visitare hello [importazione e l'esportazione di dati con SQL Server Import hello / esportazione guidata](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) pagina web.

Per una panoramica dei passaggi della procedura guidata hello, visitare hello [passaggi hello SQL Server di importazione / esportazione guidata](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) pagina web.

## <a name="next-steps"></a>Passaggi successivi:

[Database SQL di Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

