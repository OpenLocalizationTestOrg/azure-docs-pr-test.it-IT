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
# <a name="create-an-azure-iot-edge-module-with-java"></a>Creare un modulo Azure IoT Edge con Java

Questa esercitazione illustra come è possibile creare un modulo per Azure IoT Edge in Java.

In questa esercitazione, si verrà illustrata l'impostazione dell'ambiente e come toowrite un [BILITA](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) modulo convertitore di tipi di dati utilizzando pacchetti Azure IoT Edge Maven più recenti di hello.

## <a name="prerequisites"></a>Prerequisiti

In questa sezione si configurerà l'ambiente per lo sviluppo del modulo IoT Edge. Si applica tooboth *Windows a 64 bit* e *Linux a 64 bit (8 Ubuntu/Debian)* i sistemi operativi.

Hello seguente software è necessario:

* [Client Git](https://git-scm.com/downloads).
* [**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* [Maven](https://maven.apache.org/install.html).

Aprire della riga di comando terminal finestra e clone hello seguenti repository:

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>Architettura complessiva

piattaforma Azure IoT Edge Hello adotta frequentemente hello [architettura Neumann Von](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Ovvero l'architettura di Azure IoT bordo intero hello è un sistema che elabora l'input e produce l'output. e che ogni singolo modulo sia anche un piccolo sottosistema di input / output. In questa esercitazione verrà illustrata hello due moduli seguenti:

1. Un modulo che riceve un segnale [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulato e lo converte in un messaggio [JSON](https://en.wikipedia.org/wiki/JSON) formattato.
2. Un modulo che consente di stampare hello ricevuto [JSON](https://en.wikipedia.org/wiki/JSON) messaggio.

Hello seguente immagine Mostra hello tipico end-to-end del flusso di dati per questo progetto:

![Flusso di dati tra tre moduli](media/iot-hub-iot-edge-create-module/dataflow.png "Input: modulo BLE simulato; Processore: modulo convertitore; Output: modulo stampante")

## <a name="understanding-hello-code"></a>Informazioni sul codice hello

### <a name="maven-project-structure"></a>Struttura di progetto Maven

Poiché i pacchetti di Azure IoT Edge sono basati su Maven, dobbiamo toocreate una struttura di progetto Maven tipica, che contiene un `pom.xml` file.

Hello POM eredita hello `com.microsoft.azure.gateway.gateway-module-base` pacchetto, che consente di dichiarare tutte le dipendenze di hello necessarie per un progetto di modulo che include i file binari di runtime hello, percorso di file di configurazione di gateway hello e il comportamento di esecuzione hello. Ciò ci consente di risparmiare molto tempo ed eliminare toowrite necessità hello e riscrivere ripetutamente centinaia di righe di codice.

È necessario il file pom.xml tooupdate dichiarando hello necessarie dipendenze/plug-in e il nome di hello di hello toobe di file di configurazione utilizzato da questo modulo come illustrato nel seguente frammento di codice hello.

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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Conoscenza di base di un modulo Azure IoT Edge

È possibile gestire il modulo Azure IoT Edge come elaboratore di dati il cui compito è di ricevere l'input, elaborarlo e produrre l'output.

Hello input potrebbe essere dati dall'hardware (ad esempio un rilevatore di movimento), un messaggio da altri moduli, o qualsiasi altro (ad esempio, un numero casuale generato periodicamente da un timer).

output di Hello input toohello simile, potrebbe attivare il comportamento di hardware (ad esempio hello LED lampeggiante), i moduli tooother un messaggio o a qualsiasi altro (ad esempio stampa toohello console).

I moduli comunicano reciprocamente usando la classe `com.microsoft.azure.gateway.messaging.Message`. Hello **contenuto** di un `Message` è una matrice di byte che è in grado di rappresentare qualsiasi tipo di dati desiderato. **Proprietà** sono disponibili anche in hello `Message` e sono semplicemente un mapping da stringa-stringa. È possibile pensare **proprietà** come intestazioni hello in una richiesta HTTP o hello metadati di un file.

In ordine toodevelop un modulo di Azure IoT Edge in Java, è necessario toocreate una nuova classe di modulo che eredita da `com.microsoft.azure.gateway.core.GatewayModule` e implementare i metodi astratti necessario hello `receive()` e `destroy()`. A questo punto, è inoltre possibile scegliere hello tooimplement facoltativo `start()` o `create()` anche i metodi. Hello frammento di codice seguente viene illustrato come tooget iniziare la creazione di un modulo di Azure IoT Edge.

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

### <a name="converter-module"></a>Modulo convertitore

| Input                    | Processore                              | Output                 | File di origine            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Messaggio sui dati della temperatura | Analizza e crea un nuovo messaggio JSON | Messaggio JSON strutturato | `ConverterModule.java` |

Questo è un tipico modulo Azure IoT Edge. Accetta messaggi temperatura da altri moduli (modulo di hardware, o in questo caso, il modulo BILITA simulato); e quindi Normalizza il messaggio di temperatura hello nel messaggio JSON tooa strutturata (inclusi aggiungendo l'ID del messaggio hello, impostazione proprietà hello di se occorre avviso temperatura tootrigger hello e così via).

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

### <a name="printer-module"></a>Modulo della stampante

| Input                          | Processore | Output                     | File di origine          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Qualsiasi messaggio da altri moduli | N/D       | Log tooconsole messaggio hello | `PrinterModule.java` |

Si tratta di un modulo semplice e chiara interpretazione, che restituisce una finestra terminale toohello di messaggi hello ricevuto.

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Configurazione di Azure IoT Edge

passaggio finale di Hello prima di eseguire i moduli di hello è tooconfigure hello Azure IoT Edge e connessioni di hello tooestablish tra i moduli.

È prima necessario toodeclare il caricatore di Java (dal bordo IoT di Azure supporta caricatori di lingue diverse) che può fare riferimento relativo `name` nelle sezioni hello in seguito.

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

Una volta che è stato dichiarato il nostro caricatori, è anche necessario toodeclare anche i moduli. Caricatori di hello toodeclaring simili, è possibile inoltre farvi riferimento dal loro `name` attributo. Quando si dichiara un modulo, è necessario caricatore hello toospecify deve utilizzare (che deve essere hello uno è stato definito prima) e hello punto di ingresso (il nome della classe normalizzato hello del nostro modulo deve essere) per ogni modulo. Hello `simulated_device` è un modulo nativo incluso nel pacchetto di runtime di hello Azure IoT Edge core. È necessario includere sempre `args` nel file JSON, anche se hello `null`.

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

Alla fine di hello della configurazione di hello, è stabilire le connessioni di hello. Ogni connessione è espressa da `source` e `sink`. Entrambi devono fare riferimento a un modulo predefinito. messaggio di output di Hello di `source` modulo verrà inoltrato input toohello di `sink` modulo.

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

## <a name="running-hello-modules"></a>Moduli di hello in esecuzione

Utilizzare `mvn package` toobuild tutti gli elementi in hello `target/` cartella. Per eseguire una compilazione pulita, è consigliato anche `mvn clean package`.

Utilizzare `mvn exec:exec` toorun hello Azure IoT Edge e deve rispettare che i dati di temperatura hello e tutte le proprietà di hello siano toohello stampato console a un corrispettivo fisso.

Se si desidera un'applicazione hello tooterminate, premere `<Enter>` chiave.

> [!IMPORTANT]
> Non è consigliabile toouse Ctrl + C tooterminate hello IoT Edge applicazioni gateway. Come potrebbe tooterminate processo hello in modo anomalo.

