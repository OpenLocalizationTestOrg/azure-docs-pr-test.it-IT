---
title: aaaDebug microservizi Azure in Linux | Documenti Microsoft
description: Informazioni su come toomonitor e diagnosticare i servizi scritti con Microsoft Azure Service Fabric in un computer di sviluppo locale.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="ef235-103">Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale</span><span class="sxs-lookup"><span data-stu-id="ef235-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef235-104">Windows</span><span class="sxs-lookup"><span data-stu-id="ef235-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="ef235-105">Linux</span><span class="sxs-lookup"><span data-stu-id="ef235-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="ef235-106">Il monitoraggio, il rilevamento, la diagnosi e risoluzione dei problemi consentono di servizi toocontinue l'esperienza utente toohello un'interruzione minima.</span><span class="sxs-lookup"><span data-stu-id="ef235-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="ef235-107">Il monitoraggio e la diagnostica sono essenziali in un ambiente di produzione distribuito reale.</span><span class="sxs-lookup"><span data-stu-id="ef235-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="ef235-108">Adozione di un modello simile durante lo sviluppo di servizi garantisce che pipeline diagnostica hello funziona quando si sposta tooa ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ef235-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="ef235-109">Service Fabric rende più semplice per la diagnostica tooimplement agli sviluppatori di servizio che può funzionare senza problemi tra le impostazioni di sviluppo locale solo computer e le installazioni cluster di produzione reali.</span><span class="sxs-lookup"><span data-stu-id="ef235-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="ef235-110">Debug delle applicazioni Java di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ef235-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="ef235-111">Per le applicazioni Java sono disponibili [più framework di registrazione](http://en.wikipedia.org/wiki/Java_logging_framework) .</span><span class="sxs-lookup"><span data-stu-id="ef235-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="ef235-112">Poiché `java.util.logging` è l'opzione predefinita hello con JRE hello, viene inoltre utilizzato per hello [in github esempi di codice](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ef235-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="ef235-113">Hello discussione che segue viene illustrato come hello tooconfigure `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="ef235-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="ef235-114">Uso di util è possibile reindirizzare l'applicazione, i registri toomemory, flussi di output, i file di console o socket.</span><span class="sxs-lookup"><span data-stu-id="ef235-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="ef235-115">Per ognuna di queste opzioni, esistono gestori predefiniti già forniti in framework hello.</span><span class="sxs-lookup"><span data-stu-id="ef235-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="ef235-116">È possibile creare un `app.properties` gestore di file hello tooconfigure file per l'applicazione di tooredirect tutti i log file locale tooa.</span><span class="sxs-lookup"><span data-stu-id="ef235-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="ef235-117">Hello seguente frammento di codice contiene una configurazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="ef235-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="ef235-118">hello di Hello cartella punta tooby `app.properties` file deve esistere.</span><span class="sxs-lookup"><span data-stu-id="ef235-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="ef235-119">Dopo aver hello `app.properties` file viene creato, è necessario tooalso modificare lo script di punto di ingresso, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` proprietà della cartella tooset hello `java.util.logging.config.file` troppo`app.propertes` file.</span><span class="sxs-lookup"><span data-stu-id="ef235-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="ef235-120">voce Hello dovrebbe essere simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ef235-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="ef235-121">Con questa configurazione, i log verranno raccolti a rotazione in `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="ef235-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="ef235-122">file di log Hello in questo caso è denominato mysfapp%u.%g.log dove:</span><span class="sxs-lookup"><span data-stu-id="ef235-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="ef235-123">**%u** è un tooresolve numero univoco conflitti tra i processi simultanei di Java.</span><span class="sxs-lookup"><span data-stu-id="ef235-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="ef235-124">**%g** è toodistinguish numero di generazione hello tra la rotazione di log.</span><span class="sxs-lookup"><span data-stu-id="ef235-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="ef235-125">Per impostazione predefinita se nessun gestore è configurato in modo esplicito, il gestore di console hello è registrato.</span><span class="sxs-lookup"><span data-stu-id="ef235-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="ef235-126">Può visualizzare i log di hello Syslog in /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="ef235-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="ef235-127">Per ulteriori informazioni, vedere hello [in github esempi di codice](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ef235-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="ef235-128">Debug di applicazioni C# di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ef235-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="ef235-129">Sono disponibili vari framework per il tracciamento delle applicazioni CoreCLR in Linux.</span><span class="sxs-lookup"><span data-stu-id="ef235-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="ef235-130">Per altre informazioni, vedere [GitHub: logging](http:/github.com/aspnet/logging) (Accesso a GitHub).</span><span class="sxs-lookup"><span data-stu-id="ef235-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="ef235-131">Poiché EventSource è tooC # familiarità con gli sviluppatori,' in questo articolo Usa EventSource per la traccia in CoreCLR esempi in Linux.</span><span class="sxs-lookup"><span data-stu-id="ef235-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="ef235-132">primo passaggio Hello è tooinclude System.Diagnostics.Tracing in modo che sia possibile scrivere il log toomemory, flussi di output o i file di console.</span><span class="sxs-lookup"><span data-stu-id="ef235-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="ef235-133">Per la registrazione utilizzando EventSource aggiungere hello Project tooyour progetto seguente:</span><span class="sxs-lookup"><span data-stu-id="ef235-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="ef235-134">È possibile utilizzare un toolisten EventListener personalizzato per l'evento servizio hello e quindi in modo appropriato reindirizza tootrace file.</span><span class="sxs-lookup"><span data-stu-id="ef235-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="ef235-135">Hello frammento di codice seguente viene illustrato un esempio di implementazione della registrazione utilizzando EventSource e un oggetto EventListener personalizzato:</span><span class="sxs-lookup"><span data-stu-id="ef235-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need tooadd method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="ef235-136">frammento precedente Hello restituisce hello registri tooa file in `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="ef235-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="ef235-137">Il nome del file deve toobe aggiornato in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="ef235-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="ef235-138">Nel caso in cui si desidera tooredirect hello registri tooconsole, utilizzare hello seguente frammento di codice nella classe EventListener personalizzata:</span><span class="sxs-lookup"><span data-stu-id="ef235-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="ef235-139">Hello campioni [esempi c#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) utilizzare EventSource e un file tooa gli eventi di toolog EventListener personalizzato.</span><span class="sxs-lookup"><span data-stu-id="ef235-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ef235-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef235-140">Next steps</span></span>
<span data-ttu-id="ef235-141">Hello stessa analisi del codice aggiunto tooyour applicazione funziona anche con diagnostica di hello dell'applicazione in un cluster di Azure.</span><span class="sxs-lookup"><span data-stu-id="ef235-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="ef235-142">Estrazione di questi articoli che illustrano diverse opzioni di hello per strumenti di hello e descrivono come tooset tali backup.</span><span class="sxs-lookup"><span data-stu-id="ef235-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="ef235-143">Modalità di registrazione toocollect con diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="ef235-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
