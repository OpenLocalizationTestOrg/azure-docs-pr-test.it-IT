---
title: code di Azure in Visual Studio aaaOptimizing | Documenti Microsoft
description: "Informazioni su come il codice di Azure come strumento di ottimizzazione in Visual Studio consente di rendere il codice più affidabile e migliorare le prestazioni."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="a81c8-103">Ottimizzare il codice Azure</span><span class="sxs-lookup"><span data-stu-id="a81c8-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="a81c8-104">Quando si programmano App che usano Microsoft Azure, esistono alcune procedure consigliate da seguire toohelp evitare problemi di scalabilità, comportamento e le prestazioni in un ambiente cloud.</span><span class="sxs-lookup"><span data-stu-id="a81c8-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="a81c8-105">Microsoft fornisce uno strumento di analisi del codice di Azure che riconosce molti di questi problemi comunemente riscontrati e aiuta a risolverli.</span><span class="sxs-lookup"><span data-stu-id="a81c8-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="a81c8-106">È possibile scaricare lo strumento hello in Visual Studio tramite NuGet.</span><span class="sxs-lookup"><span data-stu-id="a81c8-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="a81c8-107">Regole di analisi codice di Azure</span><span class="sxs-lookup"><span data-stu-id="a81c8-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="a81c8-108">strumento di analisi del codice di Azure Hello utilizza hello seguendo regole tooautomatically flag del codice di Azure quando rileva i problemi noti che influiscono sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="a81c8-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="a81c8-109">I problemi rilevati vengono visualizzati come avvisi o errori del compilatore.</span><span class="sxs-lookup"><span data-stu-id="a81c8-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="a81c8-110">Codice avviso hello tooresolve correzioni o suggerimenti o errore vengono spesso forniti tramite un'icona lampadina.</span><span class="sxs-lookup"><span data-stu-id="a81c8-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="a81c8-111">Evitare di utilizzare la modalità stato sessione (in-process) predefinita</span><span class="sxs-lookup"><span data-stu-id="a81c8-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-112">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-112">ID</span></span>
<span data-ttu-id="a81c8-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="a81c8-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-114">Description</span></span>
<span data-ttu-id="a81c8-115">Se si Usa modalità stato sessione (in-process) predefinita di hello per le applicazioni cloud, è possibile perdere lo stato della sessione.</span><span class="sxs-lookup"><span data-stu-id="a81c8-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="a81c8-116">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-117">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-117">Reason</span></span>
<span data-ttu-id="a81c8-118">Per impostazione predefinita, modalità di stato sessione hello specificata nel file Web. config hello è in-process.</span><span class="sxs-lookup"><span data-stu-id="a81c8-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="a81c8-119">Inoltre, se non vengono specificate voci nel file di configurazione di hello, hello modalità stato sessione predefinita tooin-process.</span><span class="sxs-lookup"><span data-stu-id="a81c8-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="a81c8-120">modalità in-process Hello archivia lo stato della sessione in memoria nel server web hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="a81c8-121">Quando un'istanza viene riavviata o una nuova istanza viene utilizzata per il bilanciamento del carico o il supporto di failover, non viene salvato lo stato della sessione hello archiviato in memoria nel server web hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="a81c8-122">Questa situazione impedisce l'applicazione hello essere scalabile nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="a81c8-123">Lo stato della sessione ASP.NET supporta diverse opzioni di archiviazione per i dati dello stato sessione: InProc, StateServer, SQLServer, personalizzato e Off.</span><span class="sxs-lookup"><span data-stu-id="a81c8-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="a81c8-124">Si consiglia di utilizzare dati toohost in modalità personalizzata in un archivio di stato sessione esterno, ad esempio [provider di stato della sessione di Azure per Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="a81c8-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-125">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-125">Solution</span></span>
<span data-ttu-id="a81c8-126">Una soluzione consigliata è toostore lo stato della sessione in un servizio cache gestita.</span><span class="sxs-lookup"><span data-stu-id="a81c8-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="a81c8-127">Informazioni su come toouse [provider di stato della sessione di Azure per Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore lo stato della sessione.</span><span class="sxs-lookup"><span data-stu-id="a81c8-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="a81c8-128">È possibile inoltre archivio sessione indicare in altre posizioni di tooensure che l'applicazione sia scalabile nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="a81c8-129">altre informazioni sulle soluzioni alternative, vedere toolearn [modalità stato sessione](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="a81c8-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="a81c8-130">L’esecuzione del metodo non deve essere asincrona</span><span class="sxs-lookup"><span data-stu-id="a81c8-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-131">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-131">ID</span></span>
<span data-ttu-id="a81c8-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="a81c8-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-133">Description</span></span>
<span data-ttu-id="a81c8-134">Creare metodi asincroni (ad esempio [await](https://msdn.microsoft.com/library/hh156528.aspx)) di fuori di hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (metodo) e quindi chiamare i metodi di async hello da [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="a81c8-135">Dichiarazione di hello [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) il metodo asincrono comporta lavoro hello ruolo tooenter un ciclo di riavvio.</span><span class="sxs-lookup"><span data-stu-id="a81c8-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="a81c8-136">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-137">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-137">Reason</span></span>
<span data-ttu-id="a81c8-138">La chiamata di metodi asincroni all'interno di hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo causa hello runtime toorecycle hello lavoro ruolo del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="a81c8-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="a81c8-139">Quando viene avviato un ruolo di lavoro, l'intera esecuzione del programma ha luogo all'interno di hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo.</span><span class="sxs-lookup"><span data-stu-id="a81c8-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="a81c8-140">In fase di chiusura hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo fa sì che il lavoro hello toorestart ruolo.</span><span class="sxs-lookup"><span data-stu-id="a81c8-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="a81c8-141">Quando runtime ruolo di lavoro hello raggiunge metodo async hello, invia tutte le operazioni dopo il metodo asincrono hello e lo restituisce.</span><span class="sxs-lookup"><span data-stu-id="a81c8-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="a81c8-142">Questo comporta lavoro hello tooexit ruolo dallo hello [ [ [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (metodo) e riavviare.</span><span class="sxs-lookup"><span data-stu-id="a81c8-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="a81c8-143">Durante l'iterazione successiva di hello di esecuzione, il ruolo di lavoro hello raggiunge nuovamente metodo async hello e viene riavviato, causando lavoro hello nuovamente anche toorecycle ruolo.</span><span class="sxs-lookup"><span data-stu-id="a81c8-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-144">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-144">Solution</span></span>
<span data-ttu-id="a81c8-145">Posizionare tutte le operazioni asincrone di fuori di hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo.</span><span class="sxs-lookup"><span data-stu-id="a81c8-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="a81c8-146">Quindi, chiamare il metodo asincrono hello sottoposta a refactoring all'interno di hello [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo, ad esempio .wait di RunAsync ().</span><span class="sxs-lookup"><span data-stu-id="a81c8-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="a81c8-147">strumento di analisi del codice di Azure Hello può aiutare a risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="a81c8-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="a81c8-148">Hello seguente frammento di codice mostra correzione del codice hello per questo problema:</span><span class="sxs-lookup"><span data-stu-id="a81c8-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="a81c8-149">Autenticazione della firma di accesso condiviso con il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="a81c8-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-150">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-150">ID</span></span>
<span data-ttu-id="a81c8-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="a81c8-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-152">Description</span></span>
<span data-ttu-id="a81c8-153">Uso della firma di accesso condiviso per l’autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a81c8-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="a81c8-154">Il servizio di controllo di accesso (ACS) è deprecato per l'autenticazione di bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="a81c8-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="a81c8-155">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-156">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-156">Reason</span></span>
<span data-ttu-id="a81c8-157">Per una sicurezza ottimale, Azure Active Directory consiste nella sostituzione dell’autenticazione ACS con l'autenticazione SAS.</span><span class="sxs-lookup"><span data-stu-id="a81c8-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="a81c8-158">Vedere [Azure Active Directory è hello futuro di ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) per informazioni sul piano di transizione hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-159">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-159">Solution</span></span>
<span data-ttu-id="a81c8-160">Utilizzare l'autenticazione SAS nelle app.</span><span class="sxs-lookup"><span data-stu-id="a81c8-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="a81c8-161">Hello di esempio seguente viene illustrato come toouse un tooaccess token SAS esistente un servizio del bus di spazio dei nomi o entità.</span><span class="sxs-lookup"><span data-stu-id="a81c8-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="a81c8-162">Hello seguenti argomenti per ulteriori informazioni, vedere.</span><span class="sxs-lookup"><span data-stu-id="a81c8-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="a81c8-163">Per una panoramica, vedere [autenticazione della firma di accesso condiviso con il bus di servizio](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="a81c8-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="a81c8-164">Come toouse autenticazione della firma di accesso condiviso con il Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="a81c8-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="a81c8-165">Per un progetto di esempio, vedere l'articolo relativo all' [autenticazione tramite firma di accesso condiviso con le sottoscrizioni del bus di servizio](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="a81c8-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="a81c8-166">È consigliabile utilizzare tooavoid metodo OnMessage "ciclo di ricezione"</span><span class="sxs-lookup"><span data-stu-id="a81c8-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-167">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-167">ID</span></span>
<span data-ttu-id="a81c8-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="a81c8-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-169">Description</span></span>
<span data-ttu-id="a81c8-170">tooavoid verso un "ciclo di ricezione," hello chiamante **OnMessage** metodo è una soluzione migliore per la ricezione di messaggi rispetto a chiamata hello **ricezione** metodo.</span><span class="sxs-lookup"><span data-stu-id="a81c8-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="a81c8-171">Tuttavia, se è necessario utilizzare hello **ricezione** (metodo) e specificare un tempo di attesa del server non predefinito, assicurarsi che il tempo di attesa hello sia più di un minuto.</span><span class="sxs-lookup"><span data-stu-id="a81c8-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="a81c8-172">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-173">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-173">Reason</span></span>
<span data-ttu-id="a81c8-174">Quando si chiama **OnMessage**, client hello avvia un message pump interno che esegue il polling costantemente hello coda o sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a81c8-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="a81c8-175">Il message pump di contiene un ciclo infinito che effettua una chiamata tooreceive messaggi.</span><span class="sxs-lookup"><span data-stu-id="a81c8-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="a81c8-176">Se il timeout della chiamata di hello, genera una nuova chiamata.</span><span class="sxs-lookup"><span data-stu-id="a81c8-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="a81c8-177">intervallo di timeout Hello è determinata dal valore hello di hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) proprietà di hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)che viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a81c8-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="a81c8-178">Hello vantaggio dell'utilizzo di **OnMessage** confrontati troppo**ricezione** è che gli utenti non hanno toomanually eseguire il polling per i messaggi, gestione delle eccezioni, elaborare più messaggi in parallelo e completare hello messaggi.</span><span class="sxs-lookup"><span data-stu-id="a81c8-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="a81c8-179">Se si chiama **ricezione** senza utilizzare il valore predefinito, essere hello che *ServerWaitTime* valore è superiore a un minuto.</span><span class="sxs-lookup"><span data-stu-id="a81c8-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="a81c8-180">Impostazione *ServerWaitTime* toomore di un minuto impedisce server hello scadere prima completa ricezione del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-181">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-181">Solution</span></span>
<span data-ttu-id="a81c8-182">Vedere hello seguono esempi di codice per gli utilizzi consigliati.</span><span class="sxs-lookup"><span data-stu-id="a81c8-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="a81c8-183">Per altre informazioni, vedere [metodo QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) e [metodo QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="a81c8-184">prestazioni hello tooimprove di hello infrastruttura di messaggistica di Azure, vedere il modello di progettazione di hello [Introduzione alla messaggistica asincrona](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="a81c8-185">Hello seguito è riportato un esempio di utilizzo **OnMessage** tooreceive messaggi.</span><span class="sxs-lookup"><span data-stu-id="a81c8-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="a81c8-186">Hello seguito è riportato un esempio di utilizzo **ricezione** con server predefinito hello tempo di attesa.</span><span class="sxs-lookup"><span data-stu-id="a81c8-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="a81c8-187">Hello seguito è riportato un esempio di utilizzo **ricezione** tempo di attesa con un server non predefinito.</span><span class="sxs-lookup"><span data-stu-id="a81c8-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="a81c8-188">Si consideri l'utilizzo di metodi asincroni del Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="a81c8-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-189">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-189">ID</span></span>
<span data-ttu-id="a81c8-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="a81c8-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-191">Description</span></span>
<span data-ttu-id="a81c8-192">Utilizzare prestazioni tooimprove metodi di Service Bus asincrono con la messaggistica negoziata.</span><span class="sxs-lookup"><span data-stu-id="a81c8-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="a81c8-193">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-194">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-194">Reason</span></span>
<span data-ttu-id="a81c8-195">Utilizzare i metodi asincroni consente concorrenza delle applicazioni perché l'esecuzione di ogni chiamata non blocca il thread principale di hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="a81c8-196">Quando si utilizzano i metodi di messaggistica del Bus di servizio, l’esecuzione di un'operazione (inviare, ricevere, eliminare, ecc) richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="a81c8-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="a81c8-197">Questo tempo include l'elaborazione di hello dell'operazione hello dal servizio Bus di servizio hello latenza toohello aggiunta di hello richiesta e risposta di hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="a81c8-198">numero di hello tooincrease di operazioni per volta, le operazioni vengano eseguite simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="a81c8-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="a81c8-199">Per ulteriori informazioni, vedere troppo[procedure consigliate per prestazioni miglioramenti tramite servizio di messaggistica negoziata del Bus](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-200">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-200">Solution</span></span>
<span data-ttu-id="a81c8-201">Vedere [classe QueueClient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) per informazioni su come toouse hello consigliato metodo asincrono.</span><span class="sxs-lookup"><span data-stu-id="a81c8-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="a81c8-202">prestazioni hello tooimprove di hello infrastruttura di messaggistica di Azure, vedere il modello di progettazione di hello [Introduzione alla messaggistica asincrona](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="a81c8-203">Prendere in considerazione il partizionamento delle code e degli argomenti del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="a81c8-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-204">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-204">ID</span></span>
<span data-ttu-id="a81c8-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="a81c8-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-206">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-206">Description</span></span>
<span data-ttu-id="a81c8-207">Esegue il partizionamento delle code e degli argomenti del bus di servizio per ottenere prestazioni migliori con la messaggistica del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="a81c8-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="a81c8-208">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-209">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-209">Reason</span></span>
<span data-ttu-id="a81c8-210">Partizionamento di code e argomenti Service Bus aumenta la disponibilità di velocità effettiva e il servizio delle prestazioni perché hello velocità effettiva complessiva di una coda o argomento partizionato non è più limitata dalle prestazioni hello di un singolo broker messaggi o archivio di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="a81c8-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="a81c8-211">Una interruzione temporanea di un archivio di messaggistica non influisce sulla disponibilità di code e argomenti partizionati.</span><span class="sxs-lookup"><span data-stu-id="a81c8-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="a81c8-212">Per ulteriori informazioni, vedere [Partizionamento delle entità di messaggistica](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-213">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-213">Solution</span></span>
<span data-ttu-id="a81c8-214">Hello seguente frammento di codice viene illustrato come toopartition entità di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="a81c8-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="a81c8-215">Per ulteriori informazioni, vedere [argomenti e code del Bus di servizio partizionati | Blog di Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) ed estrarre hello [coda partizionata di Microsoft Azure Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) esempio.</span><span class="sxs-lookup"><span data-stu-id="a81c8-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="a81c8-216">Non impostare SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="a81c8-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-217">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-217">ID</span></span>
<span data-ttu-id="a81c8-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="a81c8-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-219">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-219">Description</span></span>
<span data-ttu-id="a81c8-220">Evitare di usare SharedAccessStartTimeset toohello corrente avvio tooimmediately hello criterio di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="a81c8-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="a81c8-221">È necessario solo tooset questa proprietà se si desidera criteri di accesso condiviso di toostart hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="a81c8-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="a81c8-222">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-223">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-223">Reason</span></span>
<span data-ttu-id="a81c8-224">La sincronizzazione dell'orologio comporta una differenza oraria lieve tra i Data Center.</span><span class="sxs-lookup"><span data-stu-id="a81c8-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="a81c8-225">Ad esempio, si potrebbe pensare ora di inizio hello di impostazione di un criterio di archiviazione SAS perché hello ora corrente usando Now o un metodo simile causerà l'effetto di hello SAS criteri tootake immediatamente.</span><span class="sxs-lookup"><span data-stu-id="a81c8-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="a81c8-226">Tuttavia, le differenze di orario hello tra Data Center possono causare problemi con questo, a poiché alcuni Data Center potrebbero essere leggermente successiva all'ora di inizio di hello, mentre altri in anticipo.</span><span class="sxs-lookup"><span data-stu-id="a81c8-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="a81c8-227">Di conseguenza, hello criterio SAS può scadere velocemente (o anche immediatamente) se durata criteri hello impostata è troppo breve.</span><span class="sxs-lookup"><span data-stu-id="a81c8-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="a81c8-228">Per ulteriori informazioni sull'uso di firma di accesso condiviso in archiviazione di Azure, vedere [introduzione tabella firma di accesso condiviso (firma di accesso condiviso) SAS coda aggiornamento tooBlob SAS - Blog del Team Microsoft Azure Storage - del sito e Home - blog MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-229">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-229">Solution</span></span>
<span data-ttu-id="a81c8-230">Rimuovere l'istruzione hello che imposta l'ora di inizio hello dei criteri di accesso condiviso hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="a81c8-231">strumento di analisi del codice di Azure Hello viene fornita una correzione per questo problema.</span><span class="sxs-lookup"><span data-stu-id="a81c8-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="a81c8-232">Per ulteriori informazioni sulla gestione della sicurezza, vedere il modello di struttura hello [passepartout](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="a81c8-233">Hello frammento di codice seguente viene illustrato correzione del codice hello per questo problema.</span><span class="sxs-lookup"><span data-stu-id="a81c8-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="a81c8-234">L’ora di scadenza del criterio di accesso condiviso deve essere più di cinque minuti </span><span class="sxs-lookup"><span data-stu-id="a81c8-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-235">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-235">ID</span></span>
<span data-ttu-id="a81c8-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="a81c8-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-237">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-237">Description</span></span>
<span data-ttu-id="a81c8-238">Possono esistere fino a cinque minuti una differenza di orologi tra i Data Center in posizioni diverse, a causa di tooa condizione è nota come "sfasamento."</span><span class="sxs-lookup"><span data-stu-id="a81c8-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="a81c8-239">token del criterio SAS hello tooprevent di scadenza precedente alla data di impostare hello scadenza ora toobe più di cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="a81c8-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="a81c8-240">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-241">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-241">Reason</span></span>
<span data-ttu-id="a81c8-242">Data Center in posizioni diverse in tutto il mondo hello sincronizzare un segnale di clock.</span><span class="sxs-lookup"><span data-stu-id="a81c8-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="a81c8-243">Poiché il tempo per i percorsi toodifferent tootravel segnale di clock, può esserci uno sfasamento di orario tra i Data Center in località geografiche diverse Sebbene tutto sia sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="a81c8-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="a81c8-244">Questa differenza temporale può avere implicazioni di accesso condiviso criteri inizio ora e scadenza intervallo hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="a81c8-245">Pertanto, tooensure criterio di accesso condiviso diventa effettiva immediatamente, non specificare l'ora di inizio hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="a81c8-246">Assicurarsi, inoltre, ora di scadenza hello è superiore al timeout anticipato tooprevent di 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="a81c8-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="a81c8-247">Per ulteriori informazioni sull'uso della firma di accesso condiviso in archiviazione di Azure, vedere [introduzione tabella firma di accesso condiviso (firma di accesso condiviso) SAS coda aggiornamento tooBlob SAS - Blog del Team Microsoft Azure Storage - del sito e Home - blog MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-248">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-248">Solution</span></span>
<span data-ttu-id="a81c8-249">Per ulteriori informazioni sulla gestione della sicurezza, vedere il modello di progettazione di hello [passepartout](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="a81c8-250">Hello Ecco un esempio non viene specificata un'ora di inizio dei criteri di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="a81c8-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="a81c8-251">Hello Ecco un esempio di specificare un'ora di inizio dei criteri di accesso condiviso con una scadenza del criterio maggiore di cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="a81c8-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="a81c8-252">Per ulteriori informazioni, [Creare e usare una firma di accesso condiviso](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="a81c8-253">Utilizzare CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="a81c8-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-254">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-254">ID</span></span>
<span data-ttu-id="a81c8-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="a81c8-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-256">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-256">Description</span></span>
<span data-ttu-id="a81c8-257">Utilizzo di hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) classe per i progetti, ad esempio sito Web di Azure e servizi mobili di Azure non genera problemi di runtime.</span><span class="sxs-lookup"><span data-stu-id="a81c8-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="a81c8-258">Come procedura consigliata, tuttavia, è toouse una buona idea Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) come una modalità unificata di gestione delle configurazioni per tutte le applicazioni Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="a81c8-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="a81c8-259">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-260">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-260">Reason</span></span>
<span data-ttu-id="a81c8-261">CloudConfigurationManager legge l'ambiente dell'applicazione hello configurazione file toohello appropriato.</span><span class="sxs-lookup"><span data-stu-id="a81c8-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="a81c8-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="a81c8-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="a81c8-263">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-263">Solution</span></span>
<span data-ttu-id="a81c8-264">Effettuare il refactoring del hello toouse codice [CloudConfigurationManager classe](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="a81c8-265">Una correzione del codice per questo problema viene fornita dallo strumento di analisi del codice di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="a81c8-266">Hello frammento di codice seguente viene illustrato correzione del codice hello per questo problema.</span><span class="sxs-lookup"><span data-stu-id="a81c8-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="a81c8-267">Replace</span><span class="sxs-lookup"><span data-stu-id="a81c8-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="a81c8-268">con</span><span class="sxs-lookup"><span data-stu-id="a81c8-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="a81c8-269">Di seguito è riportato un esempio di come toostore hello impostazione di configurazione in un file app. config o Web. config.</span><span class="sxs-lookup"><span data-stu-id="a81c8-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="a81c8-270">Aggiungere una sezione appSettings di hello impostazioni toohello hello del file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a81c8-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="a81c8-271">di seguito Hello è Web. config per il precedente esempio di codice hello hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="a81c8-272">Evitare di utilizzare stringhe di connessione hardcoded</span><span class="sxs-lookup"><span data-stu-id="a81c8-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-273">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-273">ID</span></span>
<span data-ttu-id="a81c8-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="a81c8-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-275">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-275">Description</span></span>
<span data-ttu-id="a81c8-276">Se si utilizzano stringhe di connessione hardcoded ed è necessario tooupdate loro in un secondo momento, si sarà toomake modifiche tooyour del codice sorgente e ricompilare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="a81c8-277">Tuttavia, se si archiviano le stringhe di connessione in un file di configurazione, è possibile modificarle successivamente semplicemente aggiornando il file di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="a81c8-278">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-279">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-279">Reason</span></span>
<span data-ttu-id="a81c8-280">Impostare come hardcoded le stringhe di connessione è sconsigliata perché si verificano problemi quando le stringhe di connessione è necessario modificare rapidamente toobe.</span><span class="sxs-lookup"><span data-stu-id="a81c8-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="a81c8-281">Inoltre, se il progetto hello deve toobe selezionato nel controllo toosource, le stringhe di connessione hardcoded introducono vulnerabilità della sicurezza perché hello stringhe possono essere visualizzate nel codice sorgente hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-282">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-282">Solution</span></span>
<span data-ttu-id="a81c8-283">Archiviare le stringhe di connessione nel file di configurazione hello o ambienti di Azure.</span><span class="sxs-lookup"><span data-stu-id="a81c8-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="a81c8-284">Per le applicazioni autonome, utilizzare le impostazioni della stringa di connessione toostore app. config.</span><span class="sxs-lookup"><span data-stu-id="a81c8-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="a81c8-285">Per le applicazioni web ospitate in IIS, utilizzare le stringhe di connessione toostore Web. config.</span><span class="sxs-lookup"><span data-stu-id="a81c8-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="a81c8-286">Per le applicazioni vNext ASP.NET, utilizzare le stringhe di connessione toostore configuration.json.</span><span class="sxs-lookup"><span data-stu-id="a81c8-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="a81c8-287">Per informazioni sull'uso di file di configurazione, ad esempio web.config o app. config, vedere [Linee guida configurazione di ASP.NET Web](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="a81c8-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="a81c8-288">Per informazioni su come funzionano le variabili di ambiente di Azure, vedere [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) (Siti Web di Microsoft Azure sul funzionamento delle stringhe di applicazione e di connessione).</span><span class="sxs-lookup"><span data-stu-id="a81c8-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="a81c8-289">Per informazioni sull'archiviazione della stringa di connessione nel codice sorgente, vedere [evitare di inserire informazioni riservate come le stringhe di connessione nei file archiviati nel repository del codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="a81c8-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="a81c8-290">Utilizzo del file di configurazione di Diagnostica.</span><span class="sxs-lookup"><span data-stu-id="a81c8-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-291">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-291">ID</span></span>
<span data-ttu-id="a81c8-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="a81c8-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-293">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-293">Description</span></span>
<span data-ttu-id="a81c8-294">Anziché configurare le impostazioni di diagnostica nel codice, ad esempio tramite hello Microsoft.WindowsAzure.Diagnostics API di programmazione, è necessario configurare le impostazioni di diagnostica nel file Diagnostics wadcfg hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="a81c8-295">(O, diagnostics.wadcfgx se si utilizza Azure SDK 2.5).</span><span class="sxs-lookup"><span data-stu-id="a81c8-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="a81c8-296">In questo modo, è possibile modificare le impostazioni di diagnostica senza toorecompile il codice.</span><span class="sxs-lookup"><span data-stu-id="a81c8-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="a81c8-297">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-298">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-298">Reason</span></span>
<span data-ttu-id="a81c8-299">Prima di Azure SDK 2.5 (che usa diagnostica di Azure 1.3), la diagnostica di Azure (WAD) è stato possibile configurare utilizzando diversi metodi: aggiungendola toohello blob di configurazione nella risorsa di archiviazione usando codice imperativo, una configurazione dichiarativa o default hello configurazione.</span><span class="sxs-lookup"><span data-stu-id="a81c8-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="a81c8-300">Tuttavia, hello preferito modo tooconfigure diagnostica è un file di configurazione XML (Diagnostics. wadcfg o wadcfgx per SDK 2.5 e versioni successive) nel progetto di applicazione hello toouse.</span><span class="sxs-lookup"><span data-stu-id="a81c8-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="a81c8-301">In questo approccio, il file Diagnostics wadcfg hello completamente definisce la configurazione di hello e possono essere aggiornate e ridistribuito come desiderato.</span><span class="sxs-lookup"><span data-stu-id="a81c8-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="a81c8-302">Combinazione utilizzare hello del file di configurazione Diagnostics. wadcfg hello con hello metodi a livello di codice di impostazione delle configurazioni tramite hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)o [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) classi possono causare tooconfusion.</span><span class="sxs-lookup"><span data-stu-id="a81c8-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="a81c8-303">Vedere [Avviare o modificare la configurazione della diagnostica di Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="a81c8-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="a81c8-304">A partire da 1.3 WAD (incluso in Azure SDK 2.5), non è più diagnostica tooconfigure del codice toouse possibili.</span><span class="sxs-lookup"><span data-stu-id="a81c8-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="a81c8-305">Di conseguenza, è possibile specificare solo configurazione hello quando l'applicazione o l'aggiornamento dell'estensione diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-306">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-306">Solution</span></span>
<span data-ttu-id="a81c8-307">Utilizzare hello diagnostica toomove Progettazione impostazioni strumenti diagnostici toohello diagnostica configurazione file di configurazione (wadcfg o wadcfgx per SDK 2.5 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="a81c8-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="a81c8-308">È inoltre consigliabile installare [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) e utilizzo funzionalità di diagnostica più recenti hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="a81c8-309">Nel menu di scelta rapida hello ruolo hello che si desidera tooconfigure, scegliere Proprietà e quindi scegliere la scheda di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="a81c8-310">In hello **diagnostica** sezione, assicurarsi che tale hello **Abilita diagnostica** casella di controllo è selezionata.</span><span class="sxs-lookup"><span data-stu-id="a81c8-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="a81c8-311">Scegliere hello **configura** pulsante.</span><span class="sxs-lookup"><span data-stu-id="a81c8-311">Choose hello **Configure** button.</span></span>

   ![Accesso opzione Abilita diagnostica hello](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="a81c8-313">Vedere [Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) .per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="a81c8-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="a81c8-314">Evitare di dichiarare gli oggetti DbContext come static</span><span class="sxs-lookup"><span data-stu-id="a81c8-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="a81c8-315">ID</span><span class="sxs-lookup"><span data-stu-id="a81c8-315">ID</span></span>
<span data-ttu-id="a81c8-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="a81c8-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="a81c8-317">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a81c8-317">Description</span></span>
<span data-ttu-id="a81c8-318">memoria toosave, evitare di dichiarare gli oggetti DBContext come statici.</span><span class="sxs-lookup"><span data-stu-id="a81c8-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="a81c8-319">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a81c8-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a81c8-320">Motivo</span><span class="sxs-lookup"><span data-stu-id="a81c8-320">Reason</span></span>
<span data-ttu-id="a81c8-321">Gli oggetti DBContext contengono hello risultati della query da ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="a81c8-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="a81c8-322">Gli oggetti DBContext statici non vengono eliminati fino a quando non viene scaricato il dominio di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a81c8-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="a81c8-323">Pertanto, un oggetto DBContext statico può utilizzare grandi quantità di memoria.</span><span class="sxs-lookup"><span data-stu-id="a81c8-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="a81c8-324">Soluzione</span><span class="sxs-lookup"><span data-stu-id="a81c8-324">Solution</span></span>
<span data-ttu-id="a81c8-325">Dichiarare DBContext come una variabile locale o un campo di istanza non statico, utilizzarlo per un'attività e poi eliminarlo dopo l'uso.</span><span class="sxs-lookup"><span data-stu-id="a81c8-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="a81c8-326">Hello classe controller MVC di esempio seguente viene illustrato come toouse hello oggetto DBContext.</span><span class="sxs-lookup"><span data-stu-id="a81c8-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="a81c8-327">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a81c8-327">Next steps</span></span>
<span data-ttu-id="a81c8-328">toolearn più sull'ottimizzazione e risoluzione dei problemi di App di Azure, vedere [risolvere i problemi relativi a un'app web nel servizio App di Azure con Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="a81c8-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
