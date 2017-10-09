---
title: aaaCreate il primo flusso di lavoro tra le app cloud e servizi cloud - App Azure per la logica | Documenti Microsoft
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
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="0895e-104">Creare la prima app logica processi tooautomate di flusso di lavoro tra le app cloud e servizi cloud</span><span class="sxs-lookup"><span data-stu-id="0895e-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="0895e-105">Senza scrivere codice, è possibile automatizzare i processi aziendali in modo più semplice e rapido durante la creazione ed esecuzione di flussi di lavoro con [App per la logica di Azure](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="0895e-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="0895e-106">Il primo esempio mostra come toocreate un flusso di lavoro app logica di base che controlla un RSS feed per il nuovo contenuto in un sito Web.</span><span class="sxs-lookup"><span data-stu-id="0895e-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="0895e-107">Quando nuovi elementi vengono visualizzati nel feed del sito Web di hello, hello logica app Invia messaggio di posta elettronica da un account di Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="0895e-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="0895e-108">toocreate ed eseguire un'app di logica, è necessario questi elementi:</span><span class="sxs-lookup"><span data-stu-id="0895e-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="0895e-109">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0895e-109">An Azure subscription.</span></span> <span data-ttu-id="0895e-110">Se non si ha una sottoscrizione, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0895e-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="0895e-111">In alternativa, è possibile [iscriversi per ottenere una sottoscrizione con pagamento in base al consumo](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="0895e-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="0895e-112">La sottoscrizione di Azure viene usata per la fatturazione dell'utilizzo delle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0895e-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="0895e-113">Per altre informazioni, vedere le pagine relative alla [misurazione dell'utilizzo](../logic-apps/logic-apps-pricing.md) e ai [prezzi](https://azure.microsoft.com/pricing/details/logic-apps) per App per la logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="0895e-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="0895e-114">Questo esempio richiede anche gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0895e-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="0895e-115">Account Outlook.com, Office 365 Outlook o Gmail</span><span class="sxs-lookup"><span data-stu-id="0895e-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="0895e-116">Se si ha un [account Microsoft](https://account.microsoft.com/account) personale, si ha un account Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="0895e-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="0895e-117">Se invece si una un account Azure aziendale o dell'istituto di istruzione, si ha un account **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="0895e-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="0895e-118">Un collegamento di tooa feed RSS del sito Web.</span><span class="sxs-lookup"><span data-stu-id="0895e-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="0895e-119">Questo esempio viene utilizzato hello [feed RSS per ultimissime dal sito Web CNN.com hello](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="0895e-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="0895e-120">Aggiungere un trigger che avvia il flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="0895e-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="0895e-121">Oggetto [ *trigger* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) è un evento che inizia il flusso di lavoro logica app ed è primo elemento hello necessari all'app di logica.</span><span class="sxs-lookup"><span data-stu-id="0895e-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="0895e-122">Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="0895e-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="0895e-123">Scegliere dal menu a sinistra hello **New** > **Enterprise Integration** > **logica App** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0895e-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Portale di Azure, Nuovo, Enterprise Integration, App per la logica](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="0895e-125">È anche possibile scegliere **New**, digitare nella casella di ricerca hello `logic app`, e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="0895e-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="0895e-126">Scegliere quindi **App per la logica** > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0895e-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="0895e-127">Assegnare un nome all'app per la logica e selezionare la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0895e-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="0895e-128">Creare quindi o selezionare un gruppo di risorse di Azure, che consente di organizzare e gestire le risorse di Azure correlate.</span><span class="sxs-lookup"><span data-stu-id="0895e-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="0895e-129">Infine, selezionare l'ubicazione del Data Center hello per le app per la logica di hosting.</span><span class="sxs-lookup"><span data-stu-id="0895e-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="0895e-130">Quando si è pronti, scegliere **Pin toodashboard** e quindi **crea**.</span><span class="sxs-lookup"><span data-stu-id="0895e-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![Dettagli dell'app per la logica](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="0895e-132">Quando si seleziona **toodashboard Pin**, app logica viene visualizzata nel dashboard di Azure hello dopo la distribuzione e viene aperta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0895e-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="0895e-133">Se l'app logica non viene visualizzato nel dashboard hello hello **tutte le risorse** riquadro, scegliere **vedere più**e selezionare l'app logica.</span><span class="sxs-lookup"><span data-stu-id="0895e-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="0895e-134">O scegliere dal menu a sinistra, hello **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="0895e-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="0895e-135">In **Enterprise Integration** scegliere **App per la logica**, quindi selezionare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0895e-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="0895e-136">Quando si apre l'app per la logica per hello prima volta, hello progettazione applicazione logica mostra i modelli che è possibile usare tooget avviato.</span><span class="sxs-lookup"><span data-stu-id="0895e-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="0895e-137">Per il momento, scegliere **App per la logica vuota**, per consentire la creazione di un'app per la logica completamente nuova.</span><span class="sxs-lookup"><span data-stu-id="0895e-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="0895e-138">Apre Hello progettazione applicazione logica e vengono mostrati i servizi disponibili e *trigger* che è possibile utilizzare nell'applicazione logica.</span><span class="sxs-lookup"><span data-stu-id="0895e-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="0895e-139">Nella casella di ricerca hello, digitare `RSS`e selezionare il trigger: **RSS - quando viene pubblicato un elemento del feed**</span><span class="sxs-lookup"><span data-stu-id="0895e-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Trigger di RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="0895e-141">Immettere il collegamento hello per feed RSS del sito Web di hello che si desidera tootrack.</span><span class="sxs-lookup"><span data-stu-id="0895e-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="0895e-142">È anche possibile cambiare i valori per **Frequenza** e **Intervallo**.</span><span class="sxs-lookup"><span data-stu-id="0895e-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="0895e-143">Queste impostazioni determinano la frequenza con cui l'app per la logica verifica la presenza di nuovi elementi e restituisce tutti gli elementi trovati durante tale periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="0895e-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="0895e-144">Per questo esempio, controlliamo ogni giorno per le storie superiore registrato del sito Web CNN toohello.</span><span class="sxs-lookup"><span data-stu-id="0895e-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![Configurare un trigger con feed RSS, frequenza e intervallo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="0895e-146">Salvare il lavoro, per il momento.</span><span class="sxs-lookup"><span data-stu-id="0895e-146">Save your work for now.</span></span> <span data-ttu-id="0895e-147">(Nella barra dei comandi della finestra di progettazione hello, scegliere **salvare**.)</span><span class="sxs-lookup"><span data-stu-id="0895e-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![Salvare l'app per la logica](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="0895e-149">Quando si salva, logica app passa in tempo reale, ma attualmente la logica app controlla solo per i nuovi elementi nel feed RSS hello.</span><span class="sxs-lookup"><span data-stu-id="0895e-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="0895e-150">toomake in questo esempio più utile, che si aggiunge un'azione che esegue l'app per la logica del trigger after viene attivato.</span><span class="sxs-lookup"><span data-stu-id="0895e-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="0895e-151">Aggiunge un'azione che risponde tooyour trigger</span><span class="sxs-lookup"><span data-stu-id="0895e-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="0895e-152">Un'[*azione*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) è un'attività eseguita dal flusso di lavoro dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0895e-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="0895e-153">Dopo avere aggiunto un'app di logica tooyour trigger, è possibile aggiungere un tooperform operazioni con i dati generati dal trigger.</span><span class="sxs-lookup"><span data-stu-id="0895e-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="0895e-154">Per questo esempio, è ora possibile aggiungere un'azione che invia messaggio di posta elettronica quando vengono visualizzati nuovi elementi nel feed RSS del sito Web di hello.</span><span class="sxs-lookup"><span data-stu-id="0895e-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="0895e-155">Nella finestra di progettazione hello in trigger, scegliere **nuovo passaggio** > **aggiungere un'azione** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0895e-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Aggiungere un'azione](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="0895e-157">finestra di progettazione Mostra Hello [connettori disponibili](../connectors/apis-list.md) in modo che è possibile selezionare tooperform un'azione quando il trigger viene attivato.</span><span class="sxs-lookup"><span data-stu-id="0895e-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="0895e-158">Basato su account di posta elettronica, seguire i passaggi di hello per Outlook o Gmail.</span><span class="sxs-lookup"><span data-stu-id="0895e-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="0895e-159">messaggio di posta elettronica toosend dall'account Outlook, nella casella di ricerca hello, immettere `outlook`.</span><span class="sxs-lookup"><span data-stu-id="0895e-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="0895e-160">In **Servizi** scegliere **Outlook.com** per gli account Microsoft personali oppure **Office 365 Outlook** per gli account Azure aziendali o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="0895e-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="0895e-161">In **Azioni** selezionare **Invia un messaggio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="0895e-161">Under **Actions**, select **Send an email**.</span></span>

       ![Selezionare l'azione "Invia un messaggio di posta elettronica" di Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="0895e-163">messaggio di posta elettronica toosend dall'account Gmail, nella casella di ricerca hello, immettere `gmail`.</span><span class="sxs-lookup"><span data-stu-id="0895e-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="0895e-164">In **Azioni** selezionare **Invia messaggio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="0895e-164">Under **Actions**, select **Send email**.</span></span>

       ![Scegliere "Gmail - Invia messaggio di posta elettronica"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="0895e-166">Quando viene chiesto di immettere le credenziali, accedere con hello username e password per l'account di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="0895e-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="0895e-167">Fornire dettagli di hello per questa azione, come indirizzo di posta elettronica di destinazione hello e scegliere parametri hello per hello dati tooinclude nel messaggio di posta elettronica di hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0895e-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![Selezionare dati tooinclude nel messaggio di posta elettronica](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="0895e-169">Se è stato scelto Outlook, l'app per la logica potrebbe avere un aspetto simile a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="0895e-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![App per la logica completata](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="0895e-171">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="0895e-171">Save your changes.</span></span> <span data-ttu-id="0895e-172">(Nella barra dei comandi della finestra di progettazione hello, scegliere **salvare**.)</span><span class="sxs-lookup"><span data-stu-id="0895e-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="0895e-173">È ora possibile eseguire manualmente l'app per la logica per i test.</span><span class="sxs-lookup"><span data-stu-id="0895e-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="0895e-174">Nella barra dei comandi della finestra di progettazione hello, scegliere **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="0895e-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="0895e-175">In caso contrario, è possibile consentire l'app logica verificare hello specificato feed RSS basato su pianificazione hello impostati.</span><span class="sxs-lookup"><span data-stu-id="0895e-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="0895e-176">Se l'app logica consente di individuare nuovi elementi, hello logica app Invia messaggio di posta elettronica che include i dati selezionati.</span><span class="sxs-lookup"><span data-stu-id="0895e-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="0895e-177">Se non è stato trovato alcun nuovo elemento, l'app logica Ignora azione hello che invia messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="0895e-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="0895e-178">toomonitor e controllare le app per la logica di esecuzione del e attivare cronologia, nel menu logica app, scegliere **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="0895e-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Monitorare e visualizzare la cronologia di esecuzione e dei trigger dell'app per la logica](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="0895e-180">Se non si trova dati hello previsti, sulla barra dei comandi di hello, provare a scegliere **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="0895e-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="0895e-181">ulteriori informazioni sullo stato dell'applicazione logica toolearn o eseguire e attivare cronologia o toodiagnose app logica, vedere [app logica di risoluzione dei problemi](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="0895e-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="0895e-182">L'esecuzione dell'app per la logica continua fino alla disattivazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0895e-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="0895e-183">tooturn disattivare l'app per il momento, nel menu logica app, scegliere **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="0895e-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="0895e-184">Nella barra dei comandi di hello, scegliere **disabilitare**.</span><span class="sxs-lookup"><span data-stu-id="0895e-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="0895e-185">La prima app per la logica è stata configurata ed eseguita.</span><span class="sxs-lookup"><span data-stu-id="0895e-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="0895e-186">È stato anche illustrato come creare con facilità flussi di lavoro per l'automazione dei processi e integrare le app cloud e i servizi cloud, senza scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="0895e-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="0895e-187">Gestire l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="0895e-187">Manage your logic app</span></span>

<span data-ttu-id="0895e-188">toomanage l'app, è possibile eseguire attività come controllare lo stato di hello, modificare, visualizzare la cronologia, disattivare o eliminare l'app logica.</span><span class="sxs-lookup"><span data-stu-id="0895e-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="0895e-189">Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="0895e-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="0895e-190">Scegliere dal menu a sinistra, hello **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="0895e-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="0895e-191">In **Enterprise Integration** scegliere **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="0895e-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="0895e-192">Selezionare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0895e-192">Select your logic app.</span></span> 

   <span data-ttu-id="0895e-193">Nel menu di applicazione hello logica, è possibile trovare queste attività di gestione di app logica:</span><span class="sxs-lookup"><span data-stu-id="0895e-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="0895e-194">Attività</span><span class="sxs-lookup"><span data-stu-id="0895e-194">Task</span></span>|<span data-ttu-id="0895e-195">Passi</span><span class="sxs-lookup"><span data-stu-id="0895e-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="0895e-196">Visualizzare lo stato, la cronologia di esecuzione e le informazioni generali dell'app</span><span class="sxs-lookup"><span data-stu-id="0895e-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="0895e-197">Scegliere **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="0895e-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="0895e-198">Modificare l'app</span><span class="sxs-lookup"><span data-stu-id="0895e-198">Edit your app</span></span> | <span data-ttu-id="0895e-199">Scegliere **Progettazione app per la logica**.</span><span class="sxs-lookup"><span data-stu-id="0895e-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="0895e-200">Visualizzare la definizione JSON del flusso di lavoro dell'app</span><span class="sxs-lookup"><span data-stu-id="0895e-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="0895e-201">Scegliere **Visualizzazione codice app per la logica**.</span><span class="sxs-lookup"><span data-stu-id="0895e-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="0895e-202">Visualizzare le operazioni eseguite nell'app per la logica</span><span class="sxs-lookup"><span data-stu-id="0895e-202">View operations performed on your logic app</span></span> | <span data-ttu-id="0895e-203">Scegliere **Log attività**.</span><span class="sxs-lookup"><span data-stu-id="0895e-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="0895e-204">Visualizzare le versioni precedenti per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="0895e-204">View past versions for your logic app</span></span> | <span data-ttu-id="0895e-205">Scegliere **Versioni**.</span><span class="sxs-lookup"><span data-stu-id="0895e-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="0895e-206">Disattivare temporaneamente l'app</span><span class="sxs-lookup"><span data-stu-id="0895e-206">Turn off your app temporarily</span></span> | <span data-ttu-id="0895e-207">Scegliere **Panoramica**, quindi nella barra dei comandi di hello, scegliere **disabilitare**.</span><span class="sxs-lookup"><span data-stu-id="0895e-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="0895e-208">Eliminare l'app</span><span class="sxs-lookup"><span data-stu-id="0895e-208">Delete your app</span></span> | <span data-ttu-id="0895e-209">Scegliere **Panoramica**, quindi nella barra dei comandi di hello, scegliere **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="0895e-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="0895e-210">Immettere il nome dell'app per la logica e scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="0895e-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="0895e-211">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="0895e-211">Get help</span></span>

<span data-ttu-id="0895e-212">rispondere alle domande di domande tooask, e informazioni su quali altri logica app di Azure in caso di utenti, visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="0895e-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="0895e-213">toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="0895e-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0895e-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0895e-214">Next steps</span></span>

*  [<span data-ttu-id="0895e-215">Aggiungere condizioni ed eseguire flussi di lavoro</span><span class="sxs-lookup"><span data-stu-id="0895e-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="0895e-216">Modelli di app per la logica</span><span class="sxs-lookup"><span data-stu-id="0895e-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="0895e-217">Creare app per la logica da modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0895e-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
