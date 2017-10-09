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
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="064f8-103">Creazione di metadati OpenAPI 2.0 (Swagger) per un'app per le funzioni (anteprima)</span><span class="sxs-lookup"><span data-stu-id="064f8-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="064f8-104">In questo documento viene hello passaggio da procedura di creazione di una definizione di OpenAPI per una semplice API ospitata in funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="064f8-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="064f8-105">Definizione di OpenAPI (Swagger)</span><span class="sxs-lookup"><span data-stu-id="064f8-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="064f8-106">[I metadati di swagger](http://swagger.io/) è un file che definisce la funzionalità di hello operative dell'API e consente a una funzione che ospita un toobe API REST utilizzato da un'ampia gamma di altri software.</span><span class="sxs-lookup"><span data-stu-id="064f8-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="064f8-107">Offerte Microsoft quali PowerApps e [App per le API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), nonché 3rd party strumenti per sviluppatori come [Postman](https://www.getpostman.com/docs/importing_swagger) e [molti altri pacchetti](http://swagger.io/tools/) tutte consentono toobe l'API utilizzata con un Definizione swagger.</span><span class="sxs-lookup"><span data-stu-id="064f8-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="064f8-108"><a name="prepare-function"></a>Creazione di una funzione con una API semplice</span><span class="sxs-lookup"><span data-stu-id="064f8-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="064f8-109">una definizione di OpenAPI toocreate, è necessario innanzitutto toocreate una funzione con una semplice API.</span><span class="sxs-lookup"><span data-stu-id="064f8-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="064f8-110">Se si dispone già di un'API ospitata in un'App di funzione, è possibile ignorare la sezione successiva toohello retta</span><span class="sxs-lookup"><span data-stu-id="064f8-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="064f8-111">Creare una nuova app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="064f8-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="064f8-112">[Portale di Azure](https://portal.azure.com) > `+ New` &gt; Eseguire una ricerca per "App per le funzioni"</span><span class="sxs-lookup"><span data-stu-id="064f8-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="064f8-113">Creare una nuova funzione trigger HTTP all'interno della nuova app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="064f8-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="064f8-114">La funzione è già popolata con codice che definisce un'API REST semplice.</span><span class="sxs-lookup"><span data-stu-id="064f8-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="064f8-115">Qualsiasi stringa passata toohello funzione come un parametro di query o nel corpo di hello viene restituito come "Hello {input}"</span><span class="sxs-lookup"><span data-stu-id="064f8-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="064f8-116">Passare toohello `Integrate` scheda della nuova funzione HTTP Trigger</span><span class="sxs-lookup"><span data-stu-id="064f8-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="064f8-117">Attiva/disattiva `Allowed HTTP methods` troppo`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="064f8-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="064f8-118">In `Selected HTTP methods` deselezionare ogni verbo tranne POST.</span><span class="sxs-lookup"><span data-stu-id="064f8-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="064f8-119">![Metodi HTTP selezionati](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="064f8-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="064f8-120">Questo passaggio semplifica la definizione dell'API in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="064f8-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="064f8-121"><a name="enable"></a>Abilitazione del supporto per la definizione API</span><span class="sxs-lookup"><span data-stu-id="064f8-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="064f8-122">Passare troppo`your function name` > `Platform Features` > `API Definition`
![scheda definizione](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="064f8-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="064f8-123">Impostare `API Definition Source` troppo`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="064f8-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="064f8-124">Questo passaggio consente a un gruppo di opzioni OpenAPI per l'applicazione di funzione, incluso un toohost endpoint file OpenAPI dal dominio dell'applicazione (funzione), una copia di inline di hello [OpenAPI Editor](http://editor.swagger.io)e un generatore di definizione della Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="064f8-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="064f8-125">![Definizioni attivate](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="064f8-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="064f8-126"><a name="create-definition"></a>Creazione della definizione dell'API da un modello</span><span class="sxs-lookup"><span data-stu-id="064f8-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="064f8-127">Fare clic su`Generate API Definition template`.</span><span class="sxs-lookup"><span data-stu-id="064f8-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="064f8-128">Questo passaggio esegue l'analisi dell'App di funzione per funzioni HTTP Trigger e utilizza informazioni di hello in functions.json toogenerate un documento OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="064f8-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="064f8-129">Aggiungere un oggetto operazione troppo`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="064f8-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="064f8-130">documento OpenAPI Guida introduttiva di Hello è una struttura di un documento OpenAPI completo. Richiede ulteriori metadati toobe una definizione di OpenAPI completa, ad esempio oggetti operazione e i modelli di risposta.</span><span class="sxs-lookup"><span data-stu-id="064f8-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="064f8-131">oggetto operazione Hello esempio riportato di seguito è un riempimento produce o utilizza sezione, un oggetto parametro e un oggetto di risposta.</span><span class="sxs-lookup"><span data-stu-id="064f8-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
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
    >  <span data-ttu-id="064f8-132">x-ms-summary indica il nome visualizzato in App per la logica, Flow e PowerApps.</span><span class="sxs-lookup"><span data-stu-id="064f8-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="064f8-133">Estrarre [personalizzare la definizione Swagger per PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="064f8-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="064f8-134">Fare clic su `save` toosave le modifiche ![aggiunta di definizione del modello](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="064f8-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="064f8-135"><a name="use-definition"></a>Utilizzo della definizione dell'API</span><span class="sxs-lookup"><span data-stu-id="064f8-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="064f8-136">Copia il `API definition URL` e incollarlo in un nuovo tooview scheda browser documento OpenAPI non elaborato.</span><span class="sxs-lookup"><span data-stu-id="064f8-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="064f8-137">È possibile importare il numero di tooany OpenAPI documento degli strumenti per test e integrazione con tale URL.</span><span class="sxs-lookup"><span data-stu-id="064f8-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="064f8-138">Molte risorse di Azure sono in grado di tooautomatically importazione del documento OpenAPI utilizzando hello URL di definizione dell'API che viene salvato nelle impostazioni dell'applicazione di funzione.</span><span class="sxs-lookup"><span data-stu-id="064f8-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="064f8-139">Come parte di hello `Function` origine definizione API, è aggiornare tale url per l'utente.</span><span class="sxs-lookup"><span data-stu-id="064f8-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="064f8-140"><a name="test-definition"></a>Utilizzando la definizione dell'API di hello Swagger dell'interfaccia utente tootest</span><span class="sxs-lookup"><span data-stu-id="064f8-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="064f8-141">Vi sono compilati in toohello di visualizzazione dell'interfaccia utente dell'editor di definizione API hello incorporato strumenti di test.</span><span class="sxs-lookup"><span data-stu-id="064f8-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="064f8-142">Aggiungere la chiave API e quindi usare hello `Try this operation` pulsante sotto ciascun metodo.</span><span class="sxs-lookup"><span data-stu-id="064f8-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="064f8-143">lo strumento di Hello utilizzerà le richieste di definizione dell'API tooformat hello e risposte ha esito positivo indica che la definizione sia corretta.</span><span class="sxs-lookup"><span data-stu-id="064f8-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="064f8-144">Passaggi:</span><span class="sxs-lookup"><span data-stu-id="064f8-144">Steps:</span></span>

1. <span data-ttu-id="064f8-145">Copiare la chiave API della funzione</span><span class="sxs-lookup"><span data-stu-id="064f8-145">Copy your function API key</span></span>
    1. <span data-ttu-id="064f8-146">chiave API Hello è reperibile nella funzione Trigger HTTP in `function name` > `Keys` > `Function Keys` 
   ![chiave (funzione)](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="064f8-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="064f8-147">Passare toohello `API Definition` pagina.</span><span class="sxs-lookup"><span data-stu-id="064f8-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="064f8-148">Fare clic su `Authenticate` e aggiungere l'oggetto di sicurezza toohello chiave API di funzione nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="064f8-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="064f8-149">![Chiave OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="064f8-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="064f8-150">Selezionare `/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="064f8-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="064f8-151">Fare clic su `Try it out` e immettere un nome tootest</span><span class="sxs-lookup"><span data-stu-id="064f8-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="064f8-152">Nel 
 ![test di definizione dell'API](./media/functions-api-definition-getting-started/definitionTest.png) di `Pretty` verrà visualizzato l'esito positivo</span><span class="sxs-lookup"><span data-stu-id="064f8-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="064f8-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="064f8-153">Next steps</span></span>
* [<span data-ttu-id="064f8-154">Definizione di OpenAPI in Panoramica di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="064f8-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="064f8-155">Leggere la documentazione completa di hello per altre informazioni sul supporto OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="064f8-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="064f8-156">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="064f8-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="064f8-157">Informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="064f8-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="064f8-158">Repository GitHub di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="064f8-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="064f8-159">Estrarre toogive GitHub funzioni hello ci commenti e suggerimenti sull'anteprima del supporto definizione API hello!</span><span class="sxs-lookup"><span data-stu-id="064f8-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="064f8-160">Crea un problema di GitHub per qualsiasi toosee aggiornato.</span><span class="sxs-lookup"><span data-stu-id="064f8-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
