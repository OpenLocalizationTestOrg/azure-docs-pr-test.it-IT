---
title: i processi di Azure Log Analitica aaaAutomate con Microsoft Flow
description: Informazioni su come utilizzare Microsoft Flow tooquickly automatizzare i processi ripetibili utilizzando il connettore di Azure Log Analitica hello.
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
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="4ed98-103">Automatizzare i processi di Log Analitica con connettore hello per Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="4ed98-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="4ed98-104">[Microsoft Flow](https://ms.flow.microsoft.com) consente con centinaia di azioni per un'ampia gamma di servizi flussi di lavoro toocreate automatizzata.</span><span class="sxs-lookup"><span data-stu-id="4ed98-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="4ed98-105">Output da un'azione può essere usato come input tooanother consentendo toocreate integrazione tra diversi servizi.</span><span class="sxs-lookup"><span data-stu-id="4ed98-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="4ed98-106">connettore di Hello Analitica di Log di Azure per Microsoft Flow consentono toobuild flussi di lavoro che includono i dati recuperati dalle ricerche log nel Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="4ed98-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="4ed98-107">Ad esempio, si può utilizzare dati di Log Analitica toouse Microsoft Flow una notifica di posta elettronica da Office 365, creare un bug in Visual Studio Team Services o invia un messaggio di flessibilità.</span><span class="sxs-lookup"><span data-stu-id="4ed98-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="4ed98-108">È possibile attivare un flusso di lavoro da una semplice pianificazione o con un'azione in un servizio connesso, ad esempio quando viene ricevuto un messaggio di posta elettronica o un tweet.</span><span class="sxs-lookup"><span data-stu-id="4ed98-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="4ed98-109">Hello Azure Log Analitica connector per Microsoft Flow richiede che l'area di lavoro toobe aggiornato toohello nuovo Log Analitica linguaggio di query.</span><span class="sxs-lookup"><span data-stu-id="4ed98-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="4ed98-110">È possibile acquisire familiarità con il nuovo linguaggio di hello e ottenere hello procedure tooupgrade l'area di lavoro in [aggiornare la ricerca di log di Azure Log Analitica dell'area di lavoro toonew](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="4ed98-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="4ed98-111">esercitazione Hello in questo articolo viene illustrato come un flusso che invia automaticamente toocreate hello risultati di una ricerca di log Log Analitica tramite posta elettronica, solo un esempio di come è possibile utilizzare i Log Analitica in Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="4ed98-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="4ed98-112">Passaggio 1: Creare un flusso</span><span class="sxs-lookup"><span data-stu-id="4ed98-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="4ed98-113">Accedi troppo[Microsoft Flow](http://flow.microsoft.com)e selezionare **flussi My**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="4ed98-114">Fare clic su **+ Crea da zero**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="4ed98-115">Passaggio 2: Creare un trigger per il flusso</span><span class="sxs-lookup"><span data-stu-id="4ed98-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="4ed98-116">Fare clic su **Search hundreds of connectors and triggers** (Cerca centinaia di connettori e trigger).</span><span class="sxs-lookup"><span data-stu-id="4ed98-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="4ed98-117">Tipo **pianificazione** nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="4ed98-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="4ed98-118">Selezionare **Pianificazione** e quindi selezionare **Pianificazione - Ricorrenza**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="4ed98-119">In hello **frequenza** selezionare **giorno** e hello **intervallo** immettere **1**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="4ed98-120">![Finestra di dialogo del trigger di Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="4ed98-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="4ed98-121">Passaggio 3: Aggiungere un'azione di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4ed98-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="4ed98-122">Fare clic su **+ Nuovo passaggio** e quindi su **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="4ed98-123">Cercare **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="4ed98-124">Fare clic su **Azure Log Analytics - Run query and visualize results** (Eseguire una query e visualizzare i risultati).</span><span class="sxs-lookup"><span data-stu-id="4ed98-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="4ed98-125">![Finestra di esecuzione query di Log Analytics](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="4ed98-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="4ed98-126">Passaggio 4: Configurare l'azione di hello Log Analitica</span><span class="sxs-lookup"><span data-stu-id="4ed98-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="4ed98-127">Specificare i dettagli di hello dell'area di lavoro inclusi hello sottoscrizione ID, gruppo di risorse e il nome dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4ed98-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="4ed98-128">Aggiungere i seguenti Log Analitica query toohello hello **Query** finestra.</span><span class="sxs-lookup"><span data-stu-id="4ed98-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="4ed98-129">Questa è una semplice query di esempio che può essere sostituita con una qualsiasi altra query che restituisce dati.</span><span class="sxs-lookup"><span data-stu-id="4ed98-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="4ed98-130">Selezionare **tabella HTML** per hello **tipo di grafico**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="4ed98-131">![Azione di Log Analytics](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="4ed98-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="4ed98-132">Passaggio 5: Configurare la posta elettronica di toosend flusso hello</span><span class="sxs-lookup"><span data-stu-id="4ed98-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="4ed98-133">Fare clic su **Nuovo passaggio** e quindi su **+ Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="4ed98-134">Cercare **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="4ed98-135">Fare clic su **Office 365 Outlook - Send an email** (Office 365 Outlook: invia un messaggio di posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="4ed98-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="4ed98-136">![Finestra di selezione di Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="4ed98-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="4ed98-137">Specificare l'indirizzo di posta elettronica hello del destinatario in hello **a** finestra e un oggetto per la posta elettronica hello in **soggetto**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="4ed98-138">Fare clic nella hello **corpo** casella.</span><span class="sxs-lookup"><span data-stu-id="4ed98-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="4ed98-139">Verrà aperta la finestra **Contenuto dinamico** con i valori delle azioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="4ed98-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="4ed98-140">Selezionare **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-140">Select **Body**.</span></span>  <span data-ttu-id="4ed98-141">Si tratta di risultati hello della query hello hello azione Analitica di Log.</span><span class="sxs-lookup"><span data-stu-id="4ed98-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="4ed98-142">Fare clic su **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="4ed98-143">In hello **è HTML** , quindi selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="4ed98-144">![Finestra di configurazione della posta elettronica di Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="4ed98-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="4ed98-145">Passaggio 6: Salvare e testare il flusso</span><span class="sxs-lookup"><span data-stu-id="4ed98-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="4ed98-146">In hello **nome flusso** casella, aggiungere un nome per il flusso e quindi fare clic su **creare flusso**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="4ed98-147">![Salva flusso](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="4ed98-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="4ed98-148">flusso Hello è stato creato, verrà eseguito dopo un giorno, ovvero hello alla pianificazione specificata.</span><span class="sxs-lookup"><span data-stu-id="4ed98-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="4ed98-149">flusso di hello tooimmediately test, fare clic su **Esegui** e quindi **eseguire flusso**.</span><span class="sxs-lookup"><span data-stu-id="4ed98-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="4ed98-150">![Esegui flusso](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="4ed98-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="4ed98-151">Al termine del flusso di hello, controllare i messaggi hello del destinatario hello specificato.</span><span class="sxs-lookup"><span data-stu-id="4ed98-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="4ed98-152">Deve aver ricevuto un messaggio e-mail con un seguente toohello simile corpo:</span><span class="sxs-lookup"><span data-stu-id="4ed98-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![Esempio di messaggio di posta elettronica](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="4ed98-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ed98-154">Next steps</span></span>

- <span data-ttu-id="4ed98-155">Altre informazioni su [Ricerche log di Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="4ed98-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="4ed98-156">Altre informazioni su [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4ed98-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



