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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

Il monitoraggio, il rilevamento, la diagnosi e risoluzione dei problemi consentono di servizi toocontinue l'esperienza utente toohello un'interruzione minima. Il monitoraggio e la diagnostica sono essenziali in un ambiente di produzione distribuito reale. Adozione di un modello simile durante lo sviluppo di servizi garantisce che pipeline diagnostica hello funziona quando si sposta tooa ambiente di produzione. Service Fabric rende più semplice per la diagnostica tooimplement agli sviluppatori di servizio che può funzionare senza problemi tra le impostazioni di sviluppo locale solo computer e le installazioni cluster di produzione reali.


## <a name="debugging-service-fabric-java-applications"></a>Debug delle applicazioni Java di Service Fabric

Per le applicazioni Java sono disponibili [più framework di registrazione](http://en.wikipedia.org/wiki/Java_logging_framework) . Poiché `java.util.logging` è l'opzione predefinita hello con JRE hello, viene inoltre utilizzato per hello [in github esempi di codice](http://github.com/Azure-Samples/service-fabric-java-getting-started).  Hello discussione che segue viene illustrato come hello tooconfigure `java.util.logging` framework.

Uso di util è possibile reindirizzare l'applicazione, i registri toomemory, flussi di output, i file di console o socket. Per ognuna di queste opzioni, esistono gestori predefiniti già forniti in framework hello. È possibile creare un `app.properties` gestore di file hello tooconfigure file per l'applicazione di tooredirect tutti i log file locale tooa.

Hello seguente frammento di codice contiene una configurazione di esempio:

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

hello di Hello cartella punta tooby `app.properties` file deve esistere. Dopo aver hello `app.properties` file viene creato, è necessario tooalso modificare lo script di punto di ingresso, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` proprietà della cartella tooset hello `java.util.logging.config.file` troppo`app.propertes` file. voce Hello dovrebbe essere simile hello frammento di codice seguente:

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


Con questa configurazione, i log verranno raccolti a rotazione in `/tmp/servicefabric/logs/`. file di log Hello in questo caso è denominato mysfapp%u.%g.log dove:
* **%u** è un tooresolve numero univoco conflitti tra i processi simultanei di Java.
* **%g** è toodistinguish numero di generazione hello tra la rotazione di log.

Per impostazione predefinita se nessun gestore è configurato in modo esplicito, il gestore di console hello è registrato. Può visualizzare i log di hello Syslog in /var/log/syslog.

Per ulteriori informazioni, vedere hello [in github esempi di codice](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Debug di applicazioni C# di Service Fabric


Sono disponibili vari framework per il tracciamento delle applicazioni CoreCLR in Linux. Per altre informazioni, vedere [GitHub: logging](http:/github.com/aspnet/logging) (Accesso a GitHub).  Poiché EventSource è tooC # familiarità con gli sviluppatori,' in questo articolo Usa EventSource per la traccia in CoreCLR esempi in Linux.

primo passaggio Hello è tooinclude System.Diagnostics.Tracing in modo che sia possibile scrivere il log toomemory, flussi di output o i file di console.  Per la registrazione utilizzando EventSource aggiungere hello Project tooyour progetto seguente:

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

È possibile utilizzare un toolisten EventListener personalizzato per l'evento servizio hello e quindi in modo appropriato reindirizza tootrace file. Hello frammento di codice seguente viene illustrato un esempio di implementazione della registrazione utilizzando EventSource e un oggetto EventListener personalizzato:


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


frammento precedente Hello restituisce hello registri tooa file in `/tmp/MyServiceLog.txt`. Il nome del file deve toobe aggiornato in modo appropriato. Nel caso in cui si desidera tooredirect hello registri tooconsole, utilizzare hello seguente frammento di codice nella classe EventListener personalizzata:

```csharp
public static TextWriter Out = Console.Out;
```

Hello campioni [esempi c#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) utilizzare EventSource e un file tooa gli eventi di toolog EventListener personalizzato.



## <a name="next-steps"></a>Passaggi successivi
Hello stessa analisi del codice aggiunto tooyour applicazione funziona anche con diagnostica di hello dell'applicazione in un cluster di Azure. Estrazione di questi articoli che illustrano diverse opzioni di hello per strumenti di hello e descrivono come tooset tali backup.
* [Modalità di registrazione toocollect con diagnostica di Azure](service-fabric-diagnostics-how-to-setup-lad.md)
