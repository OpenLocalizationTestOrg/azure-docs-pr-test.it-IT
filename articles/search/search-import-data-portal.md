---
title: dati aaaImport in ricerca di Azure nel portale di hello | Documenti Microsoft
description: Utilizzare hello Azure ricerca importazione guidata dei dati nel portale di Azure di hello toocrawl Azure dati NoSQL Azure Cosmos DB, archiviazione Blob, di archiviazione, Database SQL e SQL Server in macchine virtuali di Azure.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 00b0e59594560c0cdaea748df196518e9fba3834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-tooazure-search-using-hello-portal"></a>Importare dati tooAzure ricerca tramite il portale di hello
Hello Azure portale fornisce un **importare dati** guidata nel dashboard di ricerca di Azure hello di caricamento dei dati in un indice. 

  ![Importare i dati sulla barra dei comandi di hello][1]

Internamente, la procedura guidata hello Configura e richiama una *indicizzatore*, automatizzare diversi passaggi di processo di indicizzazione hello: 

* Connettere l'origine dati esterna tooan hello stessa sottoscrizione di Azure
* Generare uno schema di indice modificabile basato sulla struttura di dati di origine hello
* Caricare documenti JSON in un indice utilizzando un set di righe recuperate dall'origine dati hello

È possibile provare questo flusso di lavoro con dati di esempio in Azure Cosmos DB. Visitare [Introduzione alla ricerca di Azure nel portale di Azure hello](search-get-started-portal.md) per le istruzioni.

> [!NOTE]
> È possibile avviare hello **importare dati** guidata da hello Azure Cosmos DB dashboard toosimplify l'indicizzazione dell'origine dati. Nella finestra di navigazione a sinistra, andare troppo**raccolte** > **aggiungere ricerca di Azure** tooget avviato.

## <a name="data-sources-supported-by-hello-import-data-wizard"></a>Origini dati supportate da hello importazione guidata dati
la procedura guidata Importa dati Hello supporta hello seguenti origini dati: 

* Database SQL di Azure
* Dati relazionali di SQL Server in una macchina virtuale di Azure
* Azure Cosmos DB
* Archivio BLOB di Azure
* Archiviazione tabelle di Azure

Un set di dati bidimensionale è un input obbligatorio. È possibile eseguire l'importazione solo da una singola tabella, di una vista di database o di una struttura dei dati equivalente. È necessario creare questa struttura di dati prima di eseguire la procedura guidata hello.

## <a name="connect-tooyour-data"></a>Connettere i dati tooyour
1. Accedi toohello [portale di Azure](https://portal.azure.com) e dashboard del servizio aprire hello. È possibile fare clic su **più servizi** in hello jump barra toosearch esistente "ricerca servizi" nella sottoscrizione corrente hello. 
2. Fare clic su **l'importazione dei dati** sul comando hello barra blade di tooslide hello aperta l'importazione dei dati.  
3. Fare clic su **connettere i dati tooyour** toospecify una definizione dell'origine dati utilizzata da un indicizzatore. Per le origini dati all'interno di una sottoscrizione guidata hello in genere vengono rilevate e leggere le informazioni di connessione, riducendo al minimo i requisiti di configurazione generali.

|  |  |
| --- | --- |
| **Origine dati esistente** |Se nel servizio di ricerca sono già definiti indicizzatori, è possibile selezionare una definizione esistente dell'origine dati per un'altra importazione. |
| **Database SQL di Azure** |Nome del servizio, le credenziali per un utente del database con autorizzazioni di lettura e un nome di database può essere specificato nella pagina hello o tramite una stringa di connessione ADO.NET. Scegliere hello connessione stringa opzione tooview o personalizzare le proprietà. <br/><br/>Hello tabella o vista che fornisce i set di righe hello deve essere specificata nella pagina di hello. Questa opzione viene visualizzata dopo hello connessione ha esito positivo, fornendo un elenco a discesa in modo che è possibile effettuare una selezione. |
| **Macchine virtuali SQL Server in Azure** |Specificare un nome completo del servizio, un ID utente, una password e un database come stringa di connessione. toouse questa origine dati, è necessario aver precedentemente installato un certificato nell'archivio locale hello che Crittografa connessione hello. Per istruzioni, vedere [tooAzure connessione SQL VM ricerca](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md). <br/><br/>Hello tabella o vista che fornisce i set di righe hello deve essere specificata nella pagina di hello. Questa opzione viene visualizzata dopo hello connessione ha esito positivo, fornendo un elenco a discesa in modo che è possibile effettuare una selezione. |
| **Azure Cosmos DB** |I requisiti includono raccolta, il database e account hello. Tutti i documenti nella raccolta hello verranno inclusi nell'indice hello. È possibile definire una query tooflatten o filtrare i set di righe hello o toodetect modificato documenti per operazioni di aggiornamento dati successivi. |
| **Archiviazione BLOB di Azure** |I requisiti includono hello account di archiviazione e un contenitore. Facoltativamente, se i nomi di blob seguono una convenzione di denominazione virtuale per scopi di raggruppamento, è possibile specificare parte di directory virtuale hello del nome di hello come cartella nel contenitore. Per altre informazioni, vedere [Indicizzazione di documenti nell'archivio BLOB di Azure con Ricerca di Azure](search-howto-indexing-azure-blob-storage.md). |
| **Archivio tabelle di Azure** |I requisiti includono l'account di archiviazione hello e un nome di tabella. Facoltativamente, è possibile specificare un tooretrieve query un subset di tabelle hello. Per altre informazioni, vedere [Indicizzazione nell'archivio tabelle di Azure con Ricerca di Azure](search-howto-indexing-azure-tables.md). |

## <a name="customize-target-index"></a>Personalizzare l'indice di destinazione
Un indice preliminare in genere viene dedotto dal set di dati hello. Aggiungere, modificare o eliminare i campi toocomplete hello schema. Inoltre, impostare gli attributi in toodetermine di livello campo hello i comportamenti di ricerca successive.

1. In **indice di destinazione Personalizza**, specificare il nome di hello e un **chiave** utilizzati toouniquely identificano ogni documento. Hello chiave deve essere una stringa. Se i valori dei campi includono spazi o trattini essere certi tooset le opzioni avanzate **importare i dati di** toosuppress hello controllo di convalida per tali caratteri.
2. Verificare e modificare i campi rimanenti hello. Il nome del campo e il tipo sono in genere compilati automaticamente. È possibile modificare il tipo di dati hello fino a quando non viene creato l'indice di hello. Successivamente, la modifica rende necessaria la ricompilazione.
3. Impostare gli attributi dell'indice per ogni campo:
   
   * Recuperabile restituisce campo hello nei risultati della ricerca.
   * Filtrabile consente hello toobe di campo a cui fa riferimento nelle espressioni di filtro.
   * Ordinabile consente hello toobe di campo utilizzato in un ordinamento.
   * Facetable consente campo hello per la navigazione con facet.
   * Ricercabile abilita la ricerca full-text.
4. Fare clic su hello **Analyzer** scheda se si desidera toospecify un analizzatore di lingua a livello di campo hello. Al momento è possibile specificare solo gli analizzatori del linguaggio. Per usare un analizzatore personalizzato o un analizzatore non del linguaggio come Keyword, Pattern e così via, è necessario scrivere codice.
   
   * Fare clic su **Searchable** toodesignate full-text cercare campo hello e abilitare l'elenco a discesa Analyzer hello.
   * Scegliere analyzer hello desiderato. Per informazioni dettagliate, vedere [Creare un indice per i documenti in più lingue](search-language-support.md).
5. Fare clic su hello **dello strumento suggerimenti** suggerimenti di query con completamento tooenable su campi selezionati.

## <a name="import-your-data"></a>Importare i dati
1. In **importare i dati di**, specificare un nome per l'indicizzatore hello. Richiamare tale prodotto hello di hello l'importazione dei dati è un indicizzatore. In un secondo momento, se si desidera tooview o modificarlo, perché è necessario selezionarlo dal portale hello invece di ripetere la procedura guidata hello. 
2. Specificare la pianificazione di hello, che è basata su hello internazionali fuso orario in cui viene eseguito il provisioning servizio hello.
3. Impostare le soglie di toospecify opzioni avanzate per se l'indicizzazione può continuare se un documento viene eliminato. Inoltre, è possibile specificare se **chiave** i campi sono consentiti spazi toocontain e barre.  
4. Fare clic su **OK** toocreate hello indice e importare i dati di hello.

È possibile monitorare l'indicizzazione nel portale di hello. Quando vengono caricati i documenti, il numero di documenti hello aumenteranno per indice hello che è definito. In alcuni casi sono necessari alcuni minuti per hello pagina del portale toopick gli aggiornamenti più recenti, hello.

indice di Hello è pronto tooquery non appena tutti i documenti hello vengono caricati.

## <a name="query-an-index-using-search-explorer"></a>Eseguire query in un indice usando Esplora ricerche

portale Hello include **Esplora ricerche** in modo che è possibile eseguire query di un indice senza la necessità di qualsiasi codice toowrite. È possibile usare [Esplora ricerche](search-explorer.md) in qualsiasi indice.

Hello un'esperienza di ricerca è basata sulle impostazioni predefinite, ad esempio hello [sintassi semplice](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) e predefinito [parametro query searchMode (https://docs.microsoft.com/rest/api/searchservice/search-documents). 

Vengono restituiti in JSON, in un formato dettagliato, in modo che è possibile controllare l'intero documento hello.

## <a name="edit-an-existing-indexer"></a>Modificare un indicizzatore esistente
Come già indicato, hello importazione guidata dati crea un **indicizzatore**, che è possibile modificare un costrutto autonomo nel portale di hello.

Nel dashboard servizi hello, fare doppio clic su hello indicizzatore riquadro tooslide un elenco di tutti gli indicizzatori creato per la sottoscrizione. Fare doppio clic su uno dei toorun indicizzatori hello, modificare o eliminare. È possibile sostituire l'indice di hello con un altro esistente, modificare l'origine dati hello e impostare le opzioni per le soglie di errore durante l'indicizzazione.

## <a name="edit-an-existing-index"></a>Modificare un indice esistente
procedura guidata Hello creata anche un **indice**. Nella ricerca di Azure, indice tooan aggiornamenti strutturale richiederà una ricompilazione dell'indice. Una ricompilazione comporta l'eliminazione dell'indice di hello, ricreando l'indice di hello utilizzando uno schema modificato con modifiche hello desiderato e ricaricare i dati. Gli aggiornamenti strutturali includono la modifica di un tipo di dati e la ridenominazione o eliminazione di un campo.

Le modifiche che non richiedono la ricompilazione includono l'aggiunta di un nuovo campo, la modifica dei profili di punteggio, la modifica degli strumenti suggerimenti o la modifica degli analizzatori del linguaggio. Per altre informazioni, vedere [Aggiornare l'indice](https://msdn.microsoft.com/library/azure/dn800964.aspx) .


## <a name="next-steps"></a>Passaggi successivi
Esaminare queste ulteriori informazioni sugli indicizzatori toolearn di collegamenti:

* [Connessione del database SQL di Azure a Ricerca di Azure tramite gli indicizzatori](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Indicizzazione di Azure Cosmos DB](search-howto-index-documentdb.md)
* [Indicizzazione di documenti nell'archivio BLOB di Azure con Ricerca di Azure](search-howto-indexing-azure-blob-storage.md)
* [Indicizzazione nell'archivio tabelle di Azure con Ricerca di Azure](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png

