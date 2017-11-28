---
title: aaaIndexers in ricerca di Azure | Documenti Microsoft
description: Ricerca per indicizzazione dati ricercabili tooextract di archiviazione di Azure, Azure Cosmos DB o database SQL di Azure e popola un indice di ricerca di Azure.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Indicizzatori in Ricerca di Azure
> [!div class="op_single_selector"]
>
> * [Panoramica](search-indexer-overview.md)
> * [Portale](search-import-data-portal.md)
> * [SQL di Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Archiviazione BLOB di Azure](search-howto-indexing-azure-blob-storage.md)
> * [Archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md)
>
>

Un **indicizzatore** in ricerca di Azure è un crawler che estrae dati ricercabili e i metadati da un'origine dati esterna e popola un indice in base al campo mapping tra l'indice di hello e l'origine dati. Questo approccio è talvolta tooas di cui si fa riferimento un modello di' pull', perché il servizio hello estrae i dati in senza che sia necessario toowrite qualsiasi codice che inserisce dati tooan indice.

È possibile utilizzare un indicizzatore come hello unico mezzo per l'inserimento di dati o utilizzare una combinazione di tecniche che includono l'utilizzo di hello di un indicizzatore per il caricamento solo alcuni dei campi di hello nell'indice.

È possibile eseguire gli indicizzatori su richiesta o in base a una pianificazione di aggiornamento dati ricorrente che viene eseguita ogni quindici minuti. Aggiornamenti più frequenti richiedono un modello push che aggiorna contemporaneamente i dati sia in Ricerca di Azure che nell'origine dati esterna.

## <a name="approaches-for-creating-and-managing-indexers"></a>Approcci per la creazione e la gestione degli indicizzatori
Per creare e gestire gli indicizzatori disponibili a livello generale, come Azure SQL o Azure Cosmos DB, è possibile procedere nei modi seguenti:

* [Portale > Importazione guidata dati](search-get-started-portal.md)
* [API REST del servizio](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>Procedura di configurazione di base
Gli indicizzatori possono offrire funzionalità di origine dati toohello univoco. In questo senso, alcuni aspetti della configurazione dell'indicizzatore o dell'origine dati possono variare a seconda del tipo di indicizzatore. Tuttavia, tutti gli indicizzatori condividono hello stessa composizione di base e i requisiti. I passaggi che sono comuni tooall gli indicizzatori sono illustrati più avanti.

### <a name="step-1-create-an-index"></a>Passaggio 1: Creare un indice
Un indicizzatore consente di automatizzare alcuni inserimento correlato toodata attività, ma la creazione di un indice non è uno di essi. Uno dei prerequisiti prevede che sia disponibile un indice predefinito con campi corrispondenti a quelli dell'origine dati esterna. Per altre informazioni su come strutturare un indice, vedere [Creare l'indice (API REST di Ricerca di Azure)](https://msdn.microsoft.com/library/azure/dn798941.aspx).

### <a name="step-2-create-a-data-source"></a>Passaggio 2: Creare un'origine dati
Un indicizzatore effettua il pull dei dati da un' **origine dati** che contiene informazioni, ad esempio la stringa di connessione. Attualmente è supportata le seguenti origini dati hello:

* [Database SQL di Azure o SQL Server in una macchina virtuale di Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Archiviazione Blob di Azure](search-howto-indexing-azure-blob-storage.md), testo tooextract da PDF, documenti di Office, HTML o XML
* [Archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md)

Origini dati configurate e gestite in modo indipendente da indicizzatori hello utilizzarle, vale a dire che un'origine dati è utilizzabile da più tooload indicizzatori più di un indice alla volta.

### <a name="step-3create-and-schedule-hello-indexer"></a>Passaggio 3: creare e pianificare indicizzatore hello
definizione di indicizzatore Hello è un costrutto che specifica l'indice hello, origine dati e una pianificazione. Un indicizzatore può fare riferimento a un'origine dati da un altro servizio, purché tale origine dati sia da hello stessa sottoscrizione. Per altre informazioni su come strutturare un indicizzatore, vedere [Creare un indicizzatore (API REST di Ricerca di Azure)](https://msdn.microsoft.com/library/azure/dn946899.aspx).

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato l'idea alla base hello, hello sarà tooreview requisiti e attività tooeach specifiche origini dati.

* [Database SQL di Azure o SQL Server in una macchina virtuale di Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Archiviazione Blob di Azure](search-howto-indexing-azure-blob-storage.md), testo tooextract da PDF, documenti di Office, HTML o XML
* [Archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md)
* [L'indicizzazione BLOB CSV utilizzando hello indicizzatore di Blob di ricerca di Azure](search-howto-index-csv-blobs.md)
* [Indicizzazione di BLOB JSON con l'indicizzatore di BLOB di Ricerca di Azure](search-howto-index-json-blobs.md)
