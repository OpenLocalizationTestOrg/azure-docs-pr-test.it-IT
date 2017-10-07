---
title: aaaOverview di Microsoft Azure Data Lake Analitica | Documenti Microsoft
description: "Data Lake Analitica è un servizio di Azure Big Data che consente di utilizzare dati toodrive azienda utilizzando informazioni ottenute dai dati nel cloud hello, indipendentemente dal fatto che la dimensione o in cui è."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 1e1d443a-48a2-47fb-bc00-bf88274222de
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 15bcd549c5aeb167da1338f253270ad57f8c5123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-microsoft-azure-data-lake-analytics"></a>Panoramica di Microsoft Azure Data Lake Analytics
## <a name="what-is-azure-data-lake-analytics"></a>Che cos'è Azure Data Lake Analytics?
Azure Data Lake Analitica è un analitica di dati su richiesta analitica processo servizio toosimplify. Consente di concentrarsi su scrittura, esecuzione e gestione dei processi invece che sul funzionamento dell'infrastruttura distribuita. Invece di distribuzione, configurazione e regolazione hardware, scrivere query tootransform i dati ed estrarre informazioni preziose. servizio analitica Hello può gestire i processi di qualsiasi scala immediatamente impostando composizione hello per quanta capacità è necessario. Verrà addebitato un costo per il processo solo durante la sua esecuzione, per la massima convenienza. servizio analitica Hello supporta Azure Active Directory consente di gestire l'accesso e i ruoli, integrati con il sistema di identità locale. Include inoltre U-SQL, un linguaggio che unisce i vantaggi di hello di SQL con la potenza espressiva hello del codice utente. Consente di runtime distribuita scalabile U-SQL è tooefficiently analizzare i dati nell'archivio di hello e nei server SQL Azure, Database SQL di Azure e Azure SQL Data Warehouse.

## <a name="key-capabilities"></a>Funzionalità principali
* **Scalabilità dinamica**
  
    Data Lake Analytics è stato progettato per garantire scalabilità e prestazioni di livello cloud.  Il servizio effettua il provisioning dinamico delle risorse e permette di svolgere analisi su terabyte e addirittura exabyte di dati. Al termine del processo di hello, venti verso il basso le risorse automaticamente e si paga solo per l'elaborazione di energia elettrica utilizzata hello. Aumentare o diminuire le dimensioni di hello dei dati archiviati o hello quantità di risorse di calcolo utilizzate, non si dispone di codice toorewrite. È possibile concentrarsi solo sulla logica di business e non sul modo in cui elaborare e archiviare set di dati di grandi dimensioni.
* **Strumenti familiari per sviluppo più rapido, debug e ottimizzazione avanzata**
  
    Data Lake Analitica è strettamente integrato con Visual Studio, pertanto è possibile utilizzare strumenti familiari toorun, eseguire il debug e ottimizzare il codice. Le visualizzazioni dei processi U-SQL permettono di definire la scalabilità con cui viene eseguito il codice, per poter identificare i colli di bottiglia in termini di prestazioni e ridurre i costi.
* **U-SQL: semplice, familiare, potente ed estendibile**
  
    Data Lake Analitica include U-SQL, un linguaggio di query che si estende hello familiare, semplice e dichiarativa natura di SQL con la potenza espressiva hello di c#. Hello U-SQL language si basa su hello stesso distributed runtime che consente di creare sistemi di dati hello all'interno di Microsoft. Milioni di sviluppatori SQL e .NET possono elaborare e analizzare i dati con competenze hello di che dispongono già.
* **Integrazione uniforme con gli investimenti IT**
  
    Data Lake Analytics può sfruttare gli investimenti IT esistenti per identità, gestione, sicurezza e data warehousing. Questo approccio semplifica la governance dei dati e lo rende facile tooextend alle applicazioni di dati corrente. Data Lake Analytics è integrato in Active Directory per la gestione e le autorizzazioni degli utenti e viene fornito con funzionalità integrate di monitoraggio e controllo.
* **Conveniente ed economico**
  
    Data Lake Analytics è una soluzione a costi ridotti per l'esecuzione di carichi di lavoro di Big Data. Il pagamento avviene in base a ogni processo quando vengono elaborati i dati. Non sono necessari hardware, licenze o contratti di supporto specifici del servizio. sistema Hello viene automaticamente ridimensionato verso l'alto o verso il basso come processo hello viene avviato e completato, pertanto non si paga mai per più di ciò che è necessario.
* **Per tutti i dati di Azure**
  
    Data Lake Analitica è ottimizzato toowork con Azure Data Lake - fornendo hello di livello più elevato di prestazioni, velocità effettiva e la parallelizzazione per i carichi di lavoro di big data.  Data Lake Analytics può inoltre funzionare con Archiviazione BLOB di Azure e il database SQL di Azure.

## <a name="next-steps"></a>Passaggi successivi
 
  * Introduzione ad Azure Data Lake Analytics con [portale di Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [Interfaccia della riga di comando](data-lake-analytics-get-started-cli2.md)
  * Gestire Azure Data Lake Analytics con [portale di Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [interfaccia della riga di comando](data-lake-analytics-manage-use-cli.md) | [Azure .NET SDK](data-lake-analytics-manage-use-dotnet-sdk.md) | [Node.js](data-lake-analytics-manage-use-nodejs.md)
  * [Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md) 
