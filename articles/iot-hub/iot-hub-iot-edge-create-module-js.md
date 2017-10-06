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
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a>Creare un modulo Azure IoT Edge con Node.js

In questa esercitazione illustra come toocreate un modulo per Azure IoT Edge in JS.

In questa esercitazione vengono illustrate le impostazione dell'ambiente e come toowrite un [BILITA](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) modulo convertitore di tipi di dati utilizzando pacchetti Azure IoT Edge NPM più recenti hello.

## <a name="prerequisites"></a>Prerequisiti

In questa sezione si configura l'ambiente per lo sviluppo del modulo IoT Edge. Si applica tooboth *Windows a 64 bit* e *Linux a 64 bit (Ubuntu + 14)* sistemi operativi.

Hello seguente software è necessario:
* [Client Git](https://git-scm.com/downloads).
* [Nodo LTS](https://nodejs.org).
* `npm install -g yo`.
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a>Architettura

piattaforma Azure IoT Edge Hello adotta frequentemente hello [architettura Neumann Von](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Ovvero l'architettura di Azure IoT bordo intero hello è un sistema che elabora l'input e produce l'output. e che ogni singolo modulo sia anche un piccolo sottosistema di input / output. In questa esercitazione, si introduce hello due moduli seguenti:

1. Un modulo che riceve un segnale [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulato e lo converte in un messaggio [JSON](https://en.wikipedia.org/wiki/JSON) formattato.
2. Un modulo che stampa hello ricevuto [JSON](https://en.wikipedia.org/wiki/JSON) messaggio.

Hello seguente immagine Mostra hello fine tipico tooend un flusso di dati per questo progetto:

![Flusso di dati tra tre moduli](media/iot-hub-iot-edge-create-module/dataflow.png "Input: modulo BLE simulato; Processore: modulo convertitore; Output: modulo stampante")

## <a name="set-up-hello-environment"></a>Configurare un ambiente di hello
Di seguito viene illustrata la modalità tooquickly impostare ambiente toostart toowrite il primo modulo convertitore BILITA con JS.

### <a name="create-module-project"></a>Creare un progetto di modulo
1. Aprire la finestra della riga di comando ed eseguire `yo az-iot-gw-module`.
2. Seguire i passaggi di hello in hello schermata toofinish hello l'inizializzazione del progetto del modulo.

### <a name="project-structure"></a>Struttura progetto
Un progetto di modulo JS è costituito da hello seguenti componenti:

`modules`-hello personalizzata i file di origine JS modulo. Sostituire l'impostazione predefinita hello `sensor.js` e `printer.js` con i propri file di modulo.

`app.js`-istanza di hello voce file toostart hello Edge.

`gw.config.json`-toobe di hello configurazione file toocustomize hello moduli caricati dal bordo.

`package.json`-hello informazioni sui metadati per il progetto di modulo.

`README.md`-hello documentazione di base per il progetto di modulo.


### <a name="package-file"></a>File del pacchetto

Questo `package.json` dichiara tutte le informazioni dei metadati hello necessarie per un progetto di modulo che include le dipendenze di nome, versione, voce, script, runtime e sviluppo hello.

Seguente frammento di codice viene illustrato come tooconfigure per convertitore disattiva il progetto di esempio.
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


### <a name="entry-file"></a>File di voce
Hello `app.js` definisce hello modo tooinitialize hello edge istanza. In questo caso non è necessario toomake qualsiasi modifica.

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

### <a name="interface-of-module"></a>Interfaccia del modulo
È possibile gestire il modulo Azure IoT Edge come elaboratore di dati il cui compito è di ricevere l'input, elaborarlo e produrre l'output.

Hello input potrebbe essere dati dall'hardware (ad esempio un rilevatore di movimento), un messaggio da altri moduli, o qualsiasi altro (ad esempio, un numero casuale generato periodicamente da un timer).

output di Hello input toohello simile, potrebbe attivare il comportamento di hardware (ad esempio hello LED lampeggiante), i moduli tooother un messaggio o a qualsiasi altro (ad esempio stampa toohello console).

I moduli comunicano reciprocamente usando l'oggetto `message`. Hello **contenuto** di un `message` è una matrice di byte che è in grado di rappresentare qualsiasi tipo di dati desiderato. **Proprietà** sono disponibili anche in hello `message` e sono semplicemente un mapping da stringa-stringa. È possibile pensare **proprietà** come intestazioni hello in una richiesta HTTP o hello metadati di un file.

In un modulo di Azure IoT Edge in JS toodevelop di ordine, è necessario un nuovo oggetto modulo che implementa i metodi necessario hello toocreate `receive()`. A questo punto, è inoltre possibile scegliere hello tooimplement facoltativo `create()` o `start()`, o `destroy()` anche i metodi. Hello frammento di codice seguente viene illustrato come che Hello lo scaffolding dell'oggetto modulo JS.

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

### <a name="converter-module"></a>Modulo convertitore
| Input                    | Processore                              | Output                 | File di origine            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Messaggio sui dati della temperatura | Analizza e crea un nuovo messaggio JSON | Messaggio JSON strutturato | `converter.js` |

Questo è un tipico modulo Azure IoT Edge. Accetta messaggi temperatura da altri moduli (modulo di hardware, o in questo caso, il modulo BILITA simulato); e quindi Normalizza il messaggio di temperatura hello nel messaggio JSON tooa strutturata (inclusi aggiungendo l'ID del messaggio hello, impostazione proprietà hello di se occorre avviso temperatura tootrigger hello e così via).

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

### <a name="printer-module"></a>Modulo della stampante
| Input                          | Processore | Output                     | File di origine          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Qualsiasi messaggio da altri moduli | N/D       | Log tooconsole messaggio hello | `printer.js` |

Questo modulo è semplice e chiara interpretazione, che restituisce una finestra terminale toohello di hello ricevuto messaggi (proprietà, contenuto).

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a>Configurazione
passaggio finale di Hello prima di eseguire i moduli di hello è tooconfigure hello Azure IoT Edge e connessioni di hello tooestablish tra i moduli.

È prima necessario toodeclare nostri `node` caricatore (dal bordo IoT di Azure supporta caricatori di lingue diverse) che può fare riferimento relativo `name` nelle sezioni hello in seguito.

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

Una volta che è stato dichiarato il nostro caricatori, è anche necessario toodeclare anche i moduli. Caricatori di hello toodeclaring simili, è possibile inoltre farvi riferimento dal loro `name` attributo. Quando si dichiara un modulo, è necessario caricatore hello toospecify deve utilizzare (che deve essere hello uno è stato definito prima) e hello punto di ingresso (il nome della classe normalizzato hello del nostro modulo deve essere) per ogni modulo. Hello `simulated_device` è un modulo nativo incluso nel pacchetto di runtime di hello Azure IoT Edge core. Includere `args` nel file JSON, anche se hello `null`.

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

Alla fine di hello della configurazione di hello, è stabilire le connessioni di hello. Ogni connessione è espressa da `source` e `sink`. Entrambi devono fare riferimento a un modulo predefinito. messaggio di output di Hello di `source` modulo viene inoltrato input toohello di `sink` modulo.

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

## <a name="running-hello-modules"></a>Moduli di hello in esecuzione
1. `npm install`
2. `npm start`

Se si desidera un'applicazione hello tooterminate, premere `<Enter>` chiave.

> [!IMPORTANT]
> Non è consigliabile toouse Ctrl + C tooterminate hello IoT bordo dell'applicazione. In questo modo può causare tooterminate processo hello in modo anomalo.
