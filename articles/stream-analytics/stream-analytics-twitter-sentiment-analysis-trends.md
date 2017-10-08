---
title: analisi del sentiment aaaReal ora Twitter con Analitica di flusso di Azure | Documenti Microsoft
description: Informazioni su come toouse Analitica di flusso per l'analisi di valutazione di Twitter in tempo reale. Istruzioni dettagliate da toodata di generazione di eventi in un dashboard in tempo reale.
keywords: analisi delle tendenze twitter in tempo reale, analisi del sentiment, analisi dei social media, esempio di analisi delle tendenze
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="ff64f-105">Analisi del sentiment su Twitter in tempo reale in Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="ff64f-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="ff64f-106">Informazioni su come una soluzione di analisi del sentiment per analitica di social networking mettendo in tempo reale toobuild Twitter eventi nell'hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff64f-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="ff64f-107">È quindi possibile scrivere una query su Azure flusso Analitica tooanalyze hello dati e nessuno dei due archivi hello risultati per un utilizzo successivo o utilizzare un dashboard e [Power BI](https://powerbi.com/) insights tooprovide in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="ff64f-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="ff64f-108">Gli strumenti di analisi dei social media permettono alle organizzazioni di determinare gli argomenti di tendenza,</span><span class="sxs-lookup"><span data-stu-id="ff64f-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="ff64f-109">vale a dire gli argomenti e gli atteggiamenti che registrano un numero elevato di post nei social media.</span><span class="sxs-lookup"><span data-stu-id="ff64f-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="ff64f-110">Analisi del sentiment, denominato anche *data mining parere*, Usa attitudini di social networking analitica strumenti toodetermine verso un prodotto, l'idea e così via.</span><span class="sxs-lookup"><span data-stu-id="ff64f-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="ff64f-111">Analisi delle tendenze Twitter in tempo reale è un ottimo esempio di uno strumento analitica, perché hello hashtag sottoscrizione modello consente le parole chiave toospecific toolisten (hashtag) e lo sviluppo di analisi del sentiment di hello feed.</span><span class="sxs-lookup"><span data-stu-id="ff64f-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="ff64f-112">Scenario: analisi del sentiment su social media in tempo reale</span><span class="sxs-lookup"><span data-stu-id="ff64f-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="ff64f-113">Una società che ha un sito Web di notizie media è interessata a ottenere un vantaggio rispetto alla concorrenza con il contenuto del sito è lettori tooits immediatamente pertinente.</span><span class="sxs-lookup"><span data-stu-id="ff64f-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="ff64f-114">la società Hello utilizza analisi social media negli argomenti pertinenti tooreaders eseguendo l'analisi del sentiment in tempo reale dei dati di Twitter.</span><span class="sxs-lookup"><span data-stu-id="ff64f-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="ff64f-115">argomenti relativi alle tendenze di tooidentify in tempo reale su Twitter, hello analitica in tempo reale di esigenze aziendali sul volume di tweet hello e sentiment per gli argomenti principali.</span><span class="sxs-lookup"><span data-stu-id="ff64f-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="ff64f-116">In altre parole, hello necessità è un motore analitica di analisi di valutazione che si basa sul supporto social feed.</span><span class="sxs-lookup"><span data-stu-id="ff64f-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff64f-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ff64f-117">Prerequisites</span></span>
<span data-ttu-id="ff64f-118">In questa esercitazione, utilizzare un'applicazione client che si connette tooTwitter e Cerca TWEET che hanno determinate hashtag (che è possibile impostare).</span><span class="sxs-lookup"><span data-stu-id="ff64f-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="ff64f-119">In ordine toorun applicazione hello e analizzare hello TWEET utilizzando Azure Streaming Analitica, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="ff64f-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="ff64f-120">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff64f-120">An Azure subscription</span></span>
* <span data-ttu-id="ff64f-121">Un account Twitter</span><span class="sxs-lookup"><span data-stu-id="ff64f-121">A Twitter account</span></span> 
* <span data-ttu-id="ff64f-122">Un'applicazione di Twitter e hello [token di accesso OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) per tale applicazione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="ff64f-123">Si forniscono istruzioni generali sul toocreate un'applicazione di Twitter in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ff64f-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="ff64f-124">applicazione di TwitterWPFClient Hello, che legge hello Twitter feed.</span><span class="sxs-lookup"><span data-stu-id="ff64f-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="ff64f-125">tooget questa applicazione, il download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file da GitHub e quindi decomprimere il pacchetto di hello in una cartella nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ff64f-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="ff64f-126">Se si desidera il codice sorgente toosee hello ed eseguire un'applicazione hello in un debugger, è possibile ottenere il codice sorgente hello da [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="ff64f-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="ff64f-127">Creare un hub eventi per l'input di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="ff64f-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="ff64f-128">applicazione di esempio Hello genera eventi e li inserisce tooan hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff64f-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="ff64f-129">Gli hub di eventi di Azure sono hello preferito come metodo di inserimento di eventi per Analitica di flusso.</span><span class="sxs-lookup"><span data-stu-id="ff64f-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="ff64f-130">Per ulteriori informazioni, vedere hello [documentazione hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="ff64f-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="ff64f-131">Creare uno spazio dei nomi dell'hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="ff64f-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="ff64f-132">In questa procedura, creare innanzitutto un spazio dei nomi dell'hub di eventi e quindi aggiungere uno spazio dei nomi toothat hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="ff64f-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="ff64f-133">Vengono utilizzati gli spazi dei nomi di evento hub gruppo toologically relative istanze di bus di eventi.</span><span class="sxs-lookup"><span data-stu-id="ff64f-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="ff64f-134">Accedi toohello portale di Azure e fare clic su **New** > **Internet of Things** > **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="ff64f-135">In hello **Crea spazio dei nomi** pannello, immettere un nome di spazio dei nomi, ad esempio `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="ff64f-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="ff64f-136">È possibile utilizzare qualsiasi nome spazio dei nomi hello, ma il nome di hello deve essere valido per un URL e deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="ff64f-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="ff64f-137">Selezionare una sottoscrizione, creare o scegliere un gruppo di risorse e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Creare uno spazio dei nomi dell'hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="ff64f-139">Al termine dello spazio dei nomi hello distribuzione, è possibile trovare hello spazio dei nomi hub di eventi nell'elenco delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff64f-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="ff64f-140">Fare clic su nuovo spazio dei nomi hello e nel Pannello di hello dello spazio dei nomi, fare clic su  **+ &nbsp;Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="ff64f-141">pulsante Aggiungi Hub eventi Hello per la creazione di un nuovo hub eventi</span><span class="sxs-lookup"><span data-stu-id="ff64f-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="ff64f-142">Nome hello nuovo hub eventi `socialtwitter-eh`.</span><span class="sxs-lookup"><span data-stu-id="ff64f-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="ff64f-143">È possibile usare un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="ff64f-143">You can use a different name.</span></span> <span data-ttu-id="ff64f-144">In caso contrario, prendere nota di esso, in quanto è necessario il nome di hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ff64f-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="ff64f-145">Non è necessario tooset tutte le altre opzioni per l'hub di eventi hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-145">You don't need tooset any other options for hello event hub.</span></span>

    ![Pannello per creare un nuovo hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="ff64f-147">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="ff64f-148">Hub di eventi di concedere accesso toohello</span><span class="sxs-lookup"><span data-stu-id="ff64f-148">Grant access toohello event hub</span></span>

<span data-ttu-id="ff64f-149">Prima di un processo può inviare hub di eventi di dati tooan, hub eventi hello deve disporre di criteri che consente l'accesso appropriato.</span><span class="sxs-lookup"><span data-stu-id="ff64f-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="ff64f-150">i criteri di accesso Hello produce una stringa di connessione che include informazioni di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="ff64f-151">Nel Pannello di spazio dei nomi di evento hello, fare clic su **hub eventi** e quindi fare clic su nome hello del nuovo hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="ff64f-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="ff64f-152">Nel Pannello di hub eventi hello, fare clic su **criteri di accesso condiviso** e quindi fare clic su  **+ &nbsp;Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="ff64f-153">Verificare che si lavora con hub eventi hello, non nomi di hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="ff64f-154">Aggiungere criteri denominati `socialtwitter-access` e per **Attestazione** selezionare **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Pannello per creare nuovi criteri di accesso all'hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="ff64f-156">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-156">Click **Create**.</span></span>

5.  <span data-ttu-id="ff64f-157">Dopo la distribuzione di criteri di hello, selezionarla nell'elenco di hello di criteri di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="ff64f-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="ff64f-158">Casella Trova hello **chiave primaria di stringa di connessione** e fare clic su hello copia pulsante Avanti toohello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Copia chiave di stringa di connessione primaria hello dai criteri di accesso hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="ff64f-160">Incollare la stringa di connessione hello in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="ff64f-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="ff64f-161">La stringa di connessione è necessario per la sezione successiva hello, dopo aver apportato tooit alcune piccole modifiche.</span><span class="sxs-lookup"><span data-stu-id="ff64f-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="ff64f-162">stringa di connessione Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ff64f-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="ff64f-163">Si noti che la stringa di connessione hello contiene più coppie chiave-valore, separate da punti e virgola: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, e `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="ff64f-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="ff64f-164">Per la sicurezza, sono state rimosse le parti della stringa di connessione hello nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="ff64f-165">Nell'editor di testo hello, rimuovere hello `EntityPath` coppia dalla stringa di connessione hello (non dimenticare tooremove hello un punto e virgola che lo precede).</span><span class="sxs-lookup"><span data-stu-id="ff64f-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="ff64f-166">Al termine, la stringa di connessione hello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ff64f-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="ff64f-167">Configurare e avviare l'applicazione client di Twitter hello</span><span class="sxs-lookup"><span data-stu-id="ff64f-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="ff64f-168">un'applicazione Hello client ottiene gli eventi di tweet direttamente da Twitter.</span><span class="sxs-lookup"><span data-stu-id="ff64f-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="ff64f-169">In ordine toodo questa operazione, è necessario hello toocall autorizzazione Twitter API di flusso.</span><span class="sxs-lookup"><span data-stu-id="ff64f-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="ff64f-170">tooconfigure di autorizzazione, creare un'applicazione in Twitter, che genera l'errore credenziali univoche (ad esempio, un token OAuth).</span><span class="sxs-lookup"><span data-stu-id="ff64f-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="ff64f-171">È quindi possibile configurare hello client applicazione toouse queste credenziali quando si effettua chiamate API.</span><span class="sxs-lookup"><span data-stu-id="ff64f-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="ff64f-172">Creare un'applicazione Twitter</span><span class="sxs-lookup"><span data-stu-id="ff64f-172">Create a Twitter application</span></span>
<span data-ttu-id="ff64f-173">Se si ha già un'applicazione Twitter utilizzabile per questa esercitazione, è possibile crearne una.</span><span class="sxs-lookup"><span data-stu-id="ff64f-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="ff64f-174">È necessario avere già un account Twitter.</span><span class="sxs-lookup"><span data-stu-id="ff64f-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="ff64f-175">il processo effettivo Hello in Twitter per la creazione di un'applicazione e l'acquisizione di token, i segreti e le chiavi di hello potrebbe cambiare.</span><span class="sxs-lookup"><span data-stu-id="ff64f-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="ff64f-176">Se queste istruzioni non corrispondono a ciò che viene visualizzato nel sito di Twitter hello, consultare la documentazione per sviluppatori di toohello Twitter.</span><span class="sxs-lookup"><span data-stu-id="ff64f-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="ff64f-177">Passare toohello [pagina Gestione applicazioni di Twitter](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="ff64f-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="ff64f-178">Creare una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-178">Create a new application.</span></span> 

    * <span data-ttu-id="ff64f-179">Per l'URL del sito Web hello, specificare un URL valido.</span><span class="sxs-lookup"><span data-stu-id="ff64f-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="ff64f-180">È toobe un sito in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="ff64f-180">It does not have toobe a live site.</span></span> <span data-ttu-id="ff64f-181">ma non è possibile specificare semplicemente `localhost`.</span><span class="sxs-lookup"><span data-stu-id="ff64f-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="ff64f-182">Lasciare vuoto il campo di callback hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-182">Leave hello callback field blank.</span></span> <span data-ttu-id="ff64f-183">i callback non richiede l'applicazione Hello client in che uso per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Creazione di un'applicazione in Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="ff64f-185">Facoltativamente, modificare le autorizzazioni dell'applicazione hello tooread sola.</span><span class="sxs-lookup"><span data-stu-id="ff64f-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="ff64f-186">Quando viene creata un'applicazione hello, visitare toohello **chiavi e i token di accesso** pagina.</span><span class="sxs-lookup"><span data-stu-id="ff64f-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="ff64f-187">Fare clic su hello pulsante toogenerate un token di accesso e segreto del token di accesso.</span><span class="sxs-lookup"><span data-stu-id="ff64f-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="ff64f-188">Mantenere queste informazioni utili, poiché sarà necessario hello procedura descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="ff64f-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="ff64f-189">Hello chiavi e segreti per un'applicazione hello Twitter forniscono l'account di accesso tooyour Twitter.</span><span class="sxs-lookup"><span data-stu-id="ff64f-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="ff64f-190">Considerate queste informazioni riservate, hello stesso come avviene la password di Twitter.</span><span class="sxs-lookup"><span data-stu-id="ff64f-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="ff64f-191">Ad esempio, evitare di incorporare queste informazioni in un'applicazione che è possibile assegnare tooothers.</span><span class="sxs-lookup"><span data-stu-id="ff64f-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="ff64f-192">Configurare un'applicazione hello client</span><span class="sxs-lookup"><span data-stu-id="ff64f-192">Configure hello client application</span></span>
<span data-ttu-id="ff64f-193">Abbiamo creato un'applicazione client che si connette utilizzando dati tooTwitter [API del Twitter di Streaming](https://dev.twitter.com/streaming/overview) eventi tweet toocollect su un set specifico di argomenti.</span><span class="sxs-lookup"><span data-stu-id="ff64f-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="ff64f-194">un'applicazione Hello utilizza hello [Sentiment140](http://help.sentiment140.com/) strumento open source, che assegna hello tweet tooeach valore di valutazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff64f-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="ff64f-195">0 = negativo</span><span class="sxs-lookup"><span data-stu-id="ff64f-195">0 = negative</span></span>
* <span data-ttu-id="ff64f-196">2 = neutrale</span><span class="sxs-lookup"><span data-stu-id="ff64f-196">2 = neutral</span></span>
* <span data-ttu-id="ff64f-197">4 = positivo</span><span class="sxs-lookup"><span data-stu-id="ff64f-197">4 = positive</span></span>

<span data-ttu-id="ff64f-198">Dopo gli eventi tweet hello sono stati assegnati un valore di sentiment, queste vengono inviate hub eventi toohello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ff64f-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="ff64f-199">Prima dell'esecuzione di un'applicazione hello richiede alcune informazioni da parte dell'utente, ad esempio le chiavi di Twitter hello e stringa di connessione hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="ff64f-200">È possibile fornire informazioni di configurazione hello nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff64f-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="ff64f-201">Eseguire un'applicazione hello e quindi usare dell'applicazione hello UI tooenter hello chiavi, i segreti e stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="ff64f-202">In questo caso, le informazioni di configurazione hello viene utilizzate per la sessione corrente, ma non viene salvato.</span><span class="sxs-lookup"><span data-stu-id="ff64f-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="ff64f-203">Modifica file config dell'applicazione hello e impostare i valori hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="ff64f-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="ff64f-204">Questo approccio mantiene le informazioni di configurazione hello, ma significa inoltre che queste informazioni potenzialmente riservate vengono archiviate in testo normale nel computer.</span><span class="sxs-lookup"><span data-stu-id="ff64f-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="ff64f-205">Hello procedura riportata di seguito descritti entrambi gli approcci.</span><span class="sxs-lookup"><span data-stu-id="ff64f-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="ff64f-206">Assicurarsi di aver scaricato e decompresso hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) applicazione, come indicato nei prerequisiti hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="ff64f-207">i valori di hello tooset in fase di esecuzione (e solo per la sessione corrente di hello), eseguire hello `TwitterWPFClient.exe` dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="ff64f-208">Quando un'applicazione hello viene richiesto, immettere hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="ff64f-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="ff64f-209">Hello Twitter Consumer tasto (API).</span><span class="sxs-lookup"><span data-stu-id="ff64f-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="ff64f-210">Hello Twitter segreto del cliente (chiave privata API).</span><span class="sxs-lookup"><span data-stu-id="ff64f-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="ff64f-211">Token di accesso Twitter Hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="ff64f-212">Segreto Token di accesso Twitter Hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="ff64f-213">Hello stringa informazioni di connessione è stato salvato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ff64f-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="ff64f-214">Assicurarsi di utilizzare una stringa di connessione hello che sia stato rimosso hello `EntityPath` coppia chiave-valore da.</span><span class="sxs-lookup"><span data-stu-id="ff64f-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="ff64f-215">parole chiave Twitter Hello che si desidera toodetermine valutazione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![Applicazione TwitterWpfClient in esecuzione, con le impostazioni oscurate](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="ff64f-217">i valori hello tooset in modo permanente, utilizzano un file di testo dell'editor tooopen hello TwitterWpfClient.exe.config.</span><span class="sxs-lookup"><span data-stu-id="ff64f-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="ff64f-218">Quindi in hello `<appSettings>` elemento, eseguire questa operazione:</span><span class="sxs-lookup"><span data-stu-id="ff64f-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="ff64f-219">Impostare `oauth_consumer_key` toohello Twitter Consumer tasto (API).</span><span class="sxs-lookup"><span data-stu-id="ff64f-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="ff64f-220">Impostare `oauth_consumer_secret` toohello Twitter segreto del cliente (chiave privata API).</span><span class="sxs-lookup"><span data-stu-id="ff64f-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="ff64f-221">Impostare `oauth_token` toohello Twitter Token di accesso.</span><span class="sxs-lookup"><span data-stu-id="ff64f-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="ff64f-222">Impostare `oauth_token_secret` toohello segreto Token di accesso Twitter.</span><span class="sxs-lookup"><span data-stu-id="ff64f-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="ff64f-223">Più avanti in hello `<appSettings>` elemento apportare queste modifiche:</span><span class="sxs-lookup"><span data-stu-id="ff64f-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="ff64f-224">Impostare `EventHubName` nome hub di eventi toohello (vale a dire toohello valore del percorso di entità hello).</span><span class="sxs-lookup"><span data-stu-id="ff64f-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="ff64f-225">Impostare `EventHubNameConnectionString` toohello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="ff64f-226">Assicurarsi di utilizzare una stringa di connessione hello che sia stato rimosso hello `EntityPath` coppia chiave-valore da.</span><span class="sxs-lookup"><span data-stu-id="ff64f-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="ff64f-227">Hello `<appSettings>` sezione aspetto hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="ff64f-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="ff64f-228">Per motivi di chiarezza e sicurezza, è stato applicato il ritorno a capo automatico ad alcune righe e sono stati rimossi alcuni caratteri.</span><span class="sxs-lookup"><span data-stu-id="ff64f-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![File di configurazione applicazione TwitterWpfClient in un editor di testo che mostra hello Twitter chiavi e segreti e sulle stringhe di connessione hub eventi hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="ff64f-230">Se è già stato avviato l'applicazione hello, eseguire TwitterWpfClient.exe.</span><span class="sxs-lookup"><span data-stu-id="ff64f-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="ff64f-231">Fare clic su sentiment social toocollect di hello pulsante start verde.</span><span class="sxs-lookup"><span data-stu-id="ff64f-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="ff64f-232">Visualizzare gli eventi di Tweet con hello **CreatedAt**, **argomento**, e **SentimentScore** valori inviati tooyour hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="ff64f-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![Applicazione TwitterWpfClient in esecuzione, con l'elenco di tweet visualizzato](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="ff64f-234">Se si verificano errori, e non viene visualizzato un flusso di tweet visualizzato nella parte inferiore di hello della finestra hello, è necessario verificare attentamente i segreti e le chiavi di hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="ff64f-235">Controllare inoltre la stringa di connessione hello (assicurarsi che non include hello `EntityPath` chiave e il valore.)</span><span class="sxs-lookup"><span data-stu-id="ff64f-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="ff64f-236">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="ff64f-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="ff64f-237">Ora che gli eventi tweet utilizza il flusso in tempo reale da Twitter, è possibile impostare un tooanalyze processo flusso Analitica questi eventi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="ff64f-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="ff64f-238">Nel portale di Azure hello, fare clic su **New** > **Internet of Things** > **processo flusso Analitica**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="ff64f-239">Nome del processo hello `socialtwitter-sa-job` e specificare una sottoscrizione, un gruppo di risorse e un percorso.</span><span class="sxs-lookup"><span data-stu-id="ff64f-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="ff64f-240">È una buona idea tooplace hello processo e hello hub eventi in hello stessa area per prestazioni ottimali e pertanto di non prestare tootransfer dati tra aree.</span><span class="sxs-lookup"><span data-stu-id="ff64f-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![Creazione di un nuovo processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="ff64f-242">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-242">Click **Create**.</span></span>

    <span data-ttu-id="ff64f-243">viene creato il processo di Hello e portale hello Visualizza i dettagli dei processi.</span><span class="sxs-lookup"><span data-stu-id="ff64f-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="ff64f-244">Specificare l'input processo hello</span><span class="sxs-lookup"><span data-stu-id="ff64f-244">Specify hello job input</span></span>

1. <span data-ttu-id="ff64f-245">Nel processo di flusso Analitica, in **processo topologia** centro hello del pannello processo hello, fare clic su **input**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="ff64f-246">In hello **input** pannello, fare clic su  **+ &nbsp;Aggiungi** e compilare pannello hello con questi valori:</span><span class="sxs-lookup"><span data-stu-id="ff64f-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="ff64f-247">**Alias di input**: utilizza il nome di hello `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="ff64f-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="ff64f-248">Se si usa un nome diverso, tenerne traccia, poiché sarà necessario in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ff64f-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="ff64f-249">**Tipo di origine**: selezionare **Flusso dati**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="ff64f-250">**Origine**: selezionare **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="ff64f-251">**Opzioni di importazione**: selezionare **Usa l'hub eventi della sottoscrizione corrente**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="ff64f-252">**Spazio dei nomi di Service bus**: selezionare hello spazio dei nomi hub eventi creato in precedenza (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="ff64f-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="ff64f-253">**Hub eventi**: hub eventi selezionare hello creato in precedenza (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="ff64f-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="ff64f-254">**Nome criterio hub eventi**: selezionare i criteri di accesso hello creato in precedenza (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="ff64f-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Creare un nuovo input per il processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="ff64f-256">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="ff64f-257">Specificare hello processo query</span><span class="sxs-lookup"><span data-stu-id="ff64f-257">Specify hello job query</span></span>

<span data-ttu-id="ff64f-258">Analisi di flusso supporta un semplice modello di query dichiarativa per descrivere le trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="ff64f-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="ff64f-259">toolearn più sul linguaggio di hello, vedere hello [riferimenti al linguaggio di Query di Azure flusso Analitica](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff64f-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="ff64f-260">Questa esercitazione permette di creare e testare diverse query su dati di Twitter.</span><span class="sxs-lookup"><span data-stu-id="ff64f-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="ff64f-261">numero di hello toocompare di menziona tra gli argomenti, è possibile utilizzare un [finestra a cascata](https://msdn.microsoft.com/library/azure/dn835055.aspx) conteggio hello tooget di menziona dall'argomento ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="ff64f-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="ff64f-262">Chiude hello **input** pannello se hai già fatto.</span><span class="sxs-lookup"><span data-stu-id="ff64f-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="ff64f-263">Nel Pannello di hello processo, fare clic su hello **Query** casella.</span><span class="sxs-lookup"><span data-stu-id="ff64f-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="ff64f-264">Azure Elenca gli input hello e output che sono configurati per il processo di hello e consente di creare una query che consente di trasformare flusso di input hello inviata toohello output.</span><span class="sxs-lookup"><span data-stu-id="ff64f-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="ff64f-265">Verificare che tale applicazione TwitterWpfClient hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="ff64f-266">In hello **Query** pannello, fare clic su Avanti toohello di hello punti `TwitterStream` di input e quindi selezionare **dati da un input di esempio**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Dal menu Opzioni toouse dati di esempio per hello voce processi di Streaming Analitica, con "Dati di input" selezionati](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="ff64f-268">Verrà aperto un pannello che consente di specificare la quantità tooget di dati di esempio, definito in termini di tempo hello tooread flusso di input.</span><span class="sxs-lookup"><span data-stu-id="ff64f-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="ff64f-269">Impostare **minuti** too3 e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    ![Opzioni di campionamento di flusso di input hello, con "3 minuti" selezionati.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="ff64f-271">Azure esempi relativi a 3 minuti dei dati dal flusso di input hello e invia una notifica quando i dati di esempio hello sono pronti.</span><span class="sxs-lookup"><span data-stu-id="ff64f-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="ff64f-272">Questa operazione richiede un breve tempo.</span><span class="sxs-lookup"><span data-stu-id="ff64f-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="ff64f-273">dati di esempio Hello vengono archiviati temporaneamente ed sono disponibili quando è aperta la finestra di query hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="ff64f-274">Se si chiude la finestra di query hello, vengono eliminati i dati di esempio hello e aver toocreate un nuovo set di dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="ff64f-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="ff64f-275">Modificare la query hello in hello codice editor toohello che segue:</span><span class="sxs-lookup"><span data-stu-id="ff64f-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="ff64f-276">Se non sono stati `TwitterStream` come hello alias di input hello, sostituire con l'alias per `TwitterStream` nella query hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="ff64f-277">Questa query utilizza hello **TIMESTAMP BY** toospecify (parola chiave) un campo timestamp hello payload toobe utilizzata nel calcolo temporale hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="ff64f-278">Se questo campo non è specificato, utilizzando hello di ogni evento arriva all'hub eventi hello viene eseguita l'operazione di windowing hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="ff64f-279">Altre informazioni nella sezione hello "ora di arrivo vs tempo applicazione" di [flusso Analitica Query riferimento](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff64f-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="ff64f-280">La query accede anche a un timestamp di fine hello di ogni finestra utilizzando hello **timestamp** proprietà.</span><span class="sxs-lookup"><span data-stu-id="ff64f-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="ff64f-281">Fare clic su **Test**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-281">Click **Test**.</span></span> <span data-ttu-id="ff64f-282">query di Hello viene eseguita sui dati hello è campionate.</span><span class="sxs-lookup"><span data-stu-id="ff64f-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="ff64f-283">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-283">Click **Save**.</span></span> <span data-ttu-id="ff64f-284">Consente di salvare la query hello come parte del processo di Streaming Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="ff64f-285">(Non salva i dati di esempio hello).</span><span class="sxs-lookup"><span data-stu-id="ff64f-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="ff64f-286">Provare a utilizzare diversi campi dal flusso hello</span><span class="sxs-lookup"><span data-stu-id="ff64f-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="ff64f-287">Hello nella tabella seguente elenca i campi di hello che fanno parte di hello dati flusso JSON.</span><span class="sxs-lookup"><span data-stu-id="ff64f-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="ff64f-288">È possibile tooexperiment disponibile nell'editor di query hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="ff64f-289">Proprietà JSON</span><span class="sxs-lookup"><span data-stu-id="ff64f-289">JSON property</span></span> | <span data-ttu-id="ff64f-290">Definizione</span><span class="sxs-lookup"><span data-stu-id="ff64f-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="ff64f-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="ff64f-291">CreatedAt</span></span> | <span data-ttu-id="ff64f-292">tempo di Hello è stato creato tale tweet hello</span><span class="sxs-lookup"><span data-stu-id="ff64f-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="ff64f-293">Argomento</span><span class="sxs-lookup"><span data-stu-id="ff64f-293">Topic</span></span> | <span data-ttu-id="ff64f-294">argomento Hello corrispondente hello specificato (parola chiave)</span><span class="sxs-lookup"><span data-stu-id="ff64f-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="ff64f-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="ff64f-295">SentimentScore</span></span> | <span data-ttu-id="ff64f-296">punteggio sentiment Hello Sentiment140</span><span class="sxs-lookup"><span data-stu-id="ff64f-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="ff64f-297">Autore</span><span class="sxs-lookup"><span data-stu-id="ff64f-297">Author</span></span> | <span data-ttu-id="ff64f-298">handle Twitter hello inviati tweet hello</span><span class="sxs-lookup"><span data-stu-id="ff64f-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="ff64f-299">Text</span><span class="sxs-lookup"><span data-stu-id="ff64f-299">Text</span></span> | <span data-ttu-id="ff64f-300">corpo Hello della tweet hello</span><span class="sxs-lookup"><span data-stu-id="ff64f-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="ff64f-301">Creare un sink di output</span><span class="sxs-lookup"><span data-stu-id="ff64f-301">Create an output sink</span></span>

<span data-ttu-id="ff64f-302">È stata definita ora un flusso di eventi, un input tooingest degli hub eventi e tooperform una query una trasformazione tramite flusso hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="ff64f-303">ultimo passaggio Hello è toodefine sink di output per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="ff64f-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="ff64f-304">In questa esercitazione, scrivere eventi tweet hello aggregato da hello processo query tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="ff64f-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="ff64f-305">È possibile distribuire anche i risultati tooAzure Database SQL, archiviazione tabelle di Azure, gli hub di eventi o Power BI, è necessario a seconda dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="ff64f-306">Specificare l'output del processo hello</span><span class="sxs-lookup"><span data-stu-id="ff64f-306">Specify hello job output</span></span>

1. <span data-ttu-id="ff64f-307">In hello **processo topologia** fare clic su hello **Output** casella.</span><span class="sxs-lookup"><span data-stu-id="ff64f-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="ff64f-308">In hello **output** pannello, fare clic su  **+ &nbsp;Aggiungi** e compilare pannello hello con questi valori:</span><span class="sxs-lookup"><span data-stu-id="ff64f-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="ff64f-309">**Alias di output**: utilizza il nome di hello `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="ff64f-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="ff64f-310">**Sink**: selezionare **Archivio BLOB**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="ff64f-311">**Opzioni di importazione**: selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="ff64f-312">**Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-312">**Storage account**.</span></span> <span data-ttu-id="ff64f-313">Selezionare **Crea un nuovo account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="ff64f-314">**Account di archiviazione** (seconda casella).</span><span class="sxs-lookup"><span data-stu-id="ff64f-314">**Storage account** (second box).</span></span> <span data-ttu-id="ff64f-315">Immettere `YOURNAMEsa`, dove `YOURNAME` rappresenta il nome o un'altra stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="ff64f-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="ff64f-316">nome Hello può utilizzare solo lettere minuscole e numeri e deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="ff64f-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="ff64f-317">**Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-317">**Container**.</span></span> <span data-ttu-id="ff64f-318">Immettere `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="ff64f-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="ff64f-319">nome account di archiviazione Hello e nome del contenitore sono tooprovide insieme usato un URI per l'archiviazione blob di hello, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ff64f-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Pannello "Nuovo output" per il processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="ff64f-321">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-321">Click **Create**.</span></span> 

    <span data-ttu-id="ff64f-322">Azure crea account di archiviazione hello e genera automaticamente una chiave.</span><span class="sxs-lookup"><span data-stu-id="ff64f-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="ff64f-323">Chiude hello **output** blade.</span><span class="sxs-lookup"><span data-stu-id="ff64f-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="ff64f-324">Avviare il processo di hello</span><span class="sxs-lookup"><span data-stu-id="ff64f-324">Start hello job</span></span>

<span data-ttu-id="ff64f-325">Sono stati specificati l'input del processo, la query e l'output.</span><span class="sxs-lookup"><span data-stu-id="ff64f-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="ff64f-326">Sono processi di flusso Analitica hello toostart pronto.</span><span class="sxs-lookup"><span data-stu-id="ff64f-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="ff64f-327">Verificare che tale applicazione TwitterWpfClient hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="ff64f-328">Nel Pannello di hello processo, fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-328">In hello job blade, click **Start**.</span></span>

    ![Avviare il processo di flusso Analitica hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="ff64f-330">In hello **inizio processo** pannello per **ora di inizio di output del processo**selezionare **ora** e quindi fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Pannello "Avvia processo" per il processo di flusso Analitica hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="ff64f-332">Azure notifica che ha avviato il processo di hello e nel Pannello di processo hello, viene visualizzato stato hello **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![Processo in esecuzione](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="ff64f-334">Visualizzare l'output per l'analisi del sentiment</span><span class="sxs-lookup"><span data-stu-id="ff64f-334">View output for sentiment analysis</span></span>

<span data-ttu-id="ff64f-335">Dopo il processo è iniziata l'esecuzione e sta elaborando il flusso Twitter in tempo reale di hello, è possibile visualizzare l'output di hello per l'analisi di valutazione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="ff64f-336">È possibile utilizzare uno strumento come [Azure Storage Explorer](https://http://storageexplorer.com/) o [Esplora Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview il processo di output in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="ff64f-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="ff64f-337">Da qui è possibile utilizzare [Power BI](https://powerbi.com/) hello di tooextend il tooinclude applicazione un dashboard personalizzato come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="ff64f-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="ff64f-339">Creare un'altra query argomenti relativi alle tendenze tooidentify</span><span class="sxs-lookup"><span data-stu-id="ff64f-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="ff64f-340">Un'altra query, è possibile utilizzare toounderstand Twitter sentiment si basa su un [finestra temporale scorrevole](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff64f-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="ff64f-341">argomenti relativi alle tendenze tooidentify, esaminare gli argomenti che superano un valore di soglia per i riferimenti in un periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="ff64f-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="ff64f-342">Ai fini di hello di questa esercitazione, è cercare argomenti che più di 20 volte menzionati nelle hello ultimi 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="ff64f-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="ff64f-343">Nel Pannello di hello processo, fare clic su **arrestare** processo hello toostop.</span><span class="sxs-lookup"><span data-stu-id="ff64f-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="ff64f-344">In hello **processo topologia** fare clic su hello **Query** casella.</span><span class="sxs-lookup"><span data-stu-id="ff64f-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="ff64f-345">Modificare i seguenti toohello di hello query:</span><span class="sxs-lookup"><span data-stu-id="ff64f-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="ff64f-346">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ff64f-346">Click **Save**.</span></span>

5. <span data-ttu-id="ff64f-347">Verificare che tale applicazione TwitterWpfClient hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ff64f-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="ff64f-348">Fare clic su **avviare** processo hello toorestart utilizzando hello nuova query.</span><span class="sxs-lookup"><span data-stu-id="ff64f-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="ff64f-349">Supporto</span><span class="sxs-lookup"><span data-stu-id="ff64f-349">Get support</span></span>
<span data-ttu-id="ff64f-350">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="ff64f-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff64f-351">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff64f-351">Next steps</span></span>
* [<span data-ttu-id="ff64f-352">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="ff64f-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ff64f-353">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="ff64f-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ff64f-354">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="ff64f-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ff64f-355">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="ff64f-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ff64f-356">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="ff64f-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
