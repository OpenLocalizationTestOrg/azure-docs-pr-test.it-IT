---
title: Funzioni di Azure aaaTesting | Documenti Microsoft
description: Testare Funzioni di Azure con Postman, cURL e Node.js.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: funzioni di azure, funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server, test
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="90517-104">Strategie per il test del codice in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="90517-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="90517-105">In questo argomento viene illustrato hello si avvicina a diverse funzioni tootest modi, incluso l'utilizzo di hello seguente generale:</span><span class="sxs-lookup"><span data-stu-id="90517-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="90517-106">Strumenti basati su HTTP, ad esempio cURL, Postman e persino un browser Web per i trigger basati sul Web</span><span class="sxs-lookup"><span data-stu-id="90517-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="90517-107">Azure Storage Explorer, i trigger di archiviazione di Azure basato su tootest</span><span class="sxs-lookup"><span data-stu-id="90517-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="90517-108">Scheda test nel portale di Azure funzioni hello</span><span class="sxs-lookup"><span data-stu-id="90517-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="90517-109">Funzione attivata tramite timer</span><span class="sxs-lookup"><span data-stu-id="90517-109">Timer-triggered function</span></span>
+ <span data-ttu-id="90517-110">Test dell'applicazione o del framework</span><span class="sxs-lookup"><span data-stu-id="90517-110">Testing application or framework</span></span>

<span data-ttu-id="90517-111">Tutti questi metodi di test utilizzare una funzione di attivazione HTTP che accetta l'input tramite una query stringa parametro o hello corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="90517-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="90517-112">Creare questa funzione nella prima sezione hello.</span><span class="sxs-lookup"><span data-stu-id="90517-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="90517-113">Creare una funzione per i test</span><span class="sxs-lookup"><span data-stu-id="90517-113">Create a function for testing</span></span>
<span data-ttu-id="90517-114">Per la maggior parte di questa esercitazione, si utilizza una versione leggermente modificata del modello di funzione HttpTrigger JavaScript è disponibile quando si crea una funzione hello.</span><span class="sxs-lookup"><span data-stu-id="90517-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="90517-115">Se occorre assistenza nella creazione di una funzione, rivedere questa [esercitazione](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="90517-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="90517-116">Scegliere hello **HttpTrigger - JavaScript** modello quando si crea la funzione di test hello in hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="90517-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="90517-117">Hello funzione modello predefinito è fondamentalmente una funzione di "hello world" che restituisce il nome di hello indietro dalla richiesta query o corpo stringa parametro hello, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="90517-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="90517-118">Verrà aggiornata codice hello tooalso consentono tooprovide hello nome e un indirizzo come contenuto JSON nel corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="90517-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="90517-119">Funzione hello restituisce quindi questi client toohello indietro quando disponibile.</span><span class="sxs-lookup"><span data-stu-id="90517-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="90517-120">Aggiornare la funzione hello hello seguente di codice, che verrà utilizzato per il test:</span><span class="sxs-lookup"><span data-stu-id="90517-120">Update hello function with hello following code, which we will use for testing:</span></span>

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="90517-121">Eseguire il test di una funzione con gli strumenti</span><span class="sxs-lookup"><span data-stu-id="90517-121">Test a function with tools</span></span>
<span data-ttu-id="90517-122">All'esterno di hello portale di Azure, sono disponibili diversi strumenti che è possibile utilizzare tootrigger delle funzioni per i test.</span><span class="sxs-lookup"><span data-stu-id="90517-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="90517-123">Questi includono gli strumenti di test HTTP (sia basati su interfaccia utente sia sulla riga di comando), strumenti di accesso all'Archiviazione di Azure e un semplice browser Web.</span><span class="sxs-lookup"><span data-stu-id="90517-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="90517-124">Eseguire il test con un browser</span><span class="sxs-lookup"><span data-stu-id="90517-124">Test with a browser</span></span>
<span data-ttu-id="90517-125">browser web Hello è funzioni di tootrigger un modo semplice tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="90517-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="90517-126">È possibile usare un browser per le richieste GET per cui non è necessario un payload del corpo e che usi solo i parametri di stringa della query.</span><span class="sxs-lookup"><span data-stu-id="90517-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="90517-127">funzione hello tootest definita in precedenza, hello copia **funzione Url** dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="90517-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="90517-128">Dispone di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="90517-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="90517-129">Aggiungere hello `name` stringa di query toohello del parametro.</span><span class="sxs-lookup"><span data-stu-id="90517-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="90517-130">Utilizzare un nome effettivo per hello `<Enter a name here>` segnaposto.</span><span class="sxs-lookup"><span data-stu-id="90517-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="90517-131">Incolla hello URL nel browser ed è necessario ottenere toohello seguito risposta simile.</span><span class="sxs-lookup"><span data-stu-id="90517-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![Schermata della scheda del browser Chrome con risposta del test](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="90517-133">Questo esempio è browser Chrome hello, che esegue il wrapping hello ha restituito una stringa in formato XML.</span><span class="sxs-lookup"><span data-stu-id="90517-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="90517-134">Altri browser di visualizzare solo il valore di stringa hello.</span><span class="sxs-lookup"><span data-stu-id="90517-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="90517-135">Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:</span><span class="sxs-lookup"><span data-stu-id="90517-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="90517-136">Eseguire il test con Postman</span><span class="sxs-lookup"><span data-stu-id="90517-136">Test with Postman</span></span>
<span data-ttu-id="90517-137">Hello consigliato strumento tootest la maggior parte delle funzioni è Postman, che si integra con browser Chrome hello.</span><span class="sxs-lookup"><span data-stu-id="90517-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="90517-138">tooinstall Postman, vedere [Postman ottenere](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="90517-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="90517-139">Postman consente di controllare molti più attributi di una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="90517-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="90517-140">Utilizzare hello HTTP strumento di test che si ha maggiore familiarità con.</span><span class="sxs-lookup"><span data-stu-id="90517-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="90517-141">Ecco alcuni tooPostman alternative:</span><span class="sxs-lookup"><span data-stu-id="90517-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="90517-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="90517-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="90517-143">Paw</span><span class="sxs-lookup"><span data-stu-id="90517-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="90517-144">funzione di hello tootest con un corpo della richiesta in Postman:</span><span class="sxs-lookup"><span data-stu-id="90517-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="90517-145">Avviare Postman da hello **app** pulsante nell'angolo superiore sinistro hello di una finestra del browser Chrome.</span><span class="sxs-lookup"><span data-stu-id="90517-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="90517-146">Copiare l'**URL funzione** e incollarlo in Postman.</span><span class="sxs-lookup"><span data-stu-id="90517-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="90517-147">Include un parametro di stringa di query di codice di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="90517-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="90517-148">Modificare anche il metodo HTTP hello**POST**.</span><span class="sxs-lookup"><span data-stu-id="90517-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="90517-149">Fare clic su **corpo** > **raw**e aggiungere un JSON richiesta seguente toohello simile corpo:</span><span class="sxs-lookup"><span data-stu-id="90517-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="90517-150">Fare clic su **Send**.</span><span class="sxs-lookup"><span data-stu-id="90517-150">Click **Send**.</span></span>

<span data-ttu-id="90517-151">Hello immagine seguente mostra test hello echo semplice funzione esempio in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="90517-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Schermata dell'interfaccia utente di Postman](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="90517-153">Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:</span><span class="sxs-lookup"><span data-stu-id="90517-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="90517-154">Eseguire il test con cURL dalla riga di comando hello</span><span class="sxs-lookup"><span data-stu-id="90517-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="90517-155">Spesso quando si esegue il test del software, non è necessario toolook qualsiasi superiore rispetto a quello hello riga di comando toohelp debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="90517-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="90517-156">L'approccio è analogo per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="90517-156">This is no different with testing functions.</span></span> <span data-ttu-id="90517-157">Si noti che cURL hello è disponibile per impostazione predefinita nei sistemi basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="90517-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="90517-158">In Windows, è innanzitutto necessario scaricare e installare hello [cURL strumento](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="90517-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="90517-159">funzione hello tootest che è stato definito in precedenza, hello copia **funzione URL** dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="90517-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="90517-160">Dispone di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="90517-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="90517-161">Questo è l'URL di hello per l'attivazione di una funzione.</span><span class="sxs-lookup"><span data-stu-id="90517-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="90517-162">Test tramite comando cURL hello in hello toomake di riga di comando, un'operazione GET (`-G` o `--get`) richiesta per la funzione hello:</span><span class="sxs-lookup"><span data-stu-id="90517-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="90517-163">Questo particolare esempio richiede un parametro di stringa di query, può essere passato come dati (`-d`) in hello cURL comando:</span><span class="sxs-lookup"><span data-stu-id="90517-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="90517-164">Comando di esecuzione hello e visualizzato dopo l'output della funzione hello nella riga di comando hello hello:</span><span class="sxs-lookup"><span data-stu-id="90517-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![Schermata dell'output del prompt dei comandi](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="90517-166">Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:</span><span class="sxs-lookup"><span data-stu-id="90517-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="90517-167">Eseguire il test di un trigger del BLOB con Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="90517-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="90517-168">È possibile testare una funzione trigger del BLOB con [Esplora archivi di Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="90517-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="90517-169">In hello [portale di Azure] per l'app di funzione, creare una funzione di attivazione di un blob di c#, F # o JavaScript.</span><span class="sxs-lookup"><span data-stu-id="90517-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="90517-170">Impostare hello toomonitor toohello percorso del contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="90517-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="90517-171">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="90517-171">For example:</span></span>

        files
2. <span data-ttu-id="90517-172">Fare clic su hello  **+**  pulsante tooselect o creare account di archiviazione hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="90517-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="90517-173">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="90517-173">Then click **Create**.</span></span>
3. <span data-ttu-id="90517-174">Creare un file di testo con hello segue testo e salvarlo:</span><span class="sxs-lookup"><span data-stu-id="90517-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="90517-175">Eseguire [Azure Storage Explorer](http://storageexplorer.com/)e connettere toohello contenitore di blob nell'account di archiviazione hello monitorato.</span><span class="sxs-lookup"><span data-stu-id="90517-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="90517-176">Fare clic su **caricare** file di testo hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="90517-176">Click **Upload** tooupload hello text file.</span></span>

    ![Screenshot di Esplora archivi](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="90517-178">codice di funzione trigger blob predefinito Hello segnala l'elaborazione di hello del blob hello nei registri hello:</span><span class="sxs-lookup"><span data-stu-id="90517-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="90517-179">Eseguire il test di una funzione all'interno di Funzioni</span><span class="sxs-lookup"><span data-stu-id="90517-179">Test a function within functions</span></span>
<span data-ttu-id="90517-180">Hello Azure funzioni portale è progettato toolet testi HTTP e timer attivato funzioni.</span><span class="sxs-lookup"><span data-stu-id="90517-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="90517-181">È anche possibile creare funzioni tootrigger altre funzioni che si siano testando.</span><span class="sxs-lookup"><span data-stu-id="90517-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="90517-182">Eseguire il test con il pulsante Esegui portale di hello funzioni</span><span class="sxs-lookup"><span data-stu-id="90517-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="90517-183">portale Hello fornisce un **eseguire** pulsante che è possibile utilizzare alcune toodo limitato di test.</span><span class="sxs-lookup"><span data-stu-id="90517-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="90517-184">È possibile fornire un corpo della richiesta utilizzando il pulsante di hello, ma non è possibile specificare i parametri di stringa di query o aggiornare le intestazioni di richiesta.</span><span class="sxs-lookup"><span data-stu-id="90517-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="90517-185">Testare hello HTTP trigger funzione creata in precedenza tramite l'aggiunta di un toohello simile stringa JSON seguente hello **corpo della richiesta** campo.</span><span class="sxs-lookup"><span data-stu-id="90517-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="90517-186">Quindi fare clic su hello **eseguire** pulsante.</span><span class="sxs-lookup"><span data-stu-id="90517-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="90517-187">Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:</span><span class="sxs-lookup"><span data-stu-id="90517-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="90517-188">Eseguire il test con un trigger del timer</span><span class="sxs-lookup"><span data-stu-id="90517-188">Test with a timer trigger</span></span>
<span data-ttu-id="90517-189">Non è possibile testare alcune funzioni in modo adeguato con gli strumenti di hello indicati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="90517-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="90517-190">Prendiamo ad esempio una funzione trigger della coda eseguita quando un messaggio viene inserito in [Archiviazione code di Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="90517-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="90517-191">È sempre possibile scrivere codice toodrop un messaggio in coda e viene fornito un esempio in un progetto console più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="90517-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="90517-192">Esiste tuttavia un altro approccio che può essere usato per eseguire direttamente il test delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="90517-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="90517-193">È possibile usare un trigger del timer configurato con un'associazione di output della coda.</span><span class="sxs-lookup"><span data-stu-id="90517-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="90517-194">Il codice del trigger timer è quindi possibile scrivere coda toohello i messaggi di prova hello.</span><span class="sxs-lookup"><span data-stu-id="90517-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="90517-195">In questa sezione ne viene presentato un esempio.</span><span class="sxs-lookup"><span data-stu-id="90517-195">This section walks through an example.</span></span>

<span data-ttu-id="90517-196">Per informazioni più dettagliate sull'uso di associazioni con le funzioni di Azure, vedere hello [di riferimento per sviluppatori Azure funzioni](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="90517-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="90517-197">Creare trigger della coda per il test</span><span class="sxs-lookup"><span data-stu-id="90517-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="90517-198">toodemonstrate questo approccio, è necessario creare una funzione di trigger di coda da tootest per una coda denominata `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="90517-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="90517-199">Questa funzione elabora le informazioni relative a nome e indirizzo per un nuovo utente inserito nell'archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="90517-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="90517-200">Se si utilizza un nome diverso, verificare che nome hello è utilizzare conforme toohello [denominazione di code e metadati](https://msdn.microsoft.com/library/dd179349.aspx) regole.</span><span class="sxs-lookup"><span data-stu-id="90517-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="90517-201">In caso contrario, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="90517-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="90517-202">In hello [portale di Azure] per l'app di funzione, fare clic su **nuova funzione** > **QueueTrigger - c#**.</span><span class="sxs-lookup"><span data-stu-id="90517-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="90517-203">Immettere toobe nome di coda hello monitorato dalla funzione coda hello:</span><span class="sxs-lookup"><span data-stu-id="90517-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="90517-204">Fare clic su hello  **+**  pulsante tooselect o creare account di archiviazione hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="90517-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="90517-205">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="90517-205">Then click **Create**.</span></span>
4. <span data-ttu-id="90517-206">Lasciare la finestra del browser del portale, è possibile monitorare le voci di log hello codice hello predefinito coda funzione modello.</span><span class="sxs-lookup"><span data-stu-id="90517-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="90517-207">Creare un toodrop trigger timer, un messaggio nella coda di hello</span><span class="sxs-lookup"><span data-stu-id="90517-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="90517-208">Aprire hello [portale di Azure] in una nuova finestra del browser e passare tooyour funzione app.</span><span class="sxs-lookup"><span data-stu-id="90517-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="90517-209">Fare clic su **Nuova funzione** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="90517-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="90517-210">Immettere un tooset espressione cron frequenza hello codice timer verifica la funzione di coda.</span><span class="sxs-lookup"><span data-stu-id="90517-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="90517-211">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="90517-211">Then click **Create**.</span></span> <span data-ttu-id="90517-212">Se si desidera hello test toorun ogni 30 secondi, è possibile utilizzare la seguente hello [espressione CRON](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="90517-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="90517-213">Fare clic su hello **integrazione** scheda per il nuovo trigger timer.</span><span class="sxs-lookup"><span data-stu-id="90517-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="90517-214">In **Output** fare clic sul pulsante **+ Nuovo output**.</span><span class="sxs-lookup"><span data-stu-id="90517-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="90517-215">Fare clic su **coda** e quindi su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="90517-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="90517-216">Nome di hello nota da usare per hello **oggetto messaggio della coda**.</span><span class="sxs-lookup"><span data-stu-id="90517-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="90517-217">Utilizzare questo codice della funzione hello timer.</span><span class="sxs-lookup"><span data-stu-id="90517-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="90517-218">Immettere il nome di coda hello in cui viene inviato il messaggio hello:</span><span class="sxs-lookup"><span data-stu-id="90517-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="90517-219">Fare clic su hello  **+**  pulsante account di archiviazione tooselect hello è usata in precedenza con trigger coda hello.</span><span class="sxs-lookup"><span data-stu-id="90517-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="90517-220">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90517-220">Then click **Save**.</span></span>
8. <span data-ttu-id="90517-221">Fare clic su hello **sviluppare** scheda per il trigger timer.</span><span class="sxs-lookup"><span data-stu-id="90517-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="90517-222">È possibile utilizzare hello seguente codice per la funzione di timer hello in c#, purché hello stessa coda nome oggetto del messaggio illustrata in precedenza è stato utilizzato.</span><span class="sxs-lookup"><span data-stu-id="90517-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="90517-223">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90517-223">Then click **Save**.</span></span>

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

<span data-ttu-id="90517-224">Hello funzione timer c# a questo punto, viene eseguito ogni 30 secondi se è stata utilizzata nell'espressione cron di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="90517-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="90517-225">funzione timer hello nei registri Hello ogni esecuzione del report:</span><span class="sxs-lookup"><span data-stu-id="90517-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="90517-226">Nella finestra del browser hello per la funzione di coda hello, è possibile visualizzare ogni messaggio in fase di elaborazione:</span><span class="sxs-lookup"><span data-stu-id="90517-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="90517-227">Eseguire il test di una funzione con il codice</span><span class="sxs-lookup"><span data-stu-id="90517-227">Test a function with code</span></span>
<span data-ttu-id="90517-228">Potrebbe essere necessario toocreate un tootest applicazioni o framework esterno delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="90517-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="90517-229">Eseguire il test di una funzione trigger HTTP con il codice Node.js</span><span class="sxs-lookup"><span data-stu-id="90517-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="90517-230">Utilizzare la funzione un tooexecute app Node.js un tootest di richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="90517-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="90517-231">Verificare che tooset:</span><span class="sxs-lookup"><span data-stu-id="90517-231">Make sure tooset:</span></span>

* <span data-ttu-id="90517-232">Hello `host` nell'host di hello richiesta opzioni tooyour funzione app.</span><span class="sxs-lookup"><span data-stu-id="90517-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="90517-233">Il nome di funzione in hello `path`.</span><span class="sxs-lookup"><span data-stu-id="90517-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="90517-234">Il codice di accesso (`<your code>`) in hello `path`.</span><span class="sxs-lookup"><span data-stu-id="90517-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="90517-235">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="90517-235">Code example:</span></span>

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


<span data-ttu-id="90517-236">Output:</span><span class="sxs-lookup"><span data-stu-id="90517-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="90517-237">Nel portale di hello **registri** finestra di output seguenti toohello simile viene registrato durante l'esecuzione di funzione hello:</span><span class="sxs-lookup"><span data-stu-id="90517-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="90517-238">Testare una funzione trigger della coda con codice C#</span><span class="sxs-lookup"><span data-stu-id="90517-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="90517-239">Indicato in precedenza che è possibile testare un trigger di coda tramite codice toodrop un messaggio nella coda di lavoro.</span><span class="sxs-lookup"><span data-stu-id="90517-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="90517-240">Hello seguente codice di esempio è basato su codice hello c# presentati in hello [Introduzione all'archiviazione di Accodamento Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="90517-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="90517-241">Da questo collegamento è disponibile il codice anche per altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="90517-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="90517-242">tootest questo codice in un'applicazione console, è necessario:</span><span class="sxs-lookup"><span data-stu-id="90517-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="90517-243">[Configurare la stringa di connessione di archiviazione nel file app. config hello](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="90517-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="90517-244">Passare un `name` e `address` come parametri toohello app.</span><span class="sxs-lookup"><span data-stu-id="90517-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="90517-245">ad esempio `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="90517-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="90517-246">(Questo codice accetta hello nome e l'indirizzo per un nuovo utente come argomenti della riga di comando in fase di esecuzione.)</span><span class="sxs-lookup"><span data-stu-id="90517-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="90517-247">Codice C# di esempio:</span><span class="sxs-lookup"><span data-stu-id="90517-247">Example C# code:</span></span>

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="90517-248">Nella finestra del browser hello per la funzione di coda hello, è possibile visualizzare ogni messaggio in fase di elaborazione:</span><span class="sxs-lookup"><span data-stu-id="90517-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portale di Azure]: https://portal.azure.com
