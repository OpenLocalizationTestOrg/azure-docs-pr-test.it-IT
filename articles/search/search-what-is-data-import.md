---
title: caricamento di aaaData in ricerca di Azure | Documenti Microsoft
description: Informazioni su come tooupload dati tooan indici in ricerca di Azure.
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>Caricare dati tooAzure ricerca
> [!div class="op_single_selector"]
> * [Panoramica](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Esistono due modi toopopulate un indice con i dati. prima opzione Hello viene eseguita manualmente i dati nell'indice di hello utilizzando hello ricerca di Azure [API REST](search-import-data-rest-api.md) o [.NET SDK](search-import-data-dotnet.md). seconda opzione Hello è troppo[scegliere un'origine dati supportata](search-indexer-overview.md) tooyour di indice e consente di inserire automaticamente i dati di hello ricerca di Azure.

## <a name="push-data-tooan-index"></a>Indice tooan di push dei dati
Questo approccio si riferisce l'invio del toomake di ricerca di dati tooAzure tooprogrammatically è disponibile per la ricerca. Per le applicazioni con requisiti di latenza molto bassa (ad esempio, se è necessario eseguire la ricerca toobe operazioni sincronizzate con i database di inventario dinamica), il modello di push hello è l'unica opzione disponibile.

È possibile utilizzare hello [API REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) o [.NET SDK](search-import-data-dotnet.md) toopush tooan dell'indice dei dati. Attualmente non è disponibile alcun supporto di strumenti per push dei dati tramite il portale di hello.

Questo approccio è più flessibile di modello pull hello perché è possibile caricare documenti singolarmente o in batch (backup too1000 per ogni batch o 16 MB, a seconda del valore limite per primo). modello push Hello consente inoltre tooupload documenti tooAzure ricerca indipendentemente dalla posizione dei dati.

formato dei dati Hello riconosciuto da ricerca di Azure è JSON e tutti i documenti nel set di dati hello devono contenere i campi mappati toofields definito nello schema di indice. 

## <a name="pull-data-into-an-index"></a>Effettuare il pull dei dati in un indice
modello pull Hello ricerche per indicizzazione di un'origine dati supportata e carica automaticamente i dati hello nell'indice. In Ricerca di Azure questa funzionalità viene implementata tramite *indicizzatori*, attualmente disponibili per [Archivio BLOB](search-howto-indexing-azure-blob-storage.md), [Archivio tabelle](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [Database SQL di Azure e SQL Server nelle macchine virtuali di Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 

Gli indicizzatori connettono a un'origine dati tooa indice (in genere una tabella, vista o struttura equivalente) ed eseguire il mapping campi tooequivalent campi di origine nell'indice hello. Durante l'esecuzione, set di righe hello è tooJSON automaticamente trasformati e caricati in corrispondenza dell'indice specificato hello. Tutti gli indicizzatori supportano la programmazione in modo che è possibile specificare la frequenza dati hello toobe aggiornato. La maggior parte degli indicizzatori forniscono se l'origine dati hello supporta di rilevamento delle modifiche. Dal rilevamento delle modifiche ed eliminazioni tooexisting inoltre documenti toorecognizing nuovi documenti, gli indicizzatori rimuovere hello necessità tooactively gestire dati hello nell'indice. 

Indicizzatore funzionalità viene esposta in hello [portale di Azure](search-import-data-portal.md), hello [API REST](/rest/api/searchservice/Indexer-operations), hello e [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations). 

Un portale di hello toousing vantaggio è che ricerca di Azure possono in genere genera uno schema di indice predefinito per l'utente per la lettura dei metadati di hello del set di dati origine hello. È possibile modificare l'indice generato hello fino a quando non viene elaborato indice hello, dopo cui hello solo le modifiche dello schema consentiti sono quelli che non richiedono la reindicizzazione. Modifiche di hello desiderate toomake impatto hello direttamente dello schema, sarà necessario indice hello toorebuild. 

Dopo aver compilato l'indice di hello, è possibile utilizzare **Esplora ricerche** nella barra dei comandi del portale hello come passaggio di verifica.

## <a name="query-an-index-using-search-explorer"></a>Eseguire query in un indice usando Esplora ricerche

Tooperform un modo rapido un controllo preliminare nel caricamento del documento hello è toouse **Esplora ricerche** nel portale di hello. Esplora Hello consente di eseguire query di un indice senza la necessità di qualsiasi codice toowrite. Hello un'esperienza di ricerca è basata sulle impostazioni predefinite, ad esempio hello [sintassi semplice](/rest/api/searchservice/simple-query-syntax-in-azure-search) predefinito e [parametro di query searchMode](/rest/api/searchservice/search-documents). Vengono restituiti in JSON in modo che è possibile controllare l'intero documento hello.

> [!TIP]
> Numerosi [esempi di codice di ricerca di Azure](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) includere set di dati incorporato o disponibili, che offre un modo semplice di tooget avviato. portale di Hello offre anche un indicizzatore di esempio e un'origine dati composta da un set di dati piccolo immobiliare (denominato "realestate-us-sample"). Quando si esegue un indicizzatore preconfigurato hello sull'origine dati di esempio hello, un indice viene creato e caricato con i documenti che è possono eseguire query in Esplora ricerche o da codice scritto.
