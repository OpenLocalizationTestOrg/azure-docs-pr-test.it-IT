---
title: Come usare SendGrid in Funzioni di Azure | Documentazione Microsoft
description: Questo articolo mostra come usare SendGrid in Funzioni di Azure
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: 05c9f4e4a4351219da68af8b702c25f21d7d4d02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-sendgrid-in-azure-functions"></a><span data-ttu-id="9577e-103">Come usare SendGrid nelle Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9577e-103">How to use SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="9577e-104">Panoramica di SendGrid</span><span class="sxs-lookup"><span data-stu-id="9577e-104">SendGrid Overview</span></span>

<span data-ttu-id="9577e-105">Funzioni di Azure supporta le associazioni output di SendGrid per consentire alle funzioni di inviare messaggi posta elettronica con poche righe di codice e un account di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9577e-105">Azure Functions supports SendGrid output bindings to enable your functions to send email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="9577e-106">Per usare l'API SendGrid in una Funzione di Azure, è necessario un [account di SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="9577e-106">To use the SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="9577e-107">Inoltre, è necessario disporre di una chiave dell'API di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9577e-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="9577e-108">Accedere al proprio account di SendGrid e fare clic su **Impostazioni** quindi su **Chiave API** per generare una chiave API.</span><span class="sxs-lookup"><span data-stu-id="9577e-108">Log in to your SendGrid account and click **Settings** then **API Key** to generate an API key.</span></span> <span data-ttu-id="9577e-109">Fare in modo che questa chiave sia disponibile per l'uso nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="9577e-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="9577e-110">È ora possibile creare un'app per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="9577e-110">You are now ready to create an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="9577e-111">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9577e-111">Create an Azure Function app</span></span> 

<span data-ttu-id="9577e-112">Le app per le funzioni di Azure sono contenitori per uno o più funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="9577e-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="9577e-113">Le funzioni di Azure sono solo delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="9577e-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="9577e-114">Ogni funzione di Azure è associata a un trigger, ovvero a un evento che attiva l'esecuzione della funzione.</span><span class="sxs-lookup"><span data-stu-id="9577e-114">Each Azure function is tied to one trigger, which is an event that causes the function to run.</span></span>
<span data-ttu-id="9577e-115">Ogni funzione può contenere diverse associazioni di input oppure output.</span><span class="sxs-lookup"><span data-stu-id="9577e-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="9577e-116">Le associazioni sono servizi che è possibile usare in una funzione.</span><span class="sxs-lookup"><span data-stu-id="9577e-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="9577e-117">SendGrid è un'associazione di output che è possibile usare per inviare email.</span><span class="sxs-lookup"><span data-stu-id="9577e-117">SendGrid is an output binding you can use to send email.</span></span> 

1. <span data-ttu-id="9577e-118">Accedere al Portale di Azure e [creare un'app per le funzioni di Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) oppure aprire un'app per le funzioni esistente.</span><span class="sxs-lookup"><span data-stu-id="9577e-118">Log in to the Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="9577e-119">Creare una funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9577e-119">Create an Azure function.</span></span> <span data-ttu-id="9577e-120">Per farlo in modo semplice, scegliere un trigger manuale e C#.</span><span class="sxs-lookup"><span data-stu-id="9577e-120">To keep it simple, choose a manual trigger and C#.</span></span> 

 ![Creare una funzione di Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="9577e-122">Configurare SendGrid per l'uso in un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9577e-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="9577e-123">È necessario archiviare la chiave API di SendGrid come impostazione dell'app per usarla in una funzione.</span><span class="sxs-lookup"><span data-stu-id="9577e-123">You must store your SendGrid API Key as an app setting to use it in a function.</span></span> <span data-ttu-id="9577e-124">Il campo ApiKey non è la chiave API di SendGrid effettiva, ma un'impostazione dell'app definita dall'utente che rappresenta la chiave API effettiva.</span><span class="sxs-lookup"><span data-stu-id="9577e-124">The ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="9577e-125">Per sicurezza si esegue questo tipo di archiviazione della chiave, poiché è separata da qualsiasi codice o file che potrebbe essere archiviato nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="9577e-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="9577e-126">Creare una chiave **AppSettings** in **Impostazioni applicazione** dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="9577e-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Creare una funzione di Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="9577e-128">Configurare le associazioni di output di SendGrid</span><span class="sxs-lookup"><span data-stu-id="9577e-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="9577e-129">SendGrid è disponibile come associazione di output della funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9577e-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="9577e-130">Per creare un'associazione di output di SendGrid:</span><span class="sxs-lookup"><span data-stu-id="9577e-130">To create a SendGrid output binding:</span></span>

1. <span data-ttu-id="9577e-131">Andare nella scheda **Integrazione** della funzione nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9577e-131">Go to the **Integrate** tab of the function in the Azure portal.</span></span>
2. <span data-ttu-id="9577e-132">Per creare un'associazione di output di SendGrid fare clic su **Nuovo output**.</span><span class="sxs-lookup"><span data-stu-id="9577e-132">Click **New Output** to create a SendGrid output binding.</span></span>
3. <span data-ttu-id="9577e-133">Compilare le proprietà **Chiave API** e **Nome del parametro del messaggio**.</span><span class="sxs-lookup"><span data-stu-id="9577e-133">Fill in the **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="9577e-134">Se lo si desidera, a questo punto è possibile immettere le altre proprietà oppure codificarle.</span><span class="sxs-lookup"><span data-stu-id="9577e-134">If you want, you can enter the other properties now, or code them instead.</span></span> <span data-ttu-id="9577e-135">Queste impostazioni possono essere usate come impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="9577e-135">These settings can be used as defaults.</span></span>

 ![Configurare le associazioni di output di SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="9577e-137">L'aggiunta di un'associazione a una funzione crea un file denominato **function.json** nella cartella della funzione.</span><span class="sxs-lookup"><span data-stu-id="9577e-137">Adding a binding to a function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="9577e-138">Questo file contiene tutte le informazioni visualizzate nella scheda **Integrazione** della funzione di Azure , ma in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="9577e-138">This file contains all the same information that you see in the Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="9577e-139">L'impostazione dei campi **ApiKey**, **messaggio**, e **from** (da) crea le seguenti voci nel file **function.json**:</span><span class="sxs-lookup"><span data-stu-id="9577e-139">Setting the **ApiKey**, **message**, and **from** fields create the following entries in the **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="9577e-140">Se lo si preferisce, è possibile modificare direttamente questo file.</span><span class="sxs-lookup"><span data-stu-id="9577e-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="9577e-141">Ora che l'app per le funzioni e la funzione sono state create e configurate, è possibile scrivere il codice per inviare un'email.</span><span class="sxs-lookup"><span data-stu-id="9577e-141">Now that you have created and configured the Function App and function, you can write the code to send an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="9577e-142">Scrivere il codice che crea e invia email</span><span class="sxs-lookup"><span data-stu-id="9577e-142">Write code that creates and sends email</span></span>

<span data-ttu-id="9577e-143">L'API SendGrid contiene tutti i comandi necessari per creare e inviare un'email.</span><span class="sxs-lookup"><span data-stu-id="9577e-143">The SendGrid API contains all the commands you need to create and send an email.</span></span>  

- <span data-ttu-id="9577e-144">Sostituire il codice nella funzione con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9577e-144">Replace the code in the function with the following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change to email of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="9577e-145">Si noti che la prima riga contiene la direttiva ```#r``` che fa riferimento all'assembly di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9577e-145">Notice the first line contains the ```#r``` directive that references the SendGrid assembly.</span></span> <span data-ttu-id="9577e-146">Successivamente, è possibile usare un'istruzione ```using``` per accedere più facilmente agli oggetti nello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="9577e-146">After that, you can use a ```using``` statement to more easily access the objects in that namespace.</span></span> <span data-ttu-id="9577e-147">Nel codice, creare istanze degli oggetti ```Mail```, ```Personalization``` e ```Content``` dell'API di SendGrid che compongono l'email.</span><span class="sxs-lookup"><span data-stu-id="9577e-147">In the code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from the SendGrid API that compose the email.</span></span> <span data-ttu-id="9577e-148">Quando l'utente restituisce il messaggio, SendGrid lo recapita.</span><span class="sxs-lookup"><span data-stu-id="9577e-148">When you return the message, SendGrid delivers it.</span></span> 

<span data-ttu-id="9577e-149">La firma della funzione contiene inoltre un altro parametro out di tipo ```Mail``` denominato ```message```.</span><span class="sxs-lookup"><span data-stu-id="9577e-149">The function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="9577e-150">Le associazioni di input e output si esprimono come parametri di funzione nel codice.</span><span class="sxs-lookup"><span data-stu-id="9577e-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="9577e-151">Testare il codice facendo clic su **Test** e inserire un messaggio nel campo **Corpo della richiesta**, quindi fare clic sul pulsante **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="9577e-151">Test your code by clicking **Test** and entering a message into the **Request body** field, then clicking the **Run** button.</span></span>

 ![Testare il codice](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="9577e-153">Controllare i messaggi di posta elettronica per verificare che l'email sia stata inviata da SendGrid.</span><span class="sxs-lookup"><span data-stu-id="9577e-153">Check email to verify that SendGrid sent the email.</span></span> <span data-ttu-id="9577e-154">Dovrebbe essere recapitata all'indirizzo inserito nel codice del passaggio 1 e dovrebbe contenere il messaggio del **Corpo della richiesta**.</span><span class="sxs-lookup"><span data-stu-id="9577e-154">It should go to the address in the code from step 1, and contain the message from the **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9577e-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9577e-155">Next steps</span></span>
<span data-ttu-id="9577e-156">In questo articolo è stato illustrato come usare il servizio SendGrid per creare e inviare email.</span><span class="sxs-lookup"><span data-stu-id="9577e-156">This article has demonstrated how to use the SendGrid service to create and send email.</span></span> <span data-ttu-id="9577e-157">Per altre informazioni sull'uso di Funzioni di Azure nelle app, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9577e-157">To learn more about using Azure Functions in your apps, see the following topics:</span></span> 

- <span data-ttu-id="9577e-158">L'articolo [Procedure consigliate per le funzioni di Azure](functions-best-practices.md) elenca alcune procedure consigliate da usare durante la creazione di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="9577e-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="9577e-159">La [guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md) contiene informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="9577e-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="9577e-160">[Test di Funzioni di Azure](functions-test-a-function.md) descrive diversi strumenti e tecniche per il test delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="9577e-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>