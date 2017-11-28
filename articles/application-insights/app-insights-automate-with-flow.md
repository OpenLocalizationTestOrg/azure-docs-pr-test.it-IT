---
title: i processi di Azure Application Insights aaaAutomate con Microsoft Flow
description: Informazioni su come utilizzare Microsoft Flow tooquickly automatizzare i processi ripetibili utilizzando il connettore di Application Insights hello.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="96b09-103">Automatizzare i processi di Azure Application Insights con connettore hello per Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="96b09-103">Automate Azure Application Insights processes with hello connector for Microsoft Flow</span></span>

<span data-ttu-id="96b09-104">È possibile trovare autonomamente ripetutamente in hello stesse query il toocheck di dati di telemetria che il servizio funziona correttamente?</span><span class="sxs-lookup"><span data-stu-id="96b09-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck that your service is functioning properly?</span></span> <span data-ttu-id="96b09-105">Tooautomate esaminando queste query per individuare tendenze e anomalie e quindi compilare i propri flussi di lavoro attorno a esse? il connettore di Azure Application Insights Hello (anteprima) per Microsoft Flow è strumento appropriato hello per questi scopi.</span><span class="sxs-lookup"><span data-stu-id="96b09-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Microsoft Flow is hello right tool for these purposes.</span></span>

<span data-ttu-id="96b09-106">Con questa integrazione è ora possibile automatizzare numerosi processi senza dover scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="96b09-106">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="96b09-107">Dopo aver creato un flusso utilizzando un'azione di Application Insights, flusso hello esegue automaticamente la query di Application Insights Analitica.</span><span class="sxs-lookup"><span data-stu-id="96b09-107">After you create a flow by using an Application Insights action, hello flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="96b09-108">È possibile aggiungere anche altre azioni.</span><span class="sxs-lookup"><span data-stu-id="96b09-108">You can add additional actions as well.</span></span> <span data-ttu-id="96b09-109">In Microsoft Flow sono disponibili centinaia di azioni.</span><span class="sxs-lookup"><span data-stu-id="96b09-109">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="96b09-110">Ad esempio, è possibile utilizzare Microsoft Flow tooautomatically invia una notifica tramite e-mail o creare un bug in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="96b09-110">For example, you can use Microsoft Flow tooautomatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="96b09-111">È inoltre possibile utilizzare uno dei hello molti [modelli](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) che sono disponibili per il connettore di hello per Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="96b09-111">You can also use one of hello many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for hello connector for Microsoft Flow.</span></span> <span data-ttu-id="96b09-112">Aumento della velocità questi modelli di processo hello di creazione di un flusso.</span><span class="sxs-lookup"><span data-stu-id="96b09-112">These templates speed up hello process of creating a flow.</span></span> 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="96b09-113">Creare un flusso per Application Insights</span><span class="sxs-lookup"><span data-stu-id="96b09-113">Create a flow for Application Insights</span></span>

<span data-ttu-id="96b09-114">In questa esercitazione si apprenderà come toocreate attributi di un flusso che utilizza hello Analitica automatica cluster algoritmo toogroup nei dati di hello per un'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="96b09-114">In this tutorial, you will learn how toocreate a flow that uses hello Analytics auto-cluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="96b09-115">flusso Hello invia automaticamente i risultati di hello tramite posta elettronica, solo un esempio di come è possibile utilizzare Microsoft Flow e Application Insights Analitica contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="96b09-115">hello flow automatically sends hello results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="96b09-116">Passaggio 1: Creare un flusso</span><span class="sxs-lookup"><span data-stu-id="96b09-116">Step 1: Create a flow</span></span>
1. <span data-ttu-id="96b09-117">Accedi troppo[Microsoft Flow](http://flow.microsoft.com), quindi selezionare **flussi My**.</span><span class="sxs-lookup"><span data-stu-id="96b09-117">Sign in too[Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="96b09-118">Fare clic su **Crea un flusso da un modello vuoto**.</span><span class="sxs-lookup"><span data-stu-id="96b09-118">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="96b09-119">Passaggio 2: Creare un trigger per il flusso</span><span class="sxs-lookup"><span data-stu-id="96b09-119">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="96b09-120">Selezionare **Pianificazione** e quindi selezionare **Pianificazione - Ricorrenza**.</span><span class="sxs-lookup"><span data-stu-id="96b09-120">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="96b09-121">In hello **frequenza** , quindi selezionare **giorno**e in hello **intervallo** immettere **1**.</span><span class="sxs-lookup"><span data-stu-id="96b09-121">In hello **Frequency** box, select **Day**, and in hello **Interval** box, enter **1**.</span></span>

    ![Finestra di dialogo del trigger di Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="96b09-123">Passaggio 3: Aggiungere un'azione di Application Insights</span><span class="sxs-lookup"><span data-stu-id="96b09-123">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="96b09-124">Fare clic su **Nuovo passaggio** e quindi su **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="96b09-124">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="96b09-125">Cercare **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="96b09-125">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="96b09-126">Fare clic su **Application Insights - Visualize Analytics query Preview** (Application Insights - Visualizza query di Analisi Anteprima).</span><span class="sxs-lookup"><span data-stu-id="96b09-126">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Finestra di esecuzione della query di Analisi](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="96b09-128">Passaggio 4: Connettere la risorsa di Application Insights tooan</span><span class="sxs-lookup"><span data-stu-id="96b09-128">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="96b09-129">toocomplete questo passaggio, è necessario un ID applicazione e una chiave API per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="96b09-129">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="96b09-130">È possibile recuperarli dal portale di Azure hello, come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="96b09-130">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![ID dell'applicazione nel portale di Azure hello](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="96b09-132">Specificare un nome per la connessione, insieme a hello applicazione ID e la chiave API.</span><span class="sxs-lookup"><span data-stu-id="96b09-132">Provide a name for your connection, along with hello application ID and API key.</span></span>

    ![Finestra di connessione di Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="96b09-134">Passaggio 5: Specificare hello query Analitica e tipo di grafico</span><span class="sxs-lookup"><span data-stu-id="96b09-134">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="96b09-135">Questo esempio di query Seleziona le richieste di hello non riuscito all'interno di hello ultimo giorno e li correla le eccezioni che si è verificato come parte dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="96b09-135">This example query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="96b09-136">Analitica li correla in base all'identificatore hello operation_Id.</span><span class="sxs-lookup"><span data-stu-id="96b09-136">Analytics correlates them based on hello operation_Id identifier.</span></span> <span data-ttu-id="96b09-137">query Hello segmenti quindi risultati hello utilizzando l'algoritmo autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="96b09-137">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="96b09-138">Quando si crea la propria query, verificare che funzionino correttamente in Analitica prima di aggiungerlo tooyour flusso.</span><span class="sxs-lookup"><span data-stu-id="96b09-138">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

- <span data-ttu-id="96b09-139">Aggiungere hello seguente query Analitica e quindi selezionare tipo di grafico di tabella HTML hello.</span><span class="sxs-lookup"><span data-stu-id="96b09-139">Add hello following Analytics query, and then select hello HTML table chart type.</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Finestra di configurazione della query di Analisi](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a><span data-ttu-id="96b09-141">Passaggio 6: Configurare la posta elettronica di toosend flusso hello</span><span class="sxs-lookup"><span data-stu-id="96b09-141">Step 6: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="96b09-142">Fare clic su **Nuovo passaggio** e quindi su **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="96b09-142">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="96b09-143">Cercare **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="96b09-143">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="96b09-144">Fare clic su **Office 365 Outlook - Invia un messaggio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="96b09-144">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Finestra di selezione di Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="96b09-146">In hello **invia un messaggio di posta elettronica** finestra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="96b09-146">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="96b09-147">a.</span><span class="sxs-lookup"><span data-stu-id="96b09-147">a.</span></span> <span data-ttu-id="96b09-148">Digitare l'indirizzo di posta elettronica hello del destinatario hello.</span><span class="sxs-lookup"><span data-stu-id="96b09-148">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="96b09-149">b.</span><span class="sxs-lookup"><span data-stu-id="96b09-149">b.</span></span> <span data-ttu-id="96b09-150">Digitare un oggetto per la posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="96b09-150">Type a subject for hello email.</span></span>

   <span data-ttu-id="96b09-151">c.</span><span class="sxs-lookup"><span data-stu-id="96b09-151">c.</span></span> <span data-ttu-id="96b09-152">Fare clic nella hello **corpo** casella e quindi su hello contenuto menu dinamico che consente di aprire hello destro, selezionare **corpo**.</span><span class="sxs-lookup"><span data-stu-id="96b09-152">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="96b09-153">d.</span><span class="sxs-lookup"><span data-stu-id="96b09-153">d.</span></span> <span data-ttu-id="96b09-154">Fare clic su **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="96b09-154">Click **Show advanced options**.</span></span>

    ![Configurazione di Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="96b09-156">Nel menu del contenuto dinamico hello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="96b09-156">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="96b09-157">a.</span><span class="sxs-lookup"><span data-stu-id="96b09-157">a.</span></span> <span data-ttu-id="96b09-158">Selezionare **Nome allegato**.</span><span class="sxs-lookup"><span data-stu-id="96b09-158">Select **Attachment Name**.</span></span>

    <span data-ttu-id="96b09-159">b.</span><span class="sxs-lookup"><span data-stu-id="96b09-159">b.</span></span> <span data-ttu-id="96b09-160">Selezionare **Contenuto allegato**.</span><span class="sxs-lookup"><span data-stu-id="96b09-160">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="96b09-161">c.</span><span class="sxs-lookup"><span data-stu-id="96b09-161">c.</span></span> <span data-ttu-id="96b09-162">In hello **è HTML** , quindi selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="96b09-162">In hello **Is HTML** box, select **Yes**.</span></span>

    ![Finestra di configurazione della posta elettronica di Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="96b09-164">Passaggio 7: Salvare e testare il flusso</span><span class="sxs-lookup"><span data-stu-id="96b09-164">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="96b09-165">In hello **nome flusso** casella, aggiungere un nome per il flusso e quindi fare clic su **creare flusso**.</span><span class="sxs-lookup"><span data-stu-id="96b09-165">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Finestra di creazione del flusso](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="96b09-167">È possibile attendere hello trigger toorun questa azione, o è possibile eseguire immediatamente dal flusso hello [trigger hello in esecuzione su richiesta](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="96b09-167">You can wait for hello trigger toorun this action, or you can run hello flow immediately by [running hello trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="96b09-168">Quando viene eseguito il flusso di hello, i destinatari hello che è stato specificato nell'elenco di posta elettronica hello visualizzato un messaggio di posta elettronica simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="96b09-168">When hello flow runs, hello recipients you have specified in hello email list receive an email message that looks like hello following:</span></span>

![Esempio di messaggio di posta elettronica](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="96b09-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="96b09-170">Next steps</span></span>

- <span data-ttu-id="96b09-171">Altre informazioni sulla creazione di [query di Analisi](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="96b09-171">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="96b09-172">Altre informazioni su [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="96b09-172">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





