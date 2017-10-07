---
title: aaaCreate il primo modulo Azure IoT Gateway | Documenti Microsoft
description: Creare un modulo e aggiungerlo tooa esempio app toocustomize modulo comportamenti.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Lezione 5: creare il primo modulo di Azure IoT Gateway
Mentre Azure IoT Edge consente moduli toobuild scritti in Node.js, Java o .NET, questa esercitazione illustra hello passaggi per la creazione di un modulo in C.

## <a name="what-you-will-do"></a>Contenuto dell'esercitazione

- Compilare ed eseguire app di esempio hello_world hello in NUC Intel.
- Creare un modulo e compilarlo in Intel NUC.
- Aggiungere hello nuovo modulo toohello hello_world esempio app e quindi eseguire l'esempio hello in NUC Intel. il nuovo modulo Hello stampa i messaggi "hello_world" con un timestamp.

## <a name="what-you-will-learn"></a>Contenuto dell'esercitazione

- Come toocompile ed eseguire un'app di esempio in NUC Intel.
- Come toocreate un modulo.
- App di esempio come tooadd modulo tooa.

## <a name="what-you-need"></a>Elementi necessari

Azure IoT Edge installato nel computer host.

## <a name="folder-structure"></a>Struttura di cartelle

In una sottocartella hello lezione 5 hello del codice di esempio che è stato clonato nella lezione 1, è presente un `module` cartella e un `sample` cartella.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- Hello `module/my_module` cartella contiene hello codice e script toobuild hello modulo di origine.
- Hello `sample` cartella contiene hello origine codice e script toobuild hello app di esempio.

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>Compilare ed eseguire app di esempio hello_world hello in NUC Intel

Hello `hello_world` esempio crea un gateway in base a hello `hello_world.json` file specifica hello due moduli predefiniti associati a hello app. gateway Hello registra un file di tooa messaggio "hello world" ogni 5 secondi. In questa sezione, compilare ed eseguire hello `hello_world` app con il modulo predefinito.

hello toocompile ed eseguire `hello_world` app, seguire questi passaggi nel computer host:

1. Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Aggiornare i file di configurazione di gateway di hello con indirizzo MAC di Intel NUC hello. Ignorare questo passaggio se già stata consultata troppo lezione hello[configurare ed eseguire un'applicazione di esempio BILITA][config_ble].

   1. Aprire il file di configurazione di gateway hello eseguendo hello comando seguente:

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. Di indirizzi MAC del gateway hello aggiornamento quando si [impostare NUC Intel come gateway IoT][setup_nuc]e quindi salvare il file hello.

1. Compilare codice sorgente dell'esempio hello eseguendo hello comando seguente:

   ```bash
   gulp compile
   ```

   Trasferisce hello esempio origine codice tooIntel NUC Hello comando ed esegue `build.sh` toocompile è.

1. Eseguire hello `hello_world` app su Intel NUC eseguendo hello comando seguente:

   ```bash
   gulp run
   ```

   esecuzione del comando Hello `../Tools/run-hello-world.js` specificata nei `config.json` toostart app di esempio hello in NUC Intel.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Creare un nuovo modulo e compilarlo in Intel NUC

passaggi Hello riportati di seguito è illustrata la creazione di un nuovo modulo e compilarlo nella NUC Intel. modulo Hello stampa i messaggi con un timestamp alla ricezione di essi. In questa sezione è possibile creare il primo modulo di gateway personalizzato.

Qualsiasi modulo di Azure IoT bordo deve implementare hello seguenti interfacce:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

Facoltativamente, è possibile implementare hello seguente interfaccia:

   ```C
   pfModule_Start Module_Start
   ```

Hello diagramma seguente mostra i percorsi di hello importanti dello stato di un modulo. rettangoli quadrato Hello rappresentano i metodi implementare le operazioni di tooperform quando si sposta il modulo hello tra stati. ovali Hello sono stati principali hello modulo può essere in.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Ora si crea un modulo basato sul modello hello:

1. Aprire una cartella del modello di hello eseguendo hello comando seguente:

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`funge da un modello che facilita la creazione di hello di un modulo. modello Hello dichiara interfacce hello. È sufficiente toodo tooadd logica toohello `MyModule_Receive` (funzione).
   - `build.sh`è hello compilazione toocompile hello modulo di script in NUC Intel.
1. Aprire hello `src/my_module.c` include due file di intestazione e di file:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Aggiungere i seguenti toohello codice hello `MyModule_Receive` funzione:

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. Hello aggiornamento `config.json` hello toospecify file `workspace` cartella al percorso di distribuzione hello e computer host su NUC Intel. Durante la compilazione, hello file hello `workspace` cartella saranno trasferiti toohello il percorso di distribuzione.

   1. Aprire hello `config.json` file eseguendo hello comando seguente:

      ```bash
      code config.json
      ```

   1. Aggiornamento `config.json` con hello seguente configurazione:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Compilare il modulo hello eseguendo hello comando seguente:

   ```bash
   gulp compile
   ```

   Trasferisce hello origine codice tooIntel NUC Hello comando ed esegue `build.sh` modulo hello toocompile.

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>Aggiungere app di esempio hello modulo toohello hello_world ed eseguire app di hello in NUC Intel

tooperform questa attività, seguire questi passaggi:

1. Elencare tutti i file binari del modulo disponibile hello (file con estensione SO) su Intel NUC eseguendo hello comando seguente:

   ```bash
   gulp modules --list
   ```

   percorso binario di Hello del `my_module` che è stato compilato dovrebbe essere elencato come indicato di seguito:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Se si modifica nome utente account di accesso predefinito di hello in `config-gateway.json`, percorso binario hello inizierà con `home/<your username>` anziché `root`.

1. Aggiungere `my_module` toohello `hello_world` app di esempio:

   1. Aprire hello `hello_world.json` file eseguendo hello comando seguente:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Aggiungere i seguenti toohello codice hello `modules` sezione:

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      valore di Hello `module.path` deve essere `/root/gateway_sample/module/my_module/build/libmy_module.so`. codice Hello dichiara `my_module` toobe associato gateway hello, nonché il percorso di hello del file binario modulo hello specificato in `module.path`.
   1. Aggiungere i seguenti toohello codice hello `links` sezione:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Questo codice specifica che i messaggi vengono trasferiti dal hello `hello_world` modulo troppo`my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Eseguire hello `hello_world` app di esempio eseguendo hello comando seguente:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   Hello `--config` parametro forza hello `run-hello-world.js` toorun eseguire lo script utilizzando hello `hello_world.json` file.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

A questo punto È ora possibile osservare il comportamento di hello del nuovo modulo, stampa semplicemente i messaggi di "hello world" con un timestamp, un risultato diverso dal modulo di hello originale "hello_world".

## <a name="next-steps"></a>Passaggi successivi

È stato creato un nuovo modulo, aggiunto esempio hello_world toohello e get hello esempio app toorun con il nuovo modulo hello sul gateway. Se si desidera toolearn ulteriori informazioni sui moduli di Azure IoT gateway, è possibile trovare ulteriori esempi di modulo qui: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
