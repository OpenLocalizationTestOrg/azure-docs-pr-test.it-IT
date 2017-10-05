---
title: Creare il primo modulo di Azure IoT Gateway | Microsoft Docs
description: Creare un modulo e aggiungerlo a un'app di esempio per personalizzare i comportamenti del modulo.
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
ms.openlocfilehash: 5e28422158684c3aaf0ac3fdf5b19c80fbccfb02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="22db8-103">Lezione 5: creare il primo modulo di Azure IoT Gateway</span><span class="sxs-lookup"><span data-stu-id="22db8-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="22db8-104">Mentre Azure IoT Edge consente di compilare moduli scritti in Java, .NET o Node.js, questa esercitazione illustra la procedura per la compilazione di un modulo in C.</span><span class="sxs-lookup"><span data-stu-id="22db8-104">While Azure IoT Edge allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="22db8-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="22db8-105">What you will do</span></span>

- <span data-ttu-id="22db8-106">Compilare ed eseguire l'app di esempio hello_world in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="22db8-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="22db8-107">Creare un modulo e compilarlo in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="22db8-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="22db8-108">Aggiungere il nuovo modulo all'app di esempio hello_world ed eseguire l'esempio in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="22db8-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="22db8-109">Il nuovo modulo stampa i messaggi "hello_world" con un timestamp.</span><span class="sxs-lookup"><span data-stu-id="22db8-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="22db8-110">Concetti legati all'esercitazione</span><span class="sxs-lookup"><span data-stu-id="22db8-110">What you will learn</span></span>

- <span data-ttu-id="22db8-111">Come compilare ed eseguire un'app di esempio in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="22db8-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="22db8-112">Come creare un modulo.</span><span class="sxs-lookup"><span data-stu-id="22db8-112">How to create a module.</span></span>
- <span data-ttu-id="22db8-113">Come aggiungere un modulo a un'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="22db8-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="22db8-114">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="22db8-114">What you need</span></span>

<span data-ttu-id="22db8-115">Azure IoT Edge installato nel computer host.</span><span class="sxs-lookup"><span data-stu-id="22db8-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="22db8-116">Struttura di cartelle</span><span class="sxs-lookup"><span data-stu-id="22db8-116">Folder structure</span></span>

<span data-ttu-id="22db8-117">Nella sottocartella Lezione 5 del codice di esempio, che è stato clonato nella lezione 1, si trovano una cartella `module` e una cartella `sample`.</span><span class="sxs-lookup"><span data-stu-id="22db8-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="22db8-119">La cartella `module/my_module` contiene il codice sorgente e lo script per compilare il modulo.</span><span class="sxs-lookup"><span data-stu-id="22db8-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="22db8-120">La cartella `sample` contiene il codice sorgente e lo script per compilare l'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="22db8-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="22db8-121">Compilare ed eseguire l'app di esempio hello_world in Intel NUC</span><span class="sxs-lookup"><span data-stu-id="22db8-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="22db8-122">L'esempio `hello_world` crea un gateway basato sul file `hello_world.json` che specifica i due moduli predefiniti associati all'app.</span><span class="sxs-lookup"><span data-stu-id="22db8-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="22db8-123">Il gateway registra un messaggio "hello world" in un file ogni 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="22db8-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="22db8-124">In questa sezione si descrive come compilare ed eseguire l'app `hello_world` con il relativo modulo predefinito.</span><span class="sxs-lookup"><span data-stu-id="22db8-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="22db8-125">Per compilare ed eseguire l'app `hello_world`, seguire questi passaggi nel computer host:</span><span class="sxs-lookup"><span data-stu-id="22db8-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="22db8-126">Inizializzare i file di configurazione eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="22db8-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="22db8-127">Aggiornare il file di configurazione del gateway con l'indirizzo MAC di Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="22db8-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="22db8-128">Ignorare questo passaggio se è già stata consultata la lezione su come [configurare ed eseguire un'applicazione di esempio BLE][config_ble].</span><span class="sxs-lookup"><span data-stu-id="22db8-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="22db8-129">Aprire il file di configurazione del gateway eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="22db8-130">Aggiornare l'indirizzo MAC del gateway quando si deve [configurare Intel NUC come gateway IoT][setup_nuc] e salvare il file.</span><span class="sxs-lookup"><span data-stu-id="22db8-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="22db8-131">Compilare il codice sorgente di esempio eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="22db8-132">Il comando trasferisce il codice sorgente di esempio a Intel NUC ed esegue `build.sh` per compilarlo.</span><span class="sxs-lookup"><span data-stu-id="22db8-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="22db8-133">Eseguire l'app `hello_world` in Intel NUC eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="22db8-134">Il comando esegue `../Tools/run-hello-world.js` specificato in `config.json` per avviare l'app di esempio in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="22db8-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="22db8-136">Creare un nuovo modulo e compilarlo in Intel NUC</span><span class="sxs-lookup"><span data-stu-id="22db8-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="22db8-137">I passaggi seguenti illustrano come creare un nuovo modulo e compilarlo in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="22db8-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="22db8-138">Il modulo stampa i messaggi con un timestamp al momento della loro ricezione.</span><span class="sxs-lookup"><span data-stu-id="22db8-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="22db8-139">In questa sezione è possibile creare il primo modulo di gateway personalizzato.</span><span class="sxs-lookup"><span data-stu-id="22db8-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="22db8-140">Tutti i moduli Azure IoT Edge devono implementare le interfacce seguenti:</span><span class="sxs-lookup"><span data-stu-id="22db8-140">Any Azure IoT Edge module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="22db8-141">Facoltativamente è possibile implementare l'interfaccia seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="22db8-142">Il diagramma seguente mostra i percorsi di stato fondamentali di un modulo.</span><span class="sxs-lookup"><span data-stu-id="22db8-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="22db8-143">I rettangoli rappresentano i metodi implementati per eseguire operazioni quando il modulo si sposta tra stati diversi.</span><span class="sxs-lookup"><span data-stu-id="22db8-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="22db8-144">Gli ovali sono gli stati principali nei quali si può trovare il modulo.</span><span class="sxs-lookup"><span data-stu-id="22db8-144">The ovals are major states the module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="22db8-146">A questo punto si può creare un modulo basato sul modello:</span><span class="sxs-lookup"><span data-stu-id="22db8-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="22db8-147">Aprire la cartella del modello eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="22db8-149">`src/my_module.c` funge da modello per facilitare la creazione di un modulo.</span><span class="sxs-lookup"><span data-stu-id="22db8-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="22db8-150">Il modello dichiara le interfacce.</span><span class="sxs-lookup"><span data-stu-id="22db8-150">The template declares the interfaces.</span></span> <span data-ttu-id="22db8-151">È sufficiente aggiungere la logica alla funzione `MyModule_Receive`.</span><span class="sxs-lookup"><span data-stu-id="22db8-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="22db8-152">`build.sh` è lo script di compilazione necessario per compilare il modulo in Intel NUC .</span><span class="sxs-lookup"><span data-stu-id="22db8-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="22db8-153">Aprire il file `src/my_module.c` e includere due file di intestazione:</span><span class="sxs-lookup"><span data-stu-id="22db8-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="22db8-154">Aggiungere il codice seguente alla funzione `MyModule_Receive`:</span><span class="sxs-lookup"><span data-stu-id="22db8-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
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
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="22db8-155">Aggiornare il file `config.json` per specificare la cartella `workspace` nel computer host e il percorso di distribuzione in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="22db8-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="22db8-156">Durante la compilazione, i file della cartella `workspace` verranno trasferiti al percorso di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="22db8-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="22db8-157">Aprire il file `config.json` eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="22db8-158">Aggiornare `config.json` con la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="22db8-160">Compilare il modulo eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="22db8-161">Il comando trasferisce il codice sorgente in Intel NUC ed esegue `build.sh` per compilare il modulo.</span><span class="sxs-lookup"><span data-stu-id="22db8-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="22db8-162">Aggiungere il modulo all'app di esempio hello_world ed eseguire l'app in Intel NUC</span><span class="sxs-lookup"><span data-stu-id="22db8-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="22db8-163">Per eseguire questa attività seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="22db8-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="22db8-164">Elencare tutti i file binari disponibili del modulo (file con estensione .so) in Intel NUC eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="22db8-165">Il percorso binario di `my_module` che è stato compilato dovrebbe essere elencato come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="22db8-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="22db8-166">Se si modifica il nome utente di accesso predefinito in `config-gateway.json`, il percorso binario inizierà con `home/<your username>` anziché con `root`.</span><span class="sxs-lookup"><span data-stu-id="22db8-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="22db8-167">Aggiungere `my_module` all'app di esempio `hello_world`:</span><span class="sxs-lookup"><span data-stu-id="22db8-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="22db8-168">Aprire il file `hello_world.json` eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="22db8-169">Aggiungere il codice seguente alla sezione `modules`:</span><span class="sxs-lookup"><span data-stu-id="22db8-169">Add the following code to the `modules` section:</span></span>

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

      <span data-ttu-id="22db8-170">Il valore di `module.path` dovrebbe essere `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="22db8-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="22db8-171">Il codice dichiara `my_module` da associare al gateway e la posizione del file binario del modulo specificato in `module.path`.</span><span class="sxs-lookup"><span data-stu-id="22db8-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="22db8-172">Aggiungere il codice seguente alla sezione `links`:</span><span class="sxs-lookup"><span data-stu-id="22db8-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="22db8-173">Questo codice specifica che i messaggi vengono trasferiti dal modulo `hello_world` a `my_module`.</span><span class="sxs-lookup"><span data-stu-id="22db8-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="22db8-175">Eseguire l'app di esempio `hello_world` eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="22db8-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="22db8-176">Il parametro `--config` forza l'esecuzione dello script `run-hello-world.js` usando il file `hello_world.json`.</span><span class="sxs-lookup"><span data-stu-id="22db8-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="22db8-178">A questo punto</span><span class="sxs-lookup"><span data-stu-id="22db8-178">Congratulations.</span></span> <span data-ttu-id="22db8-179">È ora possibile visualizzare il comportamento di questo nuovo modulo, che stampa semplicemente i messaggi "hello world" con un timestamp, con un risultato diverso dal modulo "hello_world" originale.</span><span class="sxs-lookup"><span data-stu-id="22db8-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22db8-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22db8-180">Next Steps</span></span>

<span data-ttu-id="22db8-181">È stato creato un nuovo modulo, che è poi stato aggiunto all'esempio hello_world e l'app di esempio viene eseguita con il nuovo modulo sul gateway.</span><span class="sxs-lookup"><span data-stu-id="22db8-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="22db8-182">Per altre informazioni sui moduli di Azure IoT Gateway è possibile trovare altri esempi di modulo in: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="22db8-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
