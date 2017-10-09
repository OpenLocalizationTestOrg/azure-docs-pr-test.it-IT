---
title: aaaHow toouse SendGrid nelle funzioni di Azure | Documenti Microsoft
description: Viene illustrato come toouse SendGrid nelle funzioni di Azure
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
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a><span data-ttu-id="90998-103">Come toouse SendGrid nelle funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="90998-103">How toouse SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="90998-104">Panoramica di SendGrid</span><span class="sxs-lookup"><span data-stu-id="90998-104">SendGrid Overview</span></span>

<span data-ttu-id="90998-105">Azure supporta funzioni SendGrid output associazioni tooenable i messaggi di posta elettronica toosend funzioni con poche righe di codice e un account di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="90998-105">Azure Functions supports SendGrid output bindings tooenable your functions toosend email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="90998-106">API di SendGrid toouse hello in una funzione di Azure, è necessario disporre di un [account SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="90998-106">toouse hello SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="90998-107">Inoltre, è necessario disporre di una chiave dell'API di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="90998-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="90998-108">Accedi tooyour account SendGrid e fare clic su **impostazioni** quindi **chiave API** chiave toogenerate un'API.</span><span class="sxs-lookup"><span data-stu-id="90998-108">Log in tooyour SendGrid account and click **Settings** then **API Key** toogenerate an API key.</span></span> <span data-ttu-id="90998-109">Fare in modo che questa chiave sia disponibile per l'uso nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="90998-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="90998-110">Si è ora pronto toocreate un'app di Azure (funzione).</span><span class="sxs-lookup"><span data-stu-id="90998-110">You are now ready toocreate an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="90998-111">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="90998-111">Create an Azure Function app</span></span> 

<span data-ttu-id="90998-112">Le app per le funzioni di Azure sono contenitori per uno o più funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="90998-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="90998-113">Le funzioni di Azure sono solo delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="90998-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="90998-114">Ogni funzione di Azure è abbinato tooone trigger, che è un evento che causa toorun funzione hello.</span><span class="sxs-lookup"><span data-stu-id="90998-114">Each Azure function is tied tooone trigger, which is an event that causes hello function toorun.</span></span>
<span data-ttu-id="90998-115">Ogni funzione può contenere diverse associazioni di input oppure output.</span><span class="sxs-lookup"><span data-stu-id="90998-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="90998-116">Le associazioni sono servizi che è possibile usare in una funzione.</span><span class="sxs-lookup"><span data-stu-id="90998-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="90998-117">SendGrid è un output di associazione è possibile utilizzare posta elettronica toosend.</span><span class="sxs-lookup"><span data-stu-id="90998-117">SendGrid is an output binding you can use toosend email.</span></span> 

1. <span data-ttu-id="90998-118">Accedi al portale di Azure toohello e [creare un'App di Azure funzione](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) oppure aprire un'app di funzione esistente.</span><span class="sxs-lookup"><span data-stu-id="90998-118">Log in toohello Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="90998-119">Creare una funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="90998-119">Create an Azure function.</span></span> <span data-ttu-id="90998-120">tookeep è semplice, scegliere un trigger manuale e c#.</span><span class="sxs-lookup"><span data-stu-id="90998-120">tookeep it simple, choose a manual trigger and C#.</span></span> 

 ![Creare una funzione di Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="90998-122">Configurare SendGrid per l'uso in un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="90998-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="90998-123">È necessario archiviare la chiave API SendGrid come un toouse impostazione app in una funzione.</span><span class="sxs-lookup"><span data-stu-id="90998-123">You must store your SendGrid API Key as an app setting toouse it in a function.</span></span> <span data-ttu-id="90998-124">campo di Hello ApiKey non è la chiave API SendGrid effettiva, ma un'impostazione di app definire che rappresenta la chiave API effettiva.</span><span class="sxs-lookup"><span data-stu-id="90998-124">hello ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="90998-125">Per sicurezza si esegue questo tipo di archiviazione della chiave, poiché è separata da qualsiasi codice o file che potrebbe essere archiviato nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="90998-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="90998-126">Creare una chiave **AppSettings** in **Impostazioni applicazione** dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="90998-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Creare una funzione di Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="90998-128">Configurare le associazioni di output di SendGrid</span><span class="sxs-lookup"><span data-stu-id="90998-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="90998-129">SendGrid è disponibile come associazione di output della funzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="90998-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="90998-130">associazione di output toocreate un SendGrid:</span><span class="sxs-lookup"><span data-stu-id="90998-130">toocreate a SendGrid output binding:</span></span>

1. <span data-ttu-id="90998-131">Passare toohello **integrazione** scheda della funzione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="90998-131">Go toohello **Integrate** tab of hello function in hello Azure portal.</span></span>
2. <span data-ttu-id="90998-132">Fare clic su **nuovo Output** toocreate un SendGrid associazione di output.</span><span class="sxs-lookup"><span data-stu-id="90998-132">Click **New Output** toocreate a SendGrid output binding.</span></span>
3. <span data-ttu-id="90998-133">Compilare hello **chiave API** e **nome del parametro messaggio** proprietà.</span><span class="sxs-lookup"><span data-stu-id="90998-133">Fill in hello **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="90998-134">Se si desidera, è possibile immettere hello ora altre proprietà, o le code invece.</span><span class="sxs-lookup"><span data-stu-id="90998-134">If you want, you can enter hello other properties now, or code them instead.</span></span> <span data-ttu-id="90998-135">Queste impostazioni possono essere usate come impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="90998-135">These settings can be used as defaults.</span></span>

 ![Configurare le associazioni di output di SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="90998-137">Aggiunta di una funzione di tooa associazione crea un file denominato **function.json** nella cartella della funzione.</span><span class="sxs-lookup"><span data-stu-id="90998-137">Adding a binding tooa function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="90998-138">Questo file contiene tutti hello stesse informazioni, vedere in hello Azure funzione **integrazione** scheda, ma in Json formato.</span><span class="sxs-lookup"><span data-stu-id="90998-138">This file contains all hello same information that you see in hello Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="90998-139">Hello impostazione **ApiKey**, **messaggio**, e **da** campi creano hello seguenti voci hello **function.json** file:</span><span class="sxs-lookup"><span data-stu-id="90998-139">Setting hello **ApiKey**, **message**, and **from** fields create hello following entries in hello **function.json** file:</span></span> 

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

<span data-ttu-id="90998-140">Se lo si preferisce, è possibile modificare direttamente questo file.</span><span class="sxs-lookup"><span data-stu-id="90998-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="90998-141">Ora che è creato e configurato hello App di funzione e la funzione, è possibile scrivere un messaggio di posta elettronica toosend codice hello.</span><span class="sxs-lookup"><span data-stu-id="90998-141">Now that you have created and configured hello Function App and function, you can write hello code toosend an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="90998-142">Scrivere il codice che crea e invia email</span><span class="sxs-lookup"><span data-stu-id="90998-142">Write code that creates and sends email</span></span>

<span data-ttu-id="90998-143">Hello API SendGrid contiene tutti i comandi hello è necessario toocreate e inviare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="90998-143">hello SendGrid API contains all hello commands you need toocreate and send an email.</span></span>  

- <span data-ttu-id="90998-144">Sostituire il codice di hello nella funzione hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="90998-144">Replace hello code in hello function with hello following code:</span></span>

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
    // change tooemail of recipient
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

<span data-ttu-id="90998-145">Si noti hello prima riga contiene hello ```#r``` direttiva che fa riferimento all'assembly SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="90998-145">Notice hello first line contains hello ```#r``` directive that references hello SendGrid assembly.</span></span> <span data-ttu-id="90998-146">Successivamente, è possibile utilizzare un ```using``` toomore istruzione accedere facilmente agli oggetti di hello nello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="90998-146">After that, you can use a ```using``` statement toomore easily access hello objects in that namespace.</span></span> <span data-ttu-id="90998-147">Nel codice hello, creare istanze di ```Mail```, ```Personalization```, e ```Content``` oggetti hello API SendGrid che compongono e-mail hello.</span><span class="sxs-lookup"><span data-stu-id="90998-147">In hello code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from hello SendGrid API that compose hello email.</span></span> <span data-ttu-id="90998-148">Quando viene restituito il messaggio hello, SendGrid lo recapita.</span><span class="sxs-lookup"><span data-stu-id="90998-148">When you return hello message, SendGrid delivers it.</span></span> 

<span data-ttu-id="90998-149">Hello firma della funzione contiene inoltre un ulteriore parametro di tipo out ```Mail``` denominato ```message```.</span><span class="sxs-lookup"><span data-stu-id="90998-149">hello function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="90998-150">Le associazioni di input e output si esprimono come parametri di funzione nel codice.</span><span class="sxs-lookup"><span data-stu-id="90998-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="90998-151">Testare il codice facendo clic su **Test** e provochi un messaggio hello **corpo della richiesta** campo, quindi fare clic su hello **eseguire** pulsante.</span><span class="sxs-lookup"><span data-stu-id="90998-151">Test your code by clicking **Test** and entering a message into hello **Request body** field, then clicking hello **Run** button.</span></span>

 ![Testare il codice](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="90998-153">Verificare che SendGrid inviato tramite posta elettronica hello tooverify di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="90998-153">Check email tooverify that SendGrid sent hello email.</span></span> <span data-ttu-id="90998-154">E deve passare toohello indirizzo nel codice hello dal passaggio 1 e contiene il messaggio hello da hello **corpo della richiesta**.</span><span class="sxs-lookup"><span data-stu-id="90998-154">It should go toohello address in hello code from step 1, and contain hello message from hello **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90998-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90998-155">Next steps</span></span>
<span data-ttu-id="90998-156">In questo articolo ha dimostrato come toouse hello toocreate servizio SendGrid e inviare posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="90998-156">This article has demonstrated how toouse hello SendGrid service toocreate and send email.</span></span> <span data-ttu-id="90998-157">toolearn ulteriori informazioni sull'utilizzo delle funzioni di Azure nelle app di Windows, vedere hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="90998-157">toolearn more about using Azure Functions in your apps, see hello following topics:</span></span> 

- <span data-ttu-id="90998-158">[Procedure consigliate per le funzioni di Azure](functions-best-practices.md) sono elencate alcune procedure toouse di procedure consigliate durante la creazione di funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="90998-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="90998-159">La [guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md) contiene informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="90998-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="90998-160">[Test di Funzioni di Azure](functions-test-a-function.md) descrive diversi strumenti e tecniche per il test delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="90998-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>