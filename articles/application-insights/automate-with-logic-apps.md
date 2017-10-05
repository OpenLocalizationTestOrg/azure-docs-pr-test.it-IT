---
title: Automatizzare i processi di Azure Application Insights con app per la logica.
description: Informazioni su come automatizzare in poco tempo i processi ripetibili aggiungendo il connettore di Application Insights all'app per la logica.
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
ms.openlocfilehash: 36df5bc0a019f4197d40fd6fa5a2a9957820c8b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="8a0ff-103">Automatizzare i processi di Application Insights con app per la logica</span><span class="sxs-lookup"><span data-stu-id="8a0ff-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="8a0ff-104">Ci si trova spesso a eseguire ripetutamente le stesse query sui dati di telemetria per verificare il corretto funzionamento del servizio?</span><span class="sxs-lookup"><span data-stu-id="8a0ff-104">Do you find yourself repeatedly running the same queries on your telemetry data to check whether your service is functioning properly?</span></span> <span data-ttu-id="8a0ff-105">Si vuole automatizzare queste query per trovare tendenze e anomalie e creare quindi flussi di lavoro basati su queste informazioni?</span><span class="sxs-lookup"><span data-stu-id="8a0ff-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="8a0ff-106">Il connettore di Azure Application Insights (anteprima) per le app per la logica è lo strumento ideale.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-106">The Azure Application Insights connector (preview) for Logic Apps is the right tool for this purpose.</span></span>

<span data-ttu-id="8a0ff-107">Con questa integrazione è possibile automatizzare numerosi processi senza dover scrivere una sola riga di codice.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-107">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="8a0ff-108">È possibile creare un'app per la logica con il connettore di Application Insights per automatizzare rapidamente qualsiasi processo di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-108">You can create a logic app with the Application Insights connector to quickly automate any Application Insights process.</span></span> 

<span data-ttu-id="8a0ff-109">È possibile aggiungere anche altre azioni.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-109">You can add additional actions as well.</span></span> <span data-ttu-id="8a0ff-110">App per la logica è una funzione del Servizio app di Azure che offre centinaia di azioni.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-110">The Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="8a0ff-111">Usando un'app per la logica, è ad esempio possibile inviare automaticamente una notifica di posta elettronica o creare un bug in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-111">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="8a0ff-112">È anche possibile usare uno dei numerosi [modelli](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) disponibili per velocizzare il processo di creazione dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-112">You can also use one of the many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) to help speed up the process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="8a0ff-113">Creare un app per la logica per Application Insights</span><span class="sxs-lookup"><span data-stu-id="8a0ff-113">Create a logic app for Application Insights</span></span>

<span data-ttu-id="8a0ff-114">Questa esercitazione illustra come creare un'app per la logica che usa l'algoritmo di cluster automatico di Analisi per raggruppare gli attributi dei dati per un'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-114">In this tutorial, you learn how to create a logic app that uses the Analytics autocluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="8a0ff-115">Il flusso invia automaticamente i risultati tramite posta elettronica. Questo è solo un esempio di uso congiunto di Application Insights - Analisi e App per la logica.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-115">The flow automatically sends the results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="8a0ff-116">Passaggio 1: Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="8a0ff-116">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="8a0ff-117">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8a0ff-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8a0ff-118">Nel riquadro **Nuovo** selezionare **Web e dispositivi mobili** e scegliere **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-118">In the **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Finestra della nuova app per la logica](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="8a0ff-120">Passaggio 2: Creare un trigger per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="8a0ff-120">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="8a0ff-121">In **Inizia con un trigger comune** nella finestra **Progettazione app per la logica** scegliere **Ricorrenza**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-121">In the **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Finestra di progettazione di app per la logica](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="8a0ff-123">Nella casella **Frequenza** selezionare **Giorno** e nella casella **Intervallo** digitare **1**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-123">In the **Frequency** box, select **Day** and then, in the **Interval** box, type **1**.</span></span>

    !["Ricorrenza" nella finestra Progettazione app per la logica](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="8a0ff-125">Passaggio 3: Aggiungere un'azione di Application Insights</span><span class="sxs-lookup"><span data-stu-id="8a0ff-125">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="8a0ff-126">Fare clic su **Nuovo passaggio** e quindi su **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-126">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="8a0ff-127">Nella casella di ricerca **Scegliere un'azione** digitare **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-127">In the **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="8a0ff-128">Fare clic su **Application Insights - Visualize Analytics query Preview** (Application Insights - Visualizza query di Analisi Anteprima) in **Azioni**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-128">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    !["Scegliere un'azione" nella finestra Progettazione app per la logica](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="8a0ff-130">Passaggio 4: Connettersi a una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="8a0ff-130">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="8a0ff-131">Per completare questo passaggio, sono necessari un ID applicazione e una chiave API per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-131">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="8a0ff-132">È possibile recuperare queste informazioni dal portale di Azure, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="8a0ff-132">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![ID applicazione nel portale di Azure](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="8a0ff-134">Specificare un nome per la connessione, l'ID applicazione e la chiave API.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-134">Provide a name for your connection, the application ID, and the API key.</span></span>

![Connessione per il flusso nella finestra Progettazione app per la logica](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="8a0ff-136">Passaggio 5: Specificare la query e il tipo di grafico di Analisi</span><span class="sxs-lookup"><span data-stu-id="8a0ff-136">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="8a0ff-137">In questo esempio la query seleziona le richieste non riuscite entro l'ultimo giorno e le correla alle eccezioni che si sono verificate durante l'operazione.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-137">In the following example, the query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="8a0ff-138">La correlazione delle richieste non riuscite eseguita da Analisi si basa sull'identificatore operation_Id.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-138">Analytics correlates the failed requests, based on the operation_Id identifier.</span></span> <span data-ttu-id="8a0ff-139">La query segmenta quindi i risultati usando l'algoritmo di cluster automatico.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-139">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="8a0ff-140">Quando si creano query, verificare che funzionino correttamente in Analisi prima di aggiungerle al flusso.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-140">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

1. <span data-ttu-id="8a0ff-141">Nella casella **Query** aggiungere la query di Analisi seguente:</span><span class="sxs-lookup"><span data-stu-id="8a0ff-141">In the **Query** box, add the following Analytics query:</span></span> 

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

2. <span data-ttu-id="8a0ff-142">Nella casella **Tipo di grafico** selezionare **Tabella HTML**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-142">In the **Chart Type** box, select **Html Table**.</span></span>

    ![Finestra di configurazione della query di Analisi](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-the-logic-app-to-send-email"></a><span data-ttu-id="8a0ff-144">Passaggio 6: Configurare l'app per la logica per l'invio tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="8a0ff-144">Step 6: Configure the logic app to send email</span></span>

1. <span data-ttu-id="8a0ff-145">Fare clic su **Nuovo passaggio** e selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-145">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="8a0ff-146">Nella casella di ricerca digitare **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-146">In the search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="8a0ff-147">Fare clic su **Office 365 Outlook - Send an email** (Office 365 Outlook: invia un messaggio di posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="8a0ff-147">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Selezione di Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="8a0ff-149">Nella finestra **Invia un messaggio di posta elettronica** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8a0ff-149">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="8a0ff-150">a.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-150">a.</span></span> <span data-ttu-id="8a0ff-151">Digitare l'indirizzo e-mail del destinatario.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-151">Type the email address of the recipient.</span></span>

   <span data-ttu-id="8a0ff-152">b.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-152">b.</span></span> <span data-ttu-id="8a0ff-153">Digitare l'oggetto del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-153">Type a subject for the email.</span></span>

   <span data-ttu-id="8a0ff-154">c.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-154">c.</span></span> <span data-ttu-id="8a0ff-155">Fare clic in un punto qualsiasi della casella **Corpo** e scegliere **Corpo** dal menu di contenuto dinamico che viene visualizzato a destra.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-155">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="8a0ff-156">d.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-156">d.</span></span> <span data-ttu-id="8a0ff-157">Fare clic su **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-157">Click **Show advanced options**.</span></span>

      ![Configurazione di Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="8a0ff-159">Nel menu di contenuto dinamico seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8a0ff-159">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="8a0ff-160">a.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-160">a.</span></span> <span data-ttu-id="8a0ff-161">Selezionare **Nome allegato**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-161">Select **Attachment Name**.</span></span>

    <span data-ttu-id="8a0ff-162">b.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-162">b.</span></span> <span data-ttu-id="8a0ff-163">Selezionare **Contenuto allegato**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-163">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="8a0ff-164">c.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-164">c.</span></span> <span data-ttu-id="8a0ff-165">Nella casella **HTML** selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-165">In the **Is HTML** box, select **Yes**.</span></span>

      ![Schermata di configurazione della posta elettronica di Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="8a0ff-167">Passaggio 7: Salvare e testare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="8a0ff-167">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="8a0ff-168">Fare clic su **Salva** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-168">Click **Save** to save your changes.</span></span>

<span data-ttu-id="8a0ff-169">È possibile attendere che il trigger esegua l'app per la logica oppure è possibile eseguirla immediatamente scegliendo **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-169">You can wait for the trigger to run the logic app, or you can run the logic app immediately by selecting **Run**.</span></span>

![Schermata di creazione dell'app per la logica](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="8a0ff-171">Quando l'app per la logica è in esecuzione, i destinatari specificati nell'elenco di posta elettronica ricevono un messaggio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8a0ff-171">When your logic app runs, the recipients you specified in the email list will receive an email that looks like the following:</span></span>

![Messaggio di posta elettronica dell'app per la logica](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="8a0ff-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a0ff-173">Next steps</span></span>

- <span data-ttu-id="8a0ff-174">Altre informazioni sulla creazione di [query di Analisi](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="8a0ff-174">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="8a0ff-175">Altre informazioni su [App per la logica](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="8a0ff-175">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





