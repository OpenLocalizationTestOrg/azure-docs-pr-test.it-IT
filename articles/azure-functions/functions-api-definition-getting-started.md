---
title: aaaGetting avviato con OpenAPI Metadata nelle funzioni di Azure | Documenti Microsoft
description: Introduzione al supporto per OpenAPI in Funzioni di Azure
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>Creazione di metadati OpenAPI 2.0 (Swagger) per un'app per le funzioni (anteprima)

In questo documento viene hello passaggio da procedura di creazione di una definizione di OpenAPI per una semplice API ospitata in funzioni di Azure.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>Definizione di OpenAPI (Swagger)
[I metadati di swagger](http://swagger.io/) è un file che definisce la funzionalità di hello operative dell'API e consente a una funzione che ospita un toobe API REST utilizzato da un'ampia gamma di altri software. Offerte Microsoft quali PowerApps e [App per le API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), nonché 3rd party strumenti per sviluppatori come [Postman](https://www.getpostman.com/docs/importing_swagger) e [molti altri pacchetti](http://swagger.io/tools/) tutte consentono toobe l'API utilizzata con un Definizione swagger.

## <a name="prepare-function"></a>Creazione di una funzione con una API semplice
  una definizione di OpenAPI toocreate, è necessario innanzitutto toocreate una funzione con una semplice API. Se si dispone già di un'API ospitata in un'App di funzione, è possibile ignorare la sezione successiva toohello retta
1. Creare una nuova app per le funzioni.
    1. [Portale di Azure](https://portal.azure.com) > `+ New` &gt; Eseguire una ricerca per "App per le funzioni"
1. Creare una nuova funzione trigger HTTP all'interno della nuova app per le funzioni
    1. La funzione è già popolata con codice che definisce un'API REST semplice.
    1. Qualsiasi stringa passata toohello funzione come un parametro di query o nel corpo di hello viene restituito come "Hello {input}"
1. Passare toohello `Integrate` scheda della nuova funzione HTTP Trigger
    1. Attiva/disattiva `Allowed HTTP methods` troppo`Selected methods`
    1. In `Selected HTTP methods` deselezionare ogni verbo tranne POST.
    ![Metodi HTTP selezionati](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Questo passaggio semplifica la definizione dell'API in un secondo momento.

## <a name="enable"></a>Abilitazione del supporto per la definizione API
1. Passare troppo`your function name` > `Platform Features` > `API Definition`
![scheda definizione](./media/functions-api-definition-getting-started/definitiontab.png)
1. Impostare `API Definition Source` troppo`Function (preview)`
    1. Questo passaggio consente a un gruppo di opzioni OpenAPI per l'applicazione di funzione, incluso un toohost endpoint file OpenAPI dal dominio dell'applicazione (funzione), una copia di inline di hello [OpenAPI Editor](http://editor.swagger.io)e un generatore di definizione della Guida introduttiva.
![Definizioni attivate](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Creazione della definizione dell'API da un modello
1. Fare clic su`Generate API Definition template`.
    1. Questo passaggio esegue l'analisi dell'App di funzione per funzioni HTTP Trigger e utilizza informazioni di hello in functions.json toogenerate un documento OpenAPI.
1. Aggiungere un oggetto operazione troppo`paths: /api/yourfunctionroute post:`
    1. documento OpenAPI Guida introduttiva di Hello è una struttura di un documento OpenAPI completo. Richiede ulteriori metadati toobe una definizione di OpenAPI completa, ad esempio oggetti operazione e i modelli di risposta.
    1. oggetto operazione Hello esempio riportato di seguito è un riempimento produce o utilizza sezione, un oggetto parametro e un oggetto di risposta.
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  x-ms-summary indica il nome visualizzato in App per la logica, Flow e PowerApps.
    >
    > Estrarre [personalizzare la definizione Swagger per PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn altre.

1. Fare clic su `save` toosave le modifiche ![aggiunta di definizione del modello](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>Utilizzo della definizione dell'API
1. Copia il `API definition URL` e incollarlo in un nuovo tooview scheda browser documento OpenAPI non elaborato.
1. È possibile importare il numero di tooany OpenAPI documento degli strumenti per test e integrazione con tale URL.
    1. Molte risorse di Azure sono in grado di tooautomatically importazione del documento OpenAPI utilizzando hello URL di definizione dell'API che viene salvato nelle impostazioni dell'applicazione di funzione. Come parte di hello `Function` origine definizione API, è aggiornare tale url per l'utente.


## <a name="test-definition"></a>Utilizzando la definizione dell'API di hello Swagger dell'interfaccia utente tootest
Vi sono compilati in toohello di visualizzazione dell'interfaccia utente dell'editor di definizione API hello incorporato strumenti di test. Aggiungere la chiave API e quindi usare hello `Try this operation` pulsante sotto ciascun metodo. lo strumento di Hello utilizzerà le richieste di definizione dell'API tooformat hello e risposte ha esito positivo indica che la definizione sia corretta.

### <a name="steps"></a>Passaggi:

1. Copiare la chiave API della funzione
    1. chiave API Hello è reperibile nella funzione Trigger HTTP in `function name` > `Keys` > `Function Keys` 
   ![chiave (funzione)](./media/functions-api-definition-getting-started/functionkey.png)
1. Passare toohello `API Definition` pagina.
    1. Fare clic su `Authenticate` e aggiungere l'oggetto di sicurezza toohello chiave API di funzione nella parte superiore di hello.
  ![Chiave OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. Selezionare `/api/yourfunctionroute` > `POST`
1. Fare clic su `Try it out` e immettere un nome tootest
1. Nel 
 ![test di definizione dell'API](./media/functions-api-definition-getting-started/definitionTest.png) di `Pretty` verrà visualizzato l'esito positivo

## <a name="next-steps"></a>Passaggi successivi
* [Definizione di OpenAPI in Panoramica di Funzioni di Azure](functions-api-definition.md)
  * Leggere la documentazione completa di hello per altre informazioni sul supporto OpenAPI.
* [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md)  
  * Informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.
* [Repository GitHub di Funzioni di Azure](https://github.com/Azure/Azure-Functions/)
  * Estrarre toogive GitHub funzioni hello ci commenti e suggerimenti sull'anteprima del supporto definizione API hello! Crea un problema di GitHub per qualsiasi toosee aggiornato.
