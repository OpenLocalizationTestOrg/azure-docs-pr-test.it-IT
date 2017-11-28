---
title: una funzione in Azure attivata da un webhook generico aaaCreate | Documenti Microsoft
description: Utilizzare le funzioni di Azure toocreate una funzione senza che viene richiamata da un webhook in Azure.
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 0a4868da91d216c8d20930ce7ec82eaa059c75ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a><span data-ttu-id="bb791-103">Creare una funzione attivata da un webhook generico</span><span class="sxs-lookup"><span data-stu-id="bb791-103">Create a function triggered by a generic webhook</span></span>

<span data-ttu-id="bb791-104">Funzioni di Azure consente di eseguire il codice in un ambiente senza server senza dover toofirst crea una macchina virtuale o si pubblica un'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="bb791-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="bb791-105">Ad esempio, è possibile configurare un toobe funzione attivata da un avviso generato dal monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb791-105">For example, you can configure a function toobe triggered by an alert raised by Azure Monitor.</span></span> <span data-ttu-id="bb791-106">Questo argomento viene illustrato come tooexecute c# il codice quando un gruppo di risorse è aggiunto tooyour sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bb791-106">This topic shows you how tooexecute C# code when a resource group is added tooyour subscription.</span></span>   

![Webhook generico attivata nel portale di Azure hello (funzione)](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a><span data-ttu-id="bb791-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb791-108">Prerequisites</span></span> 

<span data-ttu-id="bb791-109">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="bb791-109">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="bb791-110">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="bb791-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="bb791-111">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="bb791-111">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

<span data-ttu-id="bb791-112">Creare quindi una funzione in hello nuova funzione app.</span><span class="sxs-lookup"><span data-stu-id="bb791-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="bb791-113"><a name="create-function"></a>Creare una funzione attivata da un webhook generico</span><span class="sxs-lookup"><span data-stu-id="bb791-113"><a name="create-function"></a>Create a generic webhook triggered function</span></span>

1. <span data-ttu-id="bb791-114">Espandere l'applicazione di funzione e fare clic su hello  **+**  accanto troppo**funzioni**.</span><span class="sxs-lookup"><span data-stu-id="bb791-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="bb791-115">Se questa funzione è hello primo nell'app di funzione, selezionare **funzione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="bb791-115">If this function is hello first one in your function app, select **Custom function**.</span></span> <span data-ttu-id="bb791-116">Consente di visualizzare il set completo di hello dei modelli di funzione.</span><span class="sxs-lookup"><span data-stu-id="bb791-116">This displays hello complete set of function templates.</span></span>

    ![Pagina di avvio rapido di funzioni in hello portale di Azure](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="bb791-118">Seleziona hello **WebHook - generico c#** modello.</span><span class="sxs-lookup"><span data-stu-id="bb791-118">Select hello **Generic WebHook - C#** template.</span></span> <span data-ttu-id="bb791-119">Digitare un nome per la funzione C# e quindi selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bb791-119">Type a name for your C# function, then select **Create**.</span></span>

     ![Creare una funzione generica webhook attivato in hello portale di Azure](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. <span data-ttu-id="bb791-121">Nella nuova funzione, fare clic su **<> / Get funzione URL**, quindi copiare e salvare il valore di hello.</span><span class="sxs-lookup"><span data-stu-id="bb791-121">In your new function, click **</> Get function URL**, then copy and save hello value.</span></span> <span data-ttu-id="bb791-122">Utilizzare questo webhook hello tooconfigure di valore.</span><span class="sxs-lookup"><span data-stu-id="bb791-122">You use this value tooconfigure hello webhook.</span></span> 

    ![Esaminare il codice di funzione hello](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
<span data-ttu-id="bb791-124">Creare quindi un endpoint del webhook in un avviso del log attività in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb791-124">Next, you create a webhook endpoint in an activity log alert in Azure Monitor.</span></span> 

## <a name="create-an-activity-log-alert"></a><span data-ttu-id="bb791-125">Creare un avviso del log attività</span><span class="sxs-lookup"><span data-stu-id="bb791-125">Create an activity log alert</span></span>

1. <span data-ttu-id="bb791-126">Nel portale di Azure hello, passare toohello **monitoraggio** servizio, seleziona **avvisi**, fare clic su **Aggiungi avviso di log attività**.</span><span class="sxs-lookup"><span data-stu-id="bb791-126">In hello Azure portal, navigate toohello **Monitor** service, select **Alerts**, and click **Add activity log alert**.</span></span>   

    ![Monitorare](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. <span data-ttu-id="bb791-128">Utilizza le impostazioni di hello come specificato nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="bb791-128">Use hello settings as specified in hello table:</span></span>

    ![Creare un avviso del log attività](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | <span data-ttu-id="bb791-130">Impostazione</span><span class="sxs-lookup"><span data-stu-id="bb791-130">Setting</span></span>      |  <span data-ttu-id="bb791-131">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="bb791-131">Suggested value</span></span>   | <span data-ttu-id="bb791-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bb791-132">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="bb791-133">**Nome avviso del log attività**</span><span class="sxs-lookup"><span data-stu-id="bb791-133">**Activity log alert name**</span></span> | <span data-ttu-id="bb791-134">resource-group-create-alert</span><span class="sxs-lookup"><span data-stu-id="bb791-134">resource-group-create-alert</span></span> | <span data-ttu-id="bb791-135">Nome dell'avviso di log attività hello.</span><span class="sxs-lookup"><span data-stu-id="bb791-135">Name of hello activity log alert.</span></span> |
    | <span data-ttu-id="bb791-136">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="bb791-136">**Subscription**</span></span> | <span data-ttu-id="bb791-137">Sottoscrizione in uso</span><span class="sxs-lookup"><span data-stu-id="bb791-137">Your subscription</span></span> | <span data-ttu-id="bb791-138">sottoscrizione di Hello in uso per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bb791-138">hello subscription you are using for this tutorial.</span></span> | 
    |  <span data-ttu-id="bb791-139">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="bb791-139">**Resource Group**</span></span> | <span data-ttu-id="bb791-140">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bb791-140">myResourceGroup</span></span> | <span data-ttu-id="bb791-141">gruppo di risorse Hello risorse avviso hello distribuiti.</span><span class="sxs-lookup"><span data-stu-id="bb791-141">hello resource group that hello alert resources are deployed to.</span></span> <span data-ttu-id="bb791-142">Utilizzando hello stesso gruppo di risorse, come l'app di funzione rende più semplice tooclean dopo aver completato l'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="bb791-142">Using hello same resource group as your function app makes it easier tooclean up after you complete hello tutorial.</span></span> |
    | <span data-ttu-id="bb791-143">**Categoria evento**</span><span class="sxs-lookup"><span data-stu-id="bb791-143">**Event category**</span></span> | <span data-ttu-id="bb791-144">Amministrativo</span><span class="sxs-lookup"><span data-stu-id="bb791-144">Administrative</span></span> | <span data-ttu-id="bb791-145">Questa categoria include le modifiche apportate alle risorse tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bb791-145">This category includes changes made tooAzure resources.</span></span>  |
    | <span data-ttu-id="bb791-146">**Tipo di risorsa**</span><span class="sxs-lookup"><span data-stu-id="bb791-146">**Resource type**</span></span> | <span data-ttu-id="bb791-147">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="bb791-147">Resource groups</span></span> | <span data-ttu-id="bb791-148">Consente di filtrare le attività di gruppo tooresource gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="bb791-148">Filters alerts tooresource group activities.</span></span> |
    | <span data-ttu-id="bb791-149">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="bb791-149">**Resource Group**</span></span><br/><span data-ttu-id="bb791-150">e **Risorsa**</span><span class="sxs-lookup"><span data-stu-id="bb791-150">and **Resource**</span></span> | <span data-ttu-id="bb791-151">Tutti</span><span class="sxs-lookup"><span data-stu-id="bb791-151">All</span></span> | <span data-ttu-id="bb791-152">Vengono monitorate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="bb791-152">Monitor all resources.</span></span> |
    | <span data-ttu-id="bb791-153">**Nome operazione**</span><span class="sxs-lookup"><span data-stu-id="bb791-153">**Operation name**</span></span> | <span data-ttu-id="bb791-154">Crea gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="bb791-154">Create Resource Group</span></span> | <span data-ttu-id="bb791-155">Filtra le operazioni di toocreate gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="bb791-155">Filters alerts toocreate operations.</span></span> |
    | <span data-ttu-id="bb791-156">**Level**</span><span class="sxs-lookup"><span data-stu-id="bb791-156">**Level**</span></span> | <span data-ttu-id="bb791-157">Informazioni</span><span class="sxs-lookup"><span data-stu-id="bb791-157">Informational</span></span> | <span data-ttu-id="bb791-158">Vengono inclusi gli avvisi di livello informativo.</span><span class="sxs-lookup"><span data-stu-id="bb791-158">Include informational level alerts.</span></span> | 
    | <span data-ttu-id="bb791-159">**Status**</span><span class="sxs-lookup"><span data-stu-id="bb791-159">**Status**</span></span> | <span data-ttu-id="bb791-160">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="bb791-160">Succeeded</span></span> | <span data-ttu-id="bb791-161">Filtra tooactions gli avvisi che sono stati completati correttamente.</span><span class="sxs-lookup"><span data-stu-id="bb791-161">Filters alerts tooactions that have completed successfully.</span></span> |
    | <span data-ttu-id="bb791-162">**Gruppo di azione**</span><span class="sxs-lookup"><span data-stu-id="bb791-162">**Action group**</span></span> | <span data-ttu-id="bb791-163">Nuovo</span><span class="sxs-lookup"><span data-stu-id="bb791-163">New</span></span> | <span data-ttu-id="bb791-164">Creare un nuovo gruppo di azione, che definisce accetta azione hello quando viene generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="bb791-164">Create a new action group, which defines hello action takes when an alert is raised.</span></span> |
    | <span data-ttu-id="bb791-165">**Nome gruppo di azione**</span><span class="sxs-lookup"><span data-stu-id="bb791-165">**Action group name**</span></span> | <span data-ttu-id="bb791-166">function-webhook</span><span class="sxs-lookup"><span data-stu-id="bb791-166">function-webhook</span></span> | <span data-ttu-id="bb791-167">Un gruppo di azioni di hello tooidentify nome.</span><span class="sxs-lookup"><span data-stu-id="bb791-167">A name tooidentify hello action group.</span></span>  | 
    | <span data-ttu-id="bb791-168">**Nome breve**</span><span class="sxs-lookup"><span data-stu-id="bb791-168">**Short name**</span></span> | <span data-ttu-id="bb791-169">funcwebhook</span><span class="sxs-lookup"><span data-stu-id="bb791-169">funcwebhook</span></span> | <span data-ttu-id="bb791-170">Un nome breve per il gruppo di azioni di hello.</span><span class="sxs-lookup"><span data-stu-id="bb791-170">A short name for hello action group.</span></span> |  

3. <span data-ttu-id="bb791-171">In **azioni**, aggiungere un'azione utilizzando le impostazioni di hello come specificato nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="bb791-171">In **Actions**, add an action using hello settings as specified in hello table:</span></span> 

    ![Aggiungere un gruppo di azione](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | <span data-ttu-id="bb791-173">Impostazione</span><span class="sxs-lookup"><span data-stu-id="bb791-173">Setting</span></span>      |  <span data-ttu-id="bb791-174">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="bb791-174">Suggested value</span></span>   | <span data-ttu-id="bb791-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bb791-175">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="bb791-176">**Nome**</span><span class="sxs-lookup"><span data-stu-id="bb791-176">**Name**</span></span> | <span data-ttu-id="bb791-177">CallFunctionWebhook</span><span class="sxs-lookup"><span data-stu-id="bb791-177">CallFunctionWebhook</span></span> | <span data-ttu-id="bb791-178">Un nome per l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="bb791-178">A name for hello action.</span></span> |
    | <span data-ttu-id="bb791-179">**Tipo di azione**</span><span class="sxs-lookup"><span data-stu-id="bb791-179">**Action type**</span></span> | <span data-ttu-id="bb791-180">webhook</span><span class="sxs-lookup"><span data-stu-id="bb791-180">Webhook</span></span> | <span data-ttu-id="bb791-181">avviso di toohello risposta Hello è che viene chiamato un URL del Webhook.</span><span class="sxs-lookup"><span data-stu-id="bb791-181">hello response toohello alert is that a Webhook URL is called.</span></span> |
    | <span data-ttu-id="bb791-182">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="bb791-182">**Details**</span></span> | <span data-ttu-id="bb791-183">URL della funzione</span><span class="sxs-lookup"><span data-stu-id="bb791-183">Function URL</span></span> | <span data-ttu-id="bb791-184">Incollare nell'URL del webhook hello della funzione hello copiato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bb791-184">Paste in hello webhook URL of hello function that you copied earlier.</span></span> |<span data-ttu-id="bb791-185">v</span><span class="sxs-lookup"><span data-stu-id="bb791-185">v</span></span>

4. <span data-ttu-id="bb791-186">Fare clic su **OK** toocreate hello avviso e azione il gruppo.</span><span class="sxs-lookup"><span data-stu-id="bb791-186">Click **OK** toocreate hello alert and action group.</span></span>  

<span data-ttu-id="bb791-187">Hello webhook ora viene chiamato quando viene creato un gruppo di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bb791-187">hello webhook is now called when a resource group is created in your subscription.</span></span> <span data-ttu-id="bb791-188">Aggiornare quindi il codice hello nel hello toohandle funzione dati del log JSON nel corpo di hello di hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="bb791-188">Next, you update hello code in your function toohandle hello JSON log data in hello body of hello request.</span></span>   

## <a name="update-hello-function-code"></a><span data-ttu-id="bb791-189">Aggiornare il codice di funzione hello</span><span class="sxs-lookup"><span data-stu-id="bb791-189">Update hello function code</span></span>

1. <span data-ttu-id="bb791-190">Spostarsi indietro tooyour funzione app nel portale di hello ed espandere la funzione.</span><span class="sxs-lookup"><span data-stu-id="bb791-190">Navigate back tooyour function app in hello portal, and expand your function.</span></span> 

2. <span data-ttu-id="bb791-191">Sostituire il codice di script c# hello nella funzione hello nel portale di hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="bb791-191">Replace hello C# script code in hello function in hello portal with hello following code:</span></span>

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get hello activityLog object from hello JSON in hello message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if hello resource in hello activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about hello created resource group toohello streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

<span data-ttu-id="bb791-192">Ora è possibile testare la funzione hello creando un nuovo gruppo di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="bb791-192">Now you can test hello function by creating a new resource group in your subscription.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="bb791-193">Funzione hello test</span><span class="sxs-lookup"><span data-stu-id="bb791-193">Test hello function</span></span>

1. <span data-ttu-id="bb791-194">Fare clic sull'icona di gruppo di risorse hello in a sinistra del portale di Azure selezionare hello hello **+ Aggiungi**, digitare un **nome gruppo di risorse**e selezionare **crea** toocreate un gruppo di risorse vuoto.</span><span class="sxs-lookup"><span data-stu-id="bb791-194">Click hello resource group icon in hello left of hello Azure portal, select **+ Add**, type a **Resource group name**, and select **Create** toocreate an empty resource group.</span></span>
    
    ![Creare un gruppo di risorse.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. <span data-ttu-id="bb791-196">Funzione tooyour torna indietro ed espandere hello **registri** finestra.</span><span class="sxs-lookup"><span data-stu-id="bb791-196">Go back tooyour function and expand hello **Logs** window.</span></span> <span data-ttu-id="bb791-197">Dopo aver creato il gruppo di risorse hello, i trigger di avviso log attività hello hello webhook ed esegue la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="bb791-197">After hello resource group is created, hello activity log alert triggers hello webhook and hello function executes.</span></span> <span data-ttu-id="bb791-198">Nome di hello di hello nuovo gruppo di risorse toohello log scritto è visualizzato.</span><span class="sxs-lookup"><span data-stu-id="bb791-198">You see hello name of hello new resource group written toohello logs.</span></span>  

    ![Aggiungere un'impostazione dell'applicazione di test.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. <span data-ttu-id="bb791-200">(Facoltativo) Tornare indietro ed eliminare il gruppo di risorse hello creato.</span><span class="sxs-lookup"><span data-stu-id="bb791-200">(Optional) Go back and delete hello resource group that you created.</span></span> <span data-ttu-id="bb791-201">Si noti che questa attività non attiva la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="bb791-201">Note that this activity doesn't trigger hello function.</span></span> <span data-ttu-id="bb791-202">Infatti, le operazioni vengono filtrate da avviso hello di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="bb791-202">This is because delete operations are filtered out by hello alert.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="bb791-203">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="bb791-203">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="bb791-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb791-204">Next steps</span></span>

<span data-ttu-id="bb791-205">È stata creata una funzione che viene eseguita quando viene ricevuta una richiesta da un webhook generico.</span><span class="sxs-lookup"><span data-stu-id="bb791-205">You have created a function that runs when a request is received from a generic webhook.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="bb791-206">Per altre informazioni sui trigger webhook, vedere [Associazioni HTTP e webhook in Funzioni di Azure](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="bb791-206">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span> <span data-ttu-id="bb791-207">toolearn più sullo sviluppo di funzioni in c#, vedere [riferimenti per sviluppatori di script c# Azure funzioni](functions-reference-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="bb791-207">toolearn more about developing functions in C#, see [Azure Functions C# script developer reference](functions-reference-csharp.md).</span></span>

