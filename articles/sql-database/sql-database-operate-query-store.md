---
title: aaaOperating archivio Query nel Database SQL di Azure
description: Informazioni su come toooperate hello archivio Query nel Database SQL di Azure
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>Hello operativa archivio Query nel Database SQL di Azure
L'archivio query di Azure è una funzionalità di database completamente gestita che raccoglie e presenta informazioni cronologiche dettagliate su tutte le query in modo continuo. Può essere considerato sull'archivio Query come utilità di traccia eventi del simili tooan aereo in modo significativo semplifica la risoluzione dei problemi di entrambi per il cloud le prestazioni delle query e i clienti in locale. Questo articolo spiega alcuni aspetti specifici dell'uso dell'archivio query in Azure. Usando questi dati di query pre-raccolti, è possibile diagnosticare e risolvere velocemente i problemi di prestazioni e dedicare così più tempo alla propria attività. 

Archivio query è [disponibile a livello globale](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) nel database SQL di Azure da novembre 2015. Archivio query è di base di hello per le analisi delle prestazioni e ottimizzazione delle funzionalità, ad esempio [guidata Database SQL e Dashboard prestazioni](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). In un momento hello della pubblicazione di questo articolo, archivio Query è in esecuzione in più di 200.000 database utente in Azure, la raccolta di informazioni relative alla query da diversi mesi, senza interruzioni.

> [!IMPORTANT]
> Microsoft è in corso di hello di attivazione di archivio Query per tutti i database SQL di Azure (nuovi ed esistenti). 
> 
> 

## <a name="optimal-query-store-configuration"></a>Configurazione ottimale dell'archivio query
Questa sezione vengono descritti i valori predefiniti di configurazione ottimale di tooensure progettato corretto funzionamento dell'archivio Query hello e delle funzionalità dipendenti, ad esempio [guidata Database SQL e Dashboard prestazioni](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). La configurazione predefinita è ottimizzata per la raccolta di dati continua, ossia per un tempo minimo di OFF/READ_ONLY.

| Configurazione | Descrizione | Default | Commento |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Specifica il limite di hello per spazio dati hello che archivio Query può occupare all'interno del database customer z |100 |Applicato per i nuovi database |
| INTERVAL_LENGTH_MINUTES |Definisce la dimensione dell'intervallo di tempo durante il quale le statistiche di runtime raccolte per i piani di query vengono aggregate e rese persistenti. Tutti i piani di query attivi hanno al massimo una riga per un periodo di tempo definito con questa configurazione |60 |Applicato per i nuovi database |
| STALE_QUERY_THRESHOLD_DAYS |Criteri di pulizia basati sul tempo che controllano il periodo di conservazione hello di statistiche di runtime persistenti e query inattive |30 |Applicato per i nuovi database e i database con un'impostazione predefinita precedente (367) |
| SIZE_BASED_CLEANUP_MODE |Specifica se la pulizia automatica dei dati ha luogo quando dimensioni di dati di archivio Query si avvicinano hello limite |AUTO |Applicato per tutti i database |
| QUERY_CAPTURE_MODE |Specifica se vengono monitorate tutte le query o solo un sottoinsieme di esse |AUTO |Applicato per tutti i database |
| FLUSH_INTERVAL_SECONDS |Specifica il periodo massimo durante il quale le statistiche di runtime acquisiti vengono mantenute nella memoria, prima di scaricare toodisk |900 |Applicato per i nuovi database |
|  | | | |

> [!IMPORTANT]
> Queste impostazioni predefinite vengono applicate automaticamente nella fase finale di hello dell'attivazione di archivio Query in tutti i database SQL di Azure (vedere la nota Importante precedente). Dopo la luce backup, Database SQL di Azure non modifica i valori di configurazione impostati dai clienti, a meno che non sono influire negativamente sulle operazioni affidabile di hello archivio Query o di carico di lavoro principale.
> 
> 

Se si desidera toostay con le impostazioni personalizzate, utilizzare [ALTER DATABASE con le opzioni di archivio Query](https://msdn.microsoft.com/library/bb522682.aspx) lo stato precedente di toorevert configurazione toohello. Estrarre [Best Practices with hello archivio Query](https://msdn.microsoft.com/library/mt604821.aspx) nell'ordine toolearn superiore come scegliere i parametri di configurazione ottimale.

## <a name="next-steps"></a>Passaggi successivi
[Informazioni dettagliate sulle prestazioni del database SQL](sql-database-performance.md)

## <a name="additional-resources"></a>Risorse aggiuntive
Per ulteriori informazioni, vedere hello seguenti articoli:

* [Un registratore dei dati di volo per il database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [Monitoraggio delle prestazioni tramite archivio Query hello](https://msdn.microsoft.com/library/dn817826.aspx)
* [Scenari di utilizzo dell'archivio query](https://msdn.microsoft.com/library/mt614796.aspx)
* [Monitoraggio delle prestazioni tramite archivio Query hello](https://msdn.microsoft.com/library/dn817826.aspx) 

