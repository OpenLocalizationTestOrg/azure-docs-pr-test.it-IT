---
title: Installare l'interfaccia della riga di comando 1.0 di Azure | Microsoft Docs
description: Installare l'interfaccia della riga di comando 1.0 di Azure per Mac, Linux e Windows per iniziare a usare i servizi di Azure
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: 63b35ed25b809a16b61b685fd35aa67474b0a369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-cli-10"></a><span data-ttu-id="d3948-103">Installare l'interfaccia della riga di comando 1.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="d3948-103">Install the Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3948-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3948-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="d3948-105">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d3948-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="d3948-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d3948-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="d3948-107">Questo argomento descrive come installare l'interfaccia della riga di comando 1.0 di Azure, che si basa su nodeJs e supporta tutte le chiamate all'API di distribuzione classica, nonché un numero elevato di attività di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d3948-107">This topic describes how to install the Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="d3948-108">È consigliabile usare l'[interfaccia della riga di comando 2.0 di Azure](/cli/azure/overview) per le distribuzioni e la gestione di interfacce della riga di comando nuove o future.</span><span class="sxs-lookup"><span data-stu-id="d3948-108">You should use the [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="d3948-109">Installare rapidamente l'interfaccia della riga di comando 1.0 di Azure per usare un set di comandi open source basati su shell per creare e gestire le risorse in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d3948-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="d3948-110">Sono disponibili diverse opzioni per installare questi strumenti multipiattaforma nel computer in uso:</span><span class="sxs-lookup"><span data-stu-id="d3948-110">You have several options to install these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="d3948-111">**Pacchetto npm** - Esegue npm (Gestione pacchetti per JavaScript) per installare il pacchetto dell'interfaccia della riga di comando 1.0 di Azure più recente nella distribuzione o sistema operativo Linux in uso.</span><span class="sxs-lookup"><span data-stu-id="d3948-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="d3948-112">Nel computer devono essere installati node.js e npm.</span><span class="sxs-lookup"><span data-stu-id="d3948-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="d3948-113">**Programma di installazione** - È possibile scaricare un programma di installazione per agevolare l'installazione in Mac o Windows.</span><span class="sxs-lookup"><span data-stu-id="d3948-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="d3948-114">**Contenitore Docker** - Per usare l'interfaccia della riga di comando più recente in un contenitore Docker pronto per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d3948-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="d3948-115">Nel computer deve essere installato l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="d3948-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="d3948-116">Per altre opzioni e informazioni, vedere il repository dei progetti in [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="d3948-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="d3948-117">Dopo l'installazione dell'interfaccia della riga di comando 1.0 di Azure, [connetterla alla sottoscrizione di Azure](xplat-cli-connect.md) ed eseguire i comandi **azure** dall'interfaccia della riga di comando (Bash, terminale, prompt dei comandi e così via) per usare le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3948-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="d3948-118">Opzione 1: Installare un pacchetto npm</span><span class="sxs-lookup"><span data-stu-id="d3948-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="d3948-119">Per installare l'interfaccia della riga di comando da un pacchetto npm, verificare che siano state caricate e installate le [versioni più recenti di Node.js e npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="d3948-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="d3948-120">Eseguire quindi il comando **npm install** per installare il pacchetto dell'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="d3948-120">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="d3948-121">Nelle distribuzioni di Linux potrebbe essere necessario usare **sudo** per la corretta esecuzione del comando **npm**, come segue:</span><span class="sxs-lookup"><span data-stu-id="d3948-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="d3948-122">Se è necessario installare o aggiornare Node.js e npm nella distribuzione o nel sistema operativo Linux, è consigliabile installare la versione più recente di Node.js LTS (4.x).</span><span class="sxs-lookup"><span data-stu-id="d3948-122">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="d3948-123">Se si usa una versione precedente, potrebbero verificarsi errori di installazione.</span><span class="sxs-lookup"><span data-stu-id="d3948-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="d3948-124">È anche possibile scaricare in locale il [file tar][linux-installer] di Linux più recente per il pacchetto npm.</span><span class="sxs-lookup"><span data-stu-id="d3948-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span></span> <span data-ttu-id="d3948-125">Installare quindi il pacchetto npm scaricato come indicato di seguito (nelle distribuzioni di Linux potrebbe essere necessario usare **sudo**):</span><span class="sxs-lookup"><span data-stu-id="d3948-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span></span>

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="d3948-126">Opzione 2: Usare un programma di installazione</span><span class="sxs-lookup"><span data-stu-id="d3948-126">Option 2: Use an installer</span></span>
<span data-ttu-id="d3948-127">Se si usa un computer Mac o Windows, è possibile scaricare i programmi di installazione del pacchetto dell'interfaccia della riga di comando seguenti:</span><span class="sxs-lookup"><span data-stu-id="d3948-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span></span>

* <span data-ttu-id="d3948-128">[Programma di installazione di Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="d3948-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="d3948-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="d3948-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="d3948-130">In Windows è anche possibile scaricare l' [Installazione guidata piattaforma Web](https://go.microsoft.com/?linkid=9828653) per installare per il pacchetto dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="d3948-130">On Windows, you can also download the [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) to install the CLI.</span></span> <span data-ttu-id="d3948-131">Questo programma di installazione consente di installare altri strumenti Azure SDK e a riga di comando dopo l'installazione dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="d3948-131">This installer gives you the option to install additional Azure SDK and command-line tools after installing the CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="d3948-132">Opzione 3: Usare un contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="d3948-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="d3948-133">Se il computer è stato configurato come host [Docker](https://docs.docker.com/engine/understanding-docker/) è possibile eseguire l'interfaccia della riga di comando 1.0 di Azure in un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="d3948-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="d3948-134">Eseguire il comando seguente (nelle distribuzioni di Linux potrebbe essere necessario usare **sudo**):</span><span class="sxs-lookup"><span data-stu-id="d3948-134">Run the following command (on Linux distributions you might need to use **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="d3948-135">Eseguire i comandi dell'interfaccia della riga di comando 1.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="d3948-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="d3948-136">Dopo aver installato l'interfaccia della riga di comando 1.0 di Azure, eseguire il comando **azure** dall'interfaccia (Bash, terminale, prompt dei comandi e così via).</span><span class="sxs-lookup"><span data-stu-id="d3948-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="d3948-137">Ad esempio, per eseguire il comando della Guida, digitare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d3948-137">For example, to run the help command, type the following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="d3948-138">In alcune distribuzioni di Linux potrebbe essere visualizzato un errore simile a `/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="d3948-138">On some Linux distributions, you may receive an error similar to `/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="d3948-139">Questo errore è causato dalle installazioni recenti di Node.js che vengono installate in /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="d3948-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="d3948-140">Per correggerlo, creare un collegamento simbolico per /usr/bin/node eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="d3948-140">To fix it, create a symbolic link to /usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="d3948-141">Per visualizzare la versione dell'interfaccia della riga di comando 1.0 di Azure installata, digitare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d3948-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="d3948-142">È ora possibile iniziare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d3948-142">Now you are ready!</span></span> <span data-ttu-id="d3948-143">Per accedere a tutti i comandi dell'interfaccia della riga di comando per usare le proprie risorse, [connettersi alla sottoscrizione di Azure dall'interfaccia della riga di comando di Azure](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d3948-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d3948-144">Quando si usa per la prima volta l'interfaccia della riga di comando di Azure, viene visualizzato un messaggio che chiede se consentire a Microsoft di raccogliere informazioni sull'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="d3948-144">When you first use Azure CLI, you see a message asking if you want to allow Microsoft to collect usage information.</span></span> <span data-ttu-id="d3948-145">La partecipazione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="d3948-145">Participation is voluntary.</span></span> <span data-ttu-id="d3948-146">Se si sceglie di partecipare, è possibile interrompere in qualsiasi momento eseguendo `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="d3948-146">If you choose to participate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="d3948-147">Per abilitare la partecipazione in qualsiasi momento, eseguire `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="d3948-147">To enable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-the-cli"></a><span data-ttu-id="d3948-148">Aggiornare l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="d3948-148">Update the CLI</span></span>
<span data-ttu-id="d3948-149">Microsoft rilascia di frequente versioni aggiornate dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3948-149">Microsoft frequently releases updated versions of the Azure CLI.</span></span> <span data-ttu-id="d3948-150">Reinstallare l'interfaccia della riga di comando per il sistema operativo o eseguire il contenitore Docker più recente.</span><span class="sxs-lookup"><span data-stu-id="d3948-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span></span> <span data-ttu-id="d3948-151">Oppure, se sono installati npm e la versione più recente di Node.js, eseguire l'aggiornamento digitando quanto riportato di seguito. Nelle distribuzioni di Linux potrebbe essere necessario usare **sudo**.</span><span class="sxs-lookup"><span data-stu-id="d3948-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="d3948-152">Attivare il completamento con tasto TAB</span><span class="sxs-lookup"><span data-stu-id="d3948-152">Enable tab completion</span></span>
<span data-ttu-id="d3948-153">Il completamento con tasto TAB dei comandi dell'interfaccia della riga di comando è supportato per Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="d3948-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="d3948-154">Per abilitarlo in zsh, eseguire:</span><span class="sxs-lookup"><span data-stu-id="d3948-154">To enable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="d3948-155">Per abilitarlo in bash, eseguire:</span><span class="sxs-lookup"><span data-stu-id="d3948-155">To enable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="d3948-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3948-156">Next steps</span></span>
* <span data-ttu-id="d3948-157">[Connettersi a una sottoscrizione di Azure dall'interfaccia della riga di comando di Azure](xplat-cli-connect.md) per creare e gestire le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3948-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span></span>
* <span data-ttu-id="d3948-158">Per altre informazioni sull'interfaccia della riga di comando di Azure, il download del codice sorgente, la segnalazione dei problemi o la collaborazione al progetto, visitare il [repository GitHub per tale interfaccia](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="d3948-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="d3948-159">In caso di domande sull'uso di Azure o dell'interfaccia della riga di comando di Azure, visitare i [forum di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="d3948-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
