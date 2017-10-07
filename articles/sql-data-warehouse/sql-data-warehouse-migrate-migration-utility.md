---
title: "Migrazione: utilità di migrazione per Data Warehouse | Documentazione Microsoft"
description: Eseguire la migrazione tooSQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a>Utilità di migrazione per data warehouse (anteprima)
> [!div class="op_single_selector"]
> * [Scaricare l'utilità di migrazione][Download Migration Utility]
> 
> 

Utilità di migrazione di Data Warehouse Hello è che uno strumento progettato toomigrate schema e i dati da tooAzure di SQL Server e Database SQL di Azure SQL Data Warehouse. Durante la migrazione dello schema, lo strumento hello esegue automaticamente il mapping dello schema corrispondente hello da toodestination di origine. Dopo che è stata eseguita la migrazione dello schema di hello, strumenti hello fornisce hello opzione toomove i dati con gli script generati automaticamente.

Migrazione tooschema e dati, in questo modo lo strumento hello i report di compatibilità toogenerate opzione che riepilogano le incompatibilità tra istanze di origine e destinazione hello che impediscono inoltre semplificata la migrazione.

## <a name="get-started"></a>Attività iniziali
Come prerequisito per l'installazione, sarà necessario script di migrazione toorun utilità della riga di comando BCP hello e report di compatibilità di Office tooview hello. Dopo l'avvio hello eseguibile che viene scaricato è sarà richiesta tooaccept un contratto di licenza standard prima che lo strumento hello verrà installato.

Inoltre, hello toorun Utiliy di migrazione, si sarà necessario hello uno queste autorizzazioni sul database hello che si tratta del toomigrate: CREATE DATABASE, ALTER ANY DATABASE o VIEW ANY DEFINITION.

### <a name="launching-hello-tool-and-connecting"></a>Avvio dello strumento di hello e la connessione
Installare utilità di avvio hello facendo clic sull'icona del desktop di hello visualizzato post. All'apertura dello strumento hello, verrà richiesto una pagina di connessione iniziale in cui è possibile scegliere l'origine e destinazione per lo strumento di migrazione hello. Al momento, sono supportati SQL Server e il database SQL di Azure come origini e SQL Data Warehouse come destinazione. Dopo aver selezionato questa verrà richiesto il server di origine tooyour tooconnect specificando nome server e l'autenticazione e quindi fare clic su 'Connetti'.

Dopo l'autenticazione, lo strumento hello verrà visualizzato un elenco dei database presenti nel server di hello che si è connessi. È possibile avviare la migrazione di hello selezionando un database che si desidera toomigrate e quindi fare clic sul 'Esegui migrazione selezionata'.

## <a name="migration-report"></a>Report di migrazione
Selezione di 'Verifica della compatibilità del Database' nello strumento hello generare un report di riepilogo di tutte le incompatibilità nel database di hello toomigrate richiesto. Un elenco più ampio di alcune delle funzionalità di SQL Server che non è presente in SQL Data Warehouse hello è reperibile nel nostro [documentazione per la migrazione][migration documentation]. Dopo la generazione di report hello sarà in grado di toosave e report hello Apri in Excel.

Si noti che durante la generazione dello schema hello di migrazione, la maggior parte dei problemi identificati come 'Object' verrà regolata ordine tooallow immediato di una migrazione dei dati. Controllare tooensure modifiche hello non si desidera toomake ulteriori modifiche prima di applicare schema hello.

## <a name="migrate-schema"></a>Eseguire la migrazione dello schema
Dopo la connessione, selezionare 'Eseguire la migrazione di Schema' genera uno script di migrazione dello schema per le tabelle di hello selezionato. Questa struttura di hello porte script della tabella hello, esegue il mapping di form compatibile toomore tipi di dati incompatibili e crea lo schema e le credenziali di sicurezza, se viene indicato dall'utente hello nelle impostazioni di migrazione hello. Questo codice può essere eseguito sull'istanza di SQL Data Warehouse hello di destinazione, stato salvato il file tooa, copiato negli Appunti tooyour o anche modificato in linea prima di eseguire ulteriori azioni.  

Come indicato in precedenza, quando la migrazione della migrazione di hello revisione schema cambia tale hello è reso uno strumento in ordine tooensure che è completamente comprendere.  

## <a name="migrate-data"></a>Eseguire la migrazione dei dati
Facendo clic hello 'Eseguire la migrazione di dati' opzione è possibile generare script BCP cui spostare i file di dati prima tooflat sul server, quindi direttamente nel proprio SQL Data Warehouse. Si consiglia di questo processo per lo spostamento di piccole quantità di dati e, come i tentativi non sono incorporati e potrebbero verificarsi errori se si verifica una perdita della connessione di rete hello. In ordine toorun questa, sarà necessario toohave hello BCP utilità riga di comando installato e lo schema di hello per dati hello deve già essere stato creato.

Dopo aver compilato parametri hello sopra riportato è semplicemente necessario tooclick esegue la migrazione e verrà generato un set di due pacchetti tooyour percorso specificato. Eseguire il file di esportazione hello dati tooexport degli ordini provenienti dall'origine della migrazione in file flat ed eseguire il file di importazione hello in ordine tooimport i dati in SQL Data Warehouse.

## <a name="next-steps"></a>Passaggi successivi
Ora che è stata eseguita la migrazione di alcuni dati, vedere come troppo[sviluppare][develop].

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
