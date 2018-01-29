---
title: Spostare dati in un database SQL di Azure per Azure Machine Learning | Microsoft Docs
description: Creare una tabella SQL e caricare dati in tabelle SQL
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: bradsev
ms.openlocfilehash: 323861d078e9beeb197333dc7e2d0314014dfdb0
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2017
---
# <a name="move-data-to-an-azure-sql-database-for-azure-machine-learning"></a>Spostamento dei dati in un database di SQL Azure per Azure Machine Learning
Questo argomento indica le opzioni per lo spostamento dei dati da file flat, con estensione csv o tsv, o da dati archiviati in SQL Server locale a un database SQL di Azure. Queste attività per lo spostamento dei dati nel cloud fanno parte del Processo di analisi scientifica dei dati per i team.

Per un argomento che descrive le opzioni per lo spostamento dei dati a SQL Server locale per Machine Learning, vedere [Spostamento dei dati in SQL Server in una macchina virtuale di Azure](move-sql-server-virtual-machine.md).

Il seguente **menu** si collega ad argomenti che descrivono come inserire dati in ambienti di destinazione in cui i dati possono essere archiviati ed elaborati durante il Processo di analisi scientifica dei dati per i team (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../../includes/cap-ingest-data-selector.md)]

Nella tabella seguente vengono riepilogate le opzioni per lo spostamento dei dati a un database di SQL Azure.

| <b>SOURCE</b> | <b>DESTINATION: database SQL di Azure</b> |
| --- | --- |
| <b>File flat (con formato CSV o TSV)</b> |<a href="#bulk-insert-sql-query">Inserimento di massa query SQL |
| <b>SQL Server locale</b> |1. <a href="#export-flat-file">Esportazione in un file flat<br> 2. <a href="#insert-tables-bcp">Migrazione guidata database SQL<br> 3. <a href="#db-migration">Backup e ripristino database<br> 4. <a href="#adf">Data factory di Azure |

## <a name="prereqs"></a>Prerequisiti
Questa procedura descritta di seguito richiede di disporre di:

* Una **sottoscrizione di Azure**. Se non si ha una sottoscrizione, è possibile iscriversi per provare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Un **account di archiviazione Azure**. In questa esercitazione si userà un account di archiviazione di Azure per archiviare i dati. Se non si dispone di un account di archiviazione di Azure, vedere l'articolo [Creare un account di archiviazione di Azure](../../storage/common/storage-create-storage-account.md#create-a-storage-account) . Dopo avere creato l'account di archiviazione, è necessario ottenere la chiave dell'account usata per accedere alla risorsa di archiviazione. Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Accesso a un **database SQL di Azure**. Se è necessario impostare un database di SQL Azure, la [Guida introduttiva al database SQL di Microsoft Azure](../../sql-database/sql-database-get-started.md) fornisce informazioni su come eseguire il provisioning di una nuova istanza di un database di SQL Azure.
* Installazione e configurazione di **Azure PowerShell** in locale. Per istruzioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).

**Dati**: i processi di migrazione vengono illustrati usando il [set di dati NYC Taxi](http://chriswhong.com/open-data/foil_nyc_taxi/). Il set di dati NYC Taxi contiene informazioni sulle tariffe e sui dati delle tratte ed è disponibile nell'archivio BLOB di Azure ([dati NYC Taxi](http://www.andresmh.com/nyctaxitrips/)). Un esempio e una descrizione di questi file sono inclusi in [Descrizione del set di dati relativo alle corse dei taxi di NYC](sql-walkthrough.md#dataset).

È possibile adattare le procedure descritte di seguito a un set di dati personalizzati o seguire i passaggi come descritto utilizzando il set di dati NYC Taxi. Per caricare il set di dati NYC Taxi nel database di SQL Server locale, seguire la procedura descritta in [Importazione in blocco dei dati nel database SQL Server](sql-walkthrough.md#dbload). Queste istruzioni sono per SQL Server in una macchina virtuale di Azure, ma la procedura per il caricamento in SQL Server locale è la stessa.

## <a name="file-to-azure-sql-database"></a> Spostamento dei dati da un'origine di file flat a un database SQL Azure
I dati nei file flat (nel formato CSV o TSV) possono essere spostati a un database Azure SQL mediante un inserimento di massa query SQL.

### <a name="bulk-insert-sql-query"></a> Inserimento di massa query SQL
I passaggi per la procedura utilizzando l’inserimento di massa query SQL sono simili a quelli descritti nelle sezioni per lo spostamento dei dati da un'origine di file flat a un Server SQL in una VM di Azure. Per altre informazioni, vedere [Inserimento di massa query SQL](move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a> Spostamento dei dati da SQL Server locale a un database SQL di Azure
Se i dati di origine vengono archiviati in SQL Server locale, esistono varie possibilità per lo spostamento di dati in un database SQL di Azure:

1. [Esportazione in un file flat](#export-flat-file)
2. [Migrazione guidata database SQL](#insert-tables-bcp)
3. [Backup e ripristino database](#db-migration)
4. [Data Factory di Azure](#adf)

I passaggi per i primi tre sono molto simili a tali sezioni in [Spostamento dei dati in SQL Server in una macchina virtuale di Azure](move-sql-server-virtual-machine.md) che coprono la medesima procedura. Le istruzioni seguenti forniscono i collegamenti alle sezioni appropriate al riguardo.

### <a name="export-flat-file"></a>Esportazione in un file flat
La procedura di questo processo di esportazione in un file flat è simile a quella descritta in [Esportazione in un file flat](move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>Migrazione guidata database SQL
I passaggi per utilizzare la migrazione guidata nel database SQL sono simili a quelli descritti in [Migrazione guidata database SQL](move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Backup e ripristino database
I passaggi per l'utilizzo del backup e ripristino del database sono simili a quelli descritti in [Backup e ripristino database](move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Data Factory di Azure
La procedura per lo spostamento di dati in un database SQL di Azure con Azure Data Factory (ADF) è illustrata nell'argomento [Spostare i dati da SQL Server locale a SQL Azure con Azure Data Factory](move-sql-azure-adf.md). Questo argomento descrive come spostare i dati da un database di SQL Server locale a un database SQL di Azure tramite l'archiviazione BLOB di Azure con ADF.

È consigliabile usare ADF quando i dati devono essere migrati continuamente in uno scenario ibrido che accede a risorse locali e cloud e quando i dati sono transazionali o devono essere modificati o avere una logica di business aggiunta durante la migrazione. L’ADF consente la pianificazione e il monitoraggio dei processi utilizzando semplici script JSON che gestiscono lo spostamento dei dati su base periodica. ADF dispone anche di altre funzionalità quali il supporto di operazioni complesse.
