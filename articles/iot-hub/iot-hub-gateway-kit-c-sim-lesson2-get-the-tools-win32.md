---
title: 'Dispositivo simulato e gateway Azure IoT: lezione 2: Ottenere gli strumenti (Windows) | Documentazione Microsoft'
description: Installare gli strumenti e il software nel computer host che esegue Windows, creare un hub IoT e registrare il dispositivo nell'hub IoT.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: sviluppo iot, software iot, servizio cloud iot, software per internet delle cose, interfaccia della riga di comando di azure, installare git in windows, esecuzione di gulp, installare node js in windows, installare npm in windows, installare python in windows
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: c16eee4c-8756-454b-82bf-3eb0dd51aa5f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ecedf5ef89677c73c5d9a3e5250eb9f45f6bad32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-tools-windows-7-and-later"></a><span data-ttu-id="4715d-104">Ottenere gli strumenti (Windows 7 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="4715d-104">Get the tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4715d-105">Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="4715d-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="4715d-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="4715d-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="4715d-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="4715d-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="4715d-108">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="4715d-108">What you will do</span></span>

- <span data-ttu-id="4715d-109">Installare Git, Node.js, Gulp e Python.</span><span class="sxs-lookup"><span data-stu-id="4715d-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="4715d-110">Installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="4715d-110">Install the Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="4715d-111">In caso di problemi, cercare le soluzioni nella pagina sulla [risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4715d-111">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4715d-112">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="4715d-112">What you will learn</span></span>

<span data-ttu-id="4715d-113">In questa lezione si apprenderà:</span><span class="sxs-lookup"><span data-stu-id="4715d-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="4715d-114">Come installare [Git](https://git-scm.com/) e [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="4715d-114">How to install [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="4715d-115">Git è un sistema distribuito open source di controllo delle versioni.</span><span class="sxs-lookup"><span data-stu-id="4715d-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="4715d-116">L'applicazione di esempio per questa lezione è archiviata in Git.</span><span class="sxs-lookup"><span data-stu-id="4715d-116">The sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="4715d-117">Node.js è un runtime JavaScript con un ampio ecosistema di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4715d-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="4715d-118">Come usare [NPM](https://www.npmjs.com/) per installare gli strumenti di sviluppo Node.js.</span><span class="sxs-lookup"><span data-stu-id="4715d-118">How to use [NPM](https://www.npmjs.com/) to install Node.js development tools.</span></span>
  - <span data-ttu-id="4715d-119">La versione minima richiesta di Node.js è 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="4715d-119">The minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="4715d-120">NPM è uno degli strumenti di gestione pacchetti per Node.js.</span><span class="sxs-lookup"><span data-stu-id="4715d-120">NPM is one of the package managers for Node.js.</span></span>
- <span data-ttu-id="4715d-121">Come installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="4715d-121">How to install Visual Studio Code.</span></span>
  - <span data-ttu-id="4715d-122">Visual Studio Code è un editor di codice sorgente multipiattaforma leggero ma potente per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="4715d-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="4715d-123">Offre un eccellente supporto per il debug, il controllo di Git incorporato, l'evidenziazione della sintassi, il completamento intelligente del codice, i frammenti e il refactoring del codice.</span><span class="sxs-lookup"><span data-stu-id="4715d-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="4715d-124">Come installare Python.</span><span class="sxs-lookup"><span data-stu-id="4715d-124">How to install Python.</span></span>
  - <span data-ttu-id="4715d-125">Python è un linguaggio di programmazione dinamico, interpretato, generico e di alto livello molto diffuso.</span><span class="sxs-lookup"><span data-stu-id="4715d-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="4715d-126">Come installare l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="4715d-126">How to install the Azure CLI.</span></span>
  - <span data-ttu-id="4715d-127">L'interfaccia della riga di comando di Azure offre un'esperienza di riga di comando multipiattaforma per Azure.</span><span class="sxs-lookup"><span data-stu-id="4715d-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="4715d-128">Il provisioning e la gestione delle risorse vengono eseguiti direttamente dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="4715d-128">You work directly from a command line to provision and manage resources.</span></span>
- <span data-ttu-id="4715d-129">Come usare l'interfaccia della riga di comando di Azure per creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4715d-129">How to use the Azure CLI to create an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4715d-130">Elementi necessari</span><span class="sxs-lookup"><span data-stu-id="4715d-130">What you need</span></span>

- <span data-ttu-id="4715d-131">Connessione Internet per scaricare gli strumenti e il software.</span><span class="sxs-lookup"><span data-stu-id="4715d-131">An Internet connection to download the tools and software.</span></span>
- <span data-ttu-id="4715d-132">Computer Windows.</span><span class="sxs-lookup"><span data-stu-id="4715d-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="4715d-133">Installare Git e Node.js</span><span class="sxs-lookup"><span data-stu-id="4715d-133">Install Git and Node.js</span></span>

<span data-ttu-id="4715d-134">Fare clic sui collegamenti seguenti per scaricare e installare Git e Node.js LTS per Windows.</span><span class="sxs-lookup"><span data-stu-id="4715d-134">Click the following links to download and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="4715d-135">Ottenere Git per Windows</span><span class="sxs-lookup"><span data-stu-id="4715d-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="4715d-136">Ottenere Node.js LTS per Windows</span><span class="sxs-lookup"><span data-stu-id="4715d-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="4715d-137">Installare gli strumenti di sviluppo Node.js</span><span class="sxs-lookup"><span data-stu-id="4715d-137">Install Node.js development tools</span></span>

<span data-ttu-id="4715d-138">Usare [gulp.js](http://gulpjs.com/) per automatizzare la distribuzione e l'esecuzione di script.</span><span class="sxs-lookup"><span data-stu-id="4715d-138">You use [gulp.js](http://gulpjs.com/) to automate deployment and execution of scripts.</span></span>

<span data-ttu-id="4715d-139">Premere `Windows + R`, digitare `cmd`, premere `Enter` per aprire una finestra del prompt dei comandi e quindi eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="4715d-139">Press `Windows + R`, type `cmd` and press `Enter` to open a Command Prompt window, and then run the following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="4715d-140">Se si verificano problemi nell'installazione, vedere la [guida alla risoluzione dei problemi](iot-hub-gateway-kit-c-sim-troubleshooting.md) per le soluzioni alle problematiche comuni.</span><span class="sxs-lookup"><span data-stu-id="4715d-140">If you experience issues with the installation, see the [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions to common problems.</span></span>

> [!Note]
> <span data-ttu-id="4715d-141">Node, NPM e Gulp sono necessari per eseguire gli script di automazione sviluppati in Node.js.</span><span class="sxs-lookup"><span data-stu-id="4715d-141">Node, NPM and Gulp are required to run automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="4715d-142">Installare Python</span><span class="sxs-lookup"><span data-stu-id="4715d-142">Install Python</span></span>

<span data-ttu-id="4715d-143">È possibile scegliere Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="4715d-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="4715d-144">In questa esercitazione si userà Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="4715d-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="4715d-145">Se è già stato installato Python, passare alla sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="4715d-145">If you've already installed python, go to the next section.</span></span>

[<span data-ttu-id="4715d-146">Ottenere Python per Windows</span><span class="sxs-lookup"><span data-stu-id="4715d-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="4715d-147">È necessario anche aggiungere il percorso delle cartelle in cui vengono installati Python.exe e pip.exe alla variabile di ambiente `PATH` del sistema.</span><span class="sxs-lookup"><span data-stu-id="4715d-147">You also need to add the path of the folders where Python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="4715d-148">Per impostazione predefinita, python.exe viene installato in `C:\Python27` e pip.exe viene installato in `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="4715d-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="4715d-149">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="4715d-149">Install the Azure CLI</span></span>

<span data-ttu-id="4715d-150">Per installare l'interfaccia della riga di comando di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="4715d-150">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="4715d-151">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4715d-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="4715d-152">Installare l'interfaccia della riga di comando di Azure eseguendo questi comandi:</span><span class="sxs-lookup"><span data-stu-id="4715d-152">Install the Azure CLI by running the following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="4715d-153">L'installazione potrebbe richiedere 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="4715d-153">The installation might take 5 minutes.</span></span>

3. <span data-ttu-id="4715d-154">Verificare l'installazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4715d-154">Verify the installation by running the following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="4715d-155">Se l'installazione ha esito positivo, verrà visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="4715d-155">You should see the following output if the installation is successful.</span></span>

   ![Verificare l'installazione dell'interfaccia della riga di comando di Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="4715d-157">Installare Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4715d-157">Install Visual Studio Code</span></span>

<span data-ttu-id="4715d-158">Visual Studio Code verrà usato più avanti nell'esercitazione per modificare i file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4715d-158">You use Visual Studio Code later in the tutorial to edit configuration files.</span></span>

<span data-ttu-id="4715d-159">[Scaricare](https://code.visualstudio.com/docs/setup/windows) e installare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="4715d-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="4715d-160">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="4715d-160">Summary</span></span>

<span data-ttu-id="4715d-161">Sono stati installati tutto il software e tutti gli strumenti necessari nel computer host.</span><span class="sxs-lookup"><span data-stu-id="4715d-161">You've installed all the required tools and software on your host computer.</span></span> <span data-ttu-id="4715d-162">L'attività successiva consiste nell'usare l'interfaccia della riga di comando di Azure per creare un hub IoT e registrarvi il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4715d-162">Your next task is to use the Azure CLI to create an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4715d-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4715d-163">Next steps</span></span>
[<span data-ttu-id="4715d-164">Creare un hub IoT e registrare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="4715d-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
