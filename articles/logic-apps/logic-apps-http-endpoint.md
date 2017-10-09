---
title: aaaCall, trigger o flussi di lavoro con gli endpoint HTTP - App Azure per la logica di nidificare | Documenti Microsoft
description: Impostare toocall endpoint HTTP, trigger o di nidificare i flussi di lavoro per le app di logica di Azure
services: logic-apps
keywords: flussi di lavoro, endpoint HTTP
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>Chiamare, attivare o annidare i flussi di lavoro con endpoint HTTP in app per la logica

È possibile esporre a livello nativo gli endpoint HTTP sincroni come trigger sulle app per la logica, permettendo in tal modo di attivare o di chiamare le app per la logica tramite un URL. È inoltre possibile annidare i flussi di lavoro nell'app per la logica usando un modello di endpoint richiamabile.

gli endpoint HTTP toocreate, è possibile aggiungere questi trigger in modo che la logica App può ricevere le richieste in ingresso:

* [Richiesta](../connectors/connectors-native-reqres.md)

* [Webhook di connessione API](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [Webhook HTTP](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > Sebbene negli esempi utilizzano hello **richiesta** trigger, è possibile utilizzare uno qualsiasi dei hello elencati trigger HTTP e tutti i principi si applicano in modo identico toohello anche altri tipi di trigger.

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>Configurare un endpoint HTTP per un'app per la logica

toocreate un endpoint HTTP, aggiungere un trigger che può ricevere le richieste in ingresso.

1. Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure"). Andare tooyour logica app e aprire Progettazione applicazione logica.

2. Aggiungere un trigger che consente all'app per la logica di ricevere richieste in ingresso. Ad esempio, aggiungere hello **richiesta** trigger tooyour logica app.

3.  In **dello Schema JSON del corpo della richiesta**, è possibile immettere uno schema JSON per il payload di hello (dati) che si prevede di hello trigger tooreceive.

    finestra di progettazione Hello schema utilizzato per generare i token che l'app di logica è possibile utilizzare tooconsume, analisi e il passaggio dei dati da un trigger di hello tramite il flusso di lavoro. 
    Altre informazioni sui [token generati da schemi JSON](#generated-tokens).

    Per questo esempio, immettere schema hello mostrato nella progettazione di hello:

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Aggiungere l'azione richiesta hello][1]

    > [!TIP]
    > 
    > È possibile generare uno schema per un payload JSON di esempio da uno strumento come [jsonschema.net](http://jsonschema.net/), o in hello **richiesta** trigger scegliendo **schema toogenerate payload di esempio utilizzare**. 
    > Immettere il payload di esempio e scegliere **Fine**.

    Ad esempio, questo payload di esempio:

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    genera questo schema:

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  Salvare l'app per la logica. In **HTTP POST toothis URL**, è ora necessario trovare un URL callback generato, come nell'esempio:

    ![URL di callback generato per endpoint](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    L'URL contiene una chiave di firma di accesso condiviso (SAS) nei parametri di query hello che vengono utilizzati per l'autenticazione. 
    È inoltre possibile ottenere l'URL dell'endpoint HTTP hello dal dashboard Panoramica di app logica nel portale di Azure hello. In **Cronologia trigger** selezionare il trigger:

    ![Ottenere l'URL dell'endpoint HTTP GET dal portale di Azure][2]

    In alternativa, è possibile ottenere l'URL di hello eseguendo questa chiamata:

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>Modificare il metodo HTTP hello del trigger

Per impostazione predefinita, hello **richiesta** trigger prevede una richiesta POST HTTP, ma è possibile utilizzare un metodo HTTP diverso. 

> [!NOTE]
> È possibile specificare solo un tipo di metodo.

1. Nel trigger **Richiesta** scegliere **Mostra opzioni avanzate**.

2. Aprire hello **metodo** elenco. Per questo esempio, selezionare **GET** (OTTIENI) in modo che sia possibile testare l'URL dell'endpoint HTTP in un secondo momento.

    > [!NOTE]
    > È possibile selezionare qualsiasi altro metodo HTTP o specificare un metodo personalizzato per la propria app per la logica.

    ![Modificare il metodo HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>Accettare i parametri tramite l'URL dell'endpoint HTTP

Quando si desidera che i parametri di tooaccept URL endpoint HTTP, è possibile personalizzare percorso relativo del trigger.

1. Nel trigger **Richiesta** scegliere **Mostra opzioni avanzate**. 

2. In **metodo**, specificare il metodo hello HTTP che si desidera toouse la richiesta. Per questo esempio, selezionare hello **ottenere** metodo, se non hai già fatto, in modo che è possibile testare l'URL dell'endpoint del HTTP.

      > [!NOTE]
      > Quando si specifica un percorso relativo per il trigger, è necessario specificare anche in modo esplicito un metodo HTTP per il trigger.

3. In **percorso relativo**, specificare hello percorso relativo per il parametro hello deve accettare l'URL, ad esempio, `customers/{customerID}`.

    ![Specificare un percorso relativo per il parametro e il metodo HTTP hello](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse hello parametro, aggiungere un **risposta** azione tooyour logica app. (Nel trigger scegliere **Nuovo passaggio** > **Aggiungi un'azione** > **Risposta**) 

5. La risposta **corpo**, includere hello token per il parametro hello specificato nel percorso relativo del trigger.

    Ad esempio, tooreturn `Hello {customerID}`, aggiornare la risposta **corpo** con `Hello {customerID token}`. 
    elenco di contenuto dinamico Hello dovrà essere visualizzato e Mostra hello `customerID` token per si tooselect.

    ![Aggiungere il parametro tooresponse corpo](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    Il **corpo** dovrebbe essere simile al seguente:

    ![Corpo della risposta con parametri](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. Salvare l'app per la logica. 

    L'URL dell'endpoint HTTP include ora percorso relativo hello, ad esempio: 

    https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. tootest l'endpoint HTTP, copia e Incolla hello URL aggiornato in un'altra finestra del browser, ma sostituire `{customerID}` con `123456`, e premere INVIO.

    Il browser deve mostrare questo testo: 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>Token generati da schemi JSON per l'app per la logica

Quando si fornisce uno schema JSON nel **richiesta** trigger, hello progettazione applicazione logica genera i token per le proprietà in tale schema. È quindi possibile usare tali token per passare dati tramite il flusso di lavoro di app per la logica.

Per questo esempio, se si aggiunta hello `title` e `name` lo schema di proprietà tooyour JSON, i relativi token sono ora disponibili toouse nei passaggi successivi di flusso di lavoro. 

Di seguito è riportato lo schema JSON completo hello:

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a>Creare flussi di lavoro annidati per le app per la logica

È possibile nidificare i flussi di lavoro nell'app per la logica aggiungendo altre app per la logica che possono ricevere richieste. tooinclude queste App per la logica, aggiungere hello **App logica di Azure - scegliere un flusso di lavoro App per la logica** trigger tooyour azione. È quindi possibile selezionare dalle app per la logica idonee.

![Aggiungere un'altra app per la logica](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>Chiamare o avviare le app per la logica tramite endpoint HTTP

Dopo aver creato l'endpoint HTTP, è possibile attivare l'app logica tramite un `POST` metodo toohello l'URL completo. Le app per la logica dispongono di supporto incorporato per gli endpoint di accesso diretto.

## <a name="reference-content-from-an-incoming-request"></a>Riferimento al contenuto dalla richiesta in ingresso

Se hello del contenuto del tipo è `application/json`, è possibile fare riferimento a proprietà hello richiesta in ingresso. In caso contrario, il contenuto viene considerato come una singola unità binaria che è possibile passare tooother API. il contenuto all'interno del flusso di lavoro hello tooreference, è necessario convertire tale contenuto. Ad esempio, se si passa `application/xml` contenuto, è possibile utilizzare `@xpath()` per l'estrazione, XPath o `@json()` per la conversione tooJSON XML. Informazioni sull'[uso dei tipi di contenuto](../logic-apps/logic-apps-content-type.md).

output di hello tooget da una richiesta in ingresso, è possibile utilizzare hello `@triggerOutputs()` (funzione). output di Hello potrebbe essere simile al seguente:

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

hello tooaccess `body` proprietà in particolare, è possibile utilizzare hello `@triggerBody()` scelta rapida. 

## <a name="respond-toorequests"></a>Rispondere toorequests

È possibile toorespond toocertain richieste avviare un'app logica restituendo toohello contenuto chiamante. codice di stato tooconstruct hello, intestazione e corpo della risposta, è possibile utilizzare hello **risposta** azione. Questa azione può trovarsi ovunque nell'app logica, non solo alla fine di hello del flusso di lavoro.

> [!NOTE] 
> Se la logica app non include un **risposta**, risponde endpoint HTTP hello *immediatamente* con un **202 accettato** stato. Inoltre, per hello richiesta tooget hello risposta originale, tutti i passaggi necessari per la risposta hello deve essere completata entro hello [il limite di timeout della richiesta](./logic-apps-limits-and-config.md) a meno che non si chiama del flusso di lavoro hello come app logica annidati. In non caso di alcuna risposta entro tale limite, la richiesta in ingresso hello scade e riceve la risposta HTTP hello **408 timeout Client**. Per le app logica annidati, hello padre logica app continua toowait per una risposta fino al completamento, indipendentemente dal tempo è obbligatorio.

### <a name="construct-hello-response"></a>Costrutto hello risposta

È possibile includere più di un'intestazione e qualsiasi tipo di contenuto nel corpo della risposta hello. Nel nostro esempio di risposta, intestazione hello specifica che la risposta hello ha tipo di contenuto `application/json`. e contiene il corpo di hello `title` e `name`, a seconda dello schema JSON hello aggiornato in precedenza per hello **richiesta** trigger.

![Azione di risposta HTTP][3]

Le risposte hanno le seguenti proprietà:

| Proprietà | Descrizione |
| --- | --- |
| statusCode |Specifica il codice di stato HTTP hello per richiesta in ingresso a toohello risponde. Può essere qualsiasi codice di stato valido che inizia con 2xx, 4xx o 5xx. I codici di stato 3xx non sono consentiti. |
| headers |Definisce un numero qualsiasi di intestazioni tooinclude in risposta hello. |
| body |Specifica un oggetto body che può essere una stringa, un oggetto JSON o anche contenuto binario a cui si fa riferimento da un passaggio precedente. |

Ecco quale schema JSON hello ora sembra di connessioni per hello **risposta** azione:

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> definizione completa JSON tooview hello per l'app di logica, in Progettazione applicazione logica, hello scegliere **Code vista**.

## <a name="q--a"></a>Domande e risposte

#### <a name="q-what-about-url-security"></a>D: Come viene garantita la sicurezza degli URL?

R: Azure genera in modo sicuro gli URL di callback dell'app per la logica mediante una firma di accesso condiviso (SAS). La firma viene trasmessa come parametro di query e deve essere convalidata prima dell'attivazione dell'app per la logica. Azure genera una firma di hello utilizzando una combinazione univoca di una chiave privata per app per la logica, nome del trigger hello e operazione hello che viene eseguita. Pertanto, a meno che un utente dispone di accesso toohello secret logica app chiave, è possibile generare una firma valida.

   > [!IMPORTANT]
   > Per la produzione e i sistemi protetti, è consigliabile evitare di chiamare logica app direttamente dal browser hello perché:
   > 
   > * chiave di accesso condiviso Hello viene visualizzato nell'URL hello.
   > * È possibile gestire i criteri di contenuto protetti a causa di tooshared domini tra i clienti di App per la logica.

#### <a name="q-can-i-configure-http-endpoints-further"></a>D: È possibile configurare ulteriormente gli endpoint HTTP?

R: Sì, gli endpoint HTTP supportano configurazioni più avanzate tramite la [**Gestione API**](../api-management/api-management-key-concepts.md). Questo servizio offre inoltre funzionalità hello per tutte le API, tra cui App per la logica di gestione è tooconsistently, impostare i nomi di dominio personalizzato, utilizzare più metodi di autenticazione e altre informazioni, ad esempio:

* [Metodo di richiesta di modifica hello](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [Modificare i segmenti di URL hello della richiesta di hello](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* Configurare i domini di gestione API in hello [portale di Azure](https://portal.azure.com/ "portale di Azure")
* Impostare i criteri toocheck l'autenticazione di base

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>D: che cosa è cambiato quando schema hello eseguita la migrazione dalla versione di anteprima 1 dicembre 2014 hello?

R: Di seguito è riportato un riepilogo di queste modifiche:

| Anteprima del 1 dicembre 2014 | 1 giugno 2016 |
| --- | --- |
| Fare clic sull'app per le API **Listener HTTP** |Fare clic su **Attivazione manuale**. Non è necessaria un'app per le API. |
| Impostazione di Listener HTTP "*Send response automatically*" (Invia risposta automaticamente) |Contengono un **risposta** azione o non in una definizione di flusso di lavoro hello |
| Configurare l'autenticazione di base o OAuth |tramite Gestione API |
| Configurare il metodo HTTP |In **Mostra opzioni avanzate** scegliere un metodo HTTP |
| Configurare il percorso relativo |In **Mostra opzioni avanzate** aggiungere un percorso relativo |
| Corpo del riferimento hello in arrivo tramite`@triggerOutputs().body.Content` |Fare riferimento tramite `@triggerOutputs().body` |
| **Inviare una risposta HTTP** azione hello HTTP Listener |Fare clic su **rispondono tooHTTP richiesta** (nessuna App API obbligatorio) |

## <a name="get-help"></a>Ottenere aiuto

rispondere alle domande di domande tooask, e informazioni su quali altri logica app di Azure in caso di utenti, visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passaggi successivi

* [Creare definizioni di app per la logica](./logic-apps-author-definitions.md)
* [Gestire errori ed eccezioni](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
