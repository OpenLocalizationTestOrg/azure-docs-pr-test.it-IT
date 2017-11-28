---
title: Chiamare, attivare o annidare i flussi di lavoro con endpoint HTTP - App per la logica di Azure | Microsoft Docs
description: Configurare endpoint HTTP per chiamare, attivare o annidare flussi di lavoro di app per la logica di Azure
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
ms.openlocfilehash: c92692db23ac59f67890e26cce6b2d3272e8901d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="a44a6-104">Chiamare, attivare o annidare i flussi di lavoro con endpoint HTTP in app per la logica</span><span class="sxs-lookup"><span data-stu-id="a44a6-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="a44a6-105">È possibile esporre a livello nativo gli endpoint HTTP sincroni come trigger sulle app per la logica, permettendo in tal modo di attivare o di chiamare le app per la logica tramite un URL.</span><span class="sxs-lookup"><span data-stu-id="a44a6-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="a44a6-106">È inoltre possibile annidare i flussi di lavoro nell'app per la logica usando un modello di endpoint richiamabile.</span><span class="sxs-lookup"><span data-stu-id="a44a6-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="a44a6-107">Per creare gli endpoint HTTP, è possibile aggiungere questi trigger in modo che le app per la logica possano ricevere le richieste in ingresso:</span><span class="sxs-lookup"><span data-stu-id="a44a6-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="a44a6-108">Richiesta</span><span class="sxs-lookup"><span data-stu-id="a44a6-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="a44a6-109">Webhook di connessione API</span><span class="sxs-lookup"><span data-stu-id="a44a6-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="a44a6-110">Webhook HTTP</span><span class="sxs-lookup"><span data-stu-id="a44a6-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="a44a6-111">Sebbene gli esempi usino il trigger **Richiesta** è possibile usare uno dei trigger HTTP elencati e tutti i principi si applicano in modo identico agli altri tipi di trigger.</span><span class="sxs-lookup"><span data-stu-id="a44a6-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="a44a6-112">Configurare un endpoint HTTP per un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="a44a6-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="a44a6-113">Per creare un endpoint HTTP, aggiungere un trigger in grado di ricevere le richieste in ingresso.</span><span class="sxs-lookup"><span data-stu-id="a44a6-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="a44a6-114">Accedere al [Portale di Azure](https://portal.azure.com "Portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="a44a6-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="a44a6-115">Andare in app per la logica e aprire Progettazione app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a44a6-115">Go to your logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="a44a6-116">Aggiungere un trigger che consente all'app per la logica di ricevere richieste in ingresso.</span><span class="sxs-lookup"><span data-stu-id="a44a6-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="a44a6-117">Ad esempio aggiungere il trigger **Request** all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a44a6-117">For example, add the **Request** trigger to your logic app.</span></span>

3.  <span data-ttu-id="a44a6-118">In **Schema JSON del corpo della richiesta** è possibile immettere uno schema JSON per il payload (dati) che si prevede il trigger possa ricevere.</span><span class="sxs-lookup"><span data-stu-id="a44a6-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span></span>

    <span data-ttu-id="a44a6-119">La finestra di progettazione usa questo schema per generare token di cui l'app per la logica si può servire per usare, analizzare e passare dati dal trigger attraverso il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a44a6-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span></span> 
    <span data-ttu-id="a44a6-120">Altre informazioni sui [token generati da schemi JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="a44a6-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="a44a6-121">In questo esempio, immettere lo schema indicato nella finestra di progettazione:</span><span class="sxs-lookup"><span data-stu-id="a44a6-121">For this example, enter the schema shown in the designer:</span></span>

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

    ![Aggiungere l'azione Request][1]

    > [!TIP]
    > 
    > <span data-ttu-id="a44a6-123">È possibile generare uno schema per un payload JSON di esempio da uno strumento come [jsonschema.net](http://jsonschema.net/), o nel trigger **Richiesta** scegliendo **Usare il payload di esempio per generare lo schema**.</span><span class="sxs-lookup"><span data-stu-id="a44a6-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span></span> 
    > <span data-ttu-id="a44a6-124">Immettere il payload di esempio e scegliere **Fine**.</span><span class="sxs-lookup"><span data-stu-id="a44a6-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="a44a6-125">Ad esempio, questo payload di esempio:</span><span class="sxs-lookup"><span data-stu-id="a44a6-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="a44a6-126">genera questo schema:</span><span class="sxs-lookup"><span data-stu-id="a44a6-126">generates this schema:</span></span>

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

4.  <span data-ttu-id="a44a6-127">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a44a6-127">Save your logic app.</span></span> <span data-ttu-id="a44a6-128">In **HTTP POST in questo URL**, è necessario individuare un URL di callback generato, come in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="a44a6-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span></span>

    ![URL di callback generato per endpoint](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="a44a6-130">L'URL contiene una chiave di firma di accesso condiviso (SAS) nei parametri di query usati per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a44a6-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="a44a6-131">È inoltre possibile ottenere l'URL dell'endpoint HTTP dalla panoramica dell'app per la logica nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a44a6-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span></span> <span data-ttu-id="a44a6-132">In **Cronologia trigger** selezionare il trigger:</span><span class="sxs-lookup"><span data-stu-id="a44a6-132">Under **Trigger History**, select your trigger:</span></span>

    ![Ottenere l'URL dell'endpoint HTTP GET dal portale di Azure][2]

    <span data-ttu-id="a44a6-134">Oppure è possibile ottenere l'URL mediante questa chiamata:</span><span class="sxs-lookup"><span data-stu-id="a44a6-134">Or you can get the URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-the-http-method-for-your-trigger"></a><span data-ttu-id="a44a6-135">Modificare il metodo HTTP per il trigger</span><span class="sxs-lookup"><span data-stu-id="a44a6-135">Change the HTTP method for your trigger</span></span>

<span data-ttu-id="a44a6-136">Per impostazione predefinita, il trigger **Richiesta** prevede una richiesta HTTP POST, ma è possibile usare un metodo HTTP diverso.</span><span class="sxs-lookup"><span data-stu-id="a44a6-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="a44a6-137">È possibile specificare solo un tipo di metodo.</span><span class="sxs-lookup"><span data-stu-id="a44a6-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="a44a6-138">Nel trigger **Richiesta** scegliere **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="a44a6-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="a44a6-139">Aprire l'elenco **Metodo**.</span><span class="sxs-lookup"><span data-stu-id="a44a6-139">Open the **Method** list.</span></span> <span data-ttu-id="a44a6-140">Per questo esempio, selezionare **GET** (OTTIENI) in modo che sia possibile testare l'URL dell'endpoint HTTP in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="a44a6-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a44a6-141">È possibile selezionare qualsiasi altro metodo HTTP o specificare un metodo personalizzato per la propria app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a44a6-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Modificare il metodo HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="a44a6-143">Accettare i parametri tramite l'URL dell'endpoint HTTP</span><span class="sxs-lookup"><span data-stu-id="a44a6-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="a44a6-144">Quando si desidera che l'URL dell'endpoint HTTP accetti i parametri, personalizzare il percorso relativo al trigger.</span><span class="sxs-lookup"><span data-stu-id="a44a6-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="a44a6-145">Nel trigger **Richiesta** scegliere **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="a44a6-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="a44a6-146">In **Metodo** specificare il metodo HTTP che la richiesta deve usare.</span><span class="sxs-lookup"><span data-stu-id="a44a6-146">Under **Method**, specify the HTTP method that you want your request to use.</span></span> <span data-ttu-id="a44a6-147">Per questo esempio, selezionare il metodo **GET** (OTTIENI), se non lo si è già fatto, in modo che sia possibile testare l'URL dell'endpoint HTTP.</span><span class="sxs-lookup"><span data-stu-id="a44a6-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="a44a6-148">Quando si specifica un percorso relativo per il trigger, è necessario specificare anche in modo esplicito un metodo HTTP per il trigger.</span><span class="sxs-lookup"><span data-stu-id="a44a6-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="a44a6-149">In **Percorso relativo** specificare il percorso relativo per il parametro che l'URL deve accettare, ad esempio, `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="a44a6-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Specificare il percorso relativo e il metodo HTTP per il parametro](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="a44a6-151">Per usare il parametro, aggiungere un'azione **Risposta** all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a44a6-151">To use the parameter, add a **Response** action to your logic app.</span></span> <span data-ttu-id="a44a6-152">(Nel trigger scegliere **Nuovo passaggio** > **Aggiungi un'azione** > **Risposta**)</span><span class="sxs-lookup"><span data-stu-id="a44a6-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="a44a6-153">Nel **corpo** della risposta includere il token per il parametro specificato nel percorso relativo del trigger.</span><span class="sxs-lookup"><span data-stu-id="a44a6-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="a44a6-154">Ad esempio, per restituire `Hello {customerID}`, aggiornare il **corpo** della risposta con `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="a44a6-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="a44a6-155">Elenco del contenuto dinamico dovrà essere visualizzato e Mostra il `customerID` token per la selezione.</span><span class="sxs-lookup"><span data-stu-id="a44a6-155">The dynamic content list should appear and show the `customerID` token for you to select.</span></span>

    ![Aggiungere un parametro al corpo della risposta](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="a44a6-157">Il **corpo** dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a44a6-157">Your **Body** should look like this example:</span></span>

    ![Corpo della risposta con parametri](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="a44a6-159">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a44a6-159">Save your logic app.</span></span> 

    <span data-ttu-id="a44a6-160">L'URL dell'endpoint HTTP include ora il percorso relativo, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a44a6-160">Your HTTP endpoint URL now includes the relative path, for example:</span></span> 

    <span data-ttu-id="a44a6-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="a44a6-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="a44a6-162">Per testare l'endpoint HTTP, copiare e incollare l'URL aggiornato in un'altra finestra del browser, ma sostituire `{customerID}` con `123456` e premere Invio.</span><span class="sxs-lookup"><span data-stu-id="a44a6-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="a44a6-163">Il browser deve mostrare questo testo:</span><span class="sxs-lookup"><span data-stu-id="a44a6-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="a44a6-164">Token generati da schemi JSON per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="a44a6-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="a44a6-165">Quando si specifica uno schema JSON nel trigger **Richiesta**, la finestra di progettazione app per la logica genera i token per le proprietà nello schema.</span><span class="sxs-lookup"><span data-stu-id="a44a6-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="a44a6-166">È quindi possibile usare tali token per passare dati tramite il flusso di lavoro di app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a44a6-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="a44a6-167">Per questo esempio, se si aggiungono le proprietà `title` e `name` allo schema JSON, i token sono ora disponibili per essere usati nei passaggi successivi del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a44a6-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span></span> 

<span data-ttu-id="a44a6-168">Di seguito è riportato lo schema JSON completo:</span><span class="sxs-lookup"><span data-stu-id="a44a6-168">Here is the complete JSON schema:</span></span>

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

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="a44a6-169">Creare flussi di lavoro annidati per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="a44a6-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="a44a6-170">È possibile nidificare i flussi di lavoro nell'app per la logica aggiungendo altre app per la logica che possono ricevere richieste.</span><span class="sxs-lookup"><span data-stu-id="a44a6-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="a44a6-171">Per includere queste app per la logica, aggiungere l'azione **Azure Logic Apps - Choose a Logic Apps workflow** (App per la logica di Azure - Scegliere un flusso di lavoro delle app per la logica) al trigger.</span><span class="sxs-lookup"><span data-stu-id="a44a6-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span></span> <span data-ttu-id="a44a6-172">È quindi possibile selezionare dalle app per la logica idonee.</span><span class="sxs-lookup"><span data-stu-id="a44a6-172">You can then select from eligible logic apps.</span></span>

![Aggiungere un'altra app per la logica](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="a44a6-174">Chiamare o avviare le app per la logica tramite endpoint HTTP</span><span class="sxs-lookup"><span data-stu-id="a44a6-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="a44a6-175">Dopo aver creato l'endpoint HTTP, è possibile attivare l'app per la logica tramite un metodo `POST` per l'URL completo.</span><span class="sxs-lookup"><span data-stu-id="a44a6-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span></span> <span data-ttu-id="a44a6-176">Le app per la logica dispongono di supporto incorporato per gli endpoint di accesso diretto.</span><span class="sxs-lookup"><span data-stu-id="a44a6-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="a44a6-177">Riferimento al contenuto dalla richiesta in ingresso</span><span class="sxs-lookup"><span data-stu-id="a44a6-177">Reference content from an incoming request</span></span>

<span data-ttu-id="a44a6-178">Se il tipo di contenuto è `application/json`, è possibile fare riferimento a proprietà dalla richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="a44a6-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span></span> <span data-ttu-id="a44a6-179">In caso contrario, il contenuto viene considerato come una singola unità binaria che è possibile passare ad altre API.</span><span class="sxs-lookup"><span data-stu-id="a44a6-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span></span> <span data-ttu-id="a44a6-180">Per fare riferimento a questo contenuto all'interno del flusso di lavoro è necessario convertire il contenuto.</span><span class="sxs-lookup"><span data-stu-id="a44a6-180">To reference this content inside the workflow, you must convert that content.</span></span> <span data-ttu-id="a44a6-181">Se ad esempio si passa il contenuto `application/xml`, è possibile usare `@xpath()` per eseguire un'estrazione XPath o `@json()` per la conversione da XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="a44a6-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span></span> <span data-ttu-id="a44a6-182">Informazioni sull'[uso dei tipi di contenuto](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="a44a6-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="a44a6-183">Per ottenere l'output da una richiesta in ingresso, è possibile usare la funzione `@triggerOutputs()`.</span><span class="sxs-lookup"><span data-stu-id="a44a6-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span></span> <span data-ttu-id="a44a6-184">L'output potrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a44a6-184">The output might look like this example:</span></span>

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

<span data-ttu-id="a44a6-185">È possibile accedere in modo specifico alla proprietà `body` mediante il collegamento `@triggerBody()`.</span><span class="sxs-lookup"><span data-stu-id="a44a6-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span></span> 

## <a name="respond-to-requests"></a><span data-ttu-id="a44a6-186">Rispondere alle richieste</span><span class="sxs-lookup"><span data-stu-id="a44a6-186">Respond to requests</span></span>

<span data-ttu-id="a44a6-187">Per alcune richieste che avviano un'app per la logica, può risultare utile rispondere restituendo contenuto al chiamante.</span><span class="sxs-lookup"><span data-stu-id="a44a6-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span></span> <span data-ttu-id="a44a6-188">Per creare il codice di stato, l'intestazione e il corpo della risposta, è possibile usare l'azione **Risposta**.</span><span class="sxs-lookup"><span data-stu-id="a44a6-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span></span> <span data-ttu-id="a44a6-189">Questa azione può trovarsi in qualsiasi punto nell'app per la logica, non solo alla fine del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a44a6-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="a44a6-190">Se l'app per la logica non include una **Risposta**, l'endpoint HTTP risponde *immediatamente* con uno stato **202 -Accettato**.</span><span class="sxs-lookup"><span data-stu-id="a44a6-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="a44a6-191">Nell'app per la logica, per far sì che la richiesta originale ottenga la risposta, tutti i passaggi necessari devono essere completati entro i [limiti di tempo della richiesta](./logic-apps-limits-and-config.md), salvo se si chiama il flusso di lavoro come app per la logica annidata.</span><span class="sxs-lookup"><span data-stu-id="a44a6-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span></span> <span data-ttu-id="a44a6-192">Se non si ottiene alcuna azione di risposta entro questo limite, si verifica il timeout della richiesta in ingresso, che riceverà una risposta HTTP **408 Client timeout** (408 - Timeout client).</span><span class="sxs-lookup"><span data-stu-id="a44a6-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="a44a6-193">Per le app per la logica annidate, l'app per la logica padre resta in attesa di una risposta fino al completamento, indipendentemente dal tempo necessario.</span><span class="sxs-lookup"><span data-stu-id="a44a6-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-the-response"></a><span data-ttu-id="a44a6-194">Costruire la risposta</span><span class="sxs-lookup"><span data-stu-id="a44a6-194">Construct the response</span></span>

<span data-ttu-id="a44a6-195">È possibile includere più di un'intestazione e qualsiasi tipo di contenuto nel corpo della risposta.</span><span class="sxs-lookup"><span data-stu-id="a44a6-195">You can include more than one header and any type of content in the response body.</span></span> <span data-ttu-id="a44a6-196">Nel nostro esempio di risposta, l'intestazione specifica che la risposta contiene il tipo di contenuto `application/json`,</span><span class="sxs-lookup"><span data-stu-id="a44a6-196">In our example response, the header specifies that the response has content type `application/json`.</span></span> <span data-ttu-id="a44a6-197">mentre il corpo contiene `title` e `name`, in base allo schema JSON aggiornato in precedenza per il trigger **Richiesta**.</span><span class="sxs-lookup"><span data-stu-id="a44a6-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span></span>

![Azione di risposta HTTP][3]

<span data-ttu-id="a44a6-199">Le risposte hanno le seguenti proprietà:</span><span class="sxs-lookup"><span data-stu-id="a44a6-199">Responses have these properties:</span></span>

| <span data-ttu-id="a44a6-200">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a44a6-200">Property</span></span> | <span data-ttu-id="a44a6-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a44a6-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a44a6-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="a44a6-202">statusCode</span></span> |<span data-ttu-id="a44a6-203">Specifica il codice di stato HTTP per la risposta alla richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="a44a6-203">Specifies the HTTP status code for responding to the incoming request.</span></span> <span data-ttu-id="a44a6-204">Può essere qualsiasi codice di stato valido che inizia con 2xx, 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="a44a6-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="a44a6-205">I codici di stato 3xx non sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="a44a6-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="a44a6-206">headers</span><span class="sxs-lookup"><span data-stu-id="a44a6-206">headers</span></span> |<span data-ttu-id="a44a6-207">Definisce un numero illimitato di intestazioni da includere nella risposta.</span><span class="sxs-lookup"><span data-stu-id="a44a6-207">Defines any number of headers to include in the response.</span></span> |
| <span data-ttu-id="a44a6-208">body</span><span class="sxs-lookup"><span data-stu-id="a44a6-208">body</span></span> |<span data-ttu-id="a44a6-209">Specifica un oggetto body che può essere una stringa, un oggetto JSON o anche contenuto binario a cui si fa riferimento da un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="a44a6-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="a44a6-210">Di seguito viene riportato l'aspetto che lo schema JSON dovrebbe avere ora per l'azione **Risposta**:</span><span class="sxs-lookup"><span data-stu-id="a44a6-210">Here's what the JSON schema looks like now for the **Response** action:</span></span>

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
> <span data-ttu-id="a44a6-211">Per visualizzare la definizione JSON completa per l'app per la logica, nella finestra di progettazione dell'app per la logica, scegliere **Visualizzazione codice**.</span><span class="sxs-lookup"><span data-stu-id="a44a6-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="a44a6-212">Domande e risposte</span><span class="sxs-lookup"><span data-stu-id="a44a6-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="a44a6-213">D: Come viene garantita la sicurezza degli URL?</span><span class="sxs-lookup"><span data-stu-id="a44a6-213">Q: What about URL security?</span></span>

<span data-ttu-id="a44a6-214">R: Azure genera in modo sicuro gli URL di callback dell'app per la logica mediante una firma di accesso condiviso (SAS).</span><span class="sxs-lookup"><span data-stu-id="a44a6-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="a44a6-215">La firma viene trasmessa come parametro di query e deve essere convalidata prima dell'attivazione dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a44a6-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="a44a6-216">Azure genera la firma con una combinazione univoca che include la chiave privata per ogni app per la logica, il nome del trigger e l'operazione in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a44a6-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span></span> <span data-ttu-id="a44a6-217">Pertanto, a meno che un utente non ottenga l'accesso alla chiave privata dell'app per la logica, non potrà generare una firma valida.</span><span class="sxs-lookup"><span data-stu-id="a44a6-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a44a6-218">Per i sistemi di produzione e protezione, è consigliabile evitare la chiamata dell'app per la logica direttamente dal browser in quanto:</span><span class="sxs-lookup"><span data-stu-id="a44a6-218">For production and secure systems, we strongly recommend against calling your logic app directly from the browser because:</span></span>
   > 
   > * <span data-ttu-id="a44a6-219">La chiave di accesso condiviso viene visualizzata nell'URL.</span><span class="sxs-lookup"><span data-stu-id="a44a6-219">The shared access key appears in the URL.</span></span>
   > * <span data-ttu-id="a44a6-220">Non è possibile gestire i criteri di contenuto protetti a causa di domini condivisi tra i clienti di App per la logica.</span><span class="sxs-lookup"><span data-stu-id="a44a6-220">You can't manage secure content policies due to shared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="a44a6-221">D: È possibile configurare ulteriormente gli endpoint HTTP?</span><span class="sxs-lookup"><span data-stu-id="a44a6-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="a44a6-222">R: Sì, gli endpoint HTTP supportano configurazioni più avanzate tramite la [**Gestione API**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="a44a6-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="a44a6-223">Questo servizio offre inoltre la possibilità di gestire tutte le API in modo coerente, incluse le app per la logica, di impostare i nomi di dominio personalizzato, usare più metodi di autenticazione e altro ancora, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a44a6-223">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="a44a6-224">Impostare il metodo della richiesta</span><span class="sxs-lookup"><span data-stu-id="a44a6-224">Change the request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="a44a6-225">Modificare i segmenti dell'URL della richiesta</span><span class="sxs-lookup"><span data-stu-id="a44a6-225">Change the URL segments of the request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="a44a6-226">Configurare i domini di Gestione API nel [portale di Azure](https://portal.azure.com/ "portale di Azure")</span><span class="sxs-lookup"><span data-stu-id="a44a6-226">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="a44a6-227">Impostare la norma per verificare l'autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="a44a6-227">Set up policy to check for Basic authentication</span></span>

#### <a name="q-what-changed-when-the-schema-migrated-from-the-december-1-2014-preview"></a><span data-ttu-id="a44a6-228">D: Che cosa è cambiato con la migrazione dello schema dall'anteprima del 1 dicembre 2014?</span><span class="sxs-lookup"><span data-stu-id="a44a6-228">Q: What changed when the schema migrated from the December 1, 2014 preview?</span></span>

<span data-ttu-id="a44a6-229">R: Di seguito è riportato un riepilogo di queste modifiche:</span><span class="sxs-lookup"><span data-stu-id="a44a6-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="a44a6-230">Anteprima del 1 dicembre 2014</span><span class="sxs-lookup"><span data-stu-id="a44a6-230">December 1, 2014 preview</span></span> | <span data-ttu-id="a44a6-231">1 giugno 2016</span><span class="sxs-lookup"><span data-stu-id="a44a6-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="a44a6-232">Fare clic sull'app per le API **Listener HTTP**</span><span class="sxs-lookup"><span data-stu-id="a44a6-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="a44a6-233">Fare clic su **Attivazione manuale**. Non è necessaria un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="a44a6-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="a44a6-234">Impostazione di Listener HTTP "*Send response automatically*" (Invia risposta automaticamente)</span><span class="sxs-lookup"><span data-stu-id="a44a6-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="a44a6-235">Includere o meno un'azione **Risposta** nella definizione del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="a44a6-235">Either include a **Response** action or not in the workflow definition</span></span> |
| <span data-ttu-id="a44a6-236">Configurare l'autenticazione di base o OAuth</span><span class="sxs-lookup"><span data-stu-id="a44a6-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="a44a6-237">tramite Gestione API</span><span class="sxs-lookup"><span data-stu-id="a44a6-237">via API Management</span></span> |
| <span data-ttu-id="a44a6-238">Configurare il metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="a44a6-238">Configure HTTP method</span></span> |<span data-ttu-id="a44a6-239">In **Mostra opzioni avanzate** scegliere un metodo HTTP</span><span class="sxs-lookup"><span data-stu-id="a44a6-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="a44a6-240">Configurare il percorso relativo</span><span class="sxs-lookup"><span data-stu-id="a44a6-240">Configure relative path</span></span> |<span data-ttu-id="a44a6-241">In **Mostra opzioni avanzate** aggiungere un percorso relativo</span><span class="sxs-lookup"><span data-stu-id="a44a6-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="a44a6-242">Fare riferimento all'oggetto body in ingresso tramite `@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="a44a6-242">Reference the incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="a44a6-243">Fare riferimento tramite `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="a44a6-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="a44a6-244">**Send HTTP response** (Invia risposta HTTP) nel Listener HTTP</span><span class="sxs-lookup"><span data-stu-id="a44a6-244">**Send HTTP response** action on the HTTP Listener</span></span> |<span data-ttu-id="a44a6-245">Fare clic su **Respond to HTTP request** (Rispondi alla richiesta HTTP). Non è necessaria un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="a44a6-245">Click **Respond to HTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="a44a6-246">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="a44a6-246">Get help</span></span>

<span data-ttu-id="a44a6-247">Per porre domande, fornire risposte e ottenere informazioni sulle attività degli altri utenti di App per la logica di Azure, vedere il [forum su App per la logica di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="a44a6-247">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="a44a6-248">Per contribuire al miglioramento delle App per la logica di Azure e dei connettori, votare o inviare idee al [sito dei commenti e suggerimenti degli utenti di App per la logica di Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="a44a6-248">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a44a6-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a44a6-249">Next steps</span></span>

* [<span data-ttu-id="a44a6-250">Creare definizioni di app per la logica</span><span class="sxs-lookup"><span data-stu-id="a44a6-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="a44a6-251">Gestire errori ed eccezioni</span><span class="sxs-lookup"><span data-stu-id="a44a6-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
