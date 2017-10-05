---
title: Creare un modulo Azure IoT Edge con Java | Microsoft Docs
description: "Questa esercitazione illustra come scrivere un modulo convertitore di dati BLE usando i pacchetti Maven di Azure IoT Edge più recenti."
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
ms.openlocfilehash: 0c430272225d79737baec2be15ed7c93991cdeac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="003ae-103">Creare un modulo Azure IoT Edge con Java</span><span class="sxs-lookup"><span data-stu-id="003ae-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="003ae-104">Questa esercitazione illustra come è possibile creare un modulo per Azure IoT Edge in Java.</span><span class="sxs-lookup"><span data-stu-id="003ae-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="003ae-105">L'esercitazione illustra i passaggi per configurare l'ambiente e spiega come scrivere un modulo convertitore di dati [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) usando la versione più recente dei pacchetti Maven di Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="003ae-105">In this tutorial, we will walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="003ae-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="003ae-106">Prerequisites</span></span>

<span data-ttu-id="003ae-107">In questa sezione si configurerà l'ambiente per lo sviluppo del modulo IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="003ae-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="003ae-108">Si applica sia a *Windows a 64 bit* sia a *Linux a 64 bit (Ubuntu/Debian 8)*.</span><span class="sxs-lookup"><span data-stu-id="003ae-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="003ae-109">È richiesto il software seguente:</span><span class="sxs-lookup"><span data-stu-id="003ae-109">The following software is required:</span></span>

* <span data-ttu-id="003ae-110">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="003ae-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="003ae-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="003ae-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="003ae-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="003ae-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="003ae-113">Aprire una finestra del terminale della riga di comando e clonare il repository seguente:</span><span class="sxs-lookup"><span data-stu-id="003ae-113">Open a command-line terminal window and clone the following repository:</span></span>

1. <span data-ttu-id="003ae-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="003ae-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="003ae-115">Architettura complessiva</span><span class="sxs-lookup"><span data-stu-id="003ae-115">Overall architecture</span></span>

<span data-ttu-id="003ae-116">La piattaforma Azure IoT Edge usa frequentemente l'[architettura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="003ae-116">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="003ae-117">L'intera architettura di Azure IoT Edge è quindi un sistema che elabora input e produce output e ogni singolo modulo è anche un piccolo sottosistema di input/output.</span><span class="sxs-lookup"><span data-stu-id="003ae-117">Which means that the entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="003ae-118">In questa esercitazione verranno presentati i due moduli seguenti:</span><span class="sxs-lookup"><span data-stu-id="003ae-118">In this tutorial, we will introduce the following two modules:</span></span>

1. <span data-ttu-id="003ae-119">Un modulo che riceve un segnale [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulato e lo converte in un messaggio [JSON](https://en.wikipedia.org/wiki/JSON) formattato.</span><span class="sxs-lookup"><span data-stu-id="003ae-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="003ae-120">Un modulo che stampa il messaggio [JSON](https://en.wikipedia.org/wiki/JSON) ricevuto.</span><span class="sxs-lookup"><span data-stu-id="003ae-120">A module which prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="003ae-121">L'immagine seguente mostra il tipico flusso di dati end-to-end per il progetto:</span><span class="sxs-lookup"><span data-stu-id="003ae-121">The following image displays the typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="003ae-122">![Flusso di dati tra tre moduli](media/iot-hub-iot-edge-create-module/dataflow.png "Input: modulo BLE simulato; Processore: modulo convertitore; Output: modulo stampante")</span><span class="sxs-lookup"><span data-stu-id="003ae-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="003ae-123">Informazioni sul codice</span><span class="sxs-lookup"><span data-stu-id="003ae-123">Understanding the code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="003ae-124">Struttura di progetto Maven</span><span class="sxs-lookup"><span data-stu-id="003ae-124">Maven project structure</span></span>

<span data-ttu-id="003ae-125">Poiché i pacchetti Azure IoT Edge sono basati su Maven, è necessario creare una tipica struttura di progetto Maven, che contiene un file `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="003ae-125">Since Azure IoT Edge packages are based on Maven, we need to create a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="003ae-126">Il modello POM eredita dal pacchetto `com.microsoft.azure.gateway.gateway-module-base`, che dichiara tutte le dipendenze necessarie per un progetto di modulo contenente i file binari di runtime, il percorso del file di configurazione del gateway e il comportamento di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="003ae-126">The POM inherits from the `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of the dependencies needed by a module project which includes the runtime binaries, the gateway configuration file path, and the execution behavior.</span></span> <span data-ttu-id="003ae-127">Questo consente di risparmiare molto tempo ed elimina la necessità di scrivere e riscrivere ripetutamente centinaia di righe di codice.</span><span class="sxs-lookup"><span data-stu-id="003ae-127">This saves us lots of time and eliminate the need to write and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="003ae-128">È necessario aggiornare il file pom.xml dichiarando i plug-in o le dipendenze necessarie e il nome del file di configurazione che deve essere usato da questo modulo, come illustrato nel frammento di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="003ae-128">We need to update the pom.xml file by declaring the required dependencies/plugins and the name of the configuration file to be used by our module as shown in the following code snippet.</span></span>

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

  <!-- Set the filename of the Azure IoT Edge configuration located
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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="003ae-129">Conoscenza di base di un modulo Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="003ae-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="003ae-130">È possibile gestire il modulo Azure IoT Edge come elaboratore di dati il cui compito è di ricevere l'input, elaborarlo e produrre l'output.</span><span class="sxs-lookup"><span data-stu-id="003ae-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="003ae-131">L'input potrebbe essere costituito da dati dell'hardware (ad esempio un rilevatore di movimento), un messaggio da altri moduli o qualsiasi altra informazione (ad esempio un numero casuale generato periodicamente da un timer).</span><span class="sxs-lookup"><span data-stu-id="003ae-131">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="003ae-132">L'output è simile all'input. Può attivare il comportamento dell'hardware, ad esempio il lampeggiamento di un LED, generare un messaggio ad altri moduli o qualsiasi altra azione, ad esempio la stampa nella console.</span><span class="sxs-lookup"><span data-stu-id="003ae-132">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="003ae-133">I moduli comunicano reciprocamente usando la classe `com.microsoft.azure.gateway.messaging.Message`.</span><span class="sxs-lookup"><span data-stu-id="003ae-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="003ae-134">Il **contenuto** di un `Message` è una matrice di byte in grado di rappresentare qualsiasi genere di dati.</span><span class="sxs-lookup"><span data-stu-id="003ae-134">The **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="003ae-135">Nel `Message` sono presenti anche **proprietà** che rappresentano semplicemente il mapping stringa-a-stringa.</span><span class="sxs-lookup"><span data-stu-id="003ae-135">**Properties** are also available in the `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="003ae-136">Si può pensare alle **proprietà** come alle intestazioni in una richiesta HTTP o ai metadati di un file.</span><span class="sxs-lookup"><span data-stu-id="003ae-136">You may think of **Properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="003ae-137">Per sviluppare un modulo Azure IoT Edge in Java, è necessario creare una nuova classe di moduli che eredita da `com.microsoft.azure.gateway.core.GatewayModule` e implementare i metodi astratti necessari `receive()` e `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="003ae-137">In order to develop an Azure IoT Edge module in Java, you need to create a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement the required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="003ae-138">A questo punto, è possibile anche implementare i metodi `start()` e `create()` facoltativi.</span><span class="sxs-lookup"><span data-stu-id="003ae-138">At this point, you may also choose to implement the optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="003ae-139">Il frammento di codice seguente illustra come iniziare la creazione di un modulo Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="003ae-139">The following code snippet shows you how to get started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let the GatewayModule do the dirty work of initialization. It's also
       a good time to parse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire the resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time to release all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic to process the input message. This method is required. */
    // ...
    /* Use publish() method to do the output. You are
       allowed to publish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="003ae-140">Modulo convertitore</span><span class="sxs-lookup"><span data-stu-id="003ae-140">Converter module</span></span>

| <span data-ttu-id="003ae-141">Input</span><span class="sxs-lookup"><span data-stu-id="003ae-141">Input</span></span>                    | <span data-ttu-id="003ae-142">Processore</span><span class="sxs-lookup"><span data-stu-id="003ae-142">Processor</span></span>                              | <span data-ttu-id="003ae-143">Output</span><span class="sxs-lookup"><span data-stu-id="003ae-143">Output</span></span>                 | <span data-ttu-id="003ae-144">File di origine</span><span class="sxs-lookup"><span data-stu-id="003ae-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="003ae-145">Messaggio sui dati della temperatura</span><span class="sxs-lookup"><span data-stu-id="003ae-145">Temperature data message</span></span> | <span data-ttu-id="003ae-146">Analizza e crea un nuovo messaggio JSON</span><span class="sxs-lookup"><span data-stu-id="003ae-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="003ae-147">Messaggio JSON strutturato</span><span class="sxs-lookup"><span data-stu-id="003ae-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="003ae-148">Questo è un tipico modulo Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="003ae-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="003ae-149">Accetta messaggi sulla temperatura da altri moduli, ad esempio un modulo hardware o in questo caso il modulo BLE simulato. Normalizza quindi il messaggio sulla temperatura in un messaggio JSON strutturato, includendo l'aggiunta dell'ID di messaggio, l'impostazione della proprietà che indica se è necessario attivare l'avviso di temperatura e così via.</span><span class="sxs-lookup"><span data-stu-id="003ae-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="003ae-150">Modulo della stampante</span><span class="sxs-lookup"><span data-stu-id="003ae-150">Printer module</span></span>

| <span data-ttu-id="003ae-151">Input</span><span class="sxs-lookup"><span data-stu-id="003ae-151">Input</span></span>                          | <span data-ttu-id="003ae-152">Processore</span><span class="sxs-lookup"><span data-stu-id="003ae-152">Processor</span></span> | <span data-ttu-id="003ae-153">Output</span><span class="sxs-lookup"><span data-stu-id="003ae-153">Output</span></span>                     | <span data-ttu-id="003ae-154">File di origine</span><span class="sxs-lookup"><span data-stu-id="003ae-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="003ae-155">Qualsiasi messaggio da altri moduli</span><span class="sxs-lookup"><span data-stu-id="003ae-155">Any message from other modules</span></span> | <span data-ttu-id="003ae-156">N/D</span><span class="sxs-lookup"><span data-stu-id="003ae-156">N/A</span></span>       | <span data-ttu-id="003ae-157">Registra il messaggio nella console</span><span class="sxs-lookup"><span data-stu-id="003ae-157">Log the message to console</span></span> | `PrinterModule.java` |

<span data-ttu-id="003ae-158">Questo modulo semplice e di chiara interpretazione restituisce i messaggi ricevuti alla finestra Terminal.</span><span class="sxs-lookup"><span data-stu-id="003ae-158">This is a simple, self-explanatory, module which outputs the received messages to the terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="003ae-159">Configurazione di Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="003ae-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="003ae-160">Il passaggio finale prima di eseguire i moduli consiste nel configurare Azure IoT Edge e stabilire le connessioni tra i moduli.</span><span class="sxs-lookup"><span data-stu-id="003ae-160">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="003ae-161">Dal momento che Azure IoT Edge supporta caricatori di varie lingue, occorre prima dichiarare il caricatore Java specifico, a cui si potrebbe fare riferimento in base al `name` nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="003ae-161">First we need to declare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

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

<span data-ttu-id="003ae-162">Dopo avere dichiarato i caricatori, sarà necessario dichiarare anche i moduli.</span><span class="sxs-lookup"><span data-stu-id="003ae-162">Once we have declared our loaders, we will also need to declare our modules as well.</span></span> <span data-ttu-id="003ae-163">Come avviene nella dichiarazione dei caricatori, anche ai moduli è possibile fare riferimento tramite il relativo attributo `name`.</span><span class="sxs-lookup"><span data-stu-id="003ae-163">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="003ae-164">Quando si dichiara un modulo, è necessario specificare il caricatore che il modulo deve usare (che dovrebbe essere quello che è stato definito prima) e il punto di ingresso (che dovrebbe essere il nome della classe normalizzata del modulo) per ogni modulo.</span><span class="sxs-lookup"><span data-stu-id="003ae-164">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="003ae-165">Il modulo `simulated_device` è un modulo nativo che è incluso nel pacchetto di runtime principale di Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="003ae-165">The `simulated_device` module is a native module which is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="003ae-166">È opportuno includere sempre `args` nel file JSON, anche se è `null`.</span><span class="sxs-lookup"><span data-stu-id="003ae-166">You should always include `args` in the JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="003ae-167">Al termine della configurazione occorre stabilire le connessioni.</span><span class="sxs-lookup"><span data-stu-id="003ae-167">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="003ae-168">Ogni connessione è espressa da `source` e `sink`.</span><span class="sxs-lookup"><span data-stu-id="003ae-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="003ae-169">Entrambi devono fare riferimento a un modulo predefinito.</span><span class="sxs-lookup"><span data-stu-id="003ae-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="003ae-170">Il messaggio di output del modulo `source` viene inoltrato all'input del modulo `sink`.</span><span class="sxs-lookup"><span data-stu-id="003ae-170">The output message of `source` module will be forwarded to the input of `sink` module.</span></span>

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

## <a name="running-the-modules"></a><span data-ttu-id="003ae-171">Esecuzione dei moduli</span><span class="sxs-lookup"><span data-stu-id="003ae-171">Running the modules</span></span>

<span data-ttu-id="003ae-172">Usare `mvn package` per compilare tutti gli elementi nella cartella `target/`.</span><span class="sxs-lookup"><span data-stu-id="003ae-172">Use `mvn package` to build everything into the `target/` folder.</span></span> <span data-ttu-id="003ae-173">Per eseguire una compilazione pulita, è consigliato anche `mvn clean package`.</span><span class="sxs-lookup"><span data-stu-id="003ae-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="003ae-174">Usare `mvn exec:exec` per eseguire Azure IoT Edge; è importante osservare che i dati sulla temperatura e tutte le proprietà vengono stampate nella console a una tariffa fissa.</span><span class="sxs-lookup"><span data-stu-id="003ae-174">Use `mvn exec:exec` to run the Azure IoT Edge and you should observe that the temperature data and all the properties are printed to the console at a fixed rate.</span></span>

<span data-ttu-id="003ae-175">Se si vuole terminare l'applicazione, premere `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="003ae-175">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="003ae-176">Non è consigliabile usare Ctrl + C per terminare l'applicazione gateway IoT Edge,</span><span class="sxs-lookup"><span data-stu-id="003ae-176">It is not recommended to use Ctrl + C to terminate the IoT Edge gateway application.</span></span> <span data-ttu-id="003ae-177">poiché questa azione può determinare un arresto anomalo del processo.</span><span class="sxs-lookup"><span data-stu-id="003ae-177">As this may cause the process to terminate abnormally.</span></span>

