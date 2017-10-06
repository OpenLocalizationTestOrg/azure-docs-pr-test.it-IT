---
title: aaaAutomate Azure Application Insights elabora tramite App per la logica.
description: "Informazioni su come è possibile automatizzare rapidamente processi ripetibili aggiungendo hello Application Insights connettore tooyour logica app."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="1a9e7-103">Automatizzare i processi di Application Insights con app per la logica</span><span class="sxs-lookup"><span data-stu-id="1a9e7-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="1a9e7-104">È possibile trovare autonomamente ripetutamente in hello stesse query il toocheck di dati di telemetria se il servizio funziona correttamente?</span><span class="sxs-lookup"><span data-stu-id="1a9e7-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="1a9e7-105">Tooautomate esaminando queste query per individuare tendenze e anomalie e quindi compilare i propri flussi di lavoro attorno a esse? il connettore di Azure Application Insights Hello (anteprima) per App per la logica è strumento appropriato hello a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="1a9e7-106">Con questa integrazione è possibile automatizzare numerosi processi senza dover scrivere una sola riga di codice.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="1a9e7-107">È possibile creare un'app logica con Application Insights hello tooquickly connettore automatizzare qualsiasi processo di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="1a9e7-108">È possibile aggiungere anche altre azioni.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-108">You can add additional actions as well.</span></span> <span data-ttu-id="1a9e7-109">funzionalità di App per la logica di Hello di servizio App di Azure rende disponibili centinaia di azioni.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="1a9e7-110">Usando un'app per la logica, è ad esempio possibile inviare automaticamente una notifica di posta elettronica o creare un bug in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="1a9e7-111">È inoltre possibile utilizzare uno dei hello disponibili molti [modelli](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp velocizzare il processo di hello di creazione dell'applicazione di logica.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="1a9e7-112">Creare un app per la logica per Application Insights</span><span class="sxs-lookup"><span data-stu-id="1a9e7-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="1a9e7-113">In questa esercitazione viene illustrato come toocreate attributi di un'applicazione di logica che utilizza hello Analitica autocluster algoritmo toogroup nei dati di hello per un'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="1a9e7-114">flusso Hello invia automaticamente i risultati di hello tramite posta elettronica, solo un esempio di come è possibile utilizzare Application Insights Analitica e la logica App contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="1a9e7-115">Passaggio 1: Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="1a9e7-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="1a9e7-116">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1a9e7-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1a9e7-117">In hello **New** riquadro, selezionare **Web e dispositivi mobili**, quindi selezionare **logica App**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Finestra della nuova app per la logica](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="1a9e7-119">Passaggio 2: Creare un trigger per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="1a9e7-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="1a9e7-120">In hello **progettazione applicazione logica** finestra, in **iniziare con un trigger**selezionare **ricorrenza**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Finestra di progettazione di app per la logica](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="1a9e7-122">In hello **frequenza** , quindi selezionare **giorno** e quindi nel hello **intervallo** digitare **1**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    !["Ricorrenza" nella finestra Progettazione app per la logica](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="1a9e7-124">Passaggio 3: Aggiungere un'azione di Application Insights</span><span class="sxs-lookup"><span data-stu-id="1a9e7-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="1a9e7-125">Fare clic su **Nuovo passaggio** e quindi su **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="1a9e7-126">In hello **scegliere un'azione** nella casella di ricerca **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="1a9e7-127">Fare clic su **Application Insights - Visualize Analytics query Preview** (Application Insights - Visualizza query di Analisi Anteprima) in **Azioni**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    !["Scegliere un'azione" nella finestra Progettazione app per la logica](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="1a9e7-129">Passaggio 4: Connettere la risorsa di Application Insights tooan</span><span class="sxs-lookup"><span data-stu-id="1a9e7-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="1a9e7-130">toocomplete questo passaggio, è necessario un ID applicazione e una chiave API per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="1a9e7-131">È possibile recuperarli dal portale di Azure hello, come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![ID dell'applicazione nel portale di Azure hello](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="1a9e7-133">Specificare un nome per la connessione, un ID applicazione hello e una chiave API hello.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![Connessione per il flusso nella finestra Progettazione app per la logica](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="1a9e7-135">Passaggio 5: Specificare hello query Analitica e tipo di grafico</span><span class="sxs-lookup"><span data-stu-id="1a9e7-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="1a9e7-136">Nell'esempio seguente di hello, query hello Seleziona richieste hello non riuscito all'interno di hello ultimo giorno e li correla le eccezioni che si è verificato come parte dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="1a9e7-137">Analitica correla le richieste di hello non è riuscita, in base all'identificatore hello operation_Id.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="1a9e7-138">query Hello segmenti quindi risultati hello utilizzando l'algoritmo autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="1a9e7-139">Quando si crea la propria query, verificare che funzionino correttamente in Analitica prima di aggiungerlo tooyour flusso.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="1a9e7-140">In hello **Query** aggiungere hello query Analitica seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-140">In hello **Query** box, add hello following Analytics query:</span></span> 

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

2. <span data-ttu-id="1a9e7-141">In hello **tipo di grafico** , quindi selezionare **tabella Html**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Finestra di configurazione della query di Analisi](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="1a9e7-143">Passaggio 6: Configurare la posta elettronica toosend di hello logica app</span><span class="sxs-lookup"><span data-stu-id="1a9e7-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="1a9e7-144">Fare clic su **Nuovo passaggio** e selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="1a9e7-145">Nella casella di ricerca hello, digitare **Outlook di Office 365**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="1a9e7-146">Fare clic su **Office 365 Outlook - Send an email** (Office 365 Outlook: invia un messaggio di posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="1a9e7-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Selezione di Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="1a9e7-148">In hello **invia un messaggio di posta elettronica** finestra hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="1a9e7-149">a.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-149">a.</span></span> <span data-ttu-id="1a9e7-150">Digitare l'indirizzo di posta elettronica hello del destinatario hello.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="1a9e7-151">b.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-151">b.</span></span> <span data-ttu-id="1a9e7-152">Digitare un oggetto per la posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="1a9e7-153">c.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-153">c.</span></span> <span data-ttu-id="1a9e7-154">Fare clic nella hello **corpo** casella e quindi su hello contenuto menu dinamico che consente di aprire hello destro, selezionare **corpo**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="1a9e7-155">d.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-155">d.</span></span> <span data-ttu-id="1a9e7-156">Fare clic su **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-156">Click **Show advanced options**.</span></span>

      ![Configurazione di Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="1a9e7-158">Nel menu del contenuto dinamico hello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="1a9e7-159">a.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-159">a.</span></span> <span data-ttu-id="1a9e7-160">Selezionare **Nome allegato**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="1a9e7-161">b.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-161">b.</span></span> <span data-ttu-id="1a9e7-162">Selezionare **Contenuto allegato**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="1a9e7-163">c.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-163">c.</span></span> <span data-ttu-id="1a9e7-164">In hello **è HTML** , quindi selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Schermata di configurazione della posta elettronica di Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="1a9e7-166">Passaggio 7: Salvare e testare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="1a9e7-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="1a9e7-167">Fare clic su **salvare** toosave le modifiche.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="1a9e7-168">È possibile attendere hello trigger toorun hello logica app oppure è possibile eseguire immediatamente hello logica app selezionando **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![Schermata di creazione dell'app per la logica](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="1a9e7-170">Quando viene eseguita l'app logica, i destinatari di hello specificato nell'elenco di posta elettronica hello riceveranno un messaggio di posta elettronica simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![Messaggio di posta elettronica dell'app per la logica](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="1a9e7-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a9e7-172">Next steps</span></span>

- <span data-ttu-id="1a9e7-173">Altre informazioni sulla creazione di [query di Analisi](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="1a9e7-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="1a9e7-174">Altre informazioni su [App per la logica](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="1a9e7-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





