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
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Raccomandazioni di Azure Machine Learning - Integrazione con JavaScript
> [!NOTE]
> È consigliabile iniziare utilizzando hello indicazioni API cognitivi servizio invece di questa versione. Hello servizio cognitivi indicazioni andrà a sostituire questo servizio e tutte le nuove funzionalità hello verranno sviluppate non esiste. Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.
> Altre informazioni, vedere [toohello migrazione nuovo servizio cognitivi](http://aka.ms/recomigrate)
> 
> 

Questo documento illustrano come toointegrate del sito utilizzando JavaScript. Hello JavaScript consente toosend gli eventi di acquisizione dei dati e indicazioni tooconsume dopo aver creato un modello di raccomandazione. Tutte le operazioni eseguite tramite JS possono essere eseguite anche dal lato server.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Panoramica generale
L'integrazione del sito con Azure ML Recommendations si articola in 2 fasi:

1. Invio di eventi ad Azure ML Recommendations. In questo modo toobuild un modello di raccomandazione.
2. Utilizzare indicazioni hello. Una volta creato il modello di hello è possibile utilizzare indicazioni hello. (Questo documento vengono descritte le modalità toobuild un modello, leggere hello tooget Guida introduttiva ulteriori informazioni su come).

<ins>Fase I</ins>

In hello prima fase di che nelle pagine html si inserisce una piccola libreria JavaScript che consente hello eventi toosend pagina che si verificano nella pagina html hello nei server di Azure ML raccomandazioni (tramite Data Market):

![Drawing1][1]

<ins>Fase II</ins>

In hello seconda fase, quando si desidera consigli hello tooshow pagina hello selezionare una delle seguenti opzioni hello:

1. il server (in fase di hello del rendering della pagina) chiama indicazioni tooget Azure ML indicazioni Server (tramite Data Market). risultati di Hello includono un elenco di id degli elementi. Il server deve risultati hello tooenrich con gli elementi di hello metadati (ad esempio immagini, descrizione) e inviare hello creato pagina toohello browser.

![Drawing2][2]

2. hello è toouse hello JavaScript file di piccole dimensioni da una tooget fase un semplice elenco di elementi consigliati. dati Hello qui ricevuti sono più snelli di hello prima opzione hello.

![Drawing3][3]

## <a name="2-prerequisites"></a>2. Prerequisiti
1. Creare un nuovo modello utilizzando le API di hello. Vedere la Guida introduttiva di hello sul toodo è.
2. Codificare &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; con codifica base64. (Questo verrà utilizzato per hello l'autenticazione di base tooenable hello JS codice toocall hello API).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Inviare eventi di acquisizione dei dati tramite JavaScript
Hello passaggi facilitare l'invio di eventi:

1. Includere la libreria JQuery nel codice. È possibile scaricarlo da nuget in hello URL seguente.
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. Libreria Script Java indicazioni hello dal seguente URL hello includono: http://aka.ms/RecoJSLib1
3. Inizializzare la libreria di Azure ML indicazioni con i parametri appropriati hello.
   
     <script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Eventi di trasmissione hello appropriato. Vedere la sezione dettagliata di seguito in merito a tutti i tipi di eventi, esempio di evento Click, <script> se (typeof AzureMLRecommendationsEvent = = "undefined") {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Limitazioni e supporto browser
Di seguito viene fornita un'implementazione di riferimento così com'è. Tutti i principali browser dovrebbero essere supportati.

### <a name="32----type-of-events"></a>3.2.    Tipi di eventi
Sono disponibili 5 tipi di evento che supporta la libreria di hello: fare clic su, fare clic su indicazione, aggiungere tooShop carrello, rimuovere dal reparto carrello e l'acquisto. È un evento aggiuntivo che è usato tooset hello utente contesto denominato account di accesso.

#### <a name="321-click-event"></a>3.2.1. Evento Click
Questo evento deve essere usato ogni volta che un utente fa clic su un elemento. In genere quando l'utente fa clic su un elemento di una nuova pagina viene aperto con i dettagli dell'elemento hello; in questa pagina, questo evento dovrebbe essere attivato.

Parametri

* event (stringa, obbligatorio) - "click"
* elemento (string, obbligatorio) - identificatore univoco dell'elemento hello
* itemName (stringa, facoltativo) nome hello dell'elemento di hello
* Descrizione articolo (stringa, facoltativo) - Descrizione hello dell'elemento di hello
* itemCategory (stringa, facoltativo) categoria hello dell'elemento hello
  
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
Questo evento deve essere usato ogni volta che un utente fa clic su un elemento ricevuto da Azure ML Recommendations come elemento raccomandato. In genere quando l'utente fa clic su un elemento di una nuova pagina viene aperto con i dettagli dell'elemento hello; in questa pagina, questo evento dovrebbe essere attivato.

Parametri

* event (stringa, obbligatorio) - "recommendationclick"
* elemento (string, obbligatorio) - identificatore univoco dell'elemento hello
* itemName (stringa, facoltativo) nome hello dell'elemento di hello
* Descrizione articolo (stringa, facoltativo) - Descrizione hello dell'elemento di hello
* itemCategory (stringa, facoltativo) categoria hello dell'elemento hello
* i valori di inizializzazione (matrice di stringhe, facoltativo) - hello i valori di inizializzazione che ha generato query raccomandazione hello.
* recoList (matrice di stringhe, facoltativo) - hello risultato della richiesta di indicazione hello che ha generato l'elemento hello che è stato fatto clic.
  
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
Questo evento deve essere utilizzato quando l'utente di hello aggiungere un elemento di toohello carrello degli acquisti.
Parametri

* event (stringa, obbligatorio) - "addshopcart"
* elemento (string, obbligatorio) - identificatore univoco dell'elemento hello
* itemName (stringa, facoltativo) nome hello dell'elemento di hello
* Descrizione articolo (stringa, facoltativo) - Descrizione hello dell'elemento di hello
* itemCategory (stringa, facoltativo) categoria hello dell'elemento hello
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Evento Remove Shopping Cart
Questo evento deve essere utilizzato quando l'utente hello rimuove un elemento toohello carrello acquisti.

Parametri

* event (stringa, obbligatorio) - "removeshopcart"
* elemento (string, obbligatorio) - identificatore univoco dell'elemento hello
* itemName (stringa, facoltativo) nome hello dell'elemento di hello
* Descrizione articolo (stringa, facoltativo) - Descrizione hello dell'elemento di hello
* itemCategory (stringa, facoltativo) categoria hello dell'elemento hello
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Evento Purchase
Questo evento deve essere utilizzato quando l'utente hello ha acquistato il carrello acquisti.

Parametri

* event (stringa) - "purchase"
* items (acquistati) - matrice contenente una voce per ogni elemento acquistato<br><br>
  Formato elementi acquistati:
  * elemento (string) - identificatore univoco dell'elemento hello.
  * count (numero intero o stringa) - numero di elementi che sono stati acquistati
  * prezzo (float o string) - campo facoltativo - hello prezzo dell'articolo hello.

esempio di Hello seguente mostra l'acquisto di 3 elementi (33, 34, 35), due con tutti i campi popolati (elemento, count, prezzo) e uno (elemento 34) senza un prezzo.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Evento User Login
Azure ML indicazioni evento libreria consente di creare e utilizzare un cookie negli eventi tooidentify ordine da cui proviene hello browser stesso. Nel modello di ordine tooimprove hello risultati Azure ML indicazioni consente tooset un'identificazione univoca di utente che eseguirà l'override dell'utilizzo di cookie hello.

Questo evento deve essere utilizzato dopo sito tooyour account di accesso utente di hello.

Parametri

* event (stringa) - "userlogin"
* utente (string) - identificazione univoca dell'utente hello.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Utilizzare le raccomandazioni tramite JavaScript
codice Hello che utilizza la raccomandazione hello viene attivato da un evento JavaScript dalla pagina Web del client hello. risposta di raccomandazione Hello include hello gli ID degli elementi, i relativi nomi e le classificazioni consigliati. È toouse migliore, è necessario eseguire questa opzione solo per visualizzare un elenco di elementi - più complessi la gestione (ad esempio l'aggiunta di metadati dell'elemento hello) consigliato hello sull'integrazione di lato server hello.

### <a name="41-consume-recommendations"></a>4.1 Utilizzare le raccomandazioni
le raccomandazioni tooconsume che necessarie tooinclude hello necessarie librerie JavaScript nella pagina e toocall AzureMLRecommendationsStart. Vedere la sezione 2.

indicazioni tooconsume per uno o più elementi, è necessario toocall chiamato un metodo: AzureMLRecommendationsGetI2IRecommendation.

Parametri

* gli elementi (matrice di stringhe): uno o più elementi tooget consigli. Se si usa una build Fbt, qui sarà possibile impostare un solo elemento.
* numberOfResults (numero intero) - numero dei risultati richiesti
* includeMetadata (valore booleano, facoltativo) - se impostato too'true' indica il campo di metadati hello deve essere popolato nel risultato hello.
* L'elaborazione di funzione, una funzione che gestirà indicazioni hello restituito. Hello dati vengono restituiti come matrice di:
  * Item - ID univoco dell'elemento
  * name - nome dell'elemento (se esiste nel catalogo)
  * rating - valutazione della raccomandazione
  * metadati - stringa che rappresenta i metadati di hello dell'elemento hello

Esempio: le richieste di hello seguente codice 8 indicazioni per l'elemento "64f6eb0d-947a-4c18-a16c-888da9e228ba" (e non specificando includeMetadata - implicitamente dichiara che i metadati non sono necessario), quindi concatenare i risultati di hello in un buffer.

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
