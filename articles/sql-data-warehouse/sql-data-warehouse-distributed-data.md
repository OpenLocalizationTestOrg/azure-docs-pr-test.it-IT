---
title: aaaHow distributed dati funziona in Azure SQL Data Warehouse | Documenti Microsoft
description: Informazioni su come i dati vengono distribuiti per altamente parallelo di elaborazione (MPP) e hello le opzioni per la distribuzione di tabelle in Azure SQL Data Warehouse e Parallel Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: bae494a6-7ac5-4c38-8ca3-ab2696c63a9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 9a712d8d5251e4391ede245105918283aaa4b193
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-data-and-distributed-tables-for-massively-parallel-processing-mpp"></a>Dati distribuiti e tabelle distribuite per l'elaborazione parallela elevata (Massively Parallel Processing, MPP)
Informazioni sulla distribuzione dei dati utente in Azure SQL Data Warehouse e Parallel Data Warehouse, i sistemi di elaborazione parallela elevata (Massively Parallel Processing, MPP) di Microsoft. La progettazione del toouse di data warehouse dati distribuiti in modo efficace consentono si tooachieve hello l'elaborazione di query vantaggi dell'architettura MPP hello. Un numero limitato di scelte nella progettazione dei database può avere un impatto significativo nel miglioramento delle prestazioni delle query.  

> [!NOTE]
> Azure SQL Data Warehouse e hello utilizzare Parallel Data Warehouse di progettazione di elaborazione parallela massiva stesso (. MPP), ma dispongono di alcune differenze a causa di hello piattaforma sottostante. SQL Data Warehouse è una piattaforma distribuita come servizio (PaaS) eseguita in Azure. Parallel Data Warehouse viene eseguita in APS (Analytics Platform System) un'appliance locale eseguita in Windows Server.
> 
> 

## <a name="what-is-distributed-data"></a>Che cosa sono i dati distribuiti?
In SQL Data Warehouse e Parallel Data Warehouse, dati distribuiti si riferiscono toouser i dati archiviati in più percorsi tra il sistema MPP hello. Ciascuno di questi percorsi funziona come un'archiviazione indipendenti e l'unità di elaborazione che consente di eseguire query sulla relativa parte di dati hello. Dati distribuiti sono fondamentale toorunning query in parallelo tooachieve prestazioni elevate delle query.

dati toodistribute, data warehouse di hello assegna ogni riga di una tabella tooone distribuita della località dell'utente.  È possibile distribuire le tabelle con un metodo di distribuzione hash o un metodo round robin. metodo di distribuzione Hello viene specificato nell'istruzione CREATE TABLE hello. 

## <a name="hash-distributed-tables"></a>Tabelle con distribuzione hash
Hello seguente diagramma viene illustrato come una procedura completa (tabella non distribuita) archiviata come una tabella hash distribuita. Una funzione deterministica assegna ogni distribuzione tooone toobelong di righe. Nella definizione della tabella hello, una delle colonne hello è designata come colonna di distribuzione hello. funzione hash Hello Usa valore hello hello distribuzione colonna tooassign ogni distribuzione tooa di righe.

Sono presenti le considerazioni sulle prestazioni per la selezione di una colonna di distribuzione, ad esempio valori DISTINCT, inclinazione di dati e tipi di hello delle query eseguite nel sistema hello hello.

![Tabella distribuita](media/sql-data-warehouse-distributed-data/hash-distributed-table.png "Tabella distribuita")  

* Ogni riga appartiene tooone distribuzione.  
* Un algoritmo hash deterministica assegna ogni distribuzione tooone di righe.  
* numero di Hello di righe della tabella per ogni distribuzione varia come illustrato da diversi formati di hello di tabelle.

## <a name="round-robin-distributed-tables"></a>Tabelle con distribuzione round robin
Una tabella di round robin distribuita distribuisce le righe di hello assegnando ogni distribuzione tooa di righe in modo sequenziale. Si tratta di dati rapido tooload in una tabella di round robin, ma le prestazioni delle query potrebbero risultare più lenta.  Aggiunta di una tabella di round robin in genere richiede ridistribuiscono hello righe tooenable hello query tooproduce risultati corretti, che richiedono tempo.

## <a name="distributed-storage-locations-are-called-distributions"></a>Le posizioni di archiviazione distribuite sono chiamate distribuzioni
Ogni posizione distribuita è una distribuzione. Quando viene eseguita una query in parallelo, la parte di dati di hello ogni distribuzione esegue una query SQL. SQL Data Warehouse utilizza query di Database SQL toorun hello. Parallel Data Warehouse utilizza query hello toorun di SQL Server. Questa progettazione dell'architettura di condivisione è fondamentale tooachieving scalabilità orizzontale calcolo parallelo.

### <a name="can-i-view-hello-distributions"></a>È possibile visualizzare le distribuzioni di hello?
Ogni distribuzione presenta un ID di distribuzione ed è visibile nelle visualizzazioni di sistema che riguardano tooSQL Data Warehouse e Parallel Data Warehouse. È possibile utilizzare le prestazioni delle query tootroubleshoot hello distribuzione ID e altri problemi. Per un elenco di viste di sistema hello, vedere hello [vista di sistema MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="difference-between-a-distribution-and-a-compute-node"></a>Differenza tra una distribuzione e un nodo di calcolo
Una distribuzione è l'unità di base hello per l'archiviazione dei dati distribuiti e l'elaborazione di query parallele. Le distribuzioni sono raggruppate in nodi di calcolo. Ogni nodo di calcolo tiene traccia di una o più distribuzioni.  

* Sistema della piattaforma Analitica utilizza nodi di calcolo come un componente fondamentale di funzionalità di scalabilità e l'architettura hardware hello. Utilizza sempre le distribuzioni di otto per ogni nodo di calcolo, come illustrato nel diagramma hello per le tabelle hash distribuita. numero di nodi di calcolo, Hello e pertanto hello numero di distribuzioni, è determinato dal numero di hello dei nodi di calcolo che si acquistano per dispositivo hello. Ad esempio, se si acquistano otto nodi di calcolo, si avranno a disposizione 64 distribuzioni (8 nodi di calcolo x 8 distribuzioni/nodo). 
* SQL Data Warehouse ha un numero fisso di 60 distribuzioni e un numero variabile di nodi di calcolo. nodi di calcolo Hello vengono implementati con risorse di elaborazione e archiviazione di Azure. numero di Hello di nodi di calcolo è possibile modificare il carico di lavoro di secondo toohello back-end del servizio e hello capacità di elaborazione (Dwu) specificato per data warehouse di hello. Quando viene modificato il numero di hello di nodi di calcolo, modifica anche numero hello di distribuzioni per ogni nodo di calcolo. 

### <a name="can-i-view-hello-compute-nodes"></a>È possibile visualizzare i nodi di calcolo hello?
Ogni nodo di calcolo è un ID di nodo ed è visibile nelle visualizzazioni di sistema che riguardano tooSQL Data Warehouse e Parallel Data Warehouse.  È possibile visualizzare il nodo di calcolo hello cercando colonna node_id hello nelle viste di sistema i cui nomi iniziano con sys.pdw_nodes. Per un elenco di viste di sistema hello, vedere hello [vista di sistema MPP](sql-data-warehouse-reference-tsql-statements.md).

## <a name="Replicated"></a>Tabelle replicate
Dispone di una tabella che viene replicata un completamente la copia della tabella hello archiviati in ciascun nodo di calcolo. La replica di una tabella rimuove i dati di tootransfer necessità di hello tra i nodi di calcolo prima di un'operazione join o aggregazione. Le tabelle replicate solo sono applicabili con tabelle di piccole dimensioni a causa di hello spazio di archiviazione richiesto toostore hello completa della tabella in ogni nodo di calcolo.  

Hello diagramma seguente mostra una tabella replicata archiviata in ogni nodo di calcolo. Per SQL Data Warehouse, tabella replicata hello è il database di distribuzione tooa completamente copiato in ogni nodo di calcolo. Per Parallel Data Warehouse, tabella replicata hello viene memorizzata in tutti i dischi assegnati toohello del nodo di calcolo.  Questa strategia di archiviazione su disco viene implementata usando i filegroup di SQL Server.  

![Tabella replicata](media/sql-data-warehouse-distributed-data/replicated-table.png "Tabella replicata") 

## <a name="next-steps"></a>Passaggi successivi
tabelle toouse distribuiti in modo efficace, vedere [distribuzione nelle tabelle SQL Data Warehouse](sql-data-warehouse-tables-distribute.md)  

