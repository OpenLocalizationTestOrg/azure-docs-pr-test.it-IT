---
title: Introduzione ai metadati OpenAPI in Funzioni di Azure | Microsoft Docs
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
ms.openlocfilehash: 9b861aacf31e17866293732dc2323f56014c1877
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="d52b9-103">Creazione di metadati OpenAPI 2.0 (Swagger) per un'app per le funzioni (anteprima)</span><span class="sxs-lookup"><span data-stu-id="d52b9-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="d52b9-104">Questo documento contiene la procedura dettagliata per la creazione di una definizione OpenAPI per una semplice API ospitata in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="d52b9-104">This document guides you through the step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="d52b9-105">Definizione di OpenAPI (Swagger)</span><span class="sxs-lookup"><span data-stu-id="d52b9-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="d52b9-106">[Swagger Metadata](http://swagger.io/) è un file che definisce le funzionalità e le modalità di funzionamento dell'API e consente a una funzione che ospita un'API REST di essere usata con un'ampia gamma di altri prodotti software.</span><span class="sxs-lookup"><span data-stu-id="d52b9-106">[Swagger Metadata](http://swagger.io/) is a file that defines the functionality and operating modes of your API, and allows a function hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="d52b9-107">Offerte Microsoft quali PowerApps e [App per le API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), nonché strumenti di sviluppatori di terze parti come [Postman](https://www.getpostman.com/docs/importing_swagger) e [altri pacchetti](http://swagger.io/tools/) consentono di usare l'API con una definizione Swagger.</span><span class="sxs-lookup"><span data-stu-id="d52b9-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API to be consumed with a Swagger definition.</span></span>

## <span data-ttu-id="d52b9-108"><a name="prepare-function"></a>Creazione di una funzione con una API semplice</span><span class="sxs-lookup"><span data-stu-id="d52b9-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="d52b9-109">Per creare una definizione OpenAPI, è innanzitutto necessario creare una funzione con un'API semplice.</span><span class="sxs-lookup"><span data-stu-id="d52b9-109">To create an OpenAPI definition, we first need to create a Function with a simple API.</span></span> <span data-ttu-id="d52b9-110">Se si dispone già di un'API ospitata in un'app per le funzioni, è possibile passare direttamente alla sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="d52b9-110">If you already have an API hosted on a Function App, you can skip straight to the next section</span></span>
1. <span data-ttu-id="d52b9-111">Creare una nuova app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d52b9-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="d52b9-112">[Portale di Azure](https://portal.azure.com)  >  `+ New` > Eseguire una ricerca per "App per le funzioni"</span><span class="sxs-lookup"><span data-stu-id="d52b9-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="d52b9-113">Creare una nuova funzione trigger HTTP all'interno della nuova app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="d52b9-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="d52b9-114">La funzione è già popolata con codice che definisce un'API REST semplice.</span><span class="sxs-lookup"><span data-stu-id="d52b9-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="d52b9-115">Ogni stringa passata alla funzione come parametro di query o nel corpo viene restituita come "Hello {input}"</span><span class="sxs-lookup"><span data-stu-id="d52b9-115">Any string passed to the Function as a query parameter or in the body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="d52b9-116">Passare alla scheda `Integrate` della nuova funzione trigger HTTP</span><span class="sxs-lookup"><span data-stu-id="d52b9-116">Go to the `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="d52b9-117">Attivare/disattivare `Allowed HTTP methods` su `Selected methods`</span><span class="sxs-lookup"><span data-stu-id="d52b9-117">Toggle `Allowed HTTP methods` to `Selected methods`</span></span>
    1. <span data-ttu-id="d52b9-118">In `Selected HTTP methods` deselezionare ogni verbo tranne POST.</span><span class="sxs-lookup"><span data-stu-id="d52b9-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="d52b9-119">![Metodi HTTP selezionati](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="d52b9-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="d52b9-120">Questo passaggio semplifica la definizione dell'API in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d52b9-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="d52b9-121"><a name="enable"></a>Abilitazione del supporto per la definizione API</span><span class="sxs-lookup"><span data-stu-id="d52b9-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="d52b9-122">Passare a `your function name`  >  `Platform Features`  >  `API Definition` 
 ![scheda definizione](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="d52b9-122">Navigate to `your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="d52b9-123">Impostare `API Definition Source` su `Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="d52b9-123">Set `API Definition Source` to `Function (preview)`</span></span>
    1. <span data-ttu-id="d52b9-124">Questo passaggio consente a una suite di opzioni di OpenAPI per l'app per le funzioni, incluso un endpoint, di ospitare un file OpenAPI dal dominio dell'app, una copia inline dell'[editor di OpenAPI](http://editor.swagger.io)e un generatore di definizioni di avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="d52b9-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint to host an OpenAPI file from your Function App's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="d52b9-125">![Definizioni attivate](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="d52b9-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="d52b9-126"><a name="create-definition"></a>Creazione della definizione dell'API da un modello</span><span class="sxs-lookup"><span data-stu-id="d52b9-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="d52b9-127">Fare clic su`Generate API Definition template`.</span><span class="sxs-lookup"><span data-stu-id="d52b9-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="d52b9-128">Questo passaggio esegue la scansione dell'app per le funzioni per le funzioni HTTP trigger e usa le informazioni contenute in functions.json per generare un documento OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="d52b9-128">This step scans your Function App for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI document.</span></span>
1. <span data-ttu-id="d52b9-129">Aggiungere un oggetto operation a `paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="d52b9-129">Add an operation object to `paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="d52b9-130">Il documento OpenAPI di avvio rapido è una struttura di un documento OpenAPI completo. Sono tuttavia necessari altri metadati affinché si tratti di una definizione OpenAPI completa, ad esempio oggetti operazione e modelli di risposta.</span><span class="sxs-lookup"><span data-stu-id="d52b9-130">The quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata to be a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="d52b9-131">L'oggetto operazione di esempio include una sezione produce/usa, un oggetto parametro e un oggetto risposta.</span><span class="sxs-lookup"><span data-stu-id="d52b9-131">The sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
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
    >  <span data-ttu-id="d52b9-132">x-ms-summary indica il nome visualizzato in App per la logica, Flow e PowerApps.</span><span class="sxs-lookup"><span data-stu-id="d52b9-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="d52b9-133">Per altre informazioni, leggere [Personalizzare la definizione Swagger per PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).</span><span class="sxs-lookup"><span data-stu-id="d52b9-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span></span>

1. <span data-ttu-id="d52b9-134">Fare clic su `save` per salvare le modifiche ![Aggiunta di definizioni del modello](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="d52b9-134">Click `save` to save your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="d52b9-135"><a name="use-definition"></a>Utilizzo della definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="d52b9-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="d52b9-136">Copiare l'`API definition URL` e incollarlo in una nuova scheda del browser per visualizzare il documento OpenAPI non elaborato.</span><span class="sxs-lookup"><span data-stu-id="d52b9-136">Copy your `API definition URL` and paste it into a new browser tab to view your raw OpenAPI document.</span></span>
1. <span data-ttu-id="d52b9-137">Tale URL consente di importare il documento OpenAPI in qualsiasi strumento per finalità di test e integrazione.</span><span class="sxs-lookup"><span data-stu-id="d52b9-137">You can import your OpenAPI document to any number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="d52b9-138">Molte risorse di Azure sono in grado di importare automaticamente il documento OpenAPI usando l'URL di definizione API salvato nelle impostazioni dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d52b9-138">Many Azure resources are able to automatically import your OpenAPI doc using the API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="d52b9-139">Nel codice sorgente della definizione API `Function`, tale URL è già stato aggiornato.</span><span class="sxs-lookup"><span data-stu-id="d52b9-139">As a part of the `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="d52b9-140"><a name="test-definition"></a>Usare l'interfaccia utente di Swagger per testare la definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="d52b9-140"><a name="test-definition"></a>Using the Swagger UI to test your API definition</span></span>
<span data-ttu-id="d52b9-141">Esistono strumenti di test integrati nell'interfaccia utente dell'editor della definizione API.</span><span class="sxs-lookup"><span data-stu-id="d52b9-141">There are testing tools built in to the UI view of the imbedded API definition editor.</span></span> <span data-ttu-id="d52b9-142">Aggiungere la chiave API e quindi usare il pulsante `Try this operation` in ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="d52b9-142">Add your API key, and then use the `Try this operation` button under each method.</span></span> <span data-ttu-id="d52b9-143">Lo strumento usa la definizione API per formattare le richieste; se le risposte conseguenti hanno esito positivo, la definizione è corretta.</span><span class="sxs-lookup"><span data-stu-id="d52b9-143">The tool will use your API Definition to format the requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="d52b9-144">Passaggi:</span><span class="sxs-lookup"><span data-stu-id="d52b9-144">Steps:</span></span>

1. <span data-ttu-id="d52b9-145">Copiare la chiave API della funzione</span><span class="sxs-lookup"><span data-stu-id="d52b9-145">Copy your function API key</span></span>
    1. <span data-ttu-id="d52b9-146">La chiave API, vedere la funzione di attivazione HTTP in `function name` > `Keys` > `Function Keys` 
   ![chiave (funzione)](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="d52b9-146">The API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="d52b9-147">Passare alla pagina `API Definition`.</span><span class="sxs-lookup"><span data-stu-id="d52b9-147">Navigate to the `API Definition` page.</span></span>
    1. <span data-ttu-id="d52b9-148">Fare clic su `Authenticate` e aggiungere la chiave API della funzione all'oggetto security, nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="d52b9-148">Click `Authenticate` and add your Function API key to the security object at the top.</span></span>
  <span data-ttu-id="d52b9-149">![Chiave OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="d52b9-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="d52b9-150">Selezionare `/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="d52b9-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="d52b9-151">Fare clic su `Try it out` e immettere un nome per il test</span><span class="sxs-lookup"><span data-stu-id="d52b9-151">Click `Try it out` and enter a name to test</span></span>
1. <span data-ttu-id="d52b9-152">Nel 
 ![test di definizione dell'API](./media/functions-api-definition-getting-started/definitionTest.png) di `Pretty` verrà visualizzato l'esito positivo</span><span class="sxs-lookup"><span data-stu-id="d52b9-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d52b9-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d52b9-153">Next steps</span></span>
* [<span data-ttu-id="d52b9-154">Definizione di OpenAPI in Panoramica di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d52b9-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="d52b9-155">Leggere la documentazione completa per altre informazioni sul supporto per OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="d52b9-155">Read the full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="d52b9-156">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d52b9-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="d52b9-157">Informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="d52b9-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="d52b9-158">Repository GitHub di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d52b9-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="d52b9-159">In GitHub di Funzioni di Azure è possibile inviare commenti e suggerimenti relativi all'anteprima del supporto della definizione API.</span><span class="sxs-lookup"><span data-stu-id="d52b9-159">Check out the Functions GitHub to give us feedback on the API definition support preview!</span></span> <span data-ttu-id="d52b9-160">La pagina consente inoltre di inviare suggerimenti su eventuali elementi che si vuole vedere aggiornati.</span><span class="sxs-lookup"><span data-stu-id="d52b9-160">Make a GitHub issue for anything you'd like to see updated.</span></span>
