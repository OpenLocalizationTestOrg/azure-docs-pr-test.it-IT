---
title: aaaHow toouse Fiddler tooevaluate e testare le API REST di ricerca di Azure | Documenti Microsoft
description: "Usare Fiddler per la disponibilità di ricerca di Azure un approccio senza codice tooverifying e provare hello API REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>Usare Fiddler tooevaluate e testare le API REST di ricerca di Azure
> [!div class="op_single_selector"]
>
> * [Panoramica](search-query-overview.md)
> * [Esplora ricerche](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Questo articolo viene illustrato come toouse Fiddler, disponibile come una [download gratuito di telerik](http://www.telerik.com/fiddler), utilizzando hello API REST di ricerca di Azure, senza la necessità di qualsiasi codice toowrite tooissue HTTP richieste tooand Visualizza risposte. Ricerca di Azure è un servizio di ricerca cloud ospitato in Microsoft Azure e completamente gestito, facilmente programmabile con le API REST e .NET. API REST sono documentate nel servizio di ricerca di Azure Hello [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).

In hello alla procedura seguente, si sarà creare un indice, caricare documenti, indice hello query e query sul sistema hello per informazioni sul servizio.

toocomplete questi passaggi, sarà necessario un servizio di ricerca di Azure e `api-key`. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per istruzioni sulla modalità di avvio tooget.

## <a name="create-an-index"></a>Creare un indice
1. Avviare Fiddler In hello **File** menu, disattivare **acquisire il traffico** toohide estranei HTTP attività non correlate toohello dell'attività corrente.
2. In hello **Composer** scheda sarà di formulare una richiesta simile al seguente cattura di schermata hello.

      ![][1]
3. Selezionare **PUT**.
4. Immettere un URL che specifica l'URL del servizio hello, attributi della richiesta e hello. api-version. Alcuni tookeep di puntatori in considerazione:

   * Utilizzo di HTTPS come prefisso hello.
   * L'attributo della richiesta è "/indexes/hotels". In questo modo toocreate di ricerca di un indice denominato 'hotel'.
   * La versione API è specificata in lettere minuscole come "?api-version=2016-09-01". Le versioni API sono importanti perché Ricerca di Azure distribuisce aggiornamenti su base regolare. In rari casi, un aggiornamento del servizio può introdurre un toohello di modifica di rilievo API. Per questo motivo, Ricerca di Azure richiede la versione dell'API in ogni richiesta per garantire il controllo completo sulla versione usata.

     URL completo di Hello dovrebbe essere simile toohello esempio seguente.

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. Specificare l'intestazione della richiesta hello, sostituendo host hello e la chiave api con i valori validi per il servizio.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. Nel corpo della richiesta, incollare i campi di hello che costituiscono la definizione di indice hello.

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. Fare clic su **Execute**.

In pochi secondi, verrà visualizzata una risposta HTTP 201 nell'elenco delle sessioni hello, indice hello che indica che è stato creato correttamente.

Se si verificano HTTP 504, verificare il che URL hello specifichi HTTPS. Se viene visualizzato HTTP 400 o 404, tooverify corpo di controllo hello richiesta si sono verificati errori di copia e Incolla. Un HTTP 403 indica in genere un problema con hello chiave api (una chiave non valida o un problema di sintassi di specifica la chiave api hello).

## <a name="load-documents"></a>Caricare i documenti
In hello **Composer** scheda documenti toopost richiesta avrà un aspetto simile al seguente hello. il corpo di Hello di hello richiesta contiene dati di ricerca hello per 4 hotel.

   ![][2]

1. Selezionare **POST**.
2. Immettere un URL che inizia con HTTPS, seguito dall'URL del servizio e quindi da "/indexes/<'nomeindice'>/docs/index?api-version=2016-09-01". URL completo di Hello dovrebbe essere simile toohello esempio seguente.

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. Intestazione della richiesta deve essere hello stesso come in precedenza. Tenere presente che è stato sostituito host hello e la chiave api con i valori validi per il servizio.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Hello corpo della richiesta contiene quattro hotel indice con documenti toobe toohello aggiunto.

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
             "hotelName": "Fancy Stay",
             "category": "Luxury",
             "tags": ["pool", "view", "wifi", "concierge"],
             "parkingIncluded": false,
             "smokingAllowed": false,
             "lastRenovationDate": "2010-06-27T00:00:00Z",
             "rating": 5,
             "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "2",
             "baseRate": 79.99,
             "description": "Cheapest hotel in town",
             "hotelName": "Roach Motel",
             "category": "Budget",
             "tags": ["motel", "budget"],
             "parkingIncluded": true,
             "smokingAllowed": true,
             "lastRenovationDate": "1982-04-28T00:00:00Z",
             "rating": 1,
             "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. Fare clic su **Execute**.

In pochi secondi, verrà visualizzata una risposta HTTP 200 nell'elenco delle sessioni hello. Ciò indica hello documenti sono stati creati correttamente. Se viene visualizzato un 207, almeno un documento non è stato possibile tooupload. Se si verifica un errore 404, si verifica un errore di sintassi nell'intestazione di hello o corpo della richiesta di hello.

## <a name="query-hello-index"></a>Indice di query hello
Ora che l'indice e i documenti sono stati caricati, è possibile eseguire query su di essi.  In hello **Composer** scheda, un **ottenere** comando che esegue una query del servizio avrà un aspetto simile toohello seguente cattura di schermata.

   ![][3]

1. Selezionare **GET**.
2. Immettere un URL che inizia con HTTPS, seguito dall'URL del servizio, seguito da "/indexes/<'nome indice'>/docs?", seguito dai parametri di query. A titolo esemplificativo, utilizzare hello URL seguente, sostituendo il nome di host di esempio hello con uno valido per il servizio.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   Questa query cerca hello termine "motel" e recupera le categorie di facet per classificazioni.
3. Intestazione della richiesta deve essere hello stesso come in precedenza. Tenere presente che è stato sostituito host hello e la chiave api con i valori validi per il servizio.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

codice di risposta Hello deve essere di 200 e output di risposta di hello dovrebbe essere simile toohello seguente cattura di schermata.

   ![][4]

Hello query di esempio seguente è tratto dall'hello [operazione di indice di ricerca (API di ricerca di Azure)](http://msdn.microsoft.com/library/dn798927.aspx) su MSDN. Molte delle query di esempio hello in questo argomento include spazi, che non sono consentiti in Fiddler. Sostituire ogni spazio con il carattere + prima di incollare in hello stringa di query prima di tentare di query hello in Fiddler.

**Prima della sostituzione degli spazi:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**Dopo la sostituzione degli spazi con il carattere +:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>query sul sistema hello
È anche possibile eseguire una query hello sistema tooget conteggi e archiviazione uso del documento. In hello **Composer** , avrà un aspetto simile toohello seguente la richiesta e risposta hello verrà restituito un conteggio hello numero di documenti e lo spazio utilizzato.

 ![][5]

1. Selezionare **GET**.
2. Immettere un URL che include l'URL del servizio, seguito da "/indexes/hotels/stats?api-version=2016-09-01":

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. Specificare l'intestazione della richiesta hello, sostituendo host hello e la chiave api con i valori validi per il servizio.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Lasciare vuoto il corpo della richiesta hello.
5. Fare clic su **Execute**. Verrà visualizzato un codice di stato HTTP 200 nell'elenco delle sessioni hello. Selezionare il movimento di hello registrato per il comando.
6. Fare clic su hello **controlli** scheda, fare clic su hello **intestazioni** scheda e quindi selezionare hello JSON formato. Dovrebbe essere hello documento numero e dimensioni di archiviazione (in KB).

## <a name="next-steps"></a>Passaggi successivi
Vedere [gestire il servizio di ricerca in Azure](search-manage.md) per toomanaging un approccio senza codice e l'utilizzo di ricerca di Azure.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
