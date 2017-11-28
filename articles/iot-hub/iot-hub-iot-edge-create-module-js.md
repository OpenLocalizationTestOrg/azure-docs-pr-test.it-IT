---
title: un modulo di Edge IoT di Azure con Node.js aaaCreate | Documenti Microsoft
description: "In questa esercitazione illustra come una tabella dati convertitore modulo utilizzando toowrite hello pacchetti Azure IoT Edge NPM più recenti e Yeoman generatore."
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
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="1333f-103">Creare un modulo Azure IoT Edge con Node.js</span><span class="sxs-lookup"><span data-stu-id="1333f-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="1333f-104">In questa esercitazione illustra come toocreate un modulo per Azure IoT Edge in JS.</span><span class="sxs-lookup"><span data-stu-id="1333f-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="1333f-105">In questa esercitazione vengono illustrate le impostazione dell'ambiente e come toowrite un [BILITA](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) modulo convertitore di tipi di dati utilizzando pacchetti Azure IoT Edge NPM più recenti hello.</span><span class="sxs-lookup"><span data-stu-id="1333f-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1333f-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1333f-106">Prerequisites</span></span>

<span data-ttu-id="1333f-107">In questa sezione si configura l'ambiente per lo sviluppo del modulo IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="1333f-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="1333f-108">Si applica tooboth *Windows a 64 bit* e *Linux a 64 bit (Ubuntu + 14)* sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="1333f-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="1333f-109">Hello seguente software è necessario:</span><span class="sxs-lookup"><span data-stu-id="1333f-109">hello following software is required:</span></span>
* <span data-ttu-id="1333f-110">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="1333f-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="1333f-111">[Nodo LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="1333f-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="1333f-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="1333f-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="1333f-113">Architettura</span><span class="sxs-lookup"><span data-stu-id="1333f-113">Architecture</span></span>

<span data-ttu-id="1333f-114">piattaforma Azure IoT Edge Hello adotta frequentemente hello [architettura Neumann Von](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="1333f-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="1333f-115">Ovvero l'architettura di Azure IoT bordo intero hello è un sistema che elabora l'input e produce l'output. e che ogni singolo modulo sia anche un piccolo sottosistema di input / output.</span><span class="sxs-lookup"><span data-stu-id="1333f-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="1333f-116">In questa esercitazione, si introduce hello due moduli seguenti:</span><span class="sxs-lookup"><span data-stu-id="1333f-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="1333f-117">Un modulo che riceve un segnale [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulato e lo converte in un messaggio [JSON](https://en.wikipedia.org/wiki/JSON) formattato.</span><span class="sxs-lookup"><span data-stu-id="1333f-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="1333f-118">Un modulo che stampa hello ricevuto [JSON](https://en.wikipedia.org/wiki/JSON) messaggio.</span><span class="sxs-lookup"><span data-stu-id="1333f-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="1333f-119">Hello seguente immagine Mostra hello fine tipico tooend un flusso di dati per questo progetto:</span><span class="sxs-lookup"><span data-stu-id="1333f-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="1333f-120">![Flusso di dati tra tre moduli](media/iot-hub-iot-edge-create-module/dataflow.png "Input: modulo BLE simulato; Processore: modulo convertitore; Output: modulo stampante")</span><span class="sxs-lookup"><span data-stu-id="1333f-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="1333f-121">Configurare un ambiente di hello</span><span class="sxs-lookup"><span data-stu-id="1333f-121">Set up hello environment</span></span>
<span data-ttu-id="1333f-122">Di seguito viene illustrata la modalità tooquickly impostare ambiente toostart toowrite il primo modulo convertitore BILITA con JS.</span><span class="sxs-lookup"><span data-stu-id="1333f-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="1333f-123">Creare un progetto di modulo</span><span class="sxs-lookup"><span data-stu-id="1333f-123">Create module project</span></span>
1. <span data-ttu-id="1333f-124">Aprire la finestra della riga di comando ed eseguire `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="1333f-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="1333f-125">Seguire i passaggi di hello in hello schermata toofinish hello l'inizializzazione del progetto del modulo.</span><span class="sxs-lookup"><span data-stu-id="1333f-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="1333f-126">Struttura progetto</span><span class="sxs-lookup"><span data-stu-id="1333f-126">Project structure</span></span>
<span data-ttu-id="1333f-127">Un progetto di modulo JS è costituito da hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="1333f-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="1333f-128">`modules`-hello personalizzata i file di origine JS modulo.</span><span class="sxs-lookup"><span data-stu-id="1333f-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="1333f-129">Sostituire l'impostazione predefinita hello `sensor.js` e `printer.js` con i propri file di modulo.</span><span class="sxs-lookup"><span data-stu-id="1333f-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="1333f-130">`app.js`-istanza di hello voce file toostart hello Edge.</span><span class="sxs-lookup"><span data-stu-id="1333f-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="1333f-131">`gw.config.json`-toobe di hello configurazione file toocustomize hello moduli caricati dal bordo.</span><span class="sxs-lookup"><span data-stu-id="1333f-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="1333f-132">`package.json`-hello informazioni sui metadati per il progetto di modulo.</span><span class="sxs-lookup"><span data-stu-id="1333f-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="1333f-133">`README.md`-hello documentazione di base per il progetto di modulo.</span><span class="sxs-lookup"><span data-stu-id="1333f-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="1333f-134">File del pacchetto</span><span class="sxs-lookup"><span data-stu-id="1333f-134">Package file</span></span>

<span data-ttu-id="1333f-135">Questo `package.json` dichiara tutte le informazioni dei metadati hello necessarie per un progetto di modulo che include le dipendenze di nome, versione, voce, script, runtime e sviluppo hello.</span><span class="sxs-lookup"><span data-stu-id="1333f-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="1333f-136">Seguente frammento di codice viene illustrato come tooconfigure per convertitore disattiva il progetto di esempio.</span><span class="sxs-lookup"><span data-stu-id="1333f-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="1333f-137">File di voce</span><span class="sxs-lookup"><span data-stu-id="1333f-137">Entry file</span></span>
<span data-ttu-id="1333f-138">Hello `app.js` definisce hello modo tooinitialize hello edge istanza.</span><span class="sxs-lookup"><span data-stu-id="1333f-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="1333f-139">In questo caso non è necessario toomake qualsiasi modifica.</span><span class="sxs-lookup"><span data-stu-id="1333f-139">Here we don't need toomake any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="1333f-140">Interfaccia del modulo</span><span class="sxs-lookup"><span data-stu-id="1333f-140">Interface of module</span></span>
<span data-ttu-id="1333f-141">È possibile gestire il modulo Azure IoT Edge come elaboratore di dati il cui compito è di ricevere l'input, elaborarlo e produrre l'output.</span><span class="sxs-lookup"><span data-stu-id="1333f-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="1333f-142">Hello input potrebbe essere dati dall'hardware (ad esempio un rilevatore di movimento), un messaggio da altri moduli, o qualsiasi altro (ad esempio, un numero casuale generato periodicamente da un timer).</span><span class="sxs-lookup"><span data-stu-id="1333f-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="1333f-143">output di Hello input toohello simile, potrebbe attivare il comportamento di hardware (ad esempio hello LED lampeggiante), i moduli tooother un messaggio o a qualsiasi altro (ad esempio stampa toohello console).</span><span class="sxs-lookup"><span data-stu-id="1333f-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="1333f-144">I moduli comunicano reciprocamente usando l'oggetto `message`.</span><span class="sxs-lookup"><span data-stu-id="1333f-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="1333f-145">Hello **contenuto** di un `message` è una matrice di byte che è in grado di rappresentare qualsiasi tipo di dati desiderato.</span><span class="sxs-lookup"><span data-stu-id="1333f-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="1333f-146">**Proprietà** sono disponibili anche in hello `message` e sono semplicemente un mapping da stringa-stringa.</span><span class="sxs-lookup"><span data-stu-id="1333f-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="1333f-147">È possibile pensare **proprietà** come intestazioni hello in una richiesta HTTP o hello metadati di un file.</span><span class="sxs-lookup"><span data-stu-id="1333f-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="1333f-148">In un modulo di Azure IoT Edge in JS toodevelop di ordine, è necessario un nuovo oggetto modulo che implementa i metodi necessario hello toocreate `receive()`.</span><span class="sxs-lookup"><span data-stu-id="1333f-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="1333f-149">A questo punto, è inoltre possibile scegliere hello tooimplement facoltativo `create()` o `start()`, o `destroy()` anche i metodi.</span><span class="sxs-lookup"><span data-stu-id="1333f-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="1333f-150">Hello frammento di codice seguente viene illustrato come che Hello lo scaffolding dell'oggetto modulo JS.</span><span class="sxs-lookup"><span data-stu-id="1333f-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="1333f-151">Modulo convertitore</span><span class="sxs-lookup"><span data-stu-id="1333f-151">Converter module</span></span>
| <span data-ttu-id="1333f-152">Input</span><span class="sxs-lookup"><span data-stu-id="1333f-152">Input</span></span>                    | <span data-ttu-id="1333f-153">Processore</span><span class="sxs-lookup"><span data-stu-id="1333f-153">Processor</span></span>                              | <span data-ttu-id="1333f-154">Output</span><span class="sxs-lookup"><span data-stu-id="1333f-154">Output</span></span>                 | <span data-ttu-id="1333f-155">File di origine</span><span class="sxs-lookup"><span data-stu-id="1333f-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="1333f-156">Messaggio sui dati della temperatura</span><span class="sxs-lookup"><span data-stu-id="1333f-156">Temperature data message</span></span> | <span data-ttu-id="1333f-157">Analizza e crea un nuovo messaggio JSON</span><span class="sxs-lookup"><span data-stu-id="1333f-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="1333f-158">Messaggio JSON strutturato</span><span class="sxs-lookup"><span data-stu-id="1333f-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="1333f-159">Questo è un tipico modulo Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="1333f-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="1333f-160">Accetta messaggi temperatura da altri moduli (modulo di hardware, o in questo caso, il modulo BILITA simulato); e quindi Normalizza il messaggio di temperatura hello nel messaggio JSON tooa strutturata (inclusi aggiungendo l'ID del messaggio hello, impostazione proprietà hello di se occorre avviso temperatura tootrigger hello e così via).</span><span class="sxs-lookup"><span data-stu-id="1333f-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
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

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="1333f-161">Modulo della stampante</span><span class="sxs-lookup"><span data-stu-id="1333f-161">Printer module</span></span>
| <span data-ttu-id="1333f-162">Input</span><span class="sxs-lookup"><span data-stu-id="1333f-162">Input</span></span>                          | <span data-ttu-id="1333f-163">Processore</span><span class="sxs-lookup"><span data-stu-id="1333f-163">Processor</span></span> | <span data-ttu-id="1333f-164">Output</span><span class="sxs-lookup"><span data-stu-id="1333f-164">Output</span></span>                     | <span data-ttu-id="1333f-165">File di origine</span><span class="sxs-lookup"><span data-stu-id="1333f-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="1333f-166">Qualsiasi messaggio da altri moduli</span><span class="sxs-lookup"><span data-stu-id="1333f-166">Any message from other modules</span></span> | <span data-ttu-id="1333f-167">N/D</span><span class="sxs-lookup"><span data-stu-id="1333f-167">N/A</span></span>       | <span data-ttu-id="1333f-168">Log tooconsole messaggio hello</span><span class="sxs-lookup"><span data-stu-id="1333f-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="1333f-169">Questo modulo è semplice e chiara interpretazione, che restituisce una finestra terminale toohello di hello ricevuto messaggi (proprietà, contenuto).</span><span class="sxs-lookup"><span data-stu-id="1333f-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="1333f-170">Configurazione</span><span class="sxs-lookup"><span data-stu-id="1333f-170">Configuration</span></span>
<span data-ttu-id="1333f-171">passaggio finale di Hello prima di eseguire i moduli di hello è tooconfigure hello Azure IoT Edge e connessioni di hello tooestablish tra i moduli.</span><span class="sxs-lookup"><span data-stu-id="1333f-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="1333f-172">È prima necessario toodeclare nostri `node` caricatore (dal bordo IoT di Azure supporta caricatori di lingue diverse) che può fare riferimento relativo `name` nelle sezioni hello in seguito.</span><span class="sxs-lookup"><span data-stu-id="1333f-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="1333f-173">Una volta che è stato dichiarato il nostro caricatori, è anche necessario toodeclare anche i moduli.</span><span class="sxs-lookup"><span data-stu-id="1333f-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="1333f-174">Caricatori di hello toodeclaring simili, è possibile inoltre farvi riferimento dal loro `name` attributo.</span><span class="sxs-lookup"><span data-stu-id="1333f-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="1333f-175">Quando si dichiara un modulo, è necessario caricatore hello toospecify deve utilizzare (che deve essere hello uno è stato definito prima) e hello punto di ingresso (il nome della classe normalizzato hello del nostro modulo deve essere) per ogni modulo.</span><span class="sxs-lookup"><span data-stu-id="1333f-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="1333f-176">Hello `simulated_device` è un modulo nativo incluso nel pacchetto di runtime di hello Azure IoT Edge core.</span><span class="sxs-lookup"><span data-stu-id="1333f-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="1333f-177">Includere `args` nel file JSON, anche se hello `null`.</span><span class="sxs-lookup"><span data-stu-id="1333f-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="1333f-178">Alla fine di hello della configurazione di hello, è stabilire le connessioni di hello.</span><span class="sxs-lookup"><span data-stu-id="1333f-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="1333f-179">Ogni connessione è espressa da `source` e `sink`.</span><span class="sxs-lookup"><span data-stu-id="1333f-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="1333f-180">Entrambi devono fare riferimento a un modulo predefinito.</span><span class="sxs-lookup"><span data-stu-id="1333f-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="1333f-181">messaggio di output di Hello di `source` modulo viene inoltrato input toohello di `sink` modulo.</span><span class="sxs-lookup"><span data-stu-id="1333f-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="1333f-182">Moduli di hello in esecuzione</span><span class="sxs-lookup"><span data-stu-id="1333f-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="1333f-183">Se si desidera un'applicazione hello tooterminate, premere `<Enter>` chiave.</span><span class="sxs-lookup"><span data-stu-id="1333f-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1333f-184">Non è consigliabile toouse Ctrl + C tooterminate hello IoT bordo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1333f-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="1333f-185">In questo modo può causare tooterminate processo hello in modo anomalo.</span><span class="sxs-lookup"><span data-stu-id="1333f-185">As this way may cause hello process tooterminate abnormally.</span></span>
