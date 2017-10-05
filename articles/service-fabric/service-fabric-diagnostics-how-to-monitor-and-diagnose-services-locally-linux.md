---
title: Eseguire il debug di microservizi di Azure in Linux | Documentazione Microsoft
description: Informazioni su come eseguire il monitoraggio e la diagnosi dei servizi scritti usando Microsoft Azure Service Fabric in un computer di sviluppo locale.
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
ms.openlocfilehash: 4bc73f581f4855ebc724df19dd56fab8bf103854
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="9ffa4-103">Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale</span><span class="sxs-lookup"><span data-stu-id="9ffa4-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ffa4-104">Windows</span><span class="sxs-lookup"><span data-stu-id="9ffa4-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="9ffa4-105">Linux</span><span class="sxs-lookup"><span data-stu-id="9ffa4-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="9ffa4-106">Le operazioni di monitoraggio, rilevamento, diagnosi e risoluzione dei problemi consentono ai servizi di continuare a funzionare con un'interruzione minima dell'esperienza utente.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="9ffa4-107">Il monitoraggio e la diagnostica sono essenziali in un ambiente di produzione distribuito reale.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="9ffa4-108">L'adozione di un modello simile durante lo sviluppo dei servizi garantisce il funzionamento della pipeline di diagnostica anche in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span></span> <span data-ttu-id="9ffa4-109">Service Fabric consente agli sviluppatori di servizi di implementare facilmente un sistema di diagnostica in grado di operare senza problemi sia in ambienti di sviluppo costituiti da un unico computer locale sia in configurazioni con cluster di produzione veri e propri.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="9ffa4-110">Debug delle applicazioni Java di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9ffa4-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="9ffa4-111">Per le applicazioni Java sono disponibili [più framework di registrazione](http://en.wikipedia.org/wiki/Java_logging_framework) .</span><span class="sxs-lookup"><span data-stu-id="9ffa4-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="9ffa4-112">Dato che `java.util.logging` è l'opzione predefinita con JRE, viene usato anche per gli [esempi di codice in GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9ffa4-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="9ffa4-113">Di seguito viene illustrato come configurare il framework `java.util.logging` .</span><span class="sxs-lookup"><span data-stu-id="9ffa4-113">The following discussion explains how to configure the `java.util.logging` framework.</span></span>

<span data-ttu-id="9ffa4-114">Usando java.util.logging è possibile reindirizzare i log dell'applicazione a memoria, flussi di output, file di console o socket.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span></span> <span data-ttu-id="9ffa4-115">Nel framework sono disponibili gestori predefiniti per ognuna di queste opzioni.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-115">For each of these options, there are default handlers already provided in the framework.</span></span> <span data-ttu-id="9ffa4-116">È possibile creare un file `app.properties` per configurare il gestore di file per l'applicazione in modo da reindirizzare tutti i log a un file locale.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span></span>

<span data-ttu-id="9ffa4-117">Il frammento di codice seguente contiene una configurazione di esempio:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-117">The following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="9ffa4-118">La cartella a cui fa riferimento il file `app.properties` deve essere presente.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-118">The folder pointed to by the `app.properties` file must exist.</span></span> <span data-ttu-id="9ffa4-119">Dopo la creazione del file `app.properties`, è anche necessario modificare lo script del punto di ingresso`entrypoint.sh`, nella cartella `<applicationfolder>/<servicePkg>/Code/` in modo da impostare la proprietà `java.util.logging.config.file` sul file `app.propertes`.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span></span> <span data-ttu-id="9ffa4-120">La voce dovrebbe essere simile al frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-120">The entry should look like the following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


<span data-ttu-id="9ffa4-121">Con questa configurazione, i log verranno raccolti a rotazione in `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="9ffa4-122">Il questo caso il file di log è denominato mysfapp%u.%g.log, dove:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-122">The log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="9ffa4-123">**%u** è un numero univoco per risolvere i conflitti tra processi simultanei di Java.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="9ffa4-124">**%g** è il numero di generazione per distinguere tra i log di rotazione.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-124">**%g** is the generation number to distinguish between rotating logs.</span></span>

<span data-ttu-id="9ffa4-125">Se non viene configurato in modo esplicito alcun gestore, per impostazione predefinita viene registrato il gestore della console.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-125">By default if no handler is explicitly configured, the console handler is registered.</span></span> <span data-ttu-id="9ffa4-126">È possibile visualizzare i log in syslog, in /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-126">One can view the logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="9ffa4-127">Per altre informazioni, vedere gli [GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9ffa4-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="9ffa4-128">Debug di applicazioni C# di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9ffa4-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="9ffa4-129">Sono disponibili vari framework per il tracciamento delle applicazioni CoreCLR in Linux.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="9ffa4-130">Per altre informazioni, vedere [GitHub: logging](http:/github.com/aspnet/logging) (Accesso a GitHub).</span><span class="sxs-lookup"><span data-stu-id="9ffa4-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="9ffa4-131">In questo articolo viene usato EventSource, già noto agli sviluppatori C#, per la traccia negli esempi CoreCLR in Linux.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="9ffa4-132">Il primo passaggio consiste nell'includere System.Diagnostics.Tracing in modo da poter scrivere i log in m in memoria, flussi di output o file di console.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span></span>  <span data-ttu-id="9ffa4-133">Per la registrazione tramite EventSource, aggiungere il seguente progetto a project.json:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-133">For logging using EventSource, add the following project to your project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="9ffa4-134">È possibile usare un EventListener personalizzato per l'ascolto dell'evento di servizio e quindi eseguire il reindirizzamento appropriato ai file di traccia.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span></span> <span data-ttu-id="9ffa4-135">Il frammento di codice seguente mostra un esempio di implementazione della registrazione tramite EventSource e un EventListener personalizzato:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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

        // TBD: Need to add method for sample event.

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


<span data-ttu-id="9ffa4-136">Il frammento di codice precedente restituisce i log a un file in `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="9ffa4-137">Il nome del file deve essere aggiornato in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-137">This file name needs to be appropriately updated.</span></span> <span data-ttu-id="9ffa4-138">Se si desidera reindirizzare i log alla console, usare il frammento di codice seguente nella classe EventListener personalizzata:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="9ffa4-139">Gli esempi in [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) (Esempio C#) usano EventSource e un EventListener personalizzato per registrare eventi in un file.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="9ffa4-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9ffa4-140">Next steps</span></span>
<span data-ttu-id="9ffa4-141">Lo stesso codice di traccia aggiunto all'applicazione potrà essere usato per la diagnostica dell'applicazione in un cluster di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="9ffa4-142">Consultare questi articoli che illustrano le diverse opzioni per gli strumenti e descrivono come configurarli.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span></span>
* [<span data-ttu-id="9ffa4-143">Come raccogliere log con Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="9ffa4-143">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
