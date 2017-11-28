---
title: Creare la prima funzione in Azure con Visual Studio | Microsoft Docs
description: Creare e pubblicare una semplice funzione attivata tramite HTTP in Azure usando Azure Functions Tools for Visual Studio.
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
ms.openlocfilehash: 04370558725d76ffe83d8aaf5d16c88fd2803ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="d964f-104">Creare la prima funzione con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d964f-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="d964f-105">Funzioni di Azure consente di eseguire il codice in un ambiente senza server senza dover prima creare una macchina virtuale o pubblicare un'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="d964f-105">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span>

<span data-ttu-id="d964f-106">Questo argomento illustra come usare gli strumenti di Visual Studio 2017 per Funzioni di Azure per creare e testare una funzione "hello world" in locale.</span><span class="sxs-lookup"><span data-stu-id="d964f-106">In this topic, you learn how to use the Visual Studio 2017 tools for Azure Functions to create and test a "hello world" function locally.</span></span> <span data-ttu-id="d964f-107">Il codice della funzione verrà quindi pubblicato in Azure.</span><span class="sxs-lookup"><span data-stu-id="d964f-107">You will then publish the function code to Azure.</span></span> <span data-ttu-id="d964f-108">Questi strumenti sono disponibili come parte del carico di lavoro di sviluppo di Azure in Visual Studio 2017 versione 15.3 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d964f-108">These tools are available as part of the Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Codice di Funzioni di Azure in un progetto di Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="d964f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d964f-110">Prerequisites</span></span>

<span data-ttu-id="d964f-111">Per completare questa esercitazione, installare:</span><span class="sxs-lookup"><span data-stu-id="d964f-111">To complete this tutorial, install:</span></span>

* <span data-ttu-id="d964f-112">[Visual Studio 2017 versione 15.3](https://www.visualstudio.com/vs/preview/), con il carico di lavoro di **sviluppo di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d964f-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>

    ![Installare Visual Studio 2017 con il carico di lavoro Sviluppo di Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="d964f-114">Dopo l'installazione o l'aggiornamento a Visual Studio 2017 versione 15.3, potrebbe essere necessario anche aggiornare manualmente gli strumenti di Visual Studio 2017 per Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="d964f-114">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="d964f-115">È possibile aggiornare gli strumenti dal menu **Strumenti** scegliendo **Estensioni e aggiornamenti** > **Aggiornamenti** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** (Strumenti per Funzioni di Azure e processi Web) > **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="d964f-115">You can update the tools from the **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="d964f-116">Creare un progetto Funzioni di Azure in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d964f-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using the Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="d964f-117">Ora che è stato creato il progetto, si può creare la prima funzione.</span><span class="sxs-lookup"><span data-stu-id="d964f-117">Now that you have created the project, you can create your first function.</span></span>

## <a name="create-the-function"></a><span data-ttu-id="d964f-118">Creare la funzione</span><span class="sxs-lookup"><span data-stu-id="d964f-118">Create the function</span></span>

1. <span data-ttu-id="d964f-119">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Aggiungi** > **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="d964f-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="d964f-120">Selezionare **Funzione di Azure** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d964f-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="d964f-121">Selezionare **HttpTrigger**, digitare un **nome di funzione**, selezionare **Anonimo** in **Diritti di accesso** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d964f-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="d964f-122">La funzione creata è accessibile da una richiesta HTTP proveniente da qualsiasi client.</span><span class="sxs-lookup"><span data-stu-id="d964f-122">The function created is accessed by an HTTP request from any client.</span></span> 

    ![Creare una nuova funzione di Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="d964f-124">Al progetto viene aggiunto un file di codice che contiene una classe che implementa il codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="d964f-124">A code file is added to your project that contains a class that implements your function code.</span></span> <span data-ttu-id="d964f-125">Questo codice è basato su un modello, che riceve un valore di nome e lo ritrasmette.</span><span class="sxs-lookup"><span data-stu-id="d964f-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="d964f-126">L'attributo **FunctionName** imposta il nome della funzione.</span><span class="sxs-lookup"><span data-stu-id="d964f-126">The **FunctionName** attribute sets the name of your function.</span></span> <span data-ttu-id="d964f-127">L'attributo **HttpTrigger** indica il messaggio che attiva la funzione.</span><span class="sxs-lookup"><span data-stu-id="d964f-127">The **HttpTrigger** attribute indicates the message that triggers the function.</span></span> 

    ![File di codice della funzione](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="d964f-129">Ora che è stata creata una funzione attivata tramite HTTP, si può testare la funzione nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="d964f-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-the-function-locally"></a><span data-ttu-id="d964f-130">Testare la funzione in locale</span><span class="sxs-lookup"><span data-stu-id="d964f-130">Test the function locally</span></span>

<span data-ttu-id="d964f-131">Azure Functions Core Tools consente di eseguire il progetto Funzioni di Azure nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="d964f-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="d964f-132">Verrà richiesto di installare questi strumenti al primo avvio di una funzione da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d964f-132">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="d964f-133">Per testare la funzione premere F5.</span><span class="sxs-lookup"><span data-stu-id="d964f-133">To test your function, press F5.</span></span> <span data-ttu-id="d964f-134">Se viene visualizzata, accettare la richiesta di Visual Studio di scaricare e installare gli strumenti dell'interfaccia della riga di comando Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="d964f-134">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="d964f-135">Potrebbe essere necessario anche abilitare un'eccezione del firewall per consentire agli strumenti di gestire le richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="d964f-135">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="d964f-136">Copiare l'URL della funzione dall'output di runtime di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="d964f-136">Copy the URL of your function from the Azure Functions runtime output.</span></span>  

    ![Runtime locale di Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="d964f-138">Incollare l'URL per la richiesta HTTP nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="d964f-138">Paste the URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="d964f-139">Aggiungere la stringa di query `&name=<yourname>` all'URL ed eseguire la richiesta.</span><span class="sxs-lookup"><span data-stu-id="d964f-139">Append the query string `&name=<yourname>` to this URL and execute the request.</span></span> <span data-ttu-id="d964f-140">Di seguito è illustrata la risposta nel browser alla richiesta GET locale restituita dalla funzione:</span><span class="sxs-lookup"><span data-stu-id="d964f-140">The following shows the response in the browser to the local GET request returned by the function:</span></span> 

    ![Risposta localhost della funzione nel browser](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="d964f-142">Per interrompere il debug, fare clic sul pulsante **Interrompi** sulla barra degli strumenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d964f-142">To stop debugging, click the **Stop** button on the Visual Studio toolbar.</span></span>

<span data-ttu-id="d964f-143">Dopo aver verificato la corretta esecuzione della funzione nel computer locale, è possibile pubblicare il progetto in Azure.</span><span class="sxs-lookup"><span data-stu-id="d964f-143">After you have verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="d964f-144">Pubblicare il progetto in Azure</span><span class="sxs-lookup"><span data-stu-id="d964f-144">Publish the project to Azure</span></span>

<span data-ttu-id="d964f-145">Per poter pubblicare il progetto, è necessario che la sottoscrizione di Azure includa un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="d964f-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="d964f-146">È possibile creare un'app per le funzioni direttamente da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d964f-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="d964f-147">Testare la funzione in Azure</span><span class="sxs-lookup"><span data-stu-id="d964f-147">Test your function in Azure</span></span>

1. <span data-ttu-id="d964f-148">Copiare l'URL di base dell'app per le funzioni dalla pagina del profilo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="d964f-148">Copy the base URL of the function app from the Publish profile page.</span></span> <span data-ttu-id="d964f-149">Sostituire la parte `localhost:port` dell'URL usato durante il test della funzione in locale con il nuovo URL di base.</span><span class="sxs-lookup"><span data-stu-id="d964f-149">Replace the `localhost:port` portion of the URL you used when testing the function locally with the new base URL.</span></span> <span data-ttu-id="d964f-150">Come prima, assicurarsi di accodare la stringa di query `&name=<yourname>` all'URL ed eseguire la richiesta.</span><span class="sxs-lookup"><span data-stu-id="d964f-150">As before, make sure to append the query string `&name=<yourname>` to this URL and execute the request.</span></span>

    <span data-ttu-id="d964f-151">L'URL che chiama la funzione attivata tramite HTTP sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d964f-151">The URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="d964f-152">Incollare questo nuovo URL per la richiesta HTTP nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="d964f-152">Paste this new URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="d964f-153">Di seguito è illustrata la risposta nel browser alla richiesta GET remota restituita dalla funzione:</span><span class="sxs-lookup"><span data-stu-id="d964f-153">The following shows the response in the browser to the remote GET request returned by the function:</span></span> 

    ![Risposta della funzione nel browser](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="d964f-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d964f-155">Next steps</span></span>

<span data-ttu-id="d964f-156">È stato usato Visual Studio per creare un'app per le funzioni C# con una semplice funzione attivata tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="d964f-156">You have used Visual Studio to create a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="d964f-157">Per informazioni su come configurare il progetto per il supporto di altri tipi di trigger e binding, vedere la sezione [Configurare il progetto per lo sviluppo locale](functions-develop-vs.md#configure-the-project-for-local-development) in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="d964f-157">To learn how to configure your project to support other types of triggers and bindings, see the [Configure the project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="d964f-158">Per altre informazioni sul test e il debug in locale con Azure Functions Core Tools, vedere [Scrivere codice per le funzioni di Azure e testarle in locale](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="d964f-158">To learn more about local testing and debugging using the Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="d964f-159">Per altre informazioni sullo sviluppo di funzioni quali le librerie della classe .NET, vedere [Uso di librerie di classi .NET con Funzioni di Azure](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="d964f-159">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

