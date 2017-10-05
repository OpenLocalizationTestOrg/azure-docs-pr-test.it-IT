---
title: Automatizzare i processi di Azure Log Analytics con Microsoft Flow
description: Informazioni su come usare Microsoft Flow per automatizzare in poco tempo i processi ripetibili usando il connettore di Azure Log Analytics.
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 4955f90de06cd720d78c5bb60c0adcd7dc633245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="automate-log-analytics-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="fb7c9-103">Automatizzare i processi di Log Analytics con il connettore per Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="fb7c9-103">Automate Log Analytics processes with the connector for Microsoft Flow</span></span>
<span data-ttu-id="fb7c9-104">[Microsoft Flow](https://ms.flow.microsoft.com) consente di creare flussi di lavoro automatizzati che includono centinaia di azioni per un'ampia gamma di servizi.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you to create automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="fb7c9-105">L'output di un'azione può essere usato come input per un'altra. È così possibile integrare servizi diversi.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-105">Output from one action can be used as input to another allowing you to create integration between different services.</span></span>  <span data-ttu-id="fb7c9-106">Il connettore di Azure Log Analytics per Microsoft Flow consente di creare flussi di lavoro che includono dati recuperati da ricerche log in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-106">The Azure Log Analytics connector for Microsoft Flow allow you to build workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="fb7c9-107">È ad esempio possibile usare Microsoft Flow per inserire i dati di Log Analytics in una notifica di posta elettronica da Office 365, creare un bug in Visual Studio Team Services o inviare un messaggio Slack.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-107">For example, you can use Microsoft Flow to use Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="fb7c9-108">È possibile attivare un flusso di lavoro da una semplice pianificazione o con un'azione in un servizio connesso, ad esempio quando viene ricevuto un messaggio di posta elettronica o un tweet.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="fb7c9-109">Il connettore di Azure Log Analytics per Microsoft Flow richiede che l'area di lavoro in uso sia aggiornata al nuovo linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-109">The Azure Log Analytics connector for Microsoft Flow requires your workspace to be upgraded to the new Log Analytics query language.</span></span> <span data-ttu-id="fb7c9-110">In [Aggiornare l'area di lavoro di Azure Log Analytics alla nuova ricerca log](log-analytics-log-search-upgrade.md) sono disponibili altre informazioni sul nuovo linguaggio e istruzioni per l'aggiornamento dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-110">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="fb7c9-111">L'esercitazione descritta in questo articolo mostra come creare un flusso che invia automaticamente i risultati di una ricerca log di Log Analytics tramite posta elettronica. Si tratta di un esempio fra tanti del possibile utilizzo di Log Analytics in Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-111">The tutorial in this article shows you how to create a flow that automatically sends the results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="fb7c9-112">Passaggio 1: Creare un flusso</span><span class="sxs-lookup"><span data-stu-id="fb7c9-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="fb7c9-113">Accedere a [Microsoft Flow](http://flow.microsoft.com) e quindi selezionare **Flussi personali**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-113">Sign in to [Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="fb7c9-114">Fare clic su **+ Crea da zero**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="fb7c9-115">Passaggio 2: Creare un trigger per il flusso</span><span class="sxs-lookup"><span data-stu-id="fb7c9-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="fb7c9-116">Fare clic su **Search hundreds of connectors and triggers** (Cerca centinaia di connettori e trigger).</span><span class="sxs-lookup"><span data-stu-id="fb7c9-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="fb7c9-117">Digitare **Pianificazione** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-117">Type **Schedule** in the search box.</span></span>
3. <span data-ttu-id="fb7c9-118">Selezionare **Pianificazione** e quindi selezionare **Pianificazione - Ricorrenza**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="fb7c9-119">Nella casella **Frequenza** selezionare **Giorno** e nella casella **Intervallo** immettere **1**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-119">In the **Frequency** box select **Day** and in the **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="fb7c9-120">![Finestra di dialogo del trigger di Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="fb7c9-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="fb7c9-121">Passaggio 3: Aggiungere un'azione di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fb7c9-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="fb7c9-122">Fare clic su **+ Nuovo passaggio** e quindi su **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="fb7c9-123">Cercare **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="fb7c9-124">Fare clic su **Azure Log Analytics - Run query and visualize results** (Eseguire una query e visualizzare i risultati).</span><span class="sxs-lookup"><span data-stu-id="fb7c9-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="fb7c9-125">![Finestra di esecuzione query di Log Analytics](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="fb7c9-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-the-log-analytics-action"></a><span data-ttu-id="fb7c9-126">Passaggio 4: Configurare l'azione di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fb7c9-126">Step 4: Configure the Log Analytics action</span></span>

1. <span data-ttu-id="fb7c9-127">Specificare i dettagli dell'area di lavoro, inclusi l'ID sottoscrizione, il gruppo di risorse e il nome dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-127">Specify the details for your workspace including the Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="fb7c9-128">Nella casella **Query** aggiungere la query di Log Analytics seguente.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-128">Add the following Log Analytics query to the **Query** window.</span></span>  <span data-ttu-id="fb7c9-129">Questa è una semplice query di esempio che può essere sostituita con una qualsiasi altra query che restituisce dati.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="fb7c9-130">Selezionare **HTML Table** (Tabella HTML) per **Chart Type** (Tipo di grafico).</span><span class="sxs-lookup"><span data-stu-id="fb7c9-130">Select **HTML Table** for the **Chart Type**.</span></span><br><br><span data-ttu-id="fb7c9-131">![Azione di Log Analytics](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="fb7c9-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-the-flow-to-send-email"></a><span data-ttu-id="fb7c9-132">Passaggio 5: Configurare il flusso per l'invio di un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="fb7c9-132">Step 5: Configure the flow to send email</span></span>

1. <span data-ttu-id="fb7c9-133">Fare clic su **Nuovo passaggio** e quindi su **+ Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="fb7c9-134">Cercare **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="fb7c9-135">Fare clic su **Office 365 Outlook - Send an email** (Office 365 Outlook: invia un messaggio di posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="fb7c9-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="fb7c9-136">![Finestra di selezione di Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="fb7c9-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="fb7c9-137">Specificare l'indirizzo di posta elettronica del destinatario nella casella **A** e l'oggetto del messaggio nella casella **Oggetto**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-137">Specify the email address of a recipient in the **To** window and a subject for the email in **Subject**.</span></span>
5. <span data-ttu-id="fb7c9-138">Fare clic nella casella **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-138">Click anywhere in the **Body** box.</span></span>  <span data-ttu-id="fb7c9-139">Verrà aperta la finestra **Contenuto dinamico** con i valori delle azioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="fb7c9-140">Selezionare **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-140">Select **Body**.</span></span>  <span data-ttu-id="fb7c9-141">Questi sono i risultati della query nell'azione di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-141">This is the results of the query in the Log Analytics action.</span></span>
6. <span data-ttu-id="fb7c9-142">Fare clic su **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="fb7c9-143">Nella casella **HTML** selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-143">In the **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="fb7c9-144">![Finestra di configurazione della posta elettronica di Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="fb7c9-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="fb7c9-145">Passaggio 6: Salvare e testare il flusso</span><span class="sxs-lookup"><span data-stu-id="fb7c9-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="fb7c9-146">Nella casella **Nome flusso** aggiungere un nome per il flusso e quindi fare clic su **Crea flusso**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-146">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="fb7c9-147">![Salva flusso](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="fb7c9-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="fb7c9-148">Il flusso è ora creato e verrà eseguito dopo un giorno come da pianificazione.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-148">The flow is now created and will run after a day which is the schedule you specified.</span></span> 
3. <span data-ttu-id="fb7c9-149">Per testare subito il flusso, fare clic su **Esegui ora** e quindi su **Esegui flusso**.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-149">To immediately test the flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="fb7c9-150">![Esegui flusso](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="fb7c9-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="fb7c9-151">Dopo che il flusso è completato, controllare la posta elettronica del destinatario specificato.</span><span class="sxs-lookup"><span data-stu-id="fb7c9-151">When the flow completes, check the mail of the recipient that you specified.</span></span>  <span data-ttu-id="fb7c9-152">Dovrebbe essere presente un messaggio di posta elettronica con un corpo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fb7c9-152">You should have received a mail with a body similar to the following:</span></span><br><br>![Esempio di messaggio di posta elettronica](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="fb7c9-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb7c9-154">Next steps</span></span>

- <span data-ttu-id="fb7c9-155">Altre informazioni su [Ricerche log di Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="fb7c9-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="fb7c9-156">Altre informazioni su [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="fb7c9-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



