---
title: Test di Funzioni di Azure | Documentazione Microsoft
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
ms.openlocfilehash: aca03ba4137893157fcbe6650336782ab88cd234
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="016ea-104">Strategie per il test del codice in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="016ea-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="016ea-105">Questo argomento illustra i vari modi per eseguire il test delle funzioni e include gli approcci generali seguenti:</span><span class="sxs-lookup"><span data-stu-id="016ea-105">This topic demonstrates the various ways to test functions, including using the following general approaches:</span></span>

+ <span data-ttu-id="016ea-106">Strumenti basati su HTTP, ad esempio cURL, Postman e persino un browser Web per i trigger basati sul Web</span><span class="sxs-lookup"><span data-stu-id="016ea-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="016ea-107">Esplora archivi di Azure per testare i trigger basati sull'Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="016ea-107">Azure Storage Explorer, to test Azure Storage-based triggers</span></span>
+ <span data-ttu-id="016ea-108">Scheda test nel portale Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="016ea-108">Test tab in the Azure Functions portal</span></span>
+ <span data-ttu-id="016ea-109">Funzione attivata tramite timer</span><span class="sxs-lookup"><span data-stu-id="016ea-109">Timer-triggered function</span></span>
+ <span data-ttu-id="016ea-110">Test dell'applicazione o del framework</span><span class="sxs-lookup"><span data-stu-id="016ea-110">Testing application or framework</span></span>

<span data-ttu-id="016ea-111">Tutti questi metodi di test usano una funzione trigger HTTP che accetta l'input tramite un parametro della stringa di query o il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="016ea-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or the request body.</span></span> <span data-ttu-id="016ea-112">Questa funzione verrà creata nella prima sezione.</span><span class="sxs-lookup"><span data-stu-id="016ea-112">You create this function in the first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="016ea-113">Creare una funzione per i test</span><span class="sxs-lookup"><span data-stu-id="016ea-113">Create a function for testing</span></span>
<span data-ttu-id="016ea-114">Per la maggior parte di questa esercitazione si userà una versione leggermente modificata del modello di funzione HttpTrigger JavaScript disponibile quando si crea una funzione.</span><span class="sxs-lookup"><span data-stu-id="016ea-114">For most of this tutorial, we use a slightly modified version of the HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="016ea-115">Se occorre assistenza nella creazione di una funzione, rivedere questa [esercitazione](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="016ea-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="016ea-116">Scegliere il modello **HttpTrigger- JavaScript** quando si crea la funzione di test nel [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="016ea-116">Choose the **HttpTrigger- JavaScript** template when creating the test function in the [Azure portal].</span></span>

<span data-ttu-id="016ea-117">Il modello di funzione predefinito è fondamentalmente una funzione Hello World che restituisce il nome dal parametro della stringa query o del corpo della richiesta, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="016ea-117">The default function template is basically a "hello world" function that echoes back the name from the request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="016ea-118">Il codice verrà aggiornato per consentire all'utente di fornire anche il nome e un indirizzo come contenuto JSON nel corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="016ea-118">We'll update the code to also allow you to provide the name and an address as JSON content in the request body.</span></span> <span data-ttu-id="016ea-119">La funzione restituirà quindi queste informazioni al client, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="016ea-119">Then the function echoes these back to the client when available.</span></span>   

<span data-ttu-id="016ea-120">Aggiornare la funzione con il codice seguente che verrà usato per il test:</span><span class="sxs-lookup"><span data-stu-id="016ea-120">Update the function with the following code, which we will use for testing:</span></span>

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
            body: "Please pass a name on the query string or in the request body"
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
        echoString += "\n" + "The address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults to 200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="016ea-121">Eseguire il test di una funzione con gli strumenti</span><span class="sxs-lookup"><span data-stu-id="016ea-121">Test a function with tools</span></span>
<span data-ttu-id="016ea-122">All'esterno del Portale di Azure, sono disponibili vari strumenti che è possibile usare per attivare le funzioni di test.</span><span class="sxs-lookup"><span data-stu-id="016ea-122">Outside the Azure portal, there are various tools that you can use to trigger your functions for testing.</span></span> <span data-ttu-id="016ea-123">Questi includono gli strumenti di test HTTP (sia basati su interfaccia utente sia sulla riga di comando), strumenti di accesso all'Archiviazione di Azure e un semplice browser Web.</span><span class="sxs-lookup"><span data-stu-id="016ea-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="016ea-124">Eseguire il test con un browser</span><span class="sxs-lookup"><span data-stu-id="016ea-124">Test with a browser</span></span>
<span data-ttu-id="016ea-125">Il browser web è un modo semplice per attivare le funzioni tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="016ea-125">The web browser is a simple way to trigger functions via HTTP.</span></span> <span data-ttu-id="016ea-126">È possibile usare un browser per le richieste GET per cui non è necessario un payload del corpo e che usi solo i parametri di stringa della query.</span><span class="sxs-lookup"><span data-stu-id="016ea-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="016ea-127">Per testare la funzione definita in precedenza, copiare l'**URL funzione** dal portale,</span><span class="sxs-lookup"><span data-stu-id="016ea-127">To test the function we defined earlier, copy the **Function Url** from the portal.</span></span> <span data-ttu-id="016ea-128">che si presenta nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="016ea-128">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="016ea-129">Aggiungere il parametro `name` alla stringa di query.</span><span class="sxs-lookup"><span data-stu-id="016ea-129">Append the `name` parameter to the query string.</span></span> <span data-ttu-id="016ea-130">Usare un nome effettivo per il segnaposto `<Enter a name here>`.</span><span class="sxs-lookup"><span data-stu-id="016ea-130">Use an actual name for the `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="016ea-131">Incollare l'URL nel browser. Verrà restituita una risposta simile alla seguente.</span><span class="sxs-lookup"><span data-stu-id="016ea-131">Paste the URL into your browser, and you should get a response similar to the following.</span></span>

![Schermata della scheda del browser Chrome con risposta del test](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="016ea-133">Questo esempio è relativo al browser Chrome, che ha restituito la stringa in XML.</span><span class="sxs-lookup"><span data-stu-id="016ea-133">This example is the Chrome browser, which wraps the returned string in XML.</span></span> <span data-ttu-id="016ea-134">Altri browser mostrano solo il valore della stringa.</span><span class="sxs-lookup"><span data-stu-id="016ea-134">Other browsers display just the string value.</span></span>

<span data-ttu-id="016ea-135">Nella finestra **Log** del portale viene registrato un output simile al seguente durante l'esecuzione della funzione:</span><span class="sxs-lookup"><span data-stu-id="016ea-135">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected to log-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="016ea-136">Eseguire il test con Postman</span><span class="sxs-lookup"><span data-stu-id="016ea-136">Test with Postman</span></span>
<span data-ttu-id="016ea-137">Postman, che si integra on il browser Chrome, è lo strumento consigliato per testare la maggior parte delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="016ea-137">The recommended tool to test most of your functions is Postman, which integrates with the Chrome browser.</span></span> <span data-ttu-id="016ea-138">Per installare Postman, vedere la pagina dalla quale è possibile [ottenere Postman](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="016ea-138">To install Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="016ea-139">Postman consente di controllare molti più attributi di una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="016ea-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="016ea-140">Usare lo strumento di test HTTP con cui si ha maggiore familiarità.</span><span class="sxs-lookup"><span data-stu-id="016ea-140">Use the HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="016ea-141">Ecco alcune alternative a Postman:</span><span class="sxs-lookup"><span data-stu-id="016ea-141">Here are some alternatives to Postman:</span></span>  
>
> * [<span data-ttu-id="016ea-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="016ea-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="016ea-143">Paw</span><span class="sxs-lookup"><span data-stu-id="016ea-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="016ea-144">Per testare la funzione con un corpo della richiesta in Postman:</span><span class="sxs-lookup"><span data-stu-id="016ea-144">To test the function with a request body in Postman:</span></span>

1. <span data-ttu-id="016ea-145">Avviare Postman dal pulsante **App** nell'angolo in alto a sinistra di una finestra del browser Chrome.</span><span class="sxs-lookup"><span data-stu-id="016ea-145">Start Postman from the **Apps** button in the upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="016ea-146">Copiare l'**URL funzione** e incollarlo in Postman.</span><span class="sxs-lookup"><span data-stu-id="016ea-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="016ea-147">Include il parametro della stringa di query del codice di accesso.</span><span class="sxs-lookup"><span data-stu-id="016ea-147">It includes the access code query string parameter.</span></span>
3. <span data-ttu-id="016ea-148">Modificare il metodo HTTP in **POST**.</span><span class="sxs-lookup"><span data-stu-id="016ea-148">Change the HTTP method to **POST**.</span></span>
4. <span data-ttu-id="016ea-149">Fare clic su **Body** > **raw** e aggiungere il corpo della richiesta JSON simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="016ea-149">Click **Body** > **raw**, and add a JSON request body similar to the following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="016ea-150">Fare clic su **Send**.</span><span class="sxs-lookup"><span data-stu-id="016ea-150">Click **Send**.</span></span>

<span data-ttu-id="016ea-151">L'immagine seguente mostra il test della semplice funzione echo di esempio in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="016ea-151">The following image shows testing the simple echo function example in this tutorial.</span></span>

![Schermata dell'interfaccia utente di Postman](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="016ea-153">Nella finestra **Log** del portale viene registrato un output simile al seguente durante l'esecuzione della funzione:</span><span class="sxs-lookup"><span data-stu-id="016ea-153">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-the-command-line"></a><span data-ttu-id="016ea-154">Eseguire il test con cURL dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="016ea-154">Test with cURL from the command line</span></span>
<span data-ttu-id="016ea-155">Spesso, quando si eseguono test del software, non è necessario eseguire ricerche particolari al di là della riga di comando per eseguire il debug dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="016ea-155">Often when you're testing software, it's not necessary to look any further than the command line to help debug your application.</span></span> <span data-ttu-id="016ea-156">L'approccio è analogo per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="016ea-156">This is no different with testing functions.</span></span> <span data-ttu-id="016ea-157">Si noti che cURL è disponibile per impostazione predefinita nei sistemi basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="016ea-157">Note that the cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="016ea-158">In Windows è necessario prima scaricare e installare lo [strumento cURL](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="016ea-158">On Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="016ea-159">Per testare la funzione definita in precedenza, copiare l'**URL funzione** dal portale,</span><span class="sxs-lookup"><span data-stu-id="016ea-159">To test the function that we defined earlier, copy the **Function URL** from the portal.</span></span> <span data-ttu-id="016ea-160">che si presenta nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="016ea-160">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="016ea-161">Si tratta dell'URL per l'attivazione di una funzione.</span><span class="sxs-lookup"><span data-stu-id="016ea-161">This is the URL for triggering your function.</span></span> <span data-ttu-id="016ea-162">È possibile testarlo con il comando cURL dalla riga di comando per eseguire una richiesta GET (`-G` o `--get`) sulla funzione:</span><span class="sxs-lookup"><span data-stu-id="016ea-162">Test this by using the cURL command on the command line to make a GET (`-G` or `--get`) request against the function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="016ea-163">Questo esempio in particolare richiede un parametro della stringa di query che può essere passato come dati (`-d`) nel comando cURL:</span><span class="sxs-lookup"><span data-stu-id="016ea-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in the cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="016ea-164">Eseguire il comando per visualizzare l'output seguente della funzione nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="016ea-164">Run the command, and you see the following output of the function on the command line:</span></span>

![Schermata dell'output del prompt dei comandi](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="016ea-166">Nella finestra **Log** del portale viene registrato un output simile al seguente durante l'esecuzione della funzione:</span><span class="sxs-lookup"><span data-stu-id="016ea-166">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected to log-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="016ea-167">Eseguire il test di un trigger del BLOB con Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="016ea-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="016ea-168">È possibile testare una funzione trigger del BLOB con [Esplora archivi di Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="016ea-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="016ea-169">Nel [Portale di Azure] creare una funzione trigger del BLOB in C#, F# o JavaScript per l'app Funzioni.</span><span class="sxs-lookup"><span data-stu-id="016ea-169">In the [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="016ea-170">Impostare il percorso da monitorare sul nome del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="016ea-170">Set the path to monitor to the name of your blob container.</span></span> <span data-ttu-id="016ea-171">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="016ea-171">For example:</span></span>

        files
2. <span data-ttu-id="016ea-172">Fare clic sul pulsante **+** per selezionare o creare l'account di archiviazione da usare.</span><span class="sxs-lookup"><span data-stu-id="016ea-172">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="016ea-173">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="016ea-173">Then click **Create**.</span></span>
3. <span data-ttu-id="016ea-174">Creare un file di testo con il contenuto seguente e salvarlo:</span><span class="sxs-lookup"><span data-stu-id="016ea-174">Create a text file with the following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="016ea-175">Eseguire [Azure Storage Explorer](http://storageexplorer.com/) e connettersi al contenitore BLOB nell'account di archiviazione monitorato.</span><span class="sxs-lookup"><span data-stu-id="016ea-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect to the blob container in the storage account being monitored.</span></span>
5. <span data-ttu-id="016ea-176">Fare clic su **Carica** per caricare il file di testo.</span><span class="sxs-lookup"><span data-stu-id="016ea-176">Click **Upload** to upload the text file.</span></span>

    ![Screenshot di Esplora archivi](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="016ea-178">Il codice della funzione trigger del BLOB predefinita segnala l'elaborazione del BLOB nei log:</span><span class="sxs-lookup"><span data-stu-id="016ea-178">The default blob trigger function code reports the processing of the blob in the logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected to log-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="016ea-179">Eseguire il test di una funzione all'interno di Funzioni</span><span class="sxs-lookup"><span data-stu-id="016ea-179">Test a function within functions</span></span>
<span data-ttu-id="016ea-180">Il portale Funzioni di Azure è progettato per consentire di testare l'HTTP e le funzioni attivate da timer.</span><span class="sxs-lookup"><span data-stu-id="016ea-180">The Azure Functions portal is designed to let you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="016ea-181">È inoltre possibile creare funzioni per attivare altre funzioni su cui si esegue il test.</span><span class="sxs-lookup"><span data-stu-id="016ea-181">You can also create functions to trigger other functions that you are testing.</span></span>

### <a name="test-with-the-functions-portal-run-button"></a><span data-ttu-id="016ea-182">Eseguire il test con il pulsante Esegui nel portale Funzioni</span><span class="sxs-lookup"><span data-stu-id="016ea-182">Test with the Functions portal Run button</span></span>
<span data-ttu-id="016ea-183">Il portale presenta un pulsante **Esegui** che consente di eseguire alcuni test limitati.</span><span class="sxs-lookup"><span data-stu-id="016ea-183">The portal provides a **Run** button that you can use to do some limited testing.</span></span> <span data-ttu-id="016ea-184">Con questo pulsante, è possibile specificare un corpo della richiesta, tuttavia non si possono specificare i parametri della stringa di query o aggiornare le intestazioni della richiesta.</span><span class="sxs-lookup"><span data-stu-id="016ea-184">You can provide a request body by using the button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="016ea-185">Eseguire il test della funzione trigger HTTP creata in precedenza aggiungendo una stringa JSON simile alla seguente nel campo **Corpo della richiesta**.</span><span class="sxs-lookup"><span data-stu-id="016ea-185">Test the HTTP trigger function we created earlier by adding a JSON string similar to the following in the **Request body** field.</span></span> <span data-ttu-id="016ea-186">Quindi, fare clic sul pulsante **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="016ea-186">Then click the **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="016ea-187">Nella finestra **Log** del portale viene registrato un output simile al seguente durante l'esecuzione della funzione:</span><span class="sxs-lookup"><span data-stu-id="016ea-187">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="016ea-188">Eseguire il test con un trigger del timer</span><span class="sxs-lookup"><span data-stu-id="016ea-188">Test with a timer trigger</span></span>
<span data-ttu-id="016ea-189">Alcune funzioni non possono essere testate adeguatamente con gli strumenti citati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="016ea-189">Some functions can't be adequately tested with the tools mentioned previously.</span></span> <span data-ttu-id="016ea-190">Prendiamo ad esempio una funzione trigger della coda eseguita quando un messaggio viene inserito in [Archiviazione code di Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="016ea-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="016ea-191">È sempre possibile scrivere codice per inserire un messaggio nella coda. Di seguito ne viene fornito un esempio in un progetto console.</span><span class="sxs-lookup"><span data-stu-id="016ea-191">You can always write code to drop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="016ea-192">Esiste tuttavia un altro approccio che può essere usato per eseguire direttamente il test delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="016ea-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="016ea-193">È possibile usare un trigger del timer configurato con un'associazione di output della coda.</span><span class="sxs-lookup"><span data-stu-id="016ea-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="016ea-194">Il codice del trigger del timer può quindi scrivere i messaggi di prova nella coda.</span><span class="sxs-lookup"><span data-stu-id="016ea-194">That timer trigger code can then write the test messages to the queue.</span></span> <span data-ttu-id="016ea-195">In questa sezione ne viene presentato un esempio.</span><span class="sxs-lookup"><span data-stu-id="016ea-195">This section walks through an example.</span></span>

<span data-ttu-id="016ea-196">Per informazioni più dettagliate sull'uso di associazioni con Funzioni di Azure, vedere la [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="016ea-196">For more in-depth information on using bindings with Azure Functions, see the [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="016ea-197">Creare trigger della coda per il test</span><span class="sxs-lookup"><span data-stu-id="016ea-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="016ea-198">Per illustrare questo approccio, si creerà prima di tutto una funzione trigger della coda che si vuole testare per una coda denominata `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="016ea-198">To demonstrate this approach, we first create a queue trigger function that we want to test for a queue named `queue-newusers`.</span></span> <span data-ttu-id="016ea-199">Questa funzione elabora le informazioni relative a nome e indirizzo per un nuovo utente inserito nell'archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="016ea-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="016ea-200">Se si usa un nome di coda diverso, assicurarsi che il nome usato sia conforme alle regole descritte in [Denominazione di code e metadati](https://msdn.microsoft.com/library/dd179349.aspx) .</span><span class="sxs-lookup"><span data-stu-id="016ea-200">If you use a different queue name, make sure the name you use conforms to the [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="016ea-201">In caso contrario, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="016ea-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="016ea-202">Nel [Portale di Azure] fare clic su **Nuova funzione** > **QueueTrigger - C#** per l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="016ea-202">In the [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="016ea-203">Immettere il nome della coda da monitorare tramite la funzione coda:</span><span class="sxs-lookup"><span data-stu-id="016ea-203">Enter the queue name to be monitored by the queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="016ea-204">Fare clic sul pulsante **+** per selezionare o creare l'account di archiviazione da usare.</span><span class="sxs-lookup"><span data-stu-id="016ea-204">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="016ea-205">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="016ea-205">Then click **Create**.</span></span>
4. <span data-ttu-id="016ea-206">Lasciare aperta la finestra del browser nel portale per monitorare le voci di log per il codice del modello di funzione coda predefinito.</span><span class="sxs-lookup"><span data-stu-id="016ea-206">Leave this portal browser window open, so you can monitor the log entries for the default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-to-drop-a-message-in-the-queue"></a><span data-ttu-id="016ea-207">Creare un trigger del timer per inserire un messaggio nella coda</span><span class="sxs-lookup"><span data-stu-id="016ea-207">Create a timer trigger to drop a message in the queue</span></span>
1. <span data-ttu-id="016ea-208">Aprire il [Portale di Azure] in una nuova finestra del browser e passare all'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="016ea-208">Open the [Azure portal] in a new browser window, and navigate to your function app.</span></span>
2. <span data-ttu-id="016ea-209">Fare clic su **Nuova funzione** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="016ea-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="016ea-210">Immettere un'espressione CRON per impostare la frequenza con cui il codice del timer eseguirà il test della funzione coda.</span><span class="sxs-lookup"><span data-stu-id="016ea-210">Enter a cron expression to set how often the timer code tests your queue function.</span></span> <span data-ttu-id="016ea-211">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="016ea-211">Then click **Create**.</span></span> <span data-ttu-id="016ea-212">Se si vuole che il test venga eseguito ogni 30 secondi, è possibile usare l'[espressione CRON](https://wikipedia.org/wiki/Cron#CRON_expression)seguente:</span><span class="sxs-lookup"><span data-stu-id="016ea-212">If you want the test to run every 30 seconds, you can use the following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="016ea-213">Fare clic sulla scheda **Integra** per il nuovo trigger del timer.</span><span class="sxs-lookup"><span data-stu-id="016ea-213">Click the **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="016ea-214">In **Output** fare clic sul pulsante **+ Nuovo output**.</span><span class="sxs-lookup"><span data-stu-id="016ea-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="016ea-215">Fare clic su **coda** e quindi su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="016ea-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="016ea-216">Prendere nota del nome usato per l'**oggetto messaggio di coda**.</span><span class="sxs-lookup"><span data-stu-id="016ea-216">Note the name you use for the **queue message object**.</span></span> <span data-ttu-id="016ea-217">Usare il codice di funzione timer.</span><span class="sxs-lookup"><span data-stu-id="016ea-217">You use this in the timer function code.</span></span>

        myQueue
6. <span data-ttu-id="016ea-218">Immettere il nome della coda a cui verrà inviato il messaggio:</span><span class="sxs-lookup"><span data-stu-id="016ea-218">Enter the queue name where the message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="016ea-219">Fare clic sul pulsante **+** per selezionare l'account di archiviazione usato in precedenza con il trigger della coda.</span><span class="sxs-lookup"><span data-stu-id="016ea-219">Click the **+** button to select the storage account you used previously with the queue trigger.</span></span> <span data-ttu-id="016ea-220">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="016ea-220">Then click **Save**.</span></span>
8. <span data-ttu-id="016ea-221">Fare clic sulla scheda **Sviluppo** per il trigger del timer.</span><span class="sxs-lookup"><span data-stu-id="016ea-221">Click the **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="016ea-222">È possibile usare il codice seguente per la funzione timer C#, a condizione di avere usato lo stesso nome di oggetto messaggio della coda indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="016ea-222">You can use the following code for the C# timer function, as long as you used the same queue message object name shown earlier.</span></span> <span data-ttu-id="016ea-223">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="016ea-223">Then click **Save**.</span></span>

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

<span data-ttu-id="016ea-224">A questo punto, se è stata usata l'espressione CRON di esempio, la funzione timer C# verrà eseguita ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="016ea-224">At this point, the C# timer function executes every 30 seconds if you used the example cron expression.</span></span> <span data-ttu-id="016ea-225">I log per la funzione timer segnalano ogni esecuzione:</span><span class="sxs-lookup"><span data-stu-id="016ea-225">The logs for the timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="016ea-226">Nella finestra del browser per la funzione coda viene visualizzato ogni messaggio in fase di elaborazione:</span><span class="sxs-lookup"><span data-stu-id="016ea-226">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="016ea-227">Eseguire il test di una funzione con il codice</span><span class="sxs-lookup"><span data-stu-id="016ea-227">Test a function with code</span></span>
<span data-ttu-id="016ea-228">Potrebbe essere necessario creare un'applicazione esterna o un framework per testare le funzioni.</span><span class="sxs-lookup"><span data-stu-id="016ea-228">You may need to create an external application or framework to test your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="016ea-229">Eseguire il test di una funzione trigger HTTP con il codice Node.js</span><span class="sxs-lookup"><span data-stu-id="016ea-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="016ea-230">È possibile usare il codice Node.js per eseguire una richiesta HTTP e testare la funzione.</span><span class="sxs-lookup"><span data-stu-id="016ea-230">You can use a Node.js app to execute an HTTP request to test your function.</span></span>
<span data-ttu-id="016ea-231">Assicurarsi di impostare:</span><span class="sxs-lookup"><span data-stu-id="016ea-231">Make sure to set:</span></span>

* <span data-ttu-id="016ea-232">`host` nelle opzioni di richiesta per l'host dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="016ea-232">The `host` in the request options to your function app host.</span></span>
* <span data-ttu-id="016ea-233">Il nome della funzione in `path`.</span><span class="sxs-lookup"><span data-stu-id="016ea-233">Your function name in the `path`.</span></span>
* <span data-ttu-id="016ea-234">Il codice di accesso (`<your code>`) in `path`.</span><span class="sxs-lookup"><span data-stu-id="016ea-234">Your access code (`<your code>`) in the `path`.</span></span>

<span data-ttu-id="016ea-235">Esempio di codice:</span><span class="sxs-lookup"><span data-stu-id="016ea-235">Code example:</span></span>

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


<span data-ttu-id="016ea-236">Output:</span><span class="sxs-lookup"><span data-stu-id="016ea-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    The address you provided is Dallas, T.X. 75201

<span data-ttu-id="016ea-237">Nella finestra **Log** del portale viene registrato un output simile al seguente durante l'esecuzione della funzione:</span><span class="sxs-lookup"><span data-stu-id="016ea-237">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="016ea-238">Testare una funzione trigger della coda con codice C#</span><span class="sxs-lookup"><span data-stu-id="016ea-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="016ea-239">Si è accennato in precedenza che è possibile testare un trigger della coda tramite codice per inserire un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="016ea-239">We mentioned earlier that you can test a queue trigger by using code to drop a message in your queue.</span></span> <span data-ttu-id="016ea-240">L'esempio di codice seguente si basa sul codice C# illustrato nell'esercitazione [Introduzione all'archiviazione code di Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) .</span><span class="sxs-lookup"><span data-stu-id="016ea-240">The following example code is based on the C# code presented in the [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="016ea-241">Da questo collegamento è disponibile il codice anche per altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="016ea-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="016ea-242">Per testare il codice in un'app console è necessario:</span><span class="sxs-lookup"><span data-stu-id="016ea-242">To test this code in a console app, you must:</span></span>

* <span data-ttu-id="016ea-243">[Configurare la stringa di connessione di archiviazione nel file app.config](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="016ea-243">[Configure your storage connection string in the app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="016ea-244">Passare `name` e `address` come parametri per l'app.</span><span class="sxs-lookup"><span data-stu-id="016ea-244">Pass a `name` and `address` as parameters to the app.</span></span> <span data-ttu-id="016ea-245">Ad esempio, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="016ea-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="016ea-246">Questo codice accetta il nome e l'indirizzo per un nuovo utente come argomenti della riga di comando in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="016ea-246">(This code accepts the name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="016ea-247">Codice C# di esempio:</span><span class="sxs-lookup"><span data-stu-id="016ea-247">Example C# code:</span></span>

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

    // Create the queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference to a queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create the queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it to the queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message to " + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="016ea-248">Nella finestra del browser per la funzione coda viene visualizzato ogni messaggio in fase di elaborazione:</span><span class="sxs-lookup"><span data-stu-id="016ea-248">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Portale di Azure]: https://portal.azure.com
