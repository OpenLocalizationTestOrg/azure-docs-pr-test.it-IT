---
title: origini dei dati in Azure Data Catalog aaaHow toodiscover | Documenti Microsoft
description: "In questo articolo illustra come asset di dati toodiscover registrati con Azure Data Catalog, tra cui la ricerca e filtro e utilizzando hello raggiunge l'evidenziazione di funzionalità del portale di Azure Data Catalog hello."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a>Come origini dei dati toodiscover in Azure Data Catalog
## <a name="introduction"></a>Introduzione
Azure Data Catalog è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per le origini dati aziendali. In altre parole, Data Catalog permette agli utenti di trovare, comprendere e usare le origini dati e consente alle organizzazioni di ottenere maggior valore dai dati esistenti. Dopo aver registrata un'origine dati con Data Catalog, dei metadati sono indicizzato dai servizio hello, in modo che è possibile cercare facilmente toodiscover hello i dati che necessari.

## <a name="searching-and-filtering"></a>Ricerca e filtri
L'individuazione in Data Catalog usa due meccanismi principali: ricerca e filtri.

La ricerca è progettato toobe sia intuitiva e potente. Per impostazione predefinita, i termini di ricerca vengono confrontati con qualsiasi proprietà nel catalogo di hello, inclusi le annotazioni fornito dall'utente.

Il filtro è progettato toocomplement la ricerca. È possibile selezionare caratteristiche specifiche, ad esempio esperti, tipo di origine dati, tipo di oggetto e tag. È possibile visualizzare solo le risorse di dati corrispondente e vincolare asset toomatching risultati di ricerca.

Utilizzando una combinazione di ricerca e filtro, è possibile passare rapidamente le origini dati hello che sono state registrate con origini dati hello toodiscover catalogo dati che è necessario.

## <a name="search-syntax"></a>Sintassi di ricerca
Anche se ricerca testo libero hello è intuitiva e semplice, è possibile utilizzare anche la sintassi di ricerca catalogo dati per un maggiore controllo sui risultati di ricerca hello. Dati del catalogo ricerca supporta hello tecniche seguenti:

| Tecnica | Uso | Esempio |
| --- | --- | --- |
| Ricerca di base |Ricerca di base che usa uno o più termini di ricerca. I risultati sono tutte le risorse che corrispondono a qualsiasi proprietà di uno o più termini hello specificati. |`sales data` |
| Ambito della proprietà |Restituito solo le origini dati in cui il termine di ricerca hello viene abbinato hello la proprietà specificata. |`name:finance` |
| Operatori booleani |Ampliare o restringere una ricerca usando operazioni booleane. |`finance NOT corporate` |
| Raggruppamento con parentesi |Utilizzare le parentesi toogroup parti di hello query tooachieve isolamento logico, soprattutto in combinazione con gli operatori booleani. |`name:finance AND (tags:Q1 OR tags:Q2)` |
| Operatori di confronto |Usare confronti invece di uguaglianze per le proprietà che hanno dati di tipo numero e data. |`modifiedTime > "11/05/2014"` |

Per ulteriori informazioni su ricerca nel catalogo dati, vedere hello [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) articolo.

## <a name="hit-highlighting"></a>Evidenziazione dei risultati
Quando si visualizzano i risultati della ricerca, qualsiasi visualizzate le proprietà che corrispondono a hello specificato termini di ricerca (ad esempio nome dell'asset hello dati, la descrizione e tag) sono evidenziati toomake è tooidentify più semplice perché un asset di dati specificato è stato restituito da una ricerca specificata.

> [!NOTE]
> tooturn off evidenziazione, utilizzare hello **evidenziare** passare nel portale di hello catalogo dati.
>
>

Quando si visualizzano i risultati della ricerca, il motivo per cui un asset di dati è incluso potrebbe non essere sempre evidente, anche con l'evidenziazione abilitata. Poiché tutte le proprietà vengono ricercate per impostazione predefinita, un asset di dati potrebbe essere restituito a causa di una corrispondenza con una proprietà a livello di colonna. E poiché più utenti è possono annotare asset di dati registrati con i relativi tag e le descrizioni, non tutti i metadati potrebbero essere visualizzato nell'elenco di hello dei risultati della ricerca.

In visualizzazione affiancata di hello impostazione predefinita, ogni riquadro visualizzato nei risultati di ricerca hello include un **il termine di ricerca di visualizzazione corrisponde** icona, in modo che è possibile visualizzare rapidamente il numero di hello di corrispondenze, il percorso e toojump toothem se si desidera.

 ![Evidenziazione dei risultati di ricerca ed corrispondenti nel portale di Azure Data Catalog hello](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a>Riepilogo
Poiché la registrazione di un'origine dati con Data Catalog copie strutturale e descrittive metadati dai dati hello origine servizio catalogo toohello, diventa più facile toodiscover hello origine dati e comprendere. Dopo aver registrato un'origine dati, è possibile individuarlo tramite l'applicazione di filtri e cercare nel portale di hello catalogo dati.

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni dettagliate su come toodiscover le origini dati, vedere [Guida introduttiva di Azure Data Catalog](data-catalog-get-started.md).
