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
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="f2459-104">Chiamare, attivare o annidare i flussi di lavoro con endpoint HTTP in app per la logica</span><span class="sxs-lookup"><span data-stu-id="f2459-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="f2459-105">È possibile esporre a livello nativo gli endpoint HTTP sincroni come trigger sulle app per la logica, permettendo in tal modo di attivare o di chiamare le app per la logica tramite un URL.</span><span class="sxs-lookup"><span data-stu-id="f2459-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="f2459-106">È inoltre possibile annidare i flussi di lavoro nell'app per la logica usando un modello di endpoint richiamabile.</span><span class="sxs-lookup"><span data-stu-id="f2459-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="f2459-107">gli endpoint HTTP toocreate, è possibile aggiungere questi trigger in modo che la logica App può ricevere le richieste in ingresso:</span><span class="sxs-lookup"><span data-stu-id="f2459-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="f2459-108">Richiesta</span><span class="sxs-lookup"><span data-stu-id="f2459-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="f2459-109">Webhook di connessione API</span><span class="sxs-lookup"><span data-stu-id="f2459-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="f2459-110">Webhook HTTP</span><span class="sxs-lookup"><span data-stu-id="f2459-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="f2459-111">Sebbene negli esempi utilizzano hello **richiesta** trigger, è possibile utilizzare uno qualsiasi dei hello elencati trigger HTTP e tutti i principi si applicano in modo identico toohello anche altri tipi di trigger.</span><span class="sxs-lookup"><span data-stu-id="f2459-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="f2459-112">Configurare un endpoint HTTP per un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="f2459-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="f2459-113">toocreate un endpoint HTTP, aggiungere un trigger che può ricevere le richieste in ingresso.</span><span class="sxs-lookup"><span data-stu-id="f2459-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="f2459-114">Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="f2459-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="f2459-115">Andare tooyour logica app e aprire Progettazione applicazione logica.</span><span class="sxs-lookup"><span data-stu-id="f2459-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="f2459-116">Aggiungere un trigger che consente all'app per la logica di ricevere richieste in ingresso.</span><span class="sxs-lookup"><span data-stu-id="f2459-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="f2459-117">Ad esempio, aggiungere hello **richiesta** trigger tooyour logica app.</span><span class="sxs-lookup"><span data-stu-id="f2459-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="f2459-118">In **dello Schema JSON del corpo della richiesta**, è possibile immettere uno schema JSON per il payload di hello (dati) che si prevede di hello trigger tooreceive.</span><span class="sxs-lookup"><span data-stu-id="f2459-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="f2459-119">finestra di progettazione Hello schema utilizzato per generare i token che l'app di logica è possibile utilizzare tooconsume, analisi e il passaggio dei dati da un trigger di hello tramite il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f2459-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="f2459-120">Altre informazioni sui [token generati da schemi JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="f2459-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="f2459-121">Per questo esempio, immettere schema hello mostrato nella progettazione di hello:</span><span class="sxs-lookup"><span data-stu-id="f2459-121">For this example, enter hello schema shown in hello designer:</span></span>

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
    > <span data-ttu-id="f2459-123">È possibile generare uno schema per un payload JSON di esempio da uno strumento come [jsonschema.net](http://jsonschema.net/), o in hello **richiesta** trigger scegliendo **schema toogenerate payload di esempio utilizzare**.</span><span class="sxs-lookup"><span data-stu-id="f2459-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="f2459-124">Immettere il payload di esempio e scegliere **Fine**.</span><span class="sxs-lookup"><span data-stu-id="f2459-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="f2459-125">Ad esempio, questo payload di esempio:</span><span class="sxs-lookup"><span data-stu-id="f2459-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="f2459-126">genera questo schema:</span><span class="sxs-lookup"><span data-stu-id="f2459-126">generates this schema:</span></span>

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

4.  <span data-ttu-id="f2459-127">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2459-127">Save your logic app.</span></span> <span data-ttu-id="f2459-128">In **HTTP POST toothis URL**, è ora necessario trovare un URL callback generato, come nell'esempio:</span><span class="sxs-lookup"><span data-stu-id="f2459-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![URL di callback generato per endpoint](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="f2459-130">L'URL contiene una chiave di firma di accesso condiviso (SAS) nei parametri di query hello che vengono utilizzati per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f2459-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="f2459-131">È inoltre possibile ottenere l'URL dell'endpoint HTTP hello dal dashboard Panoramica di app logica nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f2459-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="f2459-132">In **Cronologia trigger** selezionare il trigger:</span><span class="sxs-lookup"><span data-stu-id="f2459-132">Under **Trigger History**, select your trigger:</span></span>

    ![Ottenere l'URL dell'endpoint HTTP GET dal portale di Azure][2]

    <span data-ttu-id="f2459-134">In alternativa, è possibile ottenere l'URL di hello eseguendo questa chiamata:</span><span class="sxs-lookup"><span data-stu-id="f2459-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="f2459-135">Modificare il metodo HTTP hello del trigger</span><span class="sxs-lookup"><span data-stu-id="f2459-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="f2459-136">Per impostazione predefinita, hello **richiesta** trigger prevede una richiesta POST HTTP, ma è possibile utilizzare un metodo HTTP diverso.</span><span class="sxs-lookup"><span data-stu-id="f2459-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="f2459-137">È possibile specificare solo un tipo di metodo.</span><span class="sxs-lookup"><span data-stu-id="f2459-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="f2459-138">Nel trigger **Richiesta** scegliere **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="f2459-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="f2459-139">Aprire hello **metodo** elenco.</span><span class="sxs-lookup"><span data-stu-id="f2459-139">Open hello **Method** list.</span></span> <span data-ttu-id="f2459-140">Per questo esempio, selezionare **GET** (OTTIENI) in modo che sia possibile testare l'URL dell'endpoint HTTP in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="f2459-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f2459-141">È possibile selezionare qualsiasi altro metodo HTTP o specificare un metodo personalizzato per la propria app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2459-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Modificare il metodo HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="f2459-143">Accettare i parametri tramite l'URL dell'endpoint HTTP</span><span class="sxs-lookup"><span data-stu-id="f2459-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="f2459-144">Quando si desidera che i parametri di tooaccept URL endpoint HTTP, è possibile personalizzare percorso relativo del trigger.</span><span class="sxs-lookup"><span data-stu-id="f2459-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="f2459-145">Nel trigger **Richiesta** scegliere **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="f2459-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="f2459-146">In **metodo**, specificare il metodo hello HTTP che si desidera toouse la richiesta.</span><span class="sxs-lookup"><span data-stu-id="f2459-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="f2459-147">Per questo esempio, selezionare hello **ottenere** metodo, se non hai già fatto, in modo che è possibile testare l'URL dell'endpoint del HTTP.</span><span class="sxs-lookup"><span data-stu-id="f2459-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f2459-148">Quando si specifica un percorso relativo per il trigger, è necessario specificare anche in modo esplicito un metodo HTTP per il trigger.</span><span class="sxs-lookup"><span data-stu-id="f2459-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="f2459-149">In **percorso relativo**, specificare hello percorso relativo per il parametro hello deve accettare l'URL, ad esempio, `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="f2459-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Specificare un percorso relativo per il parametro e il metodo HTTP hello](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="f2459-151">toouse hello parametro, aggiungere un **risposta** azione tooyour logica app.</span><span class="sxs-lookup"><span data-stu-id="f2459-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="f2459-152">(Nel trigger scegliere **Nuovo passaggio** > **Aggiungi un'azione** > **Risposta**)</span><span class="sxs-lookup"><span data-stu-id="f2459-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="f2459-153">La risposta **corpo**, includere hello token per il parametro hello specificato nel percorso relativo del trigger.</span><span class="sxs-lookup"><span data-stu-id="f2459-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="f2459-154">Ad esempio, tooreturn `Hello {customerID}`, aggiornare la risposta **corpo** con `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="f2459-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="f2459-155">elenco di contenuto dinamico Hello dovrà essere visualizzato e Mostra hello `customerID` token per si tooselect.</span><span class="sxs-lookup"><span data-stu-id="f2459-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Aggiungere il parametro tooresponse corpo](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="f2459-157">Il **corpo** dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f2459-157">Your **Body** should look like this example:</span></span>

    ![Corpo della risposta con parametri](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="f2459-159">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2459-159">Save your logic app.</span></span> 

    <span data-ttu-id="f2459-160">L'URL dell'endpoint HTTP include ora percorso relativo hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f2459-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="f2459-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="f2459-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="f2459-162">tootest l'endpoint HTTP, copia e Incolla hello URL aggiornato in un'altra finestra del browser, ma sostituire `{customerID}` con `123456`, e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="f2459-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="f2459-163">Il browser deve mostrare questo testo:</span><span class="sxs-lookup"><span data-stu-id="f2459-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="f2459-164">Token generati da schemi JSON per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="f2459-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="f2459-165">Quando si fornisce uno schema JSON nel **richiesta** trigger, hello progettazione applicazione logica genera i token per le proprietà in tale schema.</span><span class="sxs-lookup"><span data-stu-id="f2459-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="f2459-166">È quindi possibile usare tali token per passare dati tramite il flusso di lavoro di app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2459-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="f2459-167">Per questo esempio, se si aggiunta hello `title` e `name` lo schema di proprietà tooyour JSON, i relativi token sono ora disponibili toouse nei passaggi successivi di flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f2459-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="f2459-168">Di seguito è riportato lo schema JSON completo hello:</span><span class="sxs-lookup"><span data-stu-id="f2459-168">Here is hello complete JSON schema:</span></span>

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

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="f2459-169">Creare flussi di lavoro annidati per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="f2459-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="f2459-170">È possibile nidificare i flussi di lavoro nell'app per la logica aggiungendo altre app per la logica che possono ricevere richieste.</span><span class="sxs-lookup"><span data-stu-id="f2459-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="f2459-171">tooinclude queste App per la logica, aggiungere hello **App logica di Azure - scegliere un flusso di lavoro App per la logica** trigger tooyour azione.</span><span class="sxs-lookup"><span data-stu-id="f2459-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="f2459-172">È quindi possibile selezionare dalle app per la logica idonee.</span><span class="sxs-lookup"><span data-stu-id="f2459-172">You can then select from eligible logic apps.</span></span>

![Aggiungere un'altra app per la logica](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="f2459-174">Chiamare o avviare le app per la logica tramite endpoint HTTP</span><span class="sxs-lookup"><span data-stu-id="f2459-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="f2459-175">Dopo aver creato l'endpoint HTTP, è possibile attivare l'app logica tramite un `POST` metodo toohello l'URL completo.</span><span class="sxs-lookup"><span data-stu-id="f2459-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="f2459-176">Le app per la logica dispongono di supporto incorporato per gli endpoint di accesso diretto.</span><span class="sxs-lookup"><span data-stu-id="f2459-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="f2459-177">Riferimento al contenuto dalla richiesta in ingresso</span><span class="sxs-lookup"><span data-stu-id="f2459-177">Reference content from an incoming request</span></span>

<span data-ttu-id="f2459-178">Se hello del contenuto del tipo è `application/json`, è possibile fare riferimento a proprietà hello richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="f2459-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="f2459-179">In caso contrario, il contenuto viene considerato come una singola unità binaria che è possibile passare tooother API.</span><span class="sxs-lookup"><span data-stu-id="f2459-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="f2459-180">il contenuto all'interno del flusso di lavoro hello tooreference, è necessario convertire tale contenuto.</span><span class="sxs-lookup"><span data-stu-id="f2459-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="f2459-181">Ad esempio, se si passa `application/xml` contenuto, è possibile utilizzare `@xpath()` per l'estrazione, XPath o `@json()` per la conversione tooJSON XML.</span><span class="sxs-lookup"><span data-stu-id="f2459-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="f2459-182">Informazioni sull'[uso dei tipi di contenuto](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="f2459-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="f2459-183">output di hello tooget da una richiesta in ingresso, è possibile utilizzare hello `@triggerOutputs()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="f2459-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="f2459-184">output di Hello potrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f2459-184">hello output might look like this example:</span></span>

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

<span data-ttu-id="f2459-185">hello tooaccess `body` proprietà in particolare, è possibile utilizzare hello `@triggerBody()` scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="f2459-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="f2459-186">Rispondere toorequests</span><span class="sxs-lookup"><span data-stu-id="f2459-186">Respond toorequests</span></span>

<span data-ttu-id="f2459-187">È possibile toorespond toocertain richieste avviare un'app logica restituendo toohello contenuto chiamante.</span><span class="sxs-lookup"><span data-stu-id="f2459-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="f2459-188">codice di stato tooconstruct hello, intestazione e corpo della risposta, è possibile utilizzare hello **risposta** azione.</span><span class="sxs-lookup"><span data-stu-id="f2459-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="f2459-189">Questa azione può trovarsi ovunque nell'app logica, non solo alla fine di hello del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f2459-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="f2459-190">Se la logica app non include un **risposta**, risponde endpoint HTTP hello *immediatamente* con un **202 accettato** stato.</span><span class="sxs-lookup"><span data-stu-id="f2459-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="f2459-191">Inoltre, per hello richiesta tooget hello risposta originale, tutti i passaggi necessari per la risposta hello deve essere completata entro hello [il limite di timeout della richiesta](./logic-apps-limits-and-config.md) a meno che non si chiama del flusso di lavoro hello come app logica annidati.</span><span class="sxs-lookup"><span data-stu-id="f2459-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="f2459-192">In non caso di alcuna risposta entro tale limite, la richiesta in ingresso hello scade e riceve la risposta HTTP hello **408 timeout Client**.</span><span class="sxs-lookup"><span data-stu-id="f2459-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="f2459-193">Per le app logica annidati, hello padre logica app continua toowait per una risposta fino al completamento, indipendentemente dal tempo è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="f2459-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="f2459-194">Costrutto hello risposta</span><span class="sxs-lookup"><span data-stu-id="f2459-194">Construct hello response</span></span>

<span data-ttu-id="f2459-195">È possibile includere più di un'intestazione e qualsiasi tipo di contenuto nel corpo della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="f2459-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="f2459-196">Nel nostro esempio di risposta, intestazione hello specifica che la risposta hello ha tipo di contenuto `application/json`.</span><span class="sxs-lookup"><span data-stu-id="f2459-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="f2459-197">e contiene il corpo di hello `title` e `name`, a seconda dello schema JSON hello aggiornato in precedenza per hello **richiesta** trigger.</span><span class="sxs-lookup"><span data-stu-id="f2459-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![Azione di risposta HTTP][3]

<span data-ttu-id="f2459-199">Le risposte hanno le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="f2459-199">Responses have these properties:</span></span>

| <span data-ttu-id="f2459-200">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f2459-200">Property</span></span> | <span data-ttu-id="f2459-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f2459-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f2459-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="f2459-202">statusCode</span></span> |<span data-ttu-id="f2459-203">Specifica il codice di stato HTTP hello per richiesta in ingresso a toohello risponde.</span><span class="sxs-lookup"><span data-stu-id="f2459-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="f2459-204">Può essere qualsiasi codice di stato valido che inizia con 2xx, 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="f2459-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="f2459-205">I codici di stato 3xx non sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="f2459-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="f2459-206">headers</span><span class="sxs-lookup"><span data-stu-id="f2459-206">headers</span></span> |<span data-ttu-id="f2459-207">Definisce un numero qualsiasi di intestazioni tooinclude in risposta hello.</span><span class="sxs-lookup"><span data-stu-id="f2459-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="f2459-208">body</span><span class="sxs-lookup"><span data-stu-id="f2459-208">body</span></span> |<span data-ttu-id="f2459-209">Specifica un oggetto body che può essere una stringa, un oggetto JSON o anche contenuto binario a cui si fa riferimento da un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="f2459-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="f2459-210">Ecco quale schema JSON hello ora sembra di connessioni per hello **risposta** azione:</span><span class="sxs-lookup"><span data-stu-id="f2459-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

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
> <span data-ttu-id="f2459-211">definizione completa JSON tooview hello per l'app di logica, in Progettazione applicazione logica, hello scegliere **Code vista**.</span><span class="sxs-lookup"><span data-stu-id="f2459-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="f2459-212">Domande e risposte</span><span class="sxs-lookup"><span data-stu-id="f2459-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="f2459-213">D: Come viene garantita la sicurezza degli URL?</span><span class="sxs-lookup"><span data-stu-id="f2459-213">Q: What about URL security?</span></span>

<span data-ttu-id="f2459-214">R: Azure genera in modo sicuro gli URL di callback dell'app per la logica mediante una firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="f2459-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="f2459-215">La firma viene trasmessa come parametro di query e deve essere convalidata prima dell'attivazione dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2459-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="f2459-216">Azure genera una firma di hello utilizzando una combinazione univoca di una chiave privata per app per la logica, nome del trigger hello e operazione hello che viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="f2459-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="f2459-217">Pertanto, a meno che un utente dispone di accesso toohello secret logica app chiave, è possibile generare una firma valida.</span><span class="sxs-lookup"><span data-stu-id="f2459-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f2459-218">Per la produzione e i sistemi protetti, è consigliabile evitare di chiamare logica app direttamente dal browser hello perché:</span><span class="sxs-lookup"><span data-stu-id="f2459-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="f2459-219">chiave di accesso condiviso Hello viene visualizzato nell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="f2459-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="f2459-220">È possibile gestire i criteri di contenuto protetti a causa di tooshared domini tra i clienti di App per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2459-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="f2459-221">D: È possibile configurare ulteriormente gli endpoint HTTP?</span><span class="sxs-lookup"><span data-stu-id="f2459-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="f2459-222">R: Sì, gli endpoint HTTP supportano configurazioni più avanzate tramite la [**Gestione API**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="f2459-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="f2459-223">Questo servizio offre inoltre funzionalità hello per tutte le API, tra cui App per la logica di gestione è tooconsistently, impostare i nomi di dominio personalizzato, utilizzare più metodi di autenticazione e altre informazioni, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f2459-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="f2459-224">Metodo di richiesta di modifica hello</span><span class="sxs-lookup"><span data-stu-id="f2459-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="f2459-225">Modificare i segmenti di URL hello della richiesta di hello</span><span class="sxs-lookup"><span data-stu-id="f2459-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="f2459-226">Configurare i domini di gestione API in hello [portale di Azure](https://portal.azure.com/ "portale di Azure")</span><span class="sxs-lookup"><span data-stu-id="f2459-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="f2459-227">Impostare i criteri toocheck l'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="f2459-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="f2459-228">D: che cosa è cambiato quando schema hello eseguita la migrazione dalla versione di anteprima 1 dicembre 2014 hello?</span><span class="sxs-lookup"><span data-stu-id="f2459-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="f2459-229">R: Di seguito è riportato un riepilogo di queste modifiche:</span><span class="sxs-lookup"><span data-stu-id="f2459-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="f2459-230">Anteprima del 1 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="f2459-230">December 1, 2014 preview</span></span> | <span data-ttu-id="f2459-231">1 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="f2459-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="f2459-232">Fare clic sull'app per le API **Listener HTTP**</span><span class="sxs-lookup"><span data-stu-id="f2459-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="f2459-233">Fare clic su **Attivazione manuale**. Non è necessaria un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="f2459-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="f2459-234">Impostazione di Listener HTTP "*Send response automatically*" (Invia risposta automaticamente)</span><span class="sxs-lookup"><span data-stu-id="f2459-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="f2459-235">Contengono un **risposta** azione o non in una definizione di flusso di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="f2459-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="f2459-236">Configurare l'autenticazione di base o OAuth</span><span class="sxs-lookup"><span data-stu-id="f2459-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="f2459-237">tramite Gestione API</span><span class="sxs-lookup"><span data-stu-id="f2459-237">via API Management</span></span> |
| <span data-ttu-id="f2459-238">Configurare il metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="f2459-238">Configure HTTP method</span></span> |<span data-ttu-id="f2459-239">In **Mostra opzioni avanzate** scegliere un metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="f2459-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="f2459-240">Configurare il percorso relativo</span><span class="sxs-lookup"><span data-stu-id="f2459-240">Configure relative path</span></span> |<span data-ttu-id="f2459-241">In **Mostra opzioni avanzate** aggiungere un percorso relativo</span><span class="sxs-lookup"><span data-stu-id="f2459-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="f2459-242">Corpo del riferimento hello in arrivo tramite`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="f2459-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="f2459-243">Fare riferimento tramite `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="f2459-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="f2459-244">**Inviare una risposta HTTP** azione hello HTTP Listener</span><span class="sxs-lookup"><span data-stu-id="f2459-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="f2459-245">Fare clic su **rispondono tooHTTP richiesta** (nessuna App API obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="f2459-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="f2459-246">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="f2459-246">Get help</span></span>

<span data-ttu-id="f2459-247">rispondere alle domande di domande tooask, e informazioni su quali altri logica app di Azure in caso di utenti, visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="f2459-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="f2459-248">toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="f2459-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2459-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2459-249">Next steps</span></span>

* [<span data-ttu-id="f2459-250">Creare definizioni di app per la logica</span><span class="sxs-lookup"><span data-stu-id="f2459-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="f2459-251">Gestire errori ed eccezioni</span><span class="sxs-lookup"><span data-stu-id="f2459-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
