---
title: Creare un modulo Azure IoT Edge con Node.js | Microsoft Docs
description: "Questa esercitazione illustra come scrivere un modulo convertitore di dati BLE usando i pacchetti NPM di Azure IoT Edge più recenti e il generatore Yeoman."
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: ba466f47e157d805600c41fa3d84ed5a0363969c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="b7799-103">Creare un modulo Azure IoT Edge con Node.js</span><span class="sxs-lookup"><span data-stu-id="b7799-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="b7799-104">Questa esercitazione illustra come creare un modulo per Azure IoT Edge in JS.</span><span class="sxs-lookup"><span data-stu-id="b7799-104">This tutorial showcases how to create a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="b7799-105">L'esercitazione illustra i passaggi per configurare l'ambiente e spiega come scrivere un modulo convertitore di dati [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) con la versione più recente dei pacchetti NPM di Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="b7799-105">In this tutorial, we walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7799-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b7799-106">Prerequisites</span></span>

<span data-ttu-id="b7799-107">In questa sezione si configura l'ambiente per lo sviluppo del modulo IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="b7799-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="b7799-108">Si applica sia a *Windows a 64 bit* che a *Linux a 64 bit (Ubuntu 14+)*.</span><span class="sxs-lookup"><span data-stu-id="b7799-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="b7799-109">È richiesto il software seguente:</span><span class="sxs-lookup"><span data-stu-id="b7799-109">The following software is required:</span></span>
* <span data-ttu-id="b7799-110">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="b7799-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="b7799-111">[Nodo LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="b7799-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="b7799-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="b7799-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="b7799-113">Architettura</span><span class="sxs-lookup"><span data-stu-id="b7799-113">Architecture</span></span>

<span data-ttu-id="b7799-114">La piattaforma Azure IoT Edge usa frequentemente l'[architettura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="b7799-114">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="b7799-115">L'intera architettura di Azure IoT Edge è quindi un sistema che elabora input e produce output e ogni singolo modulo è anche un piccolo sottosistema di input/output.</span><span class="sxs-lookup"><span data-stu-id="b7799-115">Which means that the entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="b7799-116">In questa esercitazione vengono presentati i due moduli seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7799-116">In this tutorial, we introduce the following two modules:</span></span>

1. <span data-ttu-id="b7799-117">Un modulo che riceve un segnale [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulato e lo converte in un messaggio [JSON](https://en.wikipedia.org/wiki/JSON) formattato.</span><span class="sxs-lookup"><span data-stu-id="b7799-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="b7799-118">Un modulo che stampa il messaggio [JSON](https://en.wikipedia.org/wiki/JSON) ricevuto.</span><span class="sxs-lookup"><span data-stu-id="b7799-118">A module that prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="b7799-119">L'immagine seguente mostra il tipico flusso di dati end-to-end per il progetto:</span><span class="sxs-lookup"><span data-stu-id="b7799-119">The following image displays the typical end to end dataflow for this project:</span></span>

<span data-ttu-id="b7799-120">![Flusso di dati tra tre moduli](media/iot-hub-iot-edge-create-module/dataflow.png "Input: modulo BLE simulato; Processore: modulo convertitore; Output: modulo stampante")</span><span class="sxs-lookup"><span data-stu-id="b7799-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-the-environment"></a><span data-ttu-id="b7799-121">Configurare l'ambiente</span><span class="sxs-lookup"><span data-stu-id="b7799-121">Set up the environment</span></span>
<span data-ttu-id="b7799-122">Di seguito viene mostrato come configurare rapidamente l'ambiente per iniziare a scrivere il primo modulo convertitore BLE con JS.</span><span class="sxs-lookup"><span data-stu-id="b7799-122">Below we show you how to quickly set up environment to start to write your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="b7799-123">Creare un progetto di modulo</span><span class="sxs-lookup"><span data-stu-id="b7799-123">Create module project</span></span>
1. <span data-ttu-id="b7799-124">Aprire la finestra della riga di comando ed eseguire `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="b7799-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="b7799-125">Seguire i passaggi visualizzati per completare l'inizializzazione del progetto del modulo.</span><span class="sxs-lookup"><span data-stu-id="b7799-125">Follow the steps on the screen to finish the initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="b7799-126">Struttura progetto</span><span class="sxs-lookup"><span data-stu-id="b7799-126">Project structure</span></span>
<span data-ttu-id="b7799-127">Un progetto di modulo JS è costituito dai componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7799-127">A JS module project consists of the following components:</span></span>

<span data-ttu-id="b7799-128">`modules` - I file di origine del modulo JS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="b7799-128">`modules` - The customized JS module source files.</span></span> <span data-ttu-id="b7799-129">Sostituire i file `sensor.js` e `printer.js` predefiniti con i propri file del modulo.</span><span class="sxs-lookup"><span data-stu-id="b7799-129">Replace the default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="b7799-130">`app.js` - Il file di voce per avviare l'istanza di Edge.</span><span class="sxs-lookup"><span data-stu-id="b7799-130">`app.js` - The entry file to start the Edge instance.</span></span>

<span data-ttu-id="b7799-131">`gw.config.json` - Il file di configurazione per personalizzare i moduli da caricare in Edge.</span><span class="sxs-lookup"><span data-stu-id="b7799-131">`gw.config.json` - The configuration file to customize the modules to be loaded by Edge.</span></span>

<span data-ttu-id="b7799-132">`package.json` - Le informazioni sui metadati per il progetto del modulo.</span><span class="sxs-lookup"><span data-stu-id="b7799-132">`package.json` - The metadata information for module project.</span></span>

<span data-ttu-id="b7799-133">`README.md` - La documentazione di base per il progetto del modulo.</span><span class="sxs-lookup"><span data-stu-id="b7799-133">`README.md` - The basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="b7799-134">File del pacchetto</span><span class="sxs-lookup"><span data-stu-id="b7799-134">Package file</span></span>

<span data-ttu-id="b7799-135">Il file `package.json` dichiara tutte le informazioni sui metadati necessarie a un progetto di modulo, tra cui il nome, la versione, la voce, gli script, il runtime e le dipendenze di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="b7799-135">This `package.json` declares all the metadata information needed by a module project that includes the name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="b7799-136">Il frammento di codice seguente mostra come preparare la configurazione per il progetto di esempio del convertitore BLE.</span><span class="sxs-lookup"><span data-stu-id="b7799-136">Following code snippet shows how to configure for BLE converter sample project.</span></span>
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a><span data-ttu-id="b7799-137">File di voce</span><span class="sxs-lookup"><span data-stu-id="b7799-137">Entry file</span></span>
<span data-ttu-id="b7799-138">Il file `app.js` definisce il modo per inizializzare l'istanza di Edge.</span><span class="sxs-lookup"><span data-stu-id="b7799-138">The `app.js` defines the way to initialize the edge instance.</span></span> <span data-ttu-id="b7799-139">In questo caso non sono necessarie modifiche.</span><span class="sxs-lookup"><span data-stu-id="b7799-139">Here we don't need to make any change.</span></span>

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a><span data-ttu-id="b7799-140">Interfaccia del modulo</span><span class="sxs-lookup"><span data-stu-id="b7799-140">Interface of module</span></span>
<span data-ttu-id="b7799-141">È possibile gestire il modulo Azure IoT Edge come elaboratore di dati il cui compito è di ricevere l'input, elaborarlo e produrre l'output.</span><span class="sxs-lookup"><span data-stu-id="b7799-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="b7799-142">L'input potrebbe essere costituito da dati dell'hardware (ad esempio un rilevatore di movimento), un messaggio da altri moduli o qualsiasi altra informazione (ad esempio un numero casuale generato periodicamente da un timer).</span><span class="sxs-lookup"><span data-stu-id="b7799-142">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="b7799-143">L'output è simile all'input. Può attivare il comportamento dell'hardware, ad esempio il lampeggiamento di un LED, generare un messaggio ad altri moduli o qualsiasi altra azione, ad esempio la stampa nella console.</span><span class="sxs-lookup"><span data-stu-id="b7799-143">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="b7799-144">I moduli comunicano reciprocamente usando l'oggetto `message`.</span><span class="sxs-lookup"><span data-stu-id="b7799-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="b7799-145">Il **contenuto** di un oggetto `message` è una matrice di byte in grado di rappresentare qualsiasi tipo di dati che si preferisce.</span><span class="sxs-lookup"><span data-stu-id="b7799-145">The **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="b7799-146">In `message` sono presenti anche **proprietà** che rappresentano semplicemente il mapping stringa-a-stringa.</span><span class="sxs-lookup"><span data-stu-id="b7799-146">**Properties** are also available in the `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="b7799-147">Si può pensare alle **proprietà** come alle intestazioni in una richiesta HTTP o ai metadati di un file.</span><span class="sxs-lookup"><span data-stu-id="b7799-147">You may think of **properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="b7799-148">Per sviluppare un modulo Azure IoT Edge in JS, è necessario creare un nuovo oggetto modulo che implementa i metodi `receive()` necessari.</span><span class="sxs-lookup"><span data-stu-id="b7799-148">In order to develop an Azure IoT Edge module in JS, you need to create a new module object that implements the required methods `receive()`.</span></span> <span data-ttu-id="b7799-149">È anche possibile a questo punto implementare i metodi `create()` o `start()` o `destroy()` facoltativi.</span><span class="sxs-lookup"><span data-stu-id="b7799-149">At this point, you may also choose to implement the optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="b7799-150">Il frammento di codice seguente mostra lo scaffolding dell'oggetto modulo JS.</span><span class="sxs-lookup"><span data-stu-id="b7799-150">The following code snippet shows you the scaffolding of JS module object.</span></span>

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a><span data-ttu-id="b7799-151">Modulo convertitore</span><span class="sxs-lookup"><span data-stu-id="b7799-151">Converter module</span></span>
| <span data-ttu-id="b7799-152">Input</span><span class="sxs-lookup"><span data-stu-id="b7799-152">Input</span></span>                    | <span data-ttu-id="b7799-153">Processore</span><span class="sxs-lookup"><span data-stu-id="b7799-153">Processor</span></span>                              | <span data-ttu-id="b7799-154">Output</span><span class="sxs-lookup"><span data-stu-id="b7799-154">Output</span></span>                 | <span data-ttu-id="b7799-155">File di origine</span><span class="sxs-lookup"><span data-stu-id="b7799-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="b7799-156">Messaggio sui dati della temperatura</span><span class="sxs-lookup"><span data-stu-id="b7799-156">Temperature data message</span></span> | <span data-ttu-id="b7799-157">Analizza e crea un nuovo messaggio JSON</span><span class="sxs-lookup"><span data-stu-id="b7799-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="b7799-158">Messaggio JSON strutturato</span><span class="sxs-lookup"><span data-stu-id="b7799-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="b7799-159">Questo è un tipico modulo Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="b7799-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="b7799-160">Accetta messaggi sulla temperatura da altri moduli, ad esempio un modulo hardware o in questo caso il modulo BLE simulato. Normalizza quindi il messaggio sulla temperatura in un messaggio JSON strutturato, includendo l'aggiunta dell'ID di messaggio, l'impostazione della proprietà che indica se è necessario attivare l'avviso di temperatura e così via.</span><span class="sxs-lookup"><span data-stu-id="b7799-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize the messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read the content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish the new message to broker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="b7799-161">Modulo della stampante</span><span class="sxs-lookup"><span data-stu-id="b7799-161">Printer module</span></span>
| <span data-ttu-id="b7799-162">Input</span><span class="sxs-lookup"><span data-stu-id="b7799-162">Input</span></span>                          | <span data-ttu-id="b7799-163">Processore</span><span class="sxs-lookup"><span data-stu-id="b7799-163">Processor</span></span> | <span data-ttu-id="b7799-164">Output</span><span class="sxs-lookup"><span data-stu-id="b7799-164">Output</span></span>                     | <span data-ttu-id="b7799-165">File di origine</span><span class="sxs-lookup"><span data-stu-id="b7799-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="b7799-166">Qualsiasi messaggio da altri moduli</span><span class="sxs-lookup"><span data-stu-id="b7799-166">Any message from other modules</span></span> | <span data-ttu-id="b7799-167">N/D</span><span class="sxs-lookup"><span data-stu-id="b7799-167">N/A</span></span>       | <span data-ttu-id="b7799-168">Registra il messaggio nella console</span><span class="sxs-lookup"><span data-stu-id="b7799-168">Log the message to console</span></span> | `printer.js` |

<span data-ttu-id="b7799-169">Questo modulo semplice e di chiara interpretazione restituisce i messaggi ricevuti (proprietà, contenuto) alla finestra Terminal.</span><span class="sxs-lookup"><span data-stu-id="b7799-169">This module is simple, self-explanatory, which outputs the received messages(property, content) to the terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="b7799-170">Configurazione</span><span class="sxs-lookup"><span data-stu-id="b7799-170">Configuration</span></span>
<span data-ttu-id="b7799-171">Il passaggio finale prima di eseguire i moduli consiste nel configurare Azure IoT Edge e stabilire le connessioni tra i moduli.</span><span class="sxs-lookup"><span data-stu-id="b7799-171">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="b7799-172">Dal momento che Azure IoT Edge supporta caricatori di varie lingue, occorre prima dichiarare il caricatore `node` specifico, a cui si potrebbe fare riferimento in base al `name` nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="b7799-172">First we need to declare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="b7799-173">Dopo avere dichiarato i caricatori, è necessario dichiarare anche i moduli.</span><span class="sxs-lookup"><span data-stu-id="b7799-173">Once we have declared our loaders, we also need to declare our modules as well.</span></span> <span data-ttu-id="b7799-174">Come avviene nella dichiarazione dei caricatori, anche ai moduli è possibile fare riferimento tramite il relativo attributo `name`.</span><span class="sxs-lookup"><span data-stu-id="b7799-174">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="b7799-175">Quando si dichiara un modulo, è necessario specificare il caricatore che il modulo deve usare (che dovrebbe essere quello che è stato definito prima) e il punto di ingresso (che dovrebbe essere il nome della classe normalizzata del modulo) per ogni modulo.</span><span class="sxs-lookup"><span data-stu-id="b7799-175">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="b7799-176">Il modulo `simulated_device` è un modulo nativo che è incluso nel pacchetto di runtime principale di Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="b7799-176">The `simulated_device` module is a native module that is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="b7799-177">Includere `args` nel file JSON anche se è `null`.</span><span class="sxs-lookup"><span data-stu-id="b7799-177">Include `args` in the JSON file even if it is `null`.</span></span>

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
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="b7799-178">Al termine della configurazione occorre stabilire le connessioni.</span><span class="sxs-lookup"><span data-stu-id="b7799-178">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="b7799-179">Ogni connessione è espressa da `source` e `sink`.</span><span class="sxs-lookup"><span data-stu-id="b7799-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="b7799-180">Entrambi devono fare riferimento a un modulo predefinito.</span><span class="sxs-lookup"><span data-stu-id="b7799-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="b7799-181">Il messaggio di output del modulo `source` viene inoltrato all'input del modulo `sink`.</span><span class="sxs-lookup"><span data-stu-id="b7799-181">The output message of `source` module is forwarded to the input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-the-modules"></a><span data-ttu-id="b7799-182">Esecuzione dei moduli</span><span class="sxs-lookup"><span data-stu-id="b7799-182">Running the modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="b7799-183">Se si intende terminare l'applicazione premere `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="b7799-183">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7799-184">Non è consigliabile usare Ctrl + C per terminare l'applicazione IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b7799-184">It is not recommended to use Ctrl + C to terminate the IoT Edge application.</span></span> <span data-ttu-id="b7799-185">in quanto questa azione può determinare un arresto anomalo del processo.</span><span class="sxs-lookup"><span data-stu-id="b7799-185">As this way may cause the process to terminate abnormally.</span></span>
