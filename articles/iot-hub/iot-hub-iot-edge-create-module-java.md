---
title: un modulo di Edge IoT di Azure con Java aaaCreate | Documenti Microsoft
description: "In questa esercitazione illustra come un BILITA dati convertitore modulo tramite toowrite hello pacchetti Maven Edge IoT di Azure più recenti."
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="b9bea-103">Creare un modulo Azure IoT Edge con Java</span><span class="sxs-lookup"><span data-stu-id="b9bea-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="b9bea-104">Questa esercitazione illustra come è possibile creare un modulo per Azure IoT Edge in Java.</span><span class="sxs-lookup"><span data-stu-id="b9bea-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="b9bea-105">In questa esercitazione, si verrà illustrata l'impostazione dell'ambiente e come toowrite un [BILITA](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) modulo convertitore di tipi di dati utilizzando pacchetti Azure IoT Edge Maven più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="b9bea-105">In this tutorial, we will walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9bea-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b9bea-106">Prerequisites</span></span>

<span data-ttu-id="b9bea-107">In questa sezione si configurerà l'ambiente per lo sviluppo del modulo IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="b9bea-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="b9bea-108">Si applica tooboth *Windows a 64 bit* e *Linux a 64 bit (8 Ubuntu/Debian)* i sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="b9bea-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="b9bea-109">Hello seguente software è necessario:</span><span class="sxs-lookup"><span data-stu-id="b9bea-109">hello following software is required:</span></span>

* <span data-ttu-id="b9bea-110">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="b9bea-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="b9bea-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="b9bea-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="b9bea-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="b9bea-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="b9bea-113">Aprire della riga di comando terminal finestra e clone hello seguenti repository:</span><span class="sxs-lookup"><span data-stu-id="b9bea-113">Open a command-line terminal window and clone hello following repository:</span></span>

1. <span data-ttu-id="b9bea-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="b9bea-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="b9bea-115">Architettura complessiva</span><span class="sxs-lookup"><span data-stu-id="b9bea-115">Overall architecture</span></span>

<span data-ttu-id="b9bea-116">piattaforma Azure IoT Edge Hello adotta frequentemente hello [architettura Neumann Von](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="b9bea-116">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="b9bea-117">Ovvero l'architettura di Azure IoT bordo intero hello è un sistema che elabora l'input e produce l'output. e che ogni singolo modulo sia anche un piccolo sottosistema di input / output.</span><span class="sxs-lookup"><span data-stu-id="b9bea-117">Which means that hello entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="b9bea-118">In questa esercitazione verrà illustrata hello due moduli seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bea-118">In this tutorial, we will introduce hello following two modules:</span></span>

1. <span data-ttu-id="b9bea-119">Un modulo che riceve un segnale [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulato e lo converte in un messaggio [JSON](https://en.wikipedia.org/wiki/JSON) formattato.</span><span class="sxs-lookup"><span data-stu-id="b9bea-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="b9bea-120">Un modulo che consente di stampare hello ricevuto [JSON](https://en.wikipedia.org/wiki/JSON) messaggio.</span><span class="sxs-lookup"><span data-stu-id="b9bea-120">A module which prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="b9bea-121">Hello seguente immagine Mostra hello tipico end-to-end del flusso di dati per questo progetto:</span><span class="sxs-lookup"><span data-stu-id="b9bea-121">hello following image displays hello typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="b9bea-122">![Flusso di dati tra tre moduli](media/iot-hub-iot-edge-create-module/dataflow.png "Input: modulo BLE simulato; Processore: modulo convertitore; Output: modulo stampante")</span><span class="sxs-lookup"><span data-stu-id="b9bea-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="b9bea-123">Informazioni sul codice hello</span><span class="sxs-lookup"><span data-stu-id="b9bea-123">Understanding hello code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="b9bea-124">Struttura di progetto Maven</span><span class="sxs-lookup"><span data-stu-id="b9bea-124">Maven project structure</span></span>

<span data-ttu-id="b9bea-125">Poiché i pacchetti di Azure IoT Edge sono basati su Maven, dobbiamo toocreate una struttura di progetto Maven tipica, che contiene un `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="b9bea-125">Since Azure IoT Edge packages are based on Maven, we need toocreate a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="b9bea-126">Hello POM eredita hello `com.microsoft.azure.gateway.gateway-module-base` pacchetto, che consente di dichiarare tutte le dipendenze di hello necessarie per un progetto di modulo che include i file binari di runtime hello, percorso di file di configurazione di gateway hello e il comportamento di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="b9bea-126">hello POM inherits from hello `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of hello dependencies needed by a module project which includes hello runtime binaries, hello gateway configuration file path, and hello execution behavior.</span></span> <span data-ttu-id="b9bea-127">Ciò ci consente di risparmiare molto tempo ed eliminare toowrite necessità hello e riscrivere ripetutamente centinaia di righe di codice.</span><span class="sxs-lookup"><span data-stu-id="b9bea-127">This saves us lots of time and eliminate hello need toowrite and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="b9bea-128">È necessario il file pom.xml tooupdate dichiarando hello necessarie dipendenze/plug-in e il nome di hello di hello toobe di file di configurazione utilizzato da questo modulo come illustrato nel seguente frammento di codice hello.</span><span class="sxs-lookup"><span data-stu-id="b9bea-128">We need tooupdate the pom.xml file by declaring hello required dependencies/plugins and hello name of hello configuration file toobe used by our module as shown in hello following code snippet.</span></span>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set hello filename of hello Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="b9bea-129">Conoscenza di base di un modulo Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b9bea-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="b9bea-130">È possibile gestire il modulo Azure IoT Edge come elaboratore di dati il cui compito è di ricevere l'input, elaborarlo e produrre l'output.</span><span class="sxs-lookup"><span data-stu-id="b9bea-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="b9bea-131">Hello input potrebbe essere dati dall'hardware (ad esempio un rilevatore di movimento), un messaggio da altri moduli, o qualsiasi altro (ad esempio, un numero casuale generato periodicamente da un timer).</span><span class="sxs-lookup"><span data-stu-id="b9bea-131">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="b9bea-132">output di Hello input toohello simile, potrebbe attivare il comportamento di hardware (ad esempio hello LED lampeggiante), i moduli tooother un messaggio o a qualsiasi altro (ad esempio stampa toohello console).</span><span class="sxs-lookup"><span data-stu-id="b9bea-132">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="b9bea-133">I moduli comunicano reciprocamente usando la classe `com.microsoft.azure.gateway.messaging.Message`.</span><span class="sxs-lookup"><span data-stu-id="b9bea-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="b9bea-134">Hello **contenuto** di un `Message` è una matrice di byte che è in grado di rappresentare qualsiasi tipo di dati desiderato.</span><span class="sxs-lookup"><span data-stu-id="b9bea-134">hello **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="b9bea-135">**Proprietà** sono disponibili anche in hello `Message` e sono semplicemente un mapping da stringa-stringa.</span><span class="sxs-lookup"><span data-stu-id="b9bea-135">**Properties** are also available in hello `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="b9bea-136">È possibile pensare **proprietà** come intestazioni hello in una richiesta HTTP o hello metadati di un file.</span><span class="sxs-lookup"><span data-stu-id="b9bea-136">You may think of **Properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="b9bea-137">In ordine toodevelop un modulo di Azure IoT Edge in Java, è necessario toocreate una nuova classe di modulo che eredita da `com.microsoft.azure.gateway.core.GatewayModule` e implementare i metodi astratti necessario hello `receive()` e `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="b9bea-137">In order toodevelop an Azure IoT Edge module in Java, you need toocreate a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement hello required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="b9bea-138">A questo punto, è inoltre possibile scegliere hello tooimplement facoltativo `start()` o `create()` anche i metodi.</span><span class="sxs-lookup"><span data-stu-id="b9bea-138">At this point, you may also choose tooimplement hello optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="b9bea-139">Hello frammento di codice seguente viene illustrato come tooget iniziare la creazione di un modulo di Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="b9bea-139">hello following code snippet shows you how tooget started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="b9bea-140">Modulo convertitore</span><span class="sxs-lookup"><span data-stu-id="b9bea-140">Converter module</span></span>

| <span data-ttu-id="b9bea-141">Input</span><span class="sxs-lookup"><span data-stu-id="b9bea-141">Input</span></span>                    | <span data-ttu-id="b9bea-142">Processore</span><span class="sxs-lookup"><span data-stu-id="b9bea-142">Processor</span></span>                              | <span data-ttu-id="b9bea-143">Output</span><span class="sxs-lookup"><span data-stu-id="b9bea-143">Output</span></span>                 | <span data-ttu-id="b9bea-144">File di origine</span><span class="sxs-lookup"><span data-stu-id="b9bea-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="b9bea-145">Messaggio sui dati della temperatura</span><span class="sxs-lookup"><span data-stu-id="b9bea-145">Temperature data message</span></span> | <span data-ttu-id="b9bea-146">Analizza e crea un nuovo messaggio JSON</span><span class="sxs-lookup"><span data-stu-id="b9bea-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="b9bea-147">Messaggio JSON strutturato</span><span class="sxs-lookup"><span data-stu-id="b9bea-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="b9bea-148">Questo è un tipico modulo Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="b9bea-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="b9bea-149">Accetta messaggi temperatura da altri moduli (modulo di hardware, o in questo caso, il modulo BILITA simulato); e quindi Normalizza il messaggio di temperatura hello nel messaggio JSON tooa strutturata (inclusi aggiungendo l'ID del messaggio hello, impostazione proprietà hello di se occorre avviso temperatura tootrigger hello e così via).</span><span class="sxs-lookup"><span data-stu-id="b9bea-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a><span data-ttu-id="b9bea-150">Modulo della stampante</span><span class="sxs-lookup"><span data-stu-id="b9bea-150">Printer module</span></span>

| <span data-ttu-id="b9bea-151">Input</span><span class="sxs-lookup"><span data-stu-id="b9bea-151">Input</span></span>                          | <span data-ttu-id="b9bea-152">Processore</span><span class="sxs-lookup"><span data-stu-id="b9bea-152">Processor</span></span> | <span data-ttu-id="b9bea-153">Output</span><span class="sxs-lookup"><span data-stu-id="b9bea-153">Output</span></span>                     | <span data-ttu-id="b9bea-154">File di origine</span><span class="sxs-lookup"><span data-stu-id="b9bea-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="b9bea-155">Qualsiasi messaggio da altri moduli</span><span class="sxs-lookup"><span data-stu-id="b9bea-155">Any message from other modules</span></span> | <span data-ttu-id="b9bea-156">N/D</span><span class="sxs-lookup"><span data-stu-id="b9bea-156">N/A</span></span>       | <span data-ttu-id="b9bea-157">Log tooconsole messaggio hello</span><span class="sxs-lookup"><span data-stu-id="b9bea-157">Log hello message tooconsole</span></span> | `PrinterModule.java` |

<span data-ttu-id="b9bea-158">Si tratta di un modulo semplice e chiara interpretazione, che restituisce una finestra terminale toohello di messaggi hello ricevuto.</span><span class="sxs-lookup"><span data-stu-id="b9bea-158">This is a simple, self-explanatory, module which outputs hello received messages toohello terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="b9bea-159">Configurazione di Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b9bea-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="b9bea-160">passaggio finale di Hello prima di eseguire i moduli di hello è tooconfigure hello Azure IoT Edge e connessioni di hello tooestablish tra i moduli.</span><span class="sxs-lookup"><span data-stu-id="b9bea-160">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="b9bea-161">È prima necessario toodeclare il caricatore di Java (dal bordo IoT di Azure supporta caricatori di lingue diverse) che può fare riferimento relativo `name` nelle sezioni hello in seguito.</span><span class="sxs-lookup"><span data-stu-id="b9bea-161">First we need toodeclare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

<span data-ttu-id="b9bea-162">Una volta che è stato dichiarato il nostro caricatori, è anche necessario toodeclare anche i moduli.</span><span class="sxs-lookup"><span data-stu-id="b9bea-162">Once we have declared our loaders, we will also need toodeclare our modules as well.</span></span> <span data-ttu-id="b9bea-163">Caricatori di hello toodeclaring simili, è possibile inoltre farvi riferimento dal loro `name` attributo.</span><span class="sxs-lookup"><span data-stu-id="b9bea-163">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="b9bea-164">Quando si dichiara un modulo, è necessario caricatore hello toospecify deve utilizzare (che deve essere hello uno è stato definito prima) e hello punto di ingresso (il nome della classe normalizzato hello del nostro modulo deve essere) per ogni modulo.</span><span class="sxs-lookup"><span data-stu-id="b9bea-164">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="b9bea-165">Hello `simulated_device` è un modulo nativo incluso nel pacchetto di runtime di hello Azure IoT Edge core.</span><span class="sxs-lookup"><span data-stu-id="b9bea-165">hello `simulated_device` module is a native module which is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="b9bea-166">È necessario includere sempre `args` nel file JSON, anche se hello `null`.</span><span class="sxs-lookup"><span data-stu-id="b9bea-166">You should always include `args` in hello JSON file even if it is `null`.</span></span>

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="b9bea-167">Alla fine di hello della configurazione di hello, è stabilire le connessioni di hello.</span><span class="sxs-lookup"><span data-stu-id="b9bea-167">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="b9bea-168">Ogni connessione è espressa da `source` e `sink`.</span><span class="sxs-lookup"><span data-stu-id="b9bea-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="b9bea-169">Entrambi devono fare riferimento a un modulo predefinito.</span><span class="sxs-lookup"><span data-stu-id="b9bea-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="b9bea-170">messaggio di output di Hello di `source` modulo verrà inoltrato input toohello di `sink` modulo.</span><span class="sxs-lookup"><span data-stu-id="b9bea-170">hello output message of `source` module will be forwarded toohello input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-hello-modules"></a><span data-ttu-id="b9bea-171">Moduli di hello in esecuzione</span><span class="sxs-lookup"><span data-stu-id="b9bea-171">Running hello modules</span></span>

<span data-ttu-id="b9bea-172">Utilizzare `mvn package` toobuild tutti gli elementi in hello `target/` cartella.</span><span class="sxs-lookup"><span data-stu-id="b9bea-172">Use `mvn package` toobuild everything into hello `target/` folder.</span></span> <span data-ttu-id="b9bea-173">Per eseguire una compilazione pulita, è consigliato anche `mvn clean package`.</span><span class="sxs-lookup"><span data-stu-id="b9bea-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="b9bea-174">Utilizzare `mvn exec:exec` toorun hello Azure IoT Edge e deve rispettare che i dati di temperatura hello e tutte le proprietà di hello siano toohello stampato console a un corrispettivo fisso.</span><span class="sxs-lookup"><span data-stu-id="b9bea-174">Use `mvn exec:exec` toorun hello Azure IoT Edge and you should observe that hello temperature data and all hello properties are printed toohello console at a fixed rate.</span></span>

<span data-ttu-id="b9bea-175">Se si desidera un'applicazione hello tooterminate, premere `<Enter>` chiave.</span><span class="sxs-lookup"><span data-stu-id="b9bea-175">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9bea-176">Non è consigliabile toouse Ctrl + C tooterminate hello IoT Edge applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="b9bea-176">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge gateway application.</span></span> <span data-ttu-id="b9bea-177">Come potrebbe tooterminate processo hello in modo anomalo.</span><span class="sxs-lookup"><span data-stu-id="b9bea-177">As this may cause hello process tooterminate abnormally.</span></span>

