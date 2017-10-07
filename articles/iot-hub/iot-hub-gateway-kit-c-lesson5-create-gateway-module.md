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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="aecdc-103">Lezione 5: creare il primo modulo di Azure IoT Gateway</span><span class="sxs-lookup"><span data-stu-id="aecdc-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="aecdc-104">Mentre Azure IoT Edge consente moduli toobuild scritti in Node.js, Java o .NET, questa esercitazione illustra hello passaggi per la creazione di un modulo in C.</span><span class="sxs-lookup"><span data-stu-id="aecdc-104">While Azure IoT Edge allows you toobuild modules written in Java, .NET, or Node.js, this tutorial walks you through hello steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="aecdc-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="aecdc-105">What you will do</span></span>

- <span data-ttu-id="aecdc-106">Compilare ed eseguire app di esempio hello_world hello in NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="aecdc-106">Compile and run hello hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="aecdc-107">Creare un modulo e compilarlo in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="aecdc-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="aecdc-108">Aggiungere hello nuovo modulo toohello hello_world esempio app e quindi eseguire l'esempio hello in NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="aecdc-108">Add hello new module toohello hello_world sample app and then run hello sample on Intel NUC.</span></span> <span data-ttu-id="aecdc-109">il nuovo modulo Hello stampa i messaggi "hello_world" con un timestamp.</span><span class="sxs-lookup"><span data-stu-id="aecdc-109">hello new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="aecdc-110">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="aecdc-110">What you will learn</span></span>

- <span data-ttu-id="aecdc-111">Come toocompile ed eseguire un'app di esempio in NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="aecdc-111">How toocompile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="aecdc-112">Come toocreate un modulo.</span><span class="sxs-lookup"><span data-stu-id="aecdc-112">How toocreate a module.</span></span>
- <span data-ttu-id="aecdc-113">App di esempio come tooadd modulo tooa.</span><span class="sxs-lookup"><span data-stu-id="aecdc-113">How tooadd module tooa sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aecdc-114">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="aecdc-114">What you need</span></span>

<span data-ttu-id="aecdc-115">Azure IoT Edge installato nel computer host.</span><span class="sxs-lookup"><span data-stu-id="aecdc-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="aecdc-116">Struttura di cartelle</span><span class="sxs-lookup"><span data-stu-id="aecdc-116">Folder structure</span></span>

<span data-ttu-id="aecdc-117">In una sottocartella hello lezione 5 hello del codice di esempio che è stato clonato nella lezione 1, è presente un `module` cartella e un `sample` cartella.</span><span class="sxs-lookup"><span data-stu-id="aecdc-117">In hello Lesson 5 subfolder of hello sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="aecdc-119">Hello `module/my_module` cartella contiene hello codice e script toobuild hello modulo di origine.</span><span class="sxs-lookup"><span data-stu-id="aecdc-119">hello `module/my_module` folder contains hello source code and script toobuild hello module.</span></span>
- <span data-ttu-id="aecdc-120">Hello `sample` cartella contiene hello origine codice e script toobuild hello app di esempio.</span><span class="sxs-lookup"><span data-stu-id="aecdc-120">hello `sample` folder contains hello source code and script toobuild hello sample app.</span></span>

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="aecdc-121">Compilare ed eseguire app di esempio hello_world hello in NUC Intel</span><span class="sxs-lookup"><span data-stu-id="aecdc-121">Compile and run hello hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="aecdc-122">Hello `hello_world` esempio crea un gateway in base a hello `hello_world.json` file specifica hello due moduli predefiniti associati a hello app.</span><span class="sxs-lookup"><span data-stu-id="aecdc-122">hello `hello_world` sample creates a gateway based on hello `hello_world.json` file which specifies hello two predefined modules associated with hello app.</span></span> <span data-ttu-id="aecdc-123">gateway Hello registra un file di tooa messaggio "hello world" ogni 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="aecdc-123">hello gateway logs a "hello world" message tooa file every 5 seconds.</span></span> <span data-ttu-id="aecdc-124">In questa sezione, compilare ed eseguire hello `hello_world` app con il modulo predefinito.</span><span class="sxs-lookup"><span data-stu-id="aecdc-124">In this section, you compile and run hello `hello_world` app with its default module.</span></span>

<span data-ttu-id="aecdc-125">hello toocompile ed eseguire `hello_world` app, seguire questi passaggi nel computer host:</span><span class="sxs-lookup"><span data-stu-id="aecdc-125">toocompile and run hello `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="aecdc-126">Inizializzare i file di configurazione hello eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="aecdc-126">Initialize hello configuration files by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="aecdc-127">Aggiornare i file di configurazione di gateway di hello con indirizzo MAC di Intel NUC hello.</span><span class="sxs-lookup"><span data-stu-id="aecdc-127">Update hello gateway configuration file with hello MAC address of Intel NUC.</span></span> <span data-ttu-id="aecdc-128">Ignorare questo passaggio se già stata consultata troppo lezione hello[configurare ed eseguire un'applicazione di esempio BILITA][config_ble].</span><span class="sxs-lookup"><span data-stu-id="aecdc-128">Skip this step if you have gone through hello lesson too[configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="aecdc-129">Aprire il file di configurazione di gateway hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aecdc-129">Open hello gateway configuration file by running hello following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="aecdc-130">Di indirizzi MAC del gateway hello aggiornamento quando si [impostare NUC Intel come gateway IoT][setup_nuc]e quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="aecdc-130">Update hello gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save hello file.</span></span>

1. <span data-ttu-id="aecdc-131">Compilare codice sorgente dell'esempio hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aecdc-131">Compile hello sample source code by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="aecdc-132">Trasferisce hello esempio origine codice tooIntel NUC Hello comando ed esegue `build.sh` toocompile è.</span><span class="sxs-lookup"><span data-stu-id="aecdc-132">hello command transfers hello sample source code tooIntel NUC and runs `build.sh` toocompile it.</span></span>

1. <span data-ttu-id="aecdc-133">Eseguire hello `hello_world` app su Intel NUC eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aecdc-133">Run hello `hello_world` app on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="aecdc-134">esecuzione del comando Hello `../Tools/run-hello-world.js` specificata nei `config.json` toostart app di esempio hello in NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="aecdc-134">hello command runs `../Tools/run-hello-world.js` that is specified in `config.json` toostart hello sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="aecdc-136">Creare un nuovo modulo e compilarlo in Intel NUC</span><span class="sxs-lookup"><span data-stu-id="aecdc-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="aecdc-137">passaggi Hello riportati di seguito è illustrata la creazione di un nuovo modulo e compilarlo nella NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="aecdc-137">hello steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="aecdc-138">modulo Hello stampa i messaggi con un timestamp alla ricezione di essi.</span><span class="sxs-lookup"><span data-stu-id="aecdc-138">hello module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="aecdc-139">In questa sezione è possibile creare il primo modulo di gateway personalizzato.</span><span class="sxs-lookup"><span data-stu-id="aecdc-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="aecdc-140">Qualsiasi modulo di Azure IoT bordo deve implementare hello seguenti interfacce:</span><span class="sxs-lookup"><span data-stu-id="aecdc-140">Any Azure IoT Edge module must implement hello following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="aecdc-141">Facoltativamente, è possibile implementare hello seguente interfaccia:</span><span class="sxs-lookup"><span data-stu-id="aecdc-141">You can optionally implement hello following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="aecdc-142">Hello diagramma seguente mostra i percorsi di hello importanti dello stato di un modulo.</span><span class="sxs-lookup"><span data-stu-id="aecdc-142">hello following diagram shows hello important state paths of a module.</span></span> <span data-ttu-id="aecdc-143">rettangoli quadrato Hello rappresentano i metodi implementare le operazioni di tooperform quando si sposta il modulo hello tra stati.</span><span class="sxs-lookup"><span data-stu-id="aecdc-143">hello square rectangles represent methods you implement tooperform operations when hello module moves between states.</span></span> <span data-ttu-id="aecdc-144">ovali Hello sono stati principali hello modulo può essere in.</span><span class="sxs-lookup"><span data-stu-id="aecdc-144">hello ovals are major states hello module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="aecdc-146">Ora si crea un modulo basato sul modello hello:</span><span class="sxs-lookup"><span data-stu-id="aecdc-146">Now let’s create a module based on hello template:</span></span>

1. <span data-ttu-id="aecdc-147">Aprire una cartella del modello di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aecdc-147">Open hello template folder by running hello following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="aecdc-149">`src/my_module.c`funge da un modello che facilita la creazione di hello di un modulo.</span><span class="sxs-lookup"><span data-stu-id="aecdc-149">`src/my_module.c` serves as a template that facilitates hello creation of a module.</span></span> <span data-ttu-id="aecdc-150">modello Hello dichiara interfacce hello.</span><span class="sxs-lookup"><span data-stu-id="aecdc-150">hello template declares hello interfaces.</span></span> <span data-ttu-id="aecdc-151">È sufficiente toodo tooadd logica toohello `MyModule_Receive` (funzione).</span><span class="sxs-lookup"><span data-stu-id="aecdc-151">All you need toodo is tooadd logic toohello `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="aecdc-152">`build.sh`è hello compilazione toocompile hello modulo di script in NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="aecdc-152">`build.sh` is hello build script toocompile hello module on Intel NUC.</span></span>
1. <span data-ttu-id="aecdc-153">Aprire hello `src/my_module.c` include due file di intestazione e di file:</span><span class="sxs-lookup"><span data-stu-id="aecdc-153">Open hello `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="aecdc-154">Aggiungere i seguenti toohello codice hello `MyModule_Receive` funzione:</span><span class="sxs-lookup"><span data-stu-id="aecdc-154">Add hello following code toohello `MyModule_Receive` function:</span></span>

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

1. <span data-ttu-id="aecdc-155">Hello aggiornamento `config.json` hello toospecify file `workspace` cartella al percorso di distribuzione hello e computer host su NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="aecdc-155">Update hello `config.json` file toospecify hello `workspace` folder on your host computer and hello deployment path on Intel NUC.</span></span> <span data-ttu-id="aecdc-156">Durante la compilazione, hello file hello `workspace` cartella saranno trasferiti toohello il percorso di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aecdc-156">During compiling, hello files in hello `workspace` folder will be transferred toohello deployment path.</span></span>

   1. <span data-ttu-id="aecdc-157">Aprire hello `config.json` file eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aecdc-157">Open hello `config.json` file by running hello following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="aecdc-158">Aggiornamento `config.json` con hello seguente configurazione:</span><span class="sxs-lookup"><span data-stu-id="aecdc-158">Update `config.json` with hello following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="aecdc-160">Compilare il modulo hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aecdc-160">Compile hello module by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="aecdc-161">Trasferisce hello origine codice tooIntel NUC Hello comando ed esegue `build.sh` modulo hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="aecdc-161">hello command transfers hello source code tooIntel NUC and runs `build.sh` toocompile hello module.</span></span>

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a><span data-ttu-id="aecdc-162">Aggiungere app di esempio hello modulo toohello hello_world ed eseguire app di hello in NUC Intel</span><span class="sxs-lookup"><span data-stu-id="aecdc-162">Add hello module toohello hello_world sample app and run hello app on Intel NUC</span></span>

<span data-ttu-id="aecdc-163">tooperform questa attività, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="aecdc-163">tooperform this task, follow these steps:</span></span>

1. <span data-ttu-id="aecdc-164">Elencare tutti i file binari del modulo disponibile hello (file con estensione SO) su Intel NUC eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aecdc-164">List all hello available module binaries (.so files) on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="aecdc-165">percorso binario di Hello del `my_module` che è stato compilato dovrebbe essere elencato come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="aecdc-165">hello binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="aecdc-166">Se si modifica nome utente account di accesso predefinito di hello in `config-gateway.json`, percorso binario hello inizierà con `home/<your username>` anziché `root`.</span><span class="sxs-lookup"><span data-stu-id="aecdc-166">If you change hello default login username in `config-gateway.json`, hello binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="aecdc-167">Aggiungere `my_module` toohello `hello_world` app di esempio:</span><span class="sxs-lookup"><span data-stu-id="aecdc-167">Add `my_module` toohello `hello_world` sample app:</span></span>

   1. <span data-ttu-id="aecdc-168">Aprire hello `hello_world.json` file eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aecdc-168">Open hello `hello_world.json` file by running hello following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="aecdc-169">Aggiungere i seguenti toohello codice hello `modules` sezione:</span><span class="sxs-lookup"><span data-stu-id="aecdc-169">Add hello following code toohello `modules` section:</span></span>

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

      <span data-ttu-id="aecdc-170">valore di Hello `module.path` deve essere `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="aecdc-170">hello value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="aecdc-171">codice Hello dichiara `my_module` toobe associato gateway hello, nonché il percorso di hello del file binario modulo hello specificato in `module.path`.</span><span class="sxs-lookup"><span data-stu-id="aecdc-171">hello code declares `my_module` toobe associated with hello gateway as well as hello location of hello module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="aecdc-172">Aggiungere i seguenti toohello codice hello `links` sezione:</span><span class="sxs-lookup"><span data-stu-id="aecdc-172">Add hello following code toohello `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="aecdc-173">Questo codice specifica che i messaggi vengono trasferiti dal hello `hello_world` modulo troppo`my_module`.</span><span class="sxs-lookup"><span data-stu-id="aecdc-173">This code specifies that messages are transferred from hello `hello_world` module too`my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="aecdc-175">Eseguire hello `hello_world` app di esempio eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aecdc-175">Run hello `hello_world` sample app by running hello following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="aecdc-176">Hello `--config` parametro forza hello `run-hello-world.js` toorun eseguire lo script utilizzando hello `hello_world.json` file.</span><span class="sxs-lookup"><span data-stu-id="aecdc-176">hello `--config` parameter forces hello `run-hello-world.js` script toorun by using hello `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="aecdc-178">A questo punto</span><span class="sxs-lookup"><span data-stu-id="aecdc-178">Congratulations.</span></span> <span data-ttu-id="aecdc-179">È ora possibile osservare il comportamento di hello del nuovo modulo, stampa semplicemente i messaggi di "hello world" con un timestamp, un risultato diverso dal modulo di hello originale "hello_world".</span><span class="sxs-lookup"><span data-stu-id="aecdc-179">You can now see hello behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from hello original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aecdc-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aecdc-180">Next Steps</span></span>

<span data-ttu-id="aecdc-181">È stato creato un nuovo modulo, aggiunto esempio hello_world toohello e get hello esempio app toorun con il nuovo modulo hello sul gateway.</span><span class="sxs-lookup"><span data-stu-id="aecdc-181">You’ve created a new module, added it toohello hello_world sample, and get hello sample app toorun with hello new module on your gateway.</span></span> <span data-ttu-id="aecdc-182">Se si desidera toolearn ulteriori informazioni sui moduli di Azure IoT gateway, è possibile trovare ulteriori esempi di modulo qui: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="aecdc-182">If you want toolearn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
