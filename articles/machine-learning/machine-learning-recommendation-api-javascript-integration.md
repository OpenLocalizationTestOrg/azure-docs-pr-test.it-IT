---
title: 'Raccomandazioni di Machine Learning: integrazione con JavaScript | Documentazione Microsoft'
description: Raccomandazioni di Azure Machine Learning - Integrazione con JavaScript - Documentazione
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Raccomandazioni di Azure Machine Learning - Integrazione con JavaScript
> [!NOTE]
> È consigliabile iniziare usando l'API Recommendations di Servizi cognitivi invece di questa versione. Il Servizio cognitivo di Recommendations sostituirà questo servizio e verranno sviluppate nuove funzionalità. Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.
> Per altre informazioni, vedere [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)
> 
> 

Questo documento illustra come integrare il sito usando JavaScript. JavaScript consente di inviare eventi di acquisizione dei dati e utilizzare raccomandazioni dopo aver creato un modello di raccomandazione. Tutte le operazioni eseguite tramite JS possono essere eseguite anche dal lato server.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Panoramica generale
L'integrazione del sito con Azure ML Recommendations si articola in 2 fasi:

1. Invio di eventi ad Azure ML Recommendations. In tal modo verrà creato un modello di raccomandazione.
2. Utilizzo delle raccomandazioni. Dopo aver creato il modello, è possibile utilizzare le raccomandazioni. Questo documento non spiega come creare un modello. Per altre informazioni a riguardo, leggere la guida introduttiva.

<ins>Fase I</ins>

Nella prima fase si inserisce nelle pagine HTML una piccola libreria JavaScript che consente l'invio di eventi nel momento in cui si verificano nella pagina HTML ai server di Azure ML Recommendations (tramite DataMarket):

![Drawing1][1]

<ins>Fase II</ins>

Nella seconda fase, per visualizzare le raccomandazioni nella pagina si seleziona una delle opzioni seguenti:

1. Il server (in fase di rendering della pagina) chiama il server di Azure ML Recommendations (tramite DataMarket) per ottenere le raccomandazioni. I risultati includono un elenco di ID di elementi. Il server deve arricchire i risultati con i metadati degli elementi, ad esempio immagini e descrizione, e inviare la pagina creata al browser.

![Drawing2][2]

2. L'altra opzione prevede di usare il piccolo file JavaScript della fase I per ottenere un semplice elenco degli elementi raccomandati. I dati ricevuti in questo caso sono più snelli rispetto a quelli che si ricevono utilizzando la prima opzione.

![Drawing3][3]

## <a name="2-prerequisites"></a>2. Prerequisiti
1. Creare un nuovo modello usando le API. Per istruzioni su come eseguire questa operazione, vedere la guida introduttiva.
2. Codificare &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; con codifica base64. Questi dati verranno usati per l'autenticazione di base che consente al codice JS di chiamare le API.

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Inviare eventi di acquisizione dei dati tramite JavaScript
Per inviare eventi in modo semplice, seguire questa procedura:

1. Includere la libreria JQuery nel codice. È possibile scaricarla da nuget all'URL seguente.
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. Includere la libreria JavaScript di Recommendations disponibile all'URL seguente: http://aka.ms/RecoJSLib1
3. Inizializzare la libreria di Azure ML Recommendations con i parametri appropriati.
   
     <script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Inviare l'evento appropriato. Vedere la sezione dettagliata di seguito in merito a tutti i tipi di eventi, esempio di evento Click, <script> se (typeof AzureMLRecommendationsEvent = = "undefined") {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Limitazioni e supporto browser
Di seguito viene fornita un'implementazione di riferimento così com'è. Tutti i principali browser dovrebbero essere supportati.

### <a name="32----type-of-events"></a>3.2.    Tipi di eventi
La libreria supporta 5 tipi di eventi: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart e Purchase. Esiste un evento aggiuntivo, denominato Login, che viene usato per impostare il contesto dell'utente.

#### <a name="321-click-event"></a>3.2.1. Evento Click
Questo evento deve essere usato ogni volta che un utente fa clic su un elemento. In genere, quando un utente fa clic su un elemento, si apre una nuova pagina contenente i dettagli dell'elemento dove l'evento deve essere attivato.

Parametri

* event (stringa, obbligatorio) - "click"
* item (stringa, obbligatorio) - identificatore univoco dell'elemento
* itemName (stringa, facoltativo) - nome dell'elemento
* itemDescription (stringa, facoltativo) - descrizione dell'elemento
* itemCategory (stringa, facoltativo) - categoria dell'elemento
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

In alternativa, con dati facoltativi:

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. Evento Recommendation Click
Questo evento deve essere usato ogni volta che un utente fa clic su un elemento ricevuto da Azure ML Recommendations come elemento raccomandato. In genere, quando un utente fa clic su un elemento, si apre una nuova pagina contenente i dettagli dell'elemento dove l'evento deve essere attivato.

Parametri

* event (stringa, obbligatorio) - "recommendationclick"
* item (stringa, obbligatorio) - identificatore univoco dell'elemento
* itemName (stringa, facoltativo) - nome dell'elemento
* itemDescription (stringa, facoltativo) - descrizione dell'elemento
* itemCategory (stringa, facoltativo) - categoria dell'elemento
* seeds (matrice di stringhe, facoltativo) - semi che hanno generato la query di raccomandazione
* recoList (matrice di stringhe, facoltativo) - il risultato della richiesta di raccomandazione che ha generato l'elemento selezionato
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

In alternativa, con dati facoltativi:

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. Evento Add Shopping Cart
Questo evento deve essere usato quando l'utente aggiunge un elemento al carrello acquisti.
Parametri

* event (stringa, obbligatorio) - "addshopcart"
* item (stringa, obbligatorio) - identificatore univoco dell'elemento
* itemName (stringa, facoltativo) - nome dell'elemento
* itemDescription (stringa, facoltativo) - descrizione dell'elemento
* itemCategory (stringa, facoltativo) - categoria dell'elemento
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Evento Remove Shopping Cart
Questo evento deve essere usato quando l'utente rimuove un elemento dal carrello acquisti.

Parametri

* event (stringa, obbligatorio) - "removeshopcart"
* item (stringa, obbligatorio) - identificatore univoco dell'elemento
* itemName (stringa, facoltativo) - nome dell'elemento
* itemDescription (stringa, facoltativo) - descrizione dell'elemento
* itemCategory (stringa, facoltativo) - categoria dell'elemento
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Evento Purchase
Questo evento deve essere usato quando l'utente ha acquistato gli elementi nel carrello.

Parametri

* event (stringa) - "purchase"
* items (acquistati) - matrice contenente una voce per ogni elemento acquistato<br><br>
  Formato elementi acquistati:
  * item (stringa) - identificatore univoco dell'elemento.
  * count (numero intero o stringa) - numero di elementi che sono stati acquistati
  * price (float o stringa) - campo facoltativo - prezzo dell'elemento

L'esempio seguente illustra l'acquisto di 3 elementi (33, 34, 35), di cui due con tutti i campi popolati (item, count, price) e uno (item 34) privo di prezzo.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Evento User Login
La libreria degli eventi di Azure ML Recommendations crea e usa un cookie per identificare gli eventi che provengono dallo stesso browser. Per migliorare i risultati del modello, Azure ML Recommendations consente di impostare un'identificazione univoca dell'utente che sostituirà l'utilizzo del cookie.

Questo evento deve essere usato dopo l'accesso dell'utente al sito.

Parametri

* event (stringa) - "userlogin"
* user (stringa) - identificazione univoca dell'utente
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Utilizzare le raccomandazioni tramite JavaScript
Il codice che utilizza la raccomandazione viene attivato da alcuni eventi JavaScript nella pagina Web del client. Le risposta alla raccomandazione include gli ID degli elementi raccomandati con i relativi nomi e valutazioni. È preferibile usare questa opzione solo per la visualizzazione di un elenco degli elementi consigliati. Le attività di gestione più complesse, ad esempio l'aggiunta dei metadati dell'elemento, devono essere eseguite sull'integrazione lato server.

### <a name="41-consume-recommendations"></a>4.1 Utilizzare le raccomandazioni
Per utilizzare le raccomandazioni, è necessario includere nella pagina le librerie JavaScript obbligatorie e chiamare AzureMLRecommendationsStart. Vedere la sezione 2.

Per utilizzare le raccomandazioni per uno o più elementi, è necessario chiamare un metodo denominato AzureMLRecommendationsGetI2IRecommendation.

Parametri

* items (matrice di stringhe) - uno o più elementi per i quali ottenere le raccomandazioni Se si usa una build Fbt, qui sarà possibile impostare un solo elemento.
* numberOfResults (numero intero) - numero dei risultati richiesti
* includeMetadata (booleano, facoltativo) - se impostato su 'true' indica che il campo di metadati deve essere popolato nel risultato
* Funzione di elaborazione - una funzione che gestirà le raccomandazioni restituite I dati vengono restituiti come matrice di:
  * Item - ID univoco dell'elemento
  * name - nome dell'elemento (se esiste nel catalogo)
  * rating - valutazione della raccomandazione
  * metadata - stringa che rappresenta i metadati dell'elemento

Esempio: il codice seguente richiede 8 raccomandazioni per l'elemento "64f6eb0d-947a-4c18-a16c-888da9e228ba" e, poiché il parametro includeMetadata non è specificato, è implicito che i metadati non sono obbligatori. I risultati vengono quindi concatenati in un buffer.

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
