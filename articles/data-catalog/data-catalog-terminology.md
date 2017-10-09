---
title: terminologia di catalogo dati aaaAzure | Documenti Microsoft
description: Questo articolo fornisce un'introduzione tooconcepts e termini utilizzati nella documentazione di Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a>Terminologia del Catalogo dati di Azure
## <a name="catalog"></a>Catalogo
Hello Azure Data Catalog è un repository di metadati basato su cloud quali dati di asset di dati e origini possono essere registrati. catalogo Hello funge da un percorso di archiviazione centrale per i metadati strutturali estratti dalle origini dati e metadati descrittivi aggiunti dagli utenti.

## <a name="data-source"></a>Origine dati
Un'origine dati è un sistema o un contenitore che gestisce gli asset di dati. Esempi sono i database di SQL Server, Oracle e SQL Server Analysis Services (tabulari o multidimensionali) nonché i server di SQL Server Reporting Services.

## <a name="data-asset"></a>Asset di dati
Gli asset di dati sono oggetti contenuti all'interno delle origini dati che possono essere registrate con il catalogo di hello. Ad esempio, tabelle e viste di SQL Server, tabelle e viste di Oracle, misure, dimensioni e indicatori KPI di SQL Server Analysis Services e report di SQL Server Reporting Services.

## <a name="data-asset-location"></a>Posizione degli asset di dati
catalogo Hello archivia hello percorso di un'origine dati o di un asset di dati, che può essere utilizzato tooconnect toohello origine utilizzando un'applicazione client. formato Hello e i dettagli della posizione di hello variano in base al tipo di origine dati hello. Ad esempio, una tabella SQL Server può essere identificata tramite il nome composto da quattro parti (nome del server, nome del database, nome dello schema, nome dell'oggetto) mentre un report di SQL Server Reporting Services può essere identificato tramite il relativo URL.

## <a name="structural-metadata"></a>Metadati strutturali
I metadati strutturali sono metadati hello estratti da un'origine dati che descrive la struttura hello di un asset di dati. Ciò include percorso asset hello, il nome dell'oggetto e tipo e le caratteristiche aggiuntive specifiche del tipo. Ad esempio, i metadati strutturali hello per le tabelle e viste includono hello nomi e i tipi di dati per le colonne dell'oggetto hello.

## <a name="descriptive-metadata"></a>Metadati descrittivi
Metadati descrittivi sono metadati che descrivono hello scopo o la finalità di un asset di dati. In genere aggiunto metadati descrittivi dagli utenti del catalogo tramite il portale di Azure Data Catalog hello, ma può anche essere estratto durante la registrazione dell'origine dati hello. Ad esempio, lo strumento di registrazione di Azure Data Catalog hello estrarre descrizioni da hello proprietà Description in SQL Server Analysis Services e SQL Server Reporting Services, nonché da hello [ms_descriptionproprietàestesa](https://technet.microsoft.com/library/ms190243.aspx)nei database di SQL Server, se queste proprietà sono state popolate con i valori.

## <a name="request-access"></a>Richiedere l'accesso
Metadati descrittivi dell'asset di dati possono includere informazioni sulle modalità di accesso all'origine dati o asset di dati toohello toorequest. Queste informazioni viene presentate con percorso asset di dati hello e possono includere uno o più delle seguenti opzioni hello:

* indirizzo di posta elettronica Hello di hello utente o un team responsabile della connessione dell'origine dati di access toohello.
* URL di Hello di hello documentati processo che gli utenti devono seguire l'origine dei dati toohello toogain accesso.
* Hello l'URL di un strumento identity and access management (ad esempio Microsoft Identity Manager) che può essere utilizzato toogain accesso toohello dati origine.
* Una voce di testo libero che descrive come gli utenti possono ottenere l'origine dati di access toohello.

## <a name="preview"></a>Preview
Anteprima di Azure Data Catalog è uno snapshot di record too20 che possono essere estratti dall'origine dati hello durante la registrazione e archiviati nel catalogo di hello con dati hello dei metadati dell'asset. Anteprima Hello può aiutare gli utenti che un asset di dati di individuazione comprendono meglio la funzione e lo scopo. In altre parole, visualizzare i dati di esempio può essere più importante da visualizzare solo i nomi di colonna hello e tipi di dati.
Le anteprime sono supportate solo per le tabelle e viste e devono essere selezionate in modo esplicito dall'utente hello durante la registrazione.

## <a name="data-profile"></a>Profilo dei dati
Un profilo di dati in Azure Data Catalog è uno snapshot dei metadati a livello di tabella e a livello di colonna su un asset di dati registrati che può essere estratti dall'origine dati hello durante la registrazione e archiviato nel catalogo di hello con dati hello dei metadati dell'asset. Hello dati consente di individuare un asset di dati gli utenti comprendono meglio la funzione e lo scopo. Toopreviews simile, profili dati devono essere selezionati in modo esplicito dall'utente di hello durante la registrazione.

> [!NOTE]
> L'estrazione di un profilo dei dati può essere un'operazione costosa per tabelle di grandi dimensioni e le viste e può significativamente aumentare hello tooregister di tempo necessaria un'origine dati.
>
>

## <a name="user-perspective"></a>Prospettiva dell'utente
Nel Catalogo dati di Azure, qualsiasi utente può fornire metadati descrittivi per un asset di dati registrato. Ogni utente dispone di una prospettiva distinct in dati hello e sul relativo uso. Ad esempio, l'amministratore di hello responsabile per un server può fornire dettagli di hello del contratto di servizio (SLA) o windows backup. un amministratore dei dati possono fornire collegamenti toodocumentation per le aziende hello elabora hello dati supporta; e un analista può fornire una descrizione in termini di hello, che sono più rilevanti tooother analisti e che può essere estremamente utile toothose utenti necessario toodiscover e comprendere i dati di hello.

Ognuna di queste prospettive sono intrinsecamente utili e con Azure Data Catalog ogni utente può fornire informazioni di hello che sono significativo toothem, mentre tutti gli utenti possono usare i dati hello toounderstand informazioni e lo scopo.

## <a name="expert"></a>Esperto
Un esperto è un utente che è stato identificato come avente una prospettiva informata "esperta" per un asset di dati. Qualsiasi utente può aggiungere se stesso o un altro utente come esperto di un asset. Viene elencato come un esperto non apporta ulteriori privilegi nel catalogo dati di Azure. consente agli utenti tooeasily individuare tali prospettive toobe probabilmente utile durante la revisione dei metadati descrittivi un asset.

## <a name="owner"></a>Proprietario
Un proprietario è un utente con privilegi aggiuntivi per la gestione di un asset di dati nel Catalogo dati di Azure. Gli utenti possono diventare proprietari di dati registrati e i proprietari possono aggiungere altri utenti come comproprietari. Per ulteriori informazioni vedere [come asset di dati toomanage](data-catalog-how-to-manage.md)  

> [!NOTE]
> Gestione e proprietà sono disponibili solo in hello Standard Edition di Azure Data Catalog.
>
>

## <a name="registration"></a>Registrazione
La registrazione è act hello di estrazione dei metadati di asset di dati da un'origine dati e la copia del servizio Azure Data Catalog toohello. Gli asset di dati registrati possono essere annotati e individuati.

## <a name="see-also"></a>Vedere anche
* [Che cos'è il Catalogo dei dati di Azure?](data-catalog-what-is-data-catalog.md) -Questo articolo viene fornita una panoramica del servizio Azure Data Catalog hello, valore hello che fornisce e supporta scenari di hello.
* [Guida introduttiva di Azure Data Catalog](data-catalog-get-started.md) -questo articolo fornisce un'esercitazione end-to-end che illustra come toouse catalogo dati di Azure per l'individuazione di origine dati.  
