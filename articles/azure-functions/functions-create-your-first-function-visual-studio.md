---
title: la prima funzione in Azure utilizzando Visual Studio aaaCreate | Documenti Microsoft
description: Creare e pubblicare un semplice tooAzure funzione HTTP attivato mediante gli strumenti di funzioni di Azure per Visual Studio.
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, funzioni, elaborazione eventi, calcolo, architettura senza server
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="cfeeb-104">Creare la prima funzione con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cfeeb-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="cfeeb-105">Funzioni di Azure consente di eseguire il codice in un ambiente senza server senza dover toofirst crea una macchina virtuale o si pubblica un'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="cfeeb-106">In questo argomento, è illustrato come toouse hello 2017 di Visual Studio tools per toocreate funzioni di Azure e testare una funzione di "hello world" in locale.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="cfeeb-107">Verrà quindi pubblicato tooAzure codice di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="cfeeb-108">Questi strumenti sono disponibili come parte del carico di lavoro di hello lo sviluppo di Azure in Visual Studio 2017 versione 15.3 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Codice di Funzioni di Azure in un progetto di Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="cfeeb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cfeeb-110">Prerequisites</span></span>

<span data-ttu-id="cfeeb-111">toocomplete questa esercitazione, installare:</span><span class="sxs-lookup"><span data-stu-id="cfeeb-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="cfeeb-112">[Visual Studio 2017 versione 15.3](https://www.visualstudio.com/vs/preview/), tra cui hello **lo sviluppo di Azure** carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![Installare Visual Studio 2017 con carico di lavoro di hello lo sviluppo di Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="cfeeb-114">Dopo l'installazione o aggiornamento tooVisual Studio 2017 versione 15.3, si potrebbe essere necessario anche strumenti di Visual Studio 2017 hello toomanually update per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="cfeeb-115">È possibile aggiornare gli strumenti hello hello **strumenti** menu sotto **estensioni e aggiornamenti...**   >  **Aggiornamenti** > **Visual Studio Marketplace** > **strumenti i processi di funzioni di Azure e Web**  >  **Aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="cfeeb-116">Creare un progetto Funzioni di Azure in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cfeeb-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="cfeeb-117">Ora che è stato creato il progetto di hello, è possibile creare la prima funzione.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="cfeeb-118">Creare la funzione hello</span><span class="sxs-lookup"><span data-stu-id="cfeeb-118">Create hello function</span></span>

1. <span data-ttu-id="cfeeb-119">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="cfeeb-120">Selezionare **Funzione di Azure** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="cfeeb-121">Selezionare **HttpTrigger**, digitare un **nome di funzione**, selezionare **Anonimo** in **Diritti di accesso** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="cfeeb-122">funzione di Hello creato è accessibile tramite una richiesta HTTP da qualsiasi client.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![Creare una nuova funzione di Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="cfeeb-124">Un file di codice viene aggiunto il progetto tooyour che contiene una classe che implementa il codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="cfeeb-125">Questo codice è basato su un modello, che riceve un valore di nome e lo ritrasmette.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="cfeeb-126">Hello **FunctionName** attributo imposta hello nome della funzione.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="cfeeb-127">Hello **HttpTrigger** attributo indica il messaggio hello che attiva la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![File di codice della funzione](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="cfeeb-129">Ora che è stata creata una funzione attivata tramite HTTP, si può testare la funzione nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="cfeeb-130">Funzione hello di test in locale</span><span class="sxs-lookup"><span data-stu-id="cfeeb-130">Test hello function locally</span></span>

<span data-ttu-id="cfeeb-131">Azure Functions Core Tools consente di eseguire il progetto Funzioni di Azure nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="cfeeb-132">Si è richiesta tooinstall questi strumenti hello primo avvio di una funzione da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="cfeeb-133">tootest della funzione, premere F5.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-133">tootest your function, press F5.</span></span> <span data-ttu-id="cfeeb-134">Se richiesto, accettare la richiesta di hello da toodownload di Visual Studio e installare gli strumenti di Azure funzioni Core (CLI).</span><span class="sxs-lookup"><span data-stu-id="cfeeb-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="cfeeb-135">È necessario anche tooenable un'eccezione del firewall in modo che gli strumenti di hello possono gestire le richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="cfeeb-136">Copia URL hello della funzione di runtime di Azure funzioni hello di output.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Runtime locale di Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="cfeeb-138">Incollare l'URL di hello per richiesta HTTP hello nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="cfeeb-139">Aggiungere la stringa di query hello `&name=<yourname>` toothis URL ed eseguire la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="cfeeb-140">Hello seguente risposta hello in hello browser toohello locale richiesta GET restituito dalla funzione hello:</span><span class="sxs-lookup"><span data-stu-id="cfeeb-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![Risposta della funzione localhost nel browser hello](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="cfeeb-142">toostop debug, fare clic su hello **arrestare** sulla barra degli strumenti di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="cfeeb-143">Dopo aver verificato che la funzione hello venga eseguita correttamente nel computer locale, è ora toopublish hello progetto tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="cfeeb-144">Pubblicare hello progetto tooAzure</span><span class="sxs-lookup"><span data-stu-id="cfeeb-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="cfeeb-145">Per poter pubblicare il progetto, è necessario che la sottoscrizione di Azure includa un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="cfeeb-146">È possibile creare un'app per le funzioni direttamente da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="cfeeb-147">Testare la funzione in Azure</span><span class="sxs-lookup"><span data-stu-id="cfeeb-147">Test your function in Azure</span></span>

1. <span data-ttu-id="cfeeb-148">Copiare l'URL di base dell'app di funzione hello hello dalla pagina del profilo di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="cfeeb-149">Sostituire hello `localhost:port` parte dell'URL di hello è utilizzata per la verifica di funzione hello in locale con hello nuovo URL di base.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="cfeeb-150">Come in precedenza, verificare che stringa di query hello tooappend `&name=<yourname>` toothis URL ed eseguire la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="cfeeb-151">URL di Hello che chiama HTTP attivato funzione ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="cfeeb-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="cfeeb-152">Incollare questo nuovo URL per la richiesta HTTP hello nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="cfeeb-153">Hello seguente risposta hello in hello browser toohello remoto richiesta GET restituito dalla funzione hello:</span><span class="sxs-lookup"><span data-stu-id="cfeeb-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Risposta della funzione nel browser hello](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="cfeeb-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cfeeb-155">Next steps</span></span>

<span data-ttu-id="cfeeb-156">È stata usata l'app di funzione toocreate c# di Visual Studio con una semplice funzione HTTP attivato.</span><span class="sxs-lookup"><span data-stu-id="cfeeb-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="cfeeb-157">toolearn come tooconfigure toosupport il progetto altri tipi di trigger e le associazioni, vedere hello [progetto hello Configura per lo sviluppo locale](functions-develop-vs.md#configure-the-project-for-local-development) sezione [gli strumenti di funzioni di Azure per Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="cfeeb-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="cfeeb-158">toolearn ulteriori informazioni sui test locale e il debug con strumenti di base di hello Azure funzioni, vedere [codice e testare le funzioni di Azure localmente](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="cfeeb-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="cfeeb-159">toolearn più sullo sviluppo di funzioni come librerie di classi .NET, vedere [librerie di classi .NET utilizzando con le funzioni di Azure](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="cfeeb-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

