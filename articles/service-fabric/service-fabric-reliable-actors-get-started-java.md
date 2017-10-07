---
title: aaaCreate il primo microservizio Azure basato su attori in Java | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di creazione, il debug e distribuzione di un servizio basato su attori semplice usando Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Introduzione a Reliable Actors
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-actors-get-started.md)
> * [Java su Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

In questo articolo vengono illustrati concetti fondamentali di hello di Azure Service Fabric Reliable Actors e viene illustrato come creare e distribuire una semplice applicazione Reliable Actor in Java.

## <a name="installation-and-setup"></a>Installazione e configurazione
Prima di iniziare, verificare di che aver ambiente di sviluppo di Service Fabric hello configurare nel computer.
Se è necessario tooset, configurarlo, andare troppo[introduzione su Mac](service-fabric-get-started-mac.md) o [introduzione in Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Concetti di base
tooget introduttiva Reliable Actors, è solo necessario toounderstand alcuni concetti di base:

* **Servizio attore**. Reliable Actors sono inclusi nei servizi affidabili che può essere distribuito nell'infrastruttura di Service Fabric hello. Le istanze di Actors vengono attivate in un'istanza del servizio denominata.
* **Registrazione attore**. Come con i servizi affidabili, un servizio Reliable Actor deve toobe registrato con il runtime di Service Fabric hello. Inoltre, è necessario toobe registrato con il runtime di attore hello tipo attore hello.
* **Interfaccia attore**. interfaccia attore Hello è toodefine utilizzata un'interfaccia pubblica fortemente tipizzata di un attore. Nella terminologia dei modelli Reliable Actor hello, interfaccia attore hello definisce hello tipi di messaggi hello attore possono comprendere ed elaborare. interfaccia attore Hello viene utilizzato da altri attori e le applicazioni client troppo "inviano" (in modo asincrono) attore toohello messaggi. Reliable Actors può implementare più interfacce.
* **Classe ActorProxy**. classe ActorProxy Hello viene utilizzato da client applicazioni tooinvoke hello metodi esposti tramite l'interfaccia di hello attore. classe ActorProxy Hello offre due funzionalità importanti:
  
  * Risoluzione dei nomi: è in grado di toolocate attore di hello cluster hello (Trova hello nodo del cluster di hello in cui è ospitato).
  * Gestione degli errori: può ripetere chiamate al metodo e risolvere nuovamente il percorso di attore hello dopo, ad esempio, un errore che richiede hello attore toobe rilocato tooanother nodo cluster hello.

Hello alle regole che riguardano le interfacce tooactor è utile citare:

* I metodi di interfaccia dell'attore non possono essere sottoposti a overload.
* I metodi di interfaccia dell'attore non accettano parametri facoltativi, out o ref.
* Non sono supportate interfacce generiche.

## <a name="create-an-actor-service"></a>Creare un servizio Actor
Per iniziare, creare una nuova applicazione di Service Fabric. Hello Service Fabric SDK per Linux include un Yeoman lo scaffolding di hello tooprovide generatore di un'applicazione di Service Fabric con un servizio senza stato. Avviare eseguendo hello seguenti Yeoman comando:

```bash
$ yo azuresfjava
```

Seguire hello istruzioni toocreate un **servizio Actor affidabile**. Per questa esercitazione, denominare hello applicazione "HelloWorldActorApplication" e hello attore "HelloWorldActor". verrà creato dopo lo scaffolding Hello:

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>Blocchi predefiniti di base di Reliable Actors
concetti di base Hello descritti in precedenza si traducono in hello blocchi predefiniti di base di un servizio Reliable Actor.

### <a name="actor-interface"></a>Interfaccia dell'attore
Contiene la definizione di interfaccia hello per attore hello. Questa interfaccia definisce contratto attore hello condiviso da implementazione attore hello e i client hello chiamata attore hello, pertanto è in genere senso toodefine in una posizione separati dall'implementazione attore hello e può essere condiviso da diversi altri servizi o applicazioni client.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Servizio Actor
Questo blocco contiene l'implementazione dell'attore e il codice di registrazione dell'attore. classe attore Hello implementa interfaccia attore hello. Questa è la posizione in cui l'attore svolge il suo lavoro.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>Registrazione dell'attore
servizio actor Hello deve essere registrato con un tipo di servizio nel runtime di Service Fabric hello. Per consentire hello servizio Actor toorun le istanze di attore, il tipo di attore inoltre deve essere registrato con hello servizio Actor. Hello `ActorRuntime` metodo di registrazione, questa operazione viene eseguita per attori.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>Client di prova
Si tratta di un'applicazione client di test semplice è possibile eseguire separatamente da tootest applicazione di Service Fabric hello del servizio actor. Questo è un esempio di dove hello ActorProxy può essere tooactivate utilizzato e comunicare con istanze attore. Non viene distribuito con il servizio.

### <a name="hello-application"></a>applicazione Hello
Infine, i pacchetti di applicazione hello hello servizio actor e altri servizi che è possibile aggiungere in hello futura insieme per la distribuzione. Contiene hello *ApplicationManifest.xml* e segnaposto per il pacchetto di servizio actor hello.

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

Hello Yeoman scaffolding include un gradle script toobuild hello applicazione e bash script toodeploy e rimuovere l'applicazione. applicazione hello toodeploy, prima dell'applicazione hello compilazione con gradle:

```bash
$ gradle
```

Si otterrà un pacchetto dell'applicazione di Service Fabric che può essere distribuito tramite gli strumenti dell'interfaccia della riga di comando di Service Fabric.

### <a name="deploy-service-fabric-cli"></a>Distribuire l'interfaccia della riga di comando di Service Fabric

script install.sh Hello contiene hello necessarie servizio infrastruttura CLI (sfctl) comandi toodeploy hello pacchetto dell'applicazione.
Eseguire un'applicazione hello hello install.sh script toodeploy.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Passaggi successivi

* [Introduzione all'interfaccia della riga di comando di Service Fabric](service-fabric-cli.md)
