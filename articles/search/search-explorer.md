---
title: aaa "Query di un indice (portale - ricerca di Azure) | Documenti di Microsoft"
description: Eseguire una query di ricerca in soluzioni di ricerca del portale di Azure hello.
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>Query di un indice di ricerca di Azure utilizzando Esplora ricerche in hello portale di Azure
> [!div class="op_single_selector"]
> * [Panoramica](search-query-overview.md)
> * [Portale](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Questo articolo viene illustrato come un indice utilizzando una ricerca di Azure tooquery **Esplora ricerche** in hello portale di Azure. È possibile usare Esplora ricerche toosubmit semplice o completo Lucene query stringhe tooany indice esistente nel servizio.

## <a name="open-hello-service-dashboard"></a>Dashboard del servizio aprire hello
1. Fare clic su **tutte le risorse** sulla barra di spostamento hello hello il lato sinistro di hello [portale di Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).
2. Selezionare il servizio Ricerca di Azure.

## <a name="select-an-index"></a>Selezionare un indice

Indice di hello selezionare desideri toosearch da hello **indici** riquadro.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Aprire Esplora ricerche

Fare clic sulla barra di ricerca di Esplora ricerche riquadro tooslide hello aprire hello e riquadro risultati.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Avviare la ricerca

Quando si utilizza Esplora ricerche hello, è possibile specificare [parametri di query](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) query hello tooformulate.

1. In **Stringa di query** digitare una query e quindi fare clic su **Cerca**. 

   stringa di query Hello viene analizzata automaticamente in richiesta corretto hello URL toosubmit hello Azure API REST di ricerca di una richiesta HTTP.   
   
   È possibile utilizzare qualsiasi valido semplice o completo Lucene sintassi toocreate hello richiesta di query. Hello `*` carattere è ricerca vuoto o non specificato tooan equivalente che restituisce tutti i documenti in nessun ordine particolare.

2. In **risultati**, risultati della query sono presentati in JSON non elaborati, payload toohello identici restituiti in un corpo della risposta HTTP quando si inviano richieste a livello di codice.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti risorse fornisce esempi e informazioni sulla sintassi di query aggiuntive.

 + [Sintassi di query semplice](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Sintassi di query Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Esempi di sintassi di query Lucene](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [Sintassi delle espressioni filtro OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 