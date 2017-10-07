---
title: aaaMove tooan di dati nel Database SQL di Azure per Azure Machine Learning | Documenti Microsoft
description: Creare una tabella SQL e caricare dati tooSQL tabella
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
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Spostare dati tooan Database SQL di Azure per Azure Machine Learning
In questo argomento vengono descritte le opzioni di hello per lo spostamento dei dati da file flat (formati CSV o TSV) o dai dati archiviati in un database di SQL Azure tooan di SQL Server locale. Queste attività per lo spostamento dati nel cloud toohello fanno parte del processo di analisi scientifica dei dati di Team hello.

Per un argomento che descrive le opzioni di hello per lo spostamento dati tooan locali di SQL Server per Machine Learning, vedere [spostare dati tooSQL Server in una macchina virtuale Azure](machine-learning-data-science-move-sql-server-virtual-machine.md).

esempio Hello **menu** collegamenti tootopics che descrivono come dati tooingest in ambienti di destinazione in cui i dati hello possono essere archiviati ed elaborati durante hello Team Data Science processo (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hello nella tabella seguente sono riepilogate le opzioni di hello per lo spostamento dati tooan Database SQL di Azure.

| <b>SOURCE</b> | <b>DESTINATION: database SQL di Azure</b> |
| --- | --- |
| <b>File flat (con formato CSV o TSV)</b> |<a href="#bulk-insert-sql-query">Inserimento di massa query SQL |
| <b>SQL Server locale</b> |1. <a href="#export-flat-file">Esportazione tooFlat File<br> 2. <a href="#insert-tables-bcp">Migrazione guidata database SQL<br> 3. <a href="#db-migration">Backup e ripristino database<br> 4. <a href="#adf">Data factory di Azure |

## <a name="prereqs"></a>Prerequisiti
procedure di Hello descritte di seguito è necessario disporre di:

* Una **sottoscrizione di Azure**. Se non si ha una sottoscrizione, è possibile iscriversi per provare una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Un **account di archiviazione Azure**. Utilizzare un account di archiviazione di Azure per archiviare i dati di hello in questa esercitazione. Se non si dispone di un account di archiviazione di Azure, vedere hello [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) articolo. Dopo aver creato l'account di archiviazione hello, è necessario account hello tooobtain chiave utilizzata l'archiviazione di hello tooaccess. Vedere la sezione [Gestire le chiavi di accesso alle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Accesso tooan **Database SQL di Azure**. Se è necessario impostare un Database SQL di Azure, [Guida introduttiva a Database SQL di Microsoft Azure](../sql-database/sql-database-get-started.md) fornisce informazioni su come tooprovision una nuova istanza di un Database di SQL Azure.
* Installazione e configurazione di **Azure PowerShell** in locale. Per istruzioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

**Dati**: vengono illustrati i processi di migrazione hello utilizzando hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/). contiene informazioni sui dati di andata e ritorno e fiere Hello NYC Taxi set di dati ed è disponibile in archiviazione blob di Azure: [NYC Taxi dati](http://www.andresmh.com/nyctaxitrips/). Un esempio e una descrizione di questi file sono inclusi in [Descrizione del set di dati relativo alle corse dei taxi di NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).

È possibile adattare hello procedure tooa qui descritto set di dati personalizzati o seguire i passaggi di hello, come descritto utilizzando hello NYC Taxi set di dati. hello tooupload NYC Taxi set di dati nel database di SQL Server locale, attenersi alla procedura hello [importazione Bulk dei dati nel Database di SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Queste istruzioni sono valide per un Server SQL in una macchina virtuale di Azure, ma procedure hello per il caricamento toohello on-premise SQL Server è hello stesso.

## <a name="file-to-azure-sql-database"></a>Spostamento dei dati da un database di SQL Azure tooan origine file flat
I dati in file flat (in formato CSV o TSV) possono essere spostato tooan database di SQL Azure mediante una Query SQL di Bulk Insert.

### <a name="bulk-insert-sql-query"></a> Inserimento di massa query SQL
passaggi di Hello per procedure hello utilizzando la Query SQL di inserimento Bulk hello sono simili toothose descritte nelle sezioni hello per lo spostamento dei dati da un tooSQL origine file flat Server in una macchina virtuale di Azure. Per altre informazioni, vedere [Inserimento di massa query SQL](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a>Spostamento dei dati dal database SQL di Azure tooan di SQL Server locale
Se i dati di origine hello sono archiviati in un Server SQL locale, esistono diverse possibilità per il database di SQL Azure tooan hello dati mobile:

1. [Esportazione tooFlat File](#export-flat-file)
2. [Migrazione guidata database SQL](#insert-tables-bcp)
3. [Backup e ripristino database](#db-migration)
4. [Data factory di Azure](#adf)

passaggi per hello primi tre Hello sono molto simili sezioni toothose [spostare dati tooSQL Server in una macchina virtuale Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) che coprono la medesima procedura. Sezioni appropriate toohello di collegamenti in questo argomento vengono fornite in hello attenendosi alle istruzioni.

### <a name="export-flat-file"></a>Esportazione tooFlat File
passaggi di Hello del file flat tooa esportazione sono simili toothose analizzate in [esportare tooFlat File](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>Migrazione guidata database SQL
passaggi per l'utilizzo di hello migrazione guidata Database SQL Hello sono simili toothose analizzate in [migrazione guidata Database SQL](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Backup e ripristino database
passaggi di Hello per l'utilizzo di database eseguire il backup e ripristino sono simili toothose analizzate in [back backup e ripristino dei Database](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Data Factory di Azure
procedura di Hello per database SQL di Azure tooan dati mobile con Azure Data Factory (ADF) è fornito nell'argomento hello [spostare i dati da un tooSQL di server SQL Azure con Azure Data Factory locale](machine-learning-data-science-move-sql-azure-adf.md). In questo argomento viene illustrato come toomove dati da un tooan di database di SQL Server on-premise SQL Azure database tramite l'archiviazione Blob di Azure utilizzando ADF.

È consigliabile utilizzare ADF quando dati esigenze toobe continuamente la migrazione in uno scenario ibrido che consente di accedere sia in locale e risorse del cloud e quando viene sottoposto a transazione dati hello o se deve toobe modificato o logica di business aggiunti tooit quando viene eseguita la migrazione. ADF consente hello pianificazione e monitoraggio dei processi utilizzando semplici script JSON che gestiscono lo spostamento di hello dei dati su base periodica. ADF dispone anche di altre funzionalità quali il supporto di operazioni complesse.
