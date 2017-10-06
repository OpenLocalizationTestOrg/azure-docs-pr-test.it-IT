---
title: aaaCreate del microservizio Azure affidabile prima in Java | Documenti Microsoft
description: Introduzione toocreating un'applicazione di Microsoft Azure Service Fabric con servizi senza stato.
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Introduzione a Reliable Services
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-services-quick-start.md)
> * [Java su Linux](service-fabric-reliable-services-quick-start-java.md)
>
>

In questo articolo vengono illustrati concetti fondamentali di hello di servizi di Azure Service Fabric affidabile e viene illustrato come creare e distribuire una semplice applicazione di servizio affidabile scritta in Java. In questo video Microsoft Virtual Academy illustra anche come un servizio Reliable senza stato toocreate:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Installazione e configurazione
Prima di iniziare, verificare di che aver ambiente di sviluppo di Service Fabric hello configurare nel computer.
Se è necessario tooset, configurarlo, andare troppo[introduzione su Mac](service-fabric-get-started-mac.md) o [introduzione in Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Concetti di base
tooget avviato con servizi affidabili, è solo necessario toounderstand alcuni concetti di base:

* **Tipo di servizio**: si tratta dell'implementazione del servizio. È definito dalla classe hello è scrivere che estende `StatelessService` e qualsiasi altro codice o dipendenze al suo interno, utilizzate insieme a un nome e un numero di versione.
* **Istanza di servizio denominata**: toorun il servizio, si creano le istanze denominate del tipo di servizio, molto come si creano istanze di un oggetto di un tipo classe. Le istanze del servizio sono, di fatto, istanze di oggetto della classe del servizio che si scrive.
* **Host del servizio**: hello denominata è necessario toorun all'interno di un host di creare istanze del servizio. host del servizio Hello è semplicemente un processo in cui è possono eseguire le istanze del servizio.
* **Registrazione del servizio**: la registrazione raccoglie tutti gli elementi. Hello tipo di servizio deve essere registrato con hello Service Fabric runtime in un servizio host tooallow Service Fabric toocreate istanze toorun.  

## <a name="create-a-stateless-service"></a>Creare un servizio senza stato
Iniziare a creare un'applicazione di Service Fabric. Hello Service Fabric SDK per Linux include un Yeoman lo scaffolding di hello tooprovide generatore di un'applicazione di Service Fabric con un servizio senza stato. Avviare eseguendo hello seguenti Yeoman comando:

```bash
$ yo azuresfjava
```

Seguire hello istruzioni toocreate un **affidabile di servizio senza stato**. Per questa esercitazione, hello e un'applicazione hello nome "HelloWorldApplication" servizio "HelloWorld". il risultato di Hello include directory per hello `HelloWorldApplication` e `HelloWorld`.

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>Implementare il servizio hello
Aprire **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Questa classe definisce il tipo di servizio hello e può eseguire qualsiasi codice. API del servizio Hello fornisce due punti di ingresso per il codice:

* Un metodo del punto di ingresso aperto denominato `runAsync()`, che consente di iniziare a eseguire qualsiasi carico di lavoro, inclusi carichi di lavoro di calcolo con esecuzione prolungata.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* Un punto di ingresso di comunicazione a cui è possibile collegare lo stack di comunicazione desiderato. In questo punto è possibile iniziare a ricevere richieste da utenti e da altri servizi.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

In questa esercitazione è incentrata su hello `runAsync()` metodo punto di ingresso. In questo punto è possibile iniziare immediatamente a eseguire il codice.

### <a name="runasync"></a>RunAsync
piattaforma Hello chiama questo metodo quando un'istanza di un servizio è tooexecute posizionato ed è pronto. Per un servizio senza stato, che indica semplicemente quando viene aperto l'istanza del servizio hello. Un token di annullamento viene fornito toocoordinate quando l'istanza del servizio deve toobe chiuso. In Service Fabric, questo ciclo di apertura o chiusura di un'istanza del servizio può verificarsi più volte nel ciclo di vita di hello del servizio hello nel suo complesso. Questa situazione può verificarsi per vari motivi, tra cui:

* sistema di Hello sposta le istanze del servizio di bilanciamento delle risorse.
* Si verificano errori nel codice.
* un'applicazione Hello o sistema viene aggiornato.
* hardware sottostante Hello di cui si verifichi un'interruzione del servizio.

Questa orchestrazione è gestita da Service Fabric tookeep il servizio a disponibilità elevata e bilanciato in modo corretto.

`runAsync()` non deve bloccarsi in modo sincrono. L'implementazione di runAsync deve restituire un runtime toocontinue di CompletableFuture tooallow hello. Se il carico di lavoro deve tooimplement un'attività a esecuzione prolungata che deve essere eseguita all'interno di hello CompletableFuture.

#### <a name="cancellation"></a>Annullamento
Annullamento del carico di lavoro è un lavoro cooperativo orchestrato da hello fornito token di annullamento. sistema Hello attende l'attività tooend (per il completamento, annullamento o errore) prima di spostare. È importante toohonor hello annullamento token, termina qualsiasi lavoro e chiudere `runAsync()` più rapidamente possibile quando il sistema hello richiede l'annullamento. Hello esempio seguente viene illustrato come un evento di annullamento toohandle:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>Registrazione del servizio
Tipi di servizio devono essere registrati con il runtime di Service Fabric hello. tipo di servizio Hello è definito in hello `ServiceManifest.xml` e la classe di servizio che implementa `StatelessService`. La registrazione del servizio viene eseguita nel punto di ingresso principale processo hello. In questo esempio hello processo il punto di ingresso principale è `HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

Hello Yeoman scaffolding include un gradle script toobuild hello applicazione e bash script toodeploy e rimuovere l'applicazione. applicazione hello toorun, prima dell'applicazione hello compilazione con gradle:

```bash
$ gradle
```

Questa operazione genera un pacchetto dell'applicazione Service Fabric che può essere distribuito tramite l'interfaccia della riga di comando di Service Fabric.

### <a name="deploy-with-service-fabric-cli"></a>Distribuire con l'interfaccia della riga di comando di Service Fabric

script install.sh Hello contiene hello necessarie servizio infrastruttura CLI comandi toodeploy hello pacchetto dell'applicazione. Eseguire l'applicazione di hello install.sh toodeploy script.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Passaggi successivi

* [Introduzione all'interfaccia della riga di comando di Service Fabric](service-fabric-cli.md)
