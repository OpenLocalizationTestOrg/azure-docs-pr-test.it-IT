---
title: aaa "Azure Analysis Services di Adventure Works esercitazione | Documenti di Microsoft"
description: Introduce l'esercitazione di hello Adventure Works per Azure Analysis Services
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services: esercitazione su Adventure Works

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Questa esercitazione sono incluse lezioni sulla toocreate e distribuire un modello tabulare a livello di compatibilità hello 1400 utilizzando [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

Se si nuovi servizi tooAnalysis e modellazione tabulare, completato questa esercitazione è la modalità toolearn modo più rapido hello toocreate e distribuire un modello tabulare di base. Una volta hello prerequisiti sul posto, dovrebbe richiedere tra due toothree ore toocomplete.  
  
## <a name="what-you-learn"></a>Contenuto dell'esercitazione   
  
-   La modalità di progetto toocreate un nuovo modello tabulare in hello **il livello di compatibilità 1400** in SSDT.
  
-   Come tooimport dati da un database relazionale in un progetto di modello tabulare.  
  
-   Come toocreate e gestire le relazioni tra tabelle nel modello di hello.  
  
-   La modalità di toocreate calcolo colonne, misure e indicatori di prestazioni chiave che consentono agli utenti di analizzare le metriche aziendali critici.  
  
-   Come toocreate e gestire prospettive e gerarchie che consentono agli utenti più facilmente individuare i dati del modello fornendo punti di vista specifici dell'applicazione e di business.  
  
-   Come toocreate partizioni che dividere i dati di tabella in parti logiche più piccole che possono essere elaborate indipendentemente dalle altre partizioni.  
  
-   Toosecure modello come oggetti e i dati mediante la creazione di ruoli con membri utente.  
  
-   Come toodeploy tooan un modello tabulare **Azure Analysis Services** server o un server di SQL Server 2017 Analysis Services locale.  
  
## <a name="prerequisites"></a>Prerequisiti  
toocomplete questa esercitazione, è necessario:  
  
-   Un Azure Analysis Services o Analysis Services di SQL Server 2017 istanza del modello per toodeploy. Iscriversi per ottenere una [versione di valutazione di Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) gratuita e [creare un server](../analysis-services-create-server.md). In alternativa, iscriversi e scaricare [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp). 

-   SQL Server Data Warehouse o Azure SQL Data Warehouse con hello [database di esempio AdventureWorksDW2014](http://go.microsoft.com/fwlink/?LinkID=335807). Questo database di esempio include hello dati necessarie toocomplete questa esercitazione. Scaricare le [edizioni gratuite di SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). In alternativa, iscriversi per ottenere una [versione di valutazione del database SQL di Azure](https://azure.microsoft.com/services/sql-database/) gratuita. 

    **Importante:** se si installa il database di esempio hello in un Server SQL locale, e si distribuisce il server di Azure Analysis Services tooan modello, un [gateway dati locale](../analysis-services-gateway.md) è obbligatorio.

-   versione più recente di Hello di [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

-   versione più recente di Hello di [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Un'applicazione client, ad esempio [Power BI Desktop](https://powerbi.microsoft.com/desktop/) o Excel. 

## <a name="scenario"></a>Scenario  
Questa esercitazione è basata su Adventure Works Cycles, una società fittizia. Adventure Works è un'azienda manifatturiera multinazionale che produce e commercializza biciclette, parti e accessori toocommercial mercati in America del Nord, Europa e Asia. Hello lavorano 500 dipendenti. Inoltre, Adventure Works ha diversi team di vendita locali all'interno della sua base di mercato. Il progetto è un modello tabulare per gli utenti di vendita e marketing tooanalyze i dati delle vendite Internet nel database AdventureWorksDW hello toocreate.  
  
esercitazione di hello toocomplete, è necessario completare diverse lezioni. ognuna delle quali prevede alcune attività. Completamento di ogni attività nell'ordine è necessario per completare la lezione hello. Una determinata lezione potrebbe includere più attività che producono un risultato analogo; tuttavia, le procedure per il completamento delle varie attività potrebbero essere leggermente diverse. Questo metodo mostra vi è spesso più di un modo toocomplete un'attività e toochallenge con competenze appreso in attività e lezioni precedenti.  
  
Hello lezioni hello mira tooguide tramite la creazione di un modello tabulare di base tramite molte delle funzionalità di hello incluso in SSDT. Poiché ogni lezione si basa la lezione precedente hello, è necessario completare lezioni hello in ordine.
  
In questa esercitazione non fornisce dati del modello di applicazione toobrowse lezioni sulla gestione di un server nel portale di Azure, la gestione di un server o un database utilizzando SQL Server Management Studio o utilizzando un client. 


## <a name="lessons"></a>Lezioni  
In questa esercitazione include hello lezioni seguenti:  
  
|Lezione|Tempo stimato toocomplete|  
|----------|------------------------------|  
|[1: Creare un nuovo progetto di modello tabulare](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 minuti|  
|[2: Ottenere i dati](../tutorials/aas-lesson-2-get-data.md)|10 minuti|  
|[3: Contrassegnare come tabella data](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 minuti|  
|[4: Creare relazioni](../tutorials/aas-lesson-4-create-relationships.md)|10 minuti|  
|[5: Creare colonne calcolate](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 minuti|
|[6: Creare misure](../tutorials/aas-lesson-6-create-measures.md)|30 minuti|  
|[7: Creare indicatori di prestazioni chiave (KPI)](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 minuti|  
|[8: Creare prospettive](../tutorials/aas-lesson-8-create-perspectives.md)|5 minuti|  
|[9: Creare gerarchie](../tutorials/aas-lesson-9-create-hierarchies.md)|20 minuti|  
|[10: Creare partizioni](../tutorials/aas-lesson-10-create-partitions.md)|15 minuti|  
|[11: Creare ruoli](../tutorials/aas-lesson-11-create-roles.md)|15 minuti|  
|[12: Analizzare in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 minuti| 
|[13: Distribuire](../tutorials/aas-lesson-13-deploy.md)|5 minuti|  
  
## <a name="supplemental-lessons"></a>Lezioni supplementari  
Queste lezioni non sono esercitazione hello toocomplete obbligatorio, ma possono essere utile per una migliore comprensione avanzate dei modelli tabulari le funzioni di modifica.  
  
|Lezione|Tempo stimato toocomplete|  
|----------|------------------------------|  
|[Righe di dettaglio](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 minuti|
|[Sicurezza dinamica](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 minuti|
|[Gerarchie incomplete](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 minuti| 

  
## <a name="next-steps"></a>Passaggi successivi  
tooget introduzione, vedere [lezione 1: creare un nuovo progetto di modello tabulare](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

