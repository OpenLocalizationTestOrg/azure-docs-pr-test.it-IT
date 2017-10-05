---
title: Ottimizzazione del codice di Azure in Visual Studio | Documentazione Microsoft
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
ms.openlocfilehash: 8f145502a856798d6e69ac11f324c72fa23f938e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="f3d75-103">Ottimizzare il codice Azure</span><span class="sxs-lookup"><span data-stu-id="f3d75-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="f3d75-104">Quando si programmano app che utilizzano Microsoft Azure, esistono alcune procedure consigliate da seguire per evitare problemi con la scalabilità di app, il comportamento e le prestazioni in un ambiente cloud.</span><span class="sxs-lookup"><span data-stu-id="f3d75-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow to help avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="f3d75-105">Microsoft fornisce uno strumento di analisi del codice di Azure che riconosce molti di questi problemi comunemente riscontrati e aiuta a risolverli.</span><span class="sxs-lookup"><span data-stu-id="f3d75-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="f3d75-106">È possibile scaricare lo strumento in Visual Studio tramite NuGet.</span><span class="sxs-lookup"><span data-stu-id="f3d75-106">You can download the tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="f3d75-107">Regole di analisi codice di Azure</span><span class="sxs-lookup"><span data-stu-id="f3d75-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="f3d75-108">Lo strumento di analisi del codice di Azure utilizza le regole seguenti per contrassegnare automaticamente il codice di Azure quando rileva i problemi noti che influiscono sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="f3d75-108">The Azure Code Analysis tool uses the following rules to automatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="f3d75-109">I problemi rilevati vengono visualizzati come avvisi o errori del compilatore.</span><span class="sxs-lookup"><span data-stu-id="f3d75-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="f3d75-110">Correzioni del codice o suggerimenti per risolvere l'avviso o l’errore vengono spesso forniti tramite un'icona a forma di lampadina.</span><span class="sxs-lookup"><span data-stu-id="f3d75-110">Code fixes or suggestions to resolve the warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="f3d75-111">Evitare di utilizzare la modalità stato sessione (in-process) predefinita</span><span class="sxs-lookup"><span data-stu-id="f3d75-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-112">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-112">ID</span></span>
<span data-ttu-id="f3d75-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="f3d75-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-114">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-114">Description</span></span>
<span data-ttu-id="f3d75-115">Se si utilizza la modalità di stato sessione (in-process) predefinita per le applicazioni cloud, è possibile perdere lo stato della sessione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-115">If you use the default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="f3d75-116">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-117">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-117">Reason</span></span>
<span data-ttu-id="f3d75-118">Per impostazione predefinita, la modalità stato sessione specificata nel file Web. config è in corso.</span><span class="sxs-lookup"><span data-stu-id="f3d75-118">By default, the session state mode specified in the web.config file is in-process.</span></span> <span data-ttu-id="f3d75-119">Inoltre, se nessuna voce è specificata nel file di configurazione, la modalità di stato della sessione è predefinita per in-process.</span><span class="sxs-lookup"><span data-stu-id="f3d75-119">Also, if no entry specified in the configuration file, the Session State mode defaults to in-process.</span></span> <span data-ttu-id="f3d75-120">La modalità in-process memorizza lo stato della sessione sul server web.</span><span class="sxs-lookup"><span data-stu-id="f3d75-120">The in-process mode stores session state in memory on the web server.</span></span> <span data-ttu-id="f3d75-121">Quando un'istanza viene riavviata o una nuova istanza viene utilizzata per il bilanciamento del carico o il supporto di failover, non viene salvato lo stato della sessione archiviato in memoria sul server web.</span><span class="sxs-lookup"><span data-stu-id="f3d75-121">When an instance is restarted or a new instance is used for load balancing or failover support, the session state stored in memory on the web server isn’t saved.</span></span> <span data-ttu-id="f3d75-122">Questa situazione impedisce che l'applicazione sia scalabile nel cloud.</span><span class="sxs-lookup"><span data-stu-id="f3d75-122">This situation prevents the application from being scalable on the cloud.</span></span>

<span data-ttu-id="f3d75-123">Lo stato della sessione ASP.NET supporta diverse opzioni di archiviazione per i dati dello stato sessione: InProc, StateServer, SQLServer, personalizzato e Off.</span><span class="sxs-lookup"><span data-stu-id="f3d75-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="f3d75-124">È consigliabile utilizzare la modalità personalizzata per ospitare i dati in un archivio esterno dello stato della sessione, ad esempio [Provider di stato della sessione di Azure per Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="f3d75-124">It’s recommended that you use Custom mode to host data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-125">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-125">Solution</span></span>
<span data-ttu-id="f3d75-126">Una soluzione consigliata consiste nell'archiviare lo stato della sessione in un servizio cache gestito.</span><span class="sxs-lookup"><span data-stu-id="f3d75-126">One recommended solution is to store session state on a managed cache service.</span></span> <span data-ttu-id="f3d75-127">Informazioni su come utilizzare [il provider di stato della sessione di Azure per Redis](http://go.microsoft.com/fwlink/?LinkId=401521) per archiviare lo stato della sessione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-127">Learn how to use [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) to store your session state.</span></span> <span data-ttu-id="f3d75-128">È anche possibile archiviare lo stato della sessione in altre posizioni per garantire che l'applicazione sia scalabile nel cloud.</span><span class="sxs-lookup"><span data-stu-id="f3d75-128">You can also store session state in other places to ensure your application is scalable on the cloud.</span></span> <span data-ttu-id="f3d75-129">Per ulteriori informazioni sulle soluzioni alternative, leggere [Modalità dello stato di sessione](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="f3d75-129">To learn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="f3d75-130">L’esecuzione del metodo non deve essere asincrona</span><span class="sxs-lookup"><span data-stu-id="f3d75-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-131">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-131">ID</span></span>
<span data-ttu-id="f3d75-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="f3d75-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-133">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-133">Description</span></span>
<span data-ttu-id="f3d75-134">Creare metodi asincroni, ad esempio [await](https://msdn.microsoft.com/library/hh156528.aspx), fuori dal metodo [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) e quindi chiamare i metodi asincroni da [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call the async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="f3d75-135">La dichiarazione del metodo [[Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) come asincrona fa sì che il ruolo di lavoro immetta un ciclo di riavvio.</span><span class="sxs-lookup"><span data-stu-id="f3d75-135">Declaring the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes the worker role to enter a restart loop.</span></span>

<span data-ttu-id="f3d75-136">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-137">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-137">Reason</span></span>
<span data-ttu-id="f3d75-138">La chiamata di metodi asincroni all'interno del metodo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) fa sì che il runtime del servizio cloud ricicli il ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f3d75-138">Calling async methods inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the cloud service runtime to recycle the worker role.</span></span> <span data-ttu-id="f3d75-139">Quando viene avviato un ruolo di lavoro, l'esecuzione del programma ha luogo all'interno del metodo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-139">When a worker role starts, all program execution takes place inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="f3d75-140">Chiudere il metodo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) fa sì che il ruolo di lavoro venga riavviato.</span><span class="sxs-lookup"><span data-stu-id="f3d75-140">Exiting the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the worker role to restart.</span></span> <span data-ttu-id="f3d75-141">Quando il runtime di ruolo di lavoro raggiunge il metodo asincrono, invia tutte le operazioni dopo il metodo asincrono e poi ritorna </span><span class="sxs-lookup"><span data-stu-id="f3d75-141">When the worker role runtime hits the async method, it dispatches all operations after the async method and then returns.</span></span> <span data-ttu-id="f3d75-142">In questo modo, il ruolo di lavoro esce dal metodo [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) e si riavvia.</span><span class="sxs-lookup"><span data-stu-id="f3d75-142">This causes the worker role to exit from the [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="f3d75-143">Nell'iterazione successiva dell'esecuzione, il ruolo di lavoro raggiunge nuovamente il metodo asincrono e viene riavviato, causando nuovamente il riciclo anche del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f3d75-143">In the next iteration of execution, the worker role hits the async method again and restarts, causing the worker role to recycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-144">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-144">Solution</span></span>
<span data-ttu-id="f3d75-145">Posizionare tutte le operazioni asincrone fuori dal metodo [Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f3d75-145">Place all async operations outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="f3d75-146">Quindi, chiamare il metodo asincrono refactoring dall'interno del metodo [[Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) , ad esempio RunAsync().wait.</span><span class="sxs-lookup"><span data-stu-id="f3d75-146">Then, call the refactored async method from inside the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="f3d75-147">Lo strumento di analisi del codice di Azure può aiutare a risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="f3d75-147">The Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="f3d75-148">Il seguente frammento di codice dimostra la correzione del codice per questo problema:</span><span class="sxs-lookup"><span data-stu-id="f3d75-148">The following code snippet demonstrates the code fix for this issue:</span></span>

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

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="f3d75-149">Autenticazione della firma di accesso condiviso con il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="f3d75-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-150">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-150">ID</span></span>
<span data-ttu-id="f3d75-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="f3d75-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-152">Description</span></span>
<span data-ttu-id="f3d75-153">Uso della firma di accesso condiviso per l’autenticazione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="f3d75-154">Il servizio di controllo di accesso (ACS) è deprecato per l'autenticazione di bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="f3d75-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="f3d75-155">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-156">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-156">Reason</span></span>
<span data-ttu-id="f3d75-157">Per una sicurezza ottimale, Azure Active Directory consiste nella sostituzione dell’autenticazione ACS con l'autenticazione SAS.</span><span class="sxs-lookup"><span data-stu-id="f3d75-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="f3d75-158">Vedere [Azure Active Directory è il futuro di ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) per informazioni sul piano di transizione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-158">See [Azure Active Directory is the future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on the transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-159">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-159">Solution</span></span>
<span data-ttu-id="f3d75-160">Utilizzare l'autenticazione SAS nelle app.</span><span class="sxs-lookup"><span data-stu-id="f3d75-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="f3d75-161">Nell'esempio seguente viene illustrato come utilizzare un token SAS esistente per accedere a uno spazio dei nomi o a un’entità del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="f3d75-161">The following example shows how to use an existing SAS token to access a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="f3d75-162">Per altre informazioni, vedere gli argomenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="f3d75-162">See the following topics for more information.</span></span>

* <span data-ttu-id="f3d75-163">Per una panoramica, vedere [autenticazione della firma di accesso condiviso con il bus di servizio](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="f3d75-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="f3d75-164">Come usare l'autenticazione della firma di accesso condiviso con il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="f3d75-164">How to use Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="f3d75-165">Per un progetto di esempio, vedere l'articolo relativo all' [autenticazione tramite firma di accesso condiviso con le sottoscrizioni del bus di servizio](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="f3d75-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-to-avoid-receive-loop"></a><span data-ttu-id="f3d75-166">È consigliabile utilizzare il metodo OnMessage per evitare il "ciclo di ricezione"</span><span class="sxs-lookup"><span data-stu-id="f3d75-166">Consider using OnMessage method to avoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-167">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-167">ID</span></span>
<span data-ttu-id="f3d75-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="f3d75-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-169">Description</span></span>
<span data-ttu-id="f3d75-170">Per evitare di entrare in un "ciclo di ricezione" la chiamata al metodo **OnMessage** è una soluzione ottimale, poi chiamare il metodo **Receive**.</span><span class="sxs-lookup"><span data-stu-id="f3d75-170">To avoid going into a "receive loop," calling the **OnMessage** method is a better solution for receiving messages than calling the **Receive** method.</span></span> <span data-ttu-id="f3d75-171">Tuttavia, se è necessario utilizzare il metodo **Ricezione** e si specifica un tempo di attesa del server non predefinito, assicurarsi che il tempo di attesa del server sia più di un minuto.</span><span class="sxs-lookup"><span data-stu-id="f3d75-171">However, if you must use the **Receive** method, and you specify a non-default server wait time, make sure the server wait time is more than one minute.</span></span>

<span data-ttu-id="f3d75-172">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-173">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-173">Reason</span></span>
<span data-ttu-id="f3d75-174">Quando si chiama **OnMessage**, il client avvia un message pump interno che esegue costantemente il polling della coda o della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-174">When calling **OnMessage**, the client starts an internal message pump that constantly polls the queue or subscription.</span></span> <span data-ttu-id="f3d75-175">Questo pump del messaggio contiene un ciclo infinito che emette una chiamata per ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="f3d75-175">This message pump contains an infinite loop that issues a call to receive messages.</span></span> <span data-ttu-id="f3d75-176">Se la chiamata scade, genera una nuova chiamata.</span><span class="sxs-lookup"><span data-stu-id="f3d75-176">If the call times out, it issues a new call.</span></span> <span data-ttu-id="f3d75-177">L'intervallo di timeout è determinato dal valore della proprietà [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) del [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx) che viene usato.</span><span class="sxs-lookup"><span data-stu-id="f3d75-177">The timeout interval is determined by the value of the [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of the [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="f3d75-178">Il vantaggio dell'uso di **OnMessage** rispetto a **Receive** è che gli utenti non devono eseguire manualmente il polling dei messaggi, gestire le eccezioni, elaborare più messaggi in parallelo e completare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="f3d75-178">The advantage of using **OnMessage** compared to **Receive** is that users don’t have to manually poll for messages, handle exceptions, process multiple messages in parallel, and complete the messages.</span></span>

<span data-ttu-id="f3d75-179">Se si chiama la **Ricezione** senza utilizzare il valore predefinito, assicurarsi che il valore *ServerWaitTime* sia superiore a un minuto.</span><span class="sxs-lookup"><span data-stu-id="f3d75-179">If you call **Receive** without using its default value, be sure the *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="f3d75-180">L'impostazione di *ServerWaitTime* a più di un minuto impedisce al server di scadere prima che il messaggio venga ricevuto completamente.</span><span class="sxs-lookup"><span data-stu-id="f3d75-180">Setting *ServerWaitTime* to more than one minute prevents the server from timing out before the message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-181">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-181">Solution</span></span>
<span data-ttu-id="f3d75-182">Vedere gli esempi di codice seguenti per gli utilizzi consigliati.</span><span class="sxs-lookup"><span data-stu-id="f3d75-182">Please see the following code examples for recommended usages.</span></span> <span data-ttu-id="f3d75-183">Per altre informazioni, vedere [metodo QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) e [metodo QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="f3d75-184">Per migliorare le prestazioni dell'infrastruttura di messaggistica di Azure, vedere il modello di progettazione [Nozioni di base di messaggistica asincrona](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-184">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="f3d75-185">Il seguente è un esempio dell'utilizzo di **OnMessage** per ricevere i messaggi.</span><span class="sxs-lookup"><span data-stu-id="f3d75-185">The following is an example of using **OnMessage** to receive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if the message-pump should call complete on messages after the callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates the maximum number of concurrent calls to the callback the pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you to get notified of any errors encountered by the message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates the message pump and callback is invoked for each message that is recieved, calling close on the client will stop the pump.
    {
        // Process the message.
    }, options);
    Console.WriteLine("Press any key to exit.");
    Console.ReadKey();
```

<span data-ttu-id="f3d75-186">Il seguente è un esempio dell'utilizzo di **Ricezione** con il tempo di attesa predefinito del server.</span><span class="sxs-lookup"><span data-stu-id="f3d75-186">The following is an example of using **Receive** with the default server wait time.</span></span>

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

<span data-ttu-id="f3d75-187">Il seguente è un esempio dell'utilizzo di **Ricezione** con il tempo di attesa non predefinito del server.</span><span class="sxs-lookup"><span data-stu-id="f3d75-187">The following is an example of using **Receive** with a non-default server wait time.</span></span>

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
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="f3d75-188">Si consideri l'utilizzo di metodi asincroni del Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="f3d75-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-189">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-189">ID</span></span>
<span data-ttu-id="f3d75-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="f3d75-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-191">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-191">Description</span></span>
<span data-ttu-id="f3d75-192">Utilizzare i metodi asincroni del Bus di servizio per migliorare le prestazioni con la messaggistica negoziata.</span><span class="sxs-lookup"><span data-stu-id="f3d75-192">Use asynchronous Service Bus methods to improve performance with brokered messaging.</span></span>

<span data-ttu-id="f3d75-193">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-194">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-194">Reason</span></span>
<span data-ttu-id="f3d75-195">L’utilizzo di metodi asincroni consente la concorrenza del programma di applicazione perché l'esecuzione di ogni chiamata non blocca il thread principale.</span><span class="sxs-lookup"><span data-stu-id="f3d75-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block the main thread.</span></span> <span data-ttu-id="f3d75-196">Quando si utilizzano i metodi di messaggistica del Bus di servizio, l’esecuzione di un'operazione (inviare, ricevere, eliminare, ecc) richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="f3d75-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="f3d75-197">Questa volta include l'elaborazione dell'operazione dal servizio Bus di servizio oltre alla latenza della richiesta e risposta.</span><span class="sxs-lookup"><span data-stu-id="f3d75-197">This time includes the processing of the operation by the Service Bus service in addition to the latency of the request and the reply.</span></span> <span data-ttu-id="f3d75-198">Per aumentare il numero di operazioni per volta, è necessario eseguire le operazioni contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="f3d75-198">To increase the number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="f3d75-199">Per altre informazioni, consultare le [Procedure consigliate per il miglioramento delle prestazioni tramite la messaggistica negoziata del bus di servizio](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-199">For more information please refer to [Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-200">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-200">Solution</span></span>
<span data-ttu-id="f3d75-201">Vedere [QueueClient class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) per ricevere informazioni su come utilizzare il metodo asincrono consigliato.</span><span class="sxs-lookup"><span data-stu-id="f3d75-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how to use the recommended asynchronous method.</span></span>

<span data-ttu-id="f3d75-202">Per migliorare le prestazioni dell'infrastruttura di messaggistica di Azure, vedere il modello di progettazione [Nozioni di base di messaggistica asincrona](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-202">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="f3d75-203">Prendere in considerazione il partizionamento delle code e degli argomenti del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="f3d75-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-204">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-204">ID</span></span>
<span data-ttu-id="f3d75-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="f3d75-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-206">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-206">Description</span></span>
<span data-ttu-id="f3d75-207">Esegue il partizionamento delle code e degli argomenti del bus di servizio per ottenere prestazioni migliori con la messaggistica del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="f3d75-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="f3d75-208">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-209">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-209">Reason</span></span>
<span data-ttu-id="f3d75-210">Il partizionamento delle code e degli argomenti del bus di servizio permette di aumentare la disponibilità dei servizi e la velocità effettiva delle prestazioni, perché la velocità effettiva complessiva di una coda o di un argomento partizionato non è più limitata dalle prestazioni di un singolo broker messaggi o archivio di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="f3d75-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because the overall throughput of a partitioned queue or topic is no longer limited by the performance of a single message broker or messaging store.</span></span> <span data-ttu-id="f3d75-211">Una interruzione temporanea di un archivio di messaggistica non influisce sulla disponibilità di code e argomenti partizionati.</span><span class="sxs-lookup"><span data-stu-id="f3d75-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="f3d75-212">Per ulteriori informazioni, vedere [Partizionamento delle entità di messaggistica](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-213">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-213">Solution</span></span>
<span data-ttu-id="f3d75-214">Il seguente frammento di codice mostra come suddividere le entità di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="f3d75-214">The following code snippet shows how to partition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="f3d75-215">Per altre informazioni, vedere il blog di Microsoft Azure [Partitioned Service Bus Queues and Topics](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) (Code e argomenti partizionati del bus di servizio) e l'esempio [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) (Coda partizionata del bus di servizio di Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="f3d75-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out the [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="f3d75-216">Non impostare SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="f3d75-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-217">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-217">ID</span></span>
<span data-ttu-id="f3d75-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="f3d75-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-219">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-219">Description</span></span>
<span data-ttu-id="f3d75-220">È consigliabile evitare l'utilizzo di SharedAccessStartTimeset all'ora corrente per avviare immediatamente il criterio di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="f3d75-220">You should avoid using SharedAccessStartTimeset to the current time to immediately start the Shared Access policy.</span></span> <span data-ttu-id="f3d75-221">È sufficiente impostare questa proprietà se si desidera avviare i criteri di accesso condivisi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="f3d75-221">You only need to set this property if you want to start the Shared Access policy at a later time.</span></span>

<span data-ttu-id="f3d75-222">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-223">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-223">Reason</span></span>
<span data-ttu-id="f3d75-224">La sincronizzazione dell'orologio comporta una differenza oraria lieve tra i Data Center.</span><span class="sxs-lookup"><span data-stu-id="f3d75-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="f3d75-225">Ad esempio, si pensa logicamente che impostando l'ora di inizio di un archivio criteri SAS come l'ora corrente utilizzando Now o un metodo simile si farà sì che i criteri SAS abbiano effetto immediato.</span><span class="sxs-lookup"><span data-stu-id="f3d75-225">For example, you would logically think setting the start time of a storage SAS policy as the current time by using DateTime.Now or a similar method will cause the SAS policy to take effect immediately.</span></span> <span data-ttu-id="f3d75-226">Tuttavia, le differenze lievi di tempo tra i Data Center possono provocare problemi con questo poiché alcuni tempi del datacenter potrebbero essere leggermente oltre l'ora di inizio, mentre altri la precedono.</span><span class="sxs-lookup"><span data-stu-id="f3d75-226">However, the slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than the start time, while others ahead of it.</span></span> <span data-ttu-id="f3d75-227">Di conseguenza, i criteri di firma di accesso condiviso possono scadere rapidamente (o persino immediatamente) se la durata di criteri è troppo breve.</span><span class="sxs-lookup"><span data-stu-id="f3d75-227">As a result, the SAS policy can expire quickly (or even immediately) if the policy lifetime is set too short.</span></span>

<span data-ttu-id="f3d75-228">Per ulteriori informazioni sull'utilizzo di firma di accesso condiviso sull'archiviazione di Azure, vedere [Introduzione della tabella SAS (Shared Access Signature) della coda SAS coda del BLOB SAS - Blog del Team Microsoft Azure Storage - Home page - sito blog di MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-229">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-229">Solution</span></span>
<span data-ttu-id="f3d75-230">Rimuovere l'istruzione che imposta l'ora di inizio del criterio di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="f3d75-230">Remove the statement that sets the start time of the shared access policy.</span></span> <span data-ttu-id="f3d75-231">Lo strumento di analisi del codice di Azure fornisce una correzione per questo problema.</span><span class="sxs-lookup"><span data-stu-id="f3d75-231">The Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="f3d75-232">Per ulteriori informazioni sulla gestione della protezione, vedere il modello di progettazione [Modello passepartout](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-232">For more information on security management, please see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="f3d75-233">Il seguente frammento di codice dimostra la correzione del codice per questo problema.</span><span class="sxs-lookup"><span data-stu-id="f3d75-233">The following code snippet demonstrates the code fix for this issue.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="f3d75-234">L’ora di scadenza del criterio di accesso condiviso deve essere più di cinque minuti </span><span class="sxs-lookup"><span data-stu-id="f3d75-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-235">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-235">ID</span></span>
<span data-ttu-id="f3d75-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="f3d75-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-237">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-237">Description</span></span>
<span data-ttu-id="f3d75-238">Può esistere una differenza di circa cinque minuti negli orologi tra i Data Center in posizioni diverse a causa di una condizione nota come "sfasamento."</span><span class="sxs-lookup"><span data-stu-id="f3d75-238">There can be as much as a five minute difference in clocks among datacenters at different locations due to a condition known as "clock skew."</span></span> <span data-ttu-id="f3d75-239">Per evitare che il token del criterio SAS scada prima del previsto, impostare l'ora di scadenza a più di cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="f3d75-239">To prevent the SAS policy token from expiring earlier than planned, set the expiry time to be more than five minutes.</span></span>

<span data-ttu-id="f3d75-240">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-241">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-241">Reason</span></span>
<span data-ttu-id="f3d75-242">I dataenter in diverse località del mondo sono sincronizzati da un segnale di orologio.</span><span class="sxs-lookup"><span data-stu-id="f3d75-242">Datacenters at different locations around the world synchronize by a clock signal.</span></span> <span data-ttu-id="f3d75-243">Poiché occorre tempo affinché il segnale dell’orologio viaggi in località diverse, può esistere una varianza di tempo tra i datacenter in località geografiche diverse anche se apparentemente tutto ciò viene sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="f3d75-243">Because it takes time for clock signal to travel to different locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="f3d75-244">Questa differenza di tempo può influenzare l’inizio del tempo dell'accesso condiviso e dell’intervallo di scadenza dei criteri.</span><span class="sxs-lookup"><span data-stu-id="f3d75-244">This time difference can affect the Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="f3d75-245">Per verificare che il criterio di accesso condiviso diventi effettivo immediatamente, pertanto, non specificare l'ora di inizio.</span><span class="sxs-lookup"><span data-stu-id="f3d75-245">Therefore, to ensure Shared Access policy takes effect immediately, don’t specify the start time.</span></span> <span data-ttu-id="f3d75-246">Inoltre, assicurarsi che l'ora di scadenza sia maggiore di 5 minuti per evitare una scadenza anticipata.</span><span class="sxs-lookup"><span data-stu-id="f3d75-246">In addition, make sure the expiration time is more than 5 minutes to prevent early timeout.</span></span>

<span data-ttu-id="f3d75-247">Per ulteriori informazioni sull'utilizzo di firma di accesso condiviso sull'archiviazione di Azure, vedere [Introduzione della tabella SAS (Shared Access Signature) della coda SAS coda del BLOB SAS - Blog del Team Microsoft Azure Storage - Home page - sito blog di MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-248">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-248">Solution</span></span>
<span data-ttu-id="f3d75-249">Per ulteriori informazioni sulla gestione della protezione, vedere il modello di progettazione [Modello passepartout](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-249">For more information on security management, see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="f3d75-250">Di seguito è riportato un esempio di ora di inizio dei criteri di accesso condiviso non specificata.</span><span class="sxs-lookup"><span data-stu-id="f3d75-250">The following is an example of not specifying a Shared Access policy start time.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="f3d75-251">Di seguito è riportato un esempio di un'ora di inizio dei criteri di accesso condiviso specificata, con un periodo di scadenza dei criteri maggiore di cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="f3d75-251">The following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="f3d75-252">Per ulteriori informazioni, [Creare e usare una firma di accesso condiviso](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="f3d75-253">Utilizzare CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="f3d75-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-254">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-254">ID</span></span>
<span data-ttu-id="f3d75-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="f3d75-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-256">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-256">Description</span></span>
<span data-ttu-id="f3d75-257">Usando la classe [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) per progetti, come il sito Web di Azure e i servizi mobili di Azure, non si verificano problemi di runtime.</span><span class="sxs-lookup"><span data-stu-id="f3d75-257">Using the [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="f3d75-258">Come procedura consigliata, tuttavia, è consigliabile usare Cloud [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) come modo unificato di gestione delle configurazioni per tutte le applicazioni Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d75-258">As a best practice, however, it's a good idea to use Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="f3d75-259">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-260">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-260">Reason</span></span>
<span data-ttu-id="f3d75-261">CloudConfigurationManager legge il file di configurazione appropriato per l'ambiente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-261">CloudConfigurationManager reads the configuration file appropriate to the application environment.</span></span>

[<span data-ttu-id="f3d75-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="f3d75-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="f3d75-263">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-263">Solution</span></span>
<span data-ttu-id="f3d75-264">Effettuare il refactoring del codice per utilizzare il [CloudConfigurationManager classe](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-264">Refactor your code to use the [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="f3d75-265">Una correzione del codice per questo problema viene fornita dallo strumento di analisi del codice di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d75-265">A code fix for this issue is provided by the Azure Code Analysis tool.</span></span>

<span data-ttu-id="f3d75-266">Il seguente frammento di codice dimostra la correzione del codice per questo problema.</span><span class="sxs-lookup"><span data-stu-id="f3d75-266">The following code snippet demonstrates the code fix for this issue.</span></span> <span data-ttu-id="f3d75-267">Replace</span><span class="sxs-lookup"><span data-stu-id="f3d75-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="f3d75-268">con</span><span class="sxs-lookup"><span data-stu-id="f3d75-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="f3d75-269">Di seguito è riportato un esempio di come archiviare l'impostazione di configurazione in un file app. config o Web. config.</span><span class="sxs-lookup"><span data-stu-id="f3d75-269">Here's an example of how to store the configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="f3d75-270">Aggiungere le impostazioni per la sezione appSettings del file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-270">Add the settings to the appSettings section of the configuration file.</span></span> <span data-ttu-id="f3d75-271">Di seguito è il file Web. config per l'esempio di codice precedente.</span><span class="sxs-lookup"><span data-stu-id="f3d75-271">The following is the Web.config file for the previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="f3d75-272">Evitare di utilizzare stringhe di connessione hardcoded</span><span class="sxs-lookup"><span data-stu-id="f3d75-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-273">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-273">ID</span></span>
<span data-ttu-id="f3d75-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="f3d75-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-275">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-275">Description</span></span>
<span data-ttu-id="f3d75-276">Se si utilizzano stringhe di connessione hardcoded ed è necessario aggiornarle in un secondo momento, sarà necessario apportare modifiche al codice sorgente e ricompilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-276">If you use hard-coded connection strings and you need to update them later, you’ll have to make changes to your source code and recompile the application.</span></span> <span data-ttu-id="f3d75-277">Tuttavia, se si archiviano le stringhe di connessione in un file di configurazione, è possibile cambiarle successivamente semplicemente aggiornando il file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating the configuration file.</span></span>

<span data-ttu-id="f3d75-278">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-279">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-279">Reason</span></span>
<span data-ttu-id="f3d75-280">Impostare come hardcoded le stringhe di connessione è sconsigliato perché presenta problemi quando è necessario modificare rapidamente le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need to be changed quickly.</span></span> <span data-ttu-id="f3d75-281">Inoltre, se il progetto deve essere controllato nel codice sorgente, le stringhe di connessione hardcoded presentano una vulnerabilità di protezione poiché le stringhe possono essere visualizzate nel codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="f3d75-281">In addition, if the project needs to be checked in to source control, hard-coded connection strings introduce security vulnerabilities since the strings can be viewed in the source code.</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-282">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-282">Solution</span></span>
<span data-ttu-id="f3d75-283">Archiviare le stringhe di connessione nel file di configurazione o negli ambienti di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3d75-283">Store connection strings in the configuration files or Azure environments.</span></span>

* <span data-ttu-id="f3d75-284">Per le applicazioni autonome utilizzare la config. dell’app per archiviare le impostazioni della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-284">For standalone applications, use app.config to store connection string settings.</span></span>
* <span data-ttu-id="f3d75-285">Per le applicazioni web ospitate in IIS, utilizzare config. web per archiviare le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-285">For IIS-hosted web applications, use web.config to store connection strings.</span></span>
* <span data-ttu-id="f3d75-286">Per le applicazioni ASP.NET vNext utilizzare configuration.json per archiviare le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-286">For ASP.NET vNext applications, use configuration.json to store connection strings.</span></span>

<span data-ttu-id="f3d75-287">Per informazioni sull'uso di file di configurazione, ad esempio web.config o app. config, vedere [Linee guida configurazione di ASP.NET Web](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d75-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="f3d75-288">Per informazioni su come funzionano le variabili di ambiente di Azure, vedere [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) (Siti Web di Microsoft Azure sul funzionamento delle stringhe di applicazione e di connessione).</span><span class="sxs-lookup"><span data-stu-id="f3d75-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="f3d75-289">Per informazioni sull'archiviazione della stringa di connessione nel codice sorgente, vedere [evitare di inserire informazioni riservate come le stringhe di connessione nei file archiviati nel repository del codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="f3d75-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="f3d75-290">Utilizzo del file di configurazione di Diagnostica.</span><span class="sxs-lookup"><span data-stu-id="f3d75-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-291">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-291">ID</span></span>
<span data-ttu-id="f3d75-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="f3d75-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-293">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-293">Description</span></span>
<span data-ttu-id="f3d75-294">Anziché configurare le impostazioni di diagnostica nel codice, ad esempio tramite l'API di programmazione della diagnostica di Microsoft.WindowsAzure, è necessario configurare le impostazioni di diagnostica nel file diagnostics wadcfg.</span><span class="sxs-lookup"><span data-stu-id="f3d75-294">Instead of configuring diagnostics settings in your code such as by using the Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in the diagnostics.wadcfg file.</span></span> <span data-ttu-id="f3d75-295">(O, diagnostics.wadcfgx se si utilizza Azure SDK 2.5).</span><span class="sxs-lookup"><span data-stu-id="f3d75-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="f3d75-296">In questo modo è possibile modificare le impostazioni di diagnostica senza dover ricompilare il codice.</span><span class="sxs-lookup"><span data-stu-id="f3d75-296">By doing this, you can change diagnostics settings without having to recompile your code.</span></span>

<span data-ttu-id="f3d75-297">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-298">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-298">Reason</span></span>
<span data-ttu-id="f3d75-299">Prima di Azure SDK 2.5 (che utilizza diagnostica Microsoft Azure 1.3), la diagnostica di Azure (WAD) può essere configurata utilizzando diversi metodi: aggiunta del BLOB di configurazione nel servizio di archiviazione, utilizzando il codice imperativo, la configurazione dichiarativa o la configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f3d75-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it to the configuration blob in storage, by using imperative code, declarative configuration, or the default configuration.</span></span> <span data-ttu-id="f3d75-300">Tuttavia, il modo migliore per configurare la diagnostica consiste nell'utilizzare un file di configurazione XML (wadcfg o diagnositcs.wadcfgx per SDK 2.5 e versioni successive) nel progetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-300">However, the preferred way to configure diagnostics is to use an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in the application project.</span></span> <span data-ttu-id="f3d75-301">In questo approccio, il file diagnostics wadcfg definisce completamente la configurazione e può essere aggiornato e ridistribuito a suo piacimento.</span><span class="sxs-lookup"><span data-stu-id="f3d75-301">In this approach, the diagnostics.wadcfg file completely defines the configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="f3d75-302">Combinare l'uso del file di configurazione wadcfg con i metodi a livello di codice di impostazione delle configurazioni tramite le classi [Diagnosticmonitorconfiguration](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx) o [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) può generare confusione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-302">Mixing the use of the diagnostics.wadcfg configuration file with the programmatic methods of setting configurations by using the [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead to confusion.</span></span> <span data-ttu-id="f3d75-303">Vedere [Avviare o modificare la configurazione della diagnostica di Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="f3d75-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="f3d75-304">A partire da 1.3 WAD (incluso in Azure SDK 2.5), non è più possibile utilizzare il codice per configurare la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="f3d75-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible to use code to configure diagnostics.</span></span> <span data-ttu-id="f3d75-305">Di conseguenza, è possibile specificare solo la configurazione quando si applica o si aggiorna l'estensione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="f3d75-305">As a result, you can only provide the configuration when applying or updating the diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-306">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-306">Solution</span></span>
<span data-ttu-id="f3d75-307">Utilizzare la finestra di progettazione di configurazione di diagnostica per spostare le impostazioni di diagnostica per il file di configurazione di diagnostica (diagnositcs.wadcfg o diagnositcs.wadcfgx per SDK 2.5 e versioni successive).</span><span class="sxs-lookup"><span data-stu-id="f3d75-307">Use the diagnostics configuration designer to move diagnostic settings to the diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="f3d75-308">È inoltre consigliabile installare [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) e utilizzare la funzionalità di diagnostica più recente.</span><span class="sxs-lookup"><span data-stu-id="f3d75-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use the latest diagnostics feature.</span></span>

1. <span data-ttu-id="f3d75-309">Dal menu di scelta rapida per il ruolo desiderato scegliere Proprietà, quindi selezionare la scheda Configurazione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-309">On the shortcut menu for the role that you want to configure, choose Properties, and then choose the Configuration tab.</span></span>
2. <span data-ttu-id="f3d75-310">Nella sezione **Diagnostica** verificare che la casella di controllo **Abilita diagnostica** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="f3d75-310">In the **Diagnostics** section, make sure that the **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="f3d75-311">Scegliere il pulsante **Configura** .</span><span class="sxs-lookup"><span data-stu-id="f3d75-311">Choose the **Configure** button.</span></span>

   ![Accesso all'opzione Abilita diagnostica](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="f3d75-313">Vedere [Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) .per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="f3d75-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="f3d75-314">Evitare di dichiarare gli oggetti DbContext come static</span><span class="sxs-lookup"><span data-stu-id="f3d75-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="f3d75-315">ID</span><span class="sxs-lookup"><span data-stu-id="f3d75-315">ID</span></span>
<span data-ttu-id="f3d75-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="f3d75-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="f3d75-317">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3d75-317">Description</span></span>
<span data-ttu-id="f3d75-318">Per conservare memoria, evitare di dichiarare gli oggetti DbContext come static</span><span class="sxs-lookup"><span data-stu-id="f3d75-318">To save memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="f3d75-319">Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="f3d75-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="f3d75-320">Motivo</span><span class="sxs-lookup"><span data-stu-id="f3d75-320">Reason</span></span>
<span data-ttu-id="f3d75-321">Gli oggetti DBContext contengono i risultati della query da ogni chiamata.</span><span class="sxs-lookup"><span data-stu-id="f3d75-321">DBContext objects hold the query results from each call.</span></span> <span data-ttu-id="f3d75-322">Gli oggetti DBContext statici non vengono eliminati fino a quando non viene scaricato il dominio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3d75-322">Static DBContext objects are not disposed until the application domain is unloaded.</span></span> <span data-ttu-id="f3d75-323">Pertanto, un oggetto DBContext statico può utilizzare grandi quantità di memoria.</span><span class="sxs-lookup"><span data-stu-id="f3d75-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="f3d75-324">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f3d75-324">Solution</span></span>
<span data-ttu-id="f3d75-325">Dichiarare DBContext come una variabile locale o un campo di istanza non statico, utilizzarlo per un'attività e poi eliminarlo dopo l'uso.</span><span class="sxs-lookup"><span data-stu-id="f3d75-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="f3d75-326">Il seguente esempio di classe controller MVC illustra come utilizzare l'oggetto DBContext.</span><span class="sxs-lookup"><span data-stu-id="f3d75-326">The following example MVC controller class shows how to use the DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass to DbContext        
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

## <a name="next-steps"></a><span data-ttu-id="f3d75-327">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f3d75-327">Next steps</span></span>
<span data-ttu-id="f3d75-328">Per altre informazioni sull'ottimizzazione e la risoluzione dei problemi delle app Azure, vedere [Risoluzione dei problemi di un'app Web nel servizio app di Azure tramite Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f3d75-328">To learn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
