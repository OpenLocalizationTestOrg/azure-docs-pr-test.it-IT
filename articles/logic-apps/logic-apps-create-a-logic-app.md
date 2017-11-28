---
title: Creare il primo flusso di lavoro tra app cloud e servizi cloud - App per la logica di Azure | Microsoft Docs
description: Automatizzare i processi aziendali per scenari di integrazione di sistemi e di Enterprise Application Integration (EAI) creando ed eseguendo flussi di lavoro in App per la logica di Azure
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: flusso di lavoro, app cloud, servizi cloud, processi aziendali, integrazione di sistemi, enterprise application integration, EAI
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 204bf123509729b60b55c306050cef54aa7fecc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-logic-app-workflow-to-automate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="918f2-104">Creare il primo flusso di lavoro di app per la logica per automatizzare i processi tra app cloud e servizi cloud</span><span class="sxs-lookup"><span data-stu-id="918f2-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="918f2-105">Senza scrivere codice, è possibile automatizzare i processi aziendali in modo più semplice e rapido durante la creazione ed esecuzione di flussi di lavoro con [App per la logica di Azure](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="918f2-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="918f2-106">Questo primo esempio illustra come creare un flusso di lavoro di base per app per la logica che controlla un feed RSS alla ricerca di nuovi contenuti in un sito Web.</span><span class="sxs-lookup"><span data-stu-id="918f2-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="918f2-107">Quando vengono visualizzati nuovi elementi nel feed del sito Web, l'app per la logica invia un messaggio di posta elettronica da un account Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="918f2-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="918f2-108">Per creare ed eseguire un'app per la logica, sono necessari questi elementi:</span><span class="sxs-lookup"><span data-stu-id="918f2-108">To create and run a logic app, you need these items:</span></span>

* <span data-ttu-id="918f2-109">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="918f2-109">An Azure subscription.</span></span> <span data-ttu-id="918f2-110">Se non si ha una sottoscrizione, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="918f2-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="918f2-111">In alternativa, è possibile [iscriversi per ottenere una sottoscrizione con pagamento in base al consumo](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="918f2-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="918f2-112">La sottoscrizione di Azure viene usata per la fatturazione dell'utilizzo delle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="918f2-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="918f2-113">Per altre informazioni, vedere le pagine relative alla [misurazione dell'utilizzo](../logic-apps/logic-apps-pricing.md) e ai [prezzi](https://azure.microsoft.com/pricing/details/logic-apps) per App per la logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="918f2-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="918f2-114">Questo esempio richiede anche gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="918f2-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="918f2-115">Account Outlook.com, Office 365 Outlook o Gmail</span><span class="sxs-lookup"><span data-stu-id="918f2-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="918f2-116">Se si ha un [account Microsoft](https://account.microsoft.com/account) personale, si ha un account Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="918f2-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="918f2-117">Se invece si una un account Azure aziendale o dell'istituto di istruzione, si ha un account **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="918f2-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="918f2-118">Un collegamento al feed RSS del sito Web.</span><span class="sxs-lookup"><span data-stu-id="918f2-118">A link to a website's RSS feed.</span></span> <span data-ttu-id="918f2-119">Questo esempio usa il [feed RSS delle notizie principali dal sito Web CNN.com](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="918f2-119">This example uses the [RSS feed for top stories from the CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="918f2-120">Aggiungere un trigger che avvia il flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="918f2-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="918f2-121">Un [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) è un evento che avvia il flusso di lavoro dell'app per la logica ed è il primo elemento necessario per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="918f2-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span></span>

1. <span data-ttu-id="918f2-122">Accedere al [Portale di Azure](https://portal.azure.com "Portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="918f2-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="918f2-123">Dal menu a sinistra scegliere **Nuovo** > **Enterprise Integration** > **App per la logica**, come mostrato qui:</span><span class="sxs-lookup"><span data-stu-id="918f2-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Portale di Azure, Nuovo, Enterprise Integration, App per la logica](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="918f2-125">È anche possibile scegliere **Nuovo**, digitare `logic app` nella casella di ricerca e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="918f2-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="918f2-126">Scegliere quindi **App per la logica** > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="918f2-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="918f2-127">Assegnare un nome all'app per la logica e selezionare la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="918f2-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="918f2-128">Creare quindi o selezionare un gruppo di risorse di Azure, che consente di organizzare e gestire le risorse di Azure correlate.</span><span class="sxs-lookup"><span data-stu-id="918f2-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="918f2-129">Selezionare infine la località del data center per l'hosting dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="918f2-129">Finally, select the datacenter location for hosting your logic app.</span></span> <span data-ttu-id="918f2-130">Quando si è pronti, scegliere **Aggiungi al dashboard** e quindi **Crea**.</span><span class="sxs-lookup"><span data-stu-id="918f2-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span></span>

     ![Dettagli dell'app per la logica](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="918f2-132">Quando si seleziona **Aggiungi al dashboard**, l'app per la logica viene visualizzata nel dashboard di Azure dopo la distribuzione e viene aperta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="918f2-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="918f2-133">Se l'app per la logica non viene visualizzata nel dashboard, nel riquadro **Tutte le risorse** scegliere **Vedi altri** e selezionare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="918f2-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="918f2-134">Dal menu a sinistra scegliere **More services** (Altri servizi).</span><span class="sxs-lookup"><span data-stu-id="918f2-134">Or on the left menu, choose **More services**.</span></span> <span data-ttu-id="918f2-135">In **Enterprise Integration** scegliere **App per la logica**, quindi selezionare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="918f2-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="918f2-136">Quando si apre l'app per la logica per la prima volta, la finestra di progettazione dell'app per la logica mostra i modelli disponibili per iniziare.</span><span class="sxs-lookup"><span data-stu-id="918f2-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span></span> <span data-ttu-id="918f2-137">Per il momento, scegliere **App per la logica vuota**, per consentire la creazione di un'app per la logica completamente nuova.</span><span class="sxs-lookup"><span data-stu-id="918f2-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="918f2-138">La finestra di progettazione logica App apre e visualizza i servizi disponibili e *trigger* che è possibile utilizzare nell'applicazione logica.</span><span class="sxs-lookup"><span data-stu-id="918f2-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="918f2-139">Nella casella di ricerca digitare `RSS`, quindi selezionare questo trigger: **RSS - Quando viene pubblicato un elemento del feed**</span><span class="sxs-lookup"><span data-stu-id="918f2-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Trigger di RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="918f2-141">Immettere il collegamento per il feed RSS del sito Web di cui si vuole tenere traccia.</span><span class="sxs-lookup"><span data-stu-id="918f2-141">Enter the link for the website's RSS feed that you want to track.</span></span> 

     <span data-ttu-id="918f2-142">È anche possibile cambiare i valori per **Frequenza** e **Intervallo**.</span><span class="sxs-lookup"><span data-stu-id="918f2-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="918f2-143">Queste impostazioni determinano la frequenza con cui l'app per la logica verifica la presenza di nuovi elementi e restituisce tutti gli elementi trovati durante tale periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="918f2-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="918f2-144">Per questo esempio si controllano ogni giorno le notizie principali pubblicate nel sito Web della CNN.</span><span class="sxs-lookup"><span data-stu-id="918f2-144">For this example, let's check every day for   top stories posted to the CNN website.</span></span>

     ![Configurare un trigger con feed RSS, frequenza e intervallo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="918f2-146">Salvare il lavoro, per il momento.</span><span class="sxs-lookup"><span data-stu-id="918f2-146">Save your work for now.</span></span> <span data-ttu-id="918f2-147">Sulla barra dei comandi della finestra di progettazione scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="918f2-147">(On the designer command bar, choose **Save**.)</span></span>

   ![Salvare l'app per la logica](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="918f2-149">Dopo il salvataggio, l'app per la logica viene resa disponibile, ma attualmente verifica solo la presenza di nuovi elementi nel feed RSS specificato.</span><span class="sxs-lookup"><span data-stu-id="918f2-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span></span> 
   <span data-ttu-id="918f2-150">Per rendere più utile l'esempio, è possibile aggiungere un'azione eseguita dall'app per la logica dopo l'attivazione del trigger.</span><span class="sxs-lookup"><span data-stu-id="918f2-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-to-your-trigger"></a><span data-ttu-id="918f2-151">Aggiungere un'azione che risponde al trigger</span><span class="sxs-lookup"><span data-stu-id="918f2-151">Add an action that responds to your trigger</span></span>

<span data-ttu-id="918f2-152">Un'[*azione*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) è un'attività eseguita dal flusso di lavoro dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="918f2-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="918f2-153">Dopo avere aggiunto un trigger all'app per la logica, è possibile aggiungere un'azione per eseguire operazioni con i dati generati da tale trigger.</span><span class="sxs-lookup"><span data-stu-id="918f2-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="918f2-154">Per questo esempio, viene ora aggiunta un'azione per l'invio di un messaggio di posta elettronica in caso di comparsa di nuovi elementi nel feed RSS del sito Web.</span><span class="sxs-lookup"><span data-stu-id="918f2-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span></span>

1. <span data-ttu-id="918f2-155">Nella finestra di progettazione, scegliere **Nuovo passaggio** > **Aggiungi un'azione** sotto il trigger, come mostrato qui:</span><span class="sxs-lookup"><span data-stu-id="918f2-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Aggiungere un'azione](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="918f2-157">La finestra di progettazione mostra i [connettori disponibili](../connectors/apis-list.md), per consentire di selezionare un'azione da eseguire all'attivazione del trigger.</span><span class="sxs-lookup"><span data-stu-id="918f2-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span></span>

2. <span data-ttu-id="918f2-158">In base all'account di posta elettronica, seguire la procedura per Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="918f2-158">Based on your email account, follow the steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="918f2-159">Per inviare messaggi di posta elettronica dall'account Outlook, nella casella di ricerca immettere `outlook`.</span><span class="sxs-lookup"><span data-stu-id="918f2-159">To send email from your Outlook account, in the search box, enter `outlook`.</span></span> <span data-ttu-id="918f2-160">In **Servizi** scegliere **Outlook.com** per gli account Microsoft personali oppure **Office 365 Outlook** per gli account Azure aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="918f2-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="918f2-161">In **Azioni** selezionare **Invia un messaggio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="918f2-161">Under **Actions**, select **Send an email**.</span></span>

       ![Selezionare l'azione "Invia un messaggio di posta elettronica" di Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="918f2-163">Per inviare messaggi di posta elettronica dall'account Gmail, nella casella di ricerca immettere `gmail`.</span><span class="sxs-lookup"><span data-stu-id="918f2-163">To send email from your Gmail account, in the search box, enter `gmail`.</span></span> 
   <span data-ttu-id="918f2-164">In **Azioni** selezionare **Invia messaggio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="918f2-164">Under **Actions**, select **Send email**.</span></span>

       ![Scegliere "Gmail - Invia messaggio di posta elettronica"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="918f2-166">Quando vengono richieste le credenziali, accedere con il nome utente e la password per l'account di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="918f2-166">When you're prompted for credentials, sign in with the username and password for your email account.</span></span> 

4. <span data-ttu-id="918f2-167">Specificare i dettagli per questa azione, ad esempio l'indirizzo di posta elettronica di destinazione, quindi scegliere i parametri per i dati da includere nel messaggio di posta elettronica, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="918f2-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span></span>

   ![Selezionare i dati da includere nel messaggio di posta elettronica](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="918f2-169">Se è stato scelto Outlook, l'app per la logica potrebbe avere un aspetto simile a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="918f2-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![App per la logica completata](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="918f2-171">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="918f2-171">Save your changes.</span></span> <span data-ttu-id="918f2-172">Sulla barra dei comandi della finestra di progettazione scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="918f2-172">(On the designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="918f2-173">È ora possibile eseguire manualmente l'app per la logica per i test.</span><span class="sxs-lookup"><span data-stu-id="918f2-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="918f2-174">Sulla barra dei comandi della finestra di progettazione scegliere **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="918f2-174">On the designer command bar, choose **Run**.</span></span> <span data-ttu-id="918f2-175">In alternativa, è possibile lasciare che l'app per la logica verifichi il feed RSS specificato in base alla pianificazione configurata.</span><span class="sxs-lookup"><span data-stu-id="918f2-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span></span>

   <span data-ttu-id="918f2-176">Se l'app per la logica trova nuovi elementi, invia un messaggio di posta elettronica che include i dati selezionati.</span><span class="sxs-lookup"><span data-stu-id="918f2-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="918f2-177">Se non vengono trovati nuovi elementi, l'app per la logica ignora l'azione di invio del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="918f2-177">If no new items are found, your logic app skips the action that sends email.</span></span>

7. <span data-ttu-id="918f2-178">Per monitorare e controllare la cronologia di esecuzione e dei trigger dell'app per la logica, dal menu dell'app per la logica scegliere **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="918f2-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Monitorare e visualizzare la cronologia di esecuzione e dei trigger dell'app per la logica](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="918f2-180">Se non si trovano i dati previsti, provare a scegliere **Aggiorna** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="918f2-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="918f2-181">Per altre informazioni sullo stato o sulla cronologia di esecuzione e dei trigger dell'app per la logica o per la diagnosi delle app per la logica, vedere [Risolvere i problemi dell'app per la logica](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="918f2-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="918f2-182">L'esecuzione dell'app per la logica continua fino alla disattivazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="918f2-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="918f2-183">Per disattivare temporaneamente l'app, dal menu dell'app per la logica scegliere **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="918f2-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="918f2-184">Sulla barra dei comandi fare clic su **Disabilita**.</span><span class="sxs-lookup"><span data-stu-id="918f2-184">On the command bar, choose **Disable**.</span></span>

<span data-ttu-id="918f2-185">La prima app per la logica è stata configurata ed eseguita.</span><span class="sxs-lookup"><span data-stu-id="918f2-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="918f2-186">È stato anche illustrato come creare con facilità flussi di lavoro per l'automazione dei processi e integrare le app cloud e i servizi cloud, senza scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="918f2-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="918f2-187">Gestire l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="918f2-187">Manage your logic app</span></span>

<span data-ttu-id="918f2-188">Per gestire l'app, è possibile eseguire attività come la verifica dello stato, la modifica, la visualizzazione della cronologia, la disattivazione o l'eliminazione dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="918f2-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="918f2-189">Accedere al [Portale di Azure](https://portal.azure.com "Portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="918f2-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="918f2-190">Dal menu a sinistra scegliere **More services** (Altri servizi).</span><span class="sxs-lookup"><span data-stu-id="918f2-190">On the left menu, choose **More services**.</span></span> <span data-ttu-id="918f2-191">In **Enterprise Integration** scegliere **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="918f2-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="918f2-192">Selezionare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="918f2-192">Select your logic app.</span></span> 

   <span data-ttu-id="918f2-193">Nel menu dell'app per la logica sono disponibili queste attività di gestione delle app per la logica:</span><span class="sxs-lookup"><span data-stu-id="918f2-193">In the logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="918f2-194">Attività</span><span class="sxs-lookup"><span data-stu-id="918f2-194">Task</span></span>|<span data-ttu-id="918f2-195">Passi</span><span class="sxs-lookup"><span data-stu-id="918f2-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="918f2-196">Visualizzare lo stato, la cronologia di esecuzione e le informazioni generali dell'app</span><span class="sxs-lookup"><span data-stu-id="918f2-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="918f2-197">Scegliere **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="918f2-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="918f2-198">Modificare l'app</span><span class="sxs-lookup"><span data-stu-id="918f2-198">Edit your app</span></span> | <span data-ttu-id="918f2-199">Scegliere **Progettazione app per la logica**.</span><span class="sxs-lookup"><span data-stu-id="918f2-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="918f2-200">Visualizzare la definizione JSON del flusso di lavoro dell'app</span><span class="sxs-lookup"><span data-stu-id="918f2-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="918f2-201">Scegliere **Visualizzazione codice app per la logica**.</span><span class="sxs-lookup"><span data-stu-id="918f2-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="918f2-202">Visualizzare le operazioni eseguite nell'app per la logica</span><span class="sxs-lookup"><span data-stu-id="918f2-202">View operations performed on your logic app</span></span> | <span data-ttu-id="918f2-203">Scegliere **Log attività**.</span><span class="sxs-lookup"><span data-stu-id="918f2-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="918f2-204">Visualizzare le versioni precedenti per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="918f2-204">View past versions for your logic app</span></span> | <span data-ttu-id="918f2-205">Scegliere **Versioni**.</span><span class="sxs-lookup"><span data-stu-id="918f2-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="918f2-206">Disattivare temporaneamente l'app</span><span class="sxs-lookup"><span data-stu-id="918f2-206">Turn off your app temporarily</span></span> | <span data-ttu-id="918f2-207">Scegliere **Panoramica** e quindi sulla barra dei comandi scegliere **Disabilita**.</span><span class="sxs-lookup"><span data-stu-id="918f2-207">Choose **Overview**, then on the command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="918f2-208">Eliminare l'app</span><span class="sxs-lookup"><span data-stu-id="918f2-208">Delete your app</span></span> | <span data-ttu-id="918f2-209">Scegliere **Panoramica** e quindi sulla barra dei comandi scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="918f2-209">Choose **Overview**, then on the command bar, choose **Delete**.</span></span> <span data-ttu-id="918f2-210">Immettere il nome dell'app per la logica e scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="918f2-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="918f2-211">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="918f2-211">Get help</span></span>

<span data-ttu-id="918f2-212">Per porre domande, fornire risposte e ottenere informazioni sulle attività degli altri utenti di App per la logica di Azure, vedere il [forum su App per la logica di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="918f2-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="918f2-213">Per contribuire al miglioramento delle App per la logica di Azure e dei connettori, votare o inviare idee al [sito dei commenti e suggerimenti degli utenti di App per la logica di Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="918f2-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="918f2-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="918f2-214">Next steps</span></span>

*  [<span data-ttu-id="918f2-215">Aggiungere condizioni ed eseguire flussi di lavoro</span><span class="sxs-lookup"><span data-stu-id="918f2-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="918f2-216">Modelli di app per la logica</span><span class="sxs-lookup"><span data-stu-id="918f2-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="918f2-217">Creare app per la logica da modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="918f2-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
