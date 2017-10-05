---
title: Panoramica di Microsoft Azure Data Lake Analytics | Documentazione Microsoft
description: "Data Lake Analytics è un servizio Big Data di Azure che consente di usare i dati per la gestione delle attività aziendali mediante le informazioni dettagliate ricavate dai dati archiviati nel cloud, indipendentemente dalla loro posizione o dimensione."
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
ms.openlocfilehash: 8817b511d779029421491194b50120d51ec9dbad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-microsoft-azure-data-lake-analytics"></a>Panoramica di Microsoft Azure Data Lake Analytics
## <a name="what-is-azure-data-lake-analytics"></a>Che cos'è Azure Data Lake Analytics?
Azure Data Lake Analytics è un servizio per processi di analisi su richiesta che semplifica l'analisi dei Big Data. Consente di concentrarsi su scrittura, esecuzione e gestione dei processi invece che sul funzionamento dell'infrastruttura distribuita. Anziché distribuire, configurare e ottimizzare l'hardware, è possibile scrivere query per trasformare i dati ed estrarre informazioni di interesse. Con il servizio di analisi è possibile gestire processi di qualsiasi dimensione immediatamente definendo il livello e l'ambito necessari. Verrà addebitato un costo per il processo solo durante la sua esecuzione, per la massima convenienza. Il servizio di analisi supporta l'integrazione di Azure Active Directory, che consente di gestire l'accesso e i ruoli, con il sistema di gestione delle identità locale in uso. È incluso anche U-SQL, un linguaggio che combina i vantaggi di SQL con la potenza espressiva del codice utente. Il runtime distribuito scalabile di U-SQL permette di analizzare in modo efficiente i dati nell'archivio e nel server SQL in Azure, nel database SQL di Azure e SQL Data Warehouse di Azure.

## <a name="key-capabilities"></a>Funzionalità principali
* **Scalabilità dinamica**
  
    Data Lake Analytics è stato progettato per garantire scalabilità e prestazioni di livello cloud.  Il servizio effettua il provisioning dinamico delle risorse e permette di svolgere analisi su terabyte e addirittura exabyte di dati. Al termine del processo, il servizio riduce automaticamente le risorse, permettendo di pagare solo per la potenza di elaborazione effettivamente usata. Se si aumentano o si riducono le dimensioni dei dati archiviati o la quantità di risorse di calcolo usata, non è necessario riscrivere il codice. È possibile concentrarsi solo sulla logica di business e non sul modo in cui elaborare e archiviare set di dati di grandi dimensioni.
* **Strumenti familiari per sviluppo più rapido, debug e ottimizzazione avanzata**
  
    Data Lake Analytics offre una stretta integrazione con Visual Studio, quindi è possibile usare strumenti familiari per esecuzione, debug e ottimizzazione del codice. Le visualizzazioni dei processi U-SQL permettono di definire la scalabilità con cui viene eseguito il codice, per poter identificare i colli di bottiglia in termini di prestazioni e ridurre i costi.
* **U-SQL: semplice, familiare, potente ed estendibile**
  
    Data Lake Analytics include U-SQL, un linguaggio di query che estende la natura dichiarativa, semplice e familiare di SQL con l'efficacia espressiva di C#. Il linguaggio U-SQL si basa sullo stesso runtime distribuito usato per i sistemi di Big Data all'interno di Microsoft. Milioni di sviluppatori SQL e .NET possono ora elaborare e analizzare i propri dati sfruttando le competenze già acquisite.
* **Integrazione uniforme con gli investimenti IT**
  
    Data Lake Analytics può sfruttare gli investimenti IT esistenti per identità, gestione, sicurezza e data warehousing. Questo approccio semplifica la governance dei dati e l'estensione delle attuali applicazioni dati. Data Lake Analytics è integrato in Active Directory per la gestione e le autorizzazioni degli utenti e viene fornito con funzionalità integrate di monitoraggio e controllo.
* **Conveniente ed economico**
  
    Data Lake Analytics è una soluzione a costi ridotti per l'esecuzione di carichi di lavoro di Big Data. Il pagamento avviene in base a ogni processo quando vengono elaborati i dati. Non sono necessari hardware, licenze o contratti di supporto specifici del servizio. Poiché il sistema è in grado di ridimensionarsi automaticamente all'avvio e al completamento del processo, non si paga mai più del necessario.
* **Per tutti i dati di Azure**
  
    Data Lake Analytics è ottimizzato per usare Azure Data Lake in modo da fornire il più elevato livello di prestazioni, velocità effettiva e parallelizzazione dei carichi di lavoro dei Big Data.  Data Lake Analytics può inoltre funzionare con Archiviazione BLOB di Azure e il database SQL di Azure.

## <a name="next-steps"></a>Passaggi successivi
 
  * Introduzione ad Azure Data Lake Analytics con [portale di Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [Interfaccia della riga di comando](data-lake-analytics-get-started-cli2.md)
  * Gestire Azure Data Lake Analytics con [portale di Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [interfaccia della riga di comando](data-lake-analytics-manage-use-cli.md) | [Azure .NET SDK](data-lake-analytics-manage-use-dotnet-sdk.md) | [Node.js](data-lake-analytics-manage-use-nodejs.md)
  * [Monitorare e risolvere i problemi dei processi di Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md) 
