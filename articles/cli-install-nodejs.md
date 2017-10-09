---
title: aaaInstall hello Azure CLI 1.0 | Documenti Microsoft
description: Installare hello 1.0 CLI di Azure per Mac, Linux e Windows toostart utilizzando servizi di Azure
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
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="4a49a-103">Installare hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4a49a-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a49a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a49a-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="4a49a-105">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="4a49a-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="4a49a-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4a49a-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="4a49a-107">Questo argomento viene descritto come tooinstall hello Azure CLI 1.0, che si basa su nodeJs e supporta tutte le API di distribuzione classica chiama nonché un numero elevato di attività di distribuzione di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="4a49a-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="4a49a-108">È consigliabile utilizzare hello [CLI di Azure 2.0](/cli/azure/overview) per la gestione e le distribuzioni di CLI nuove o stampa.</span><span class="sxs-lookup"><span data-stu-id="4a49a-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="4a49a-109">Installare rapidamente hello interfaccia della riga di comando di Azure (Azure CLI 1.0) toouse un set di comandi basati su shell open source per la creazione e la gestione delle risorse in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4a49a-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="4a49a-110">Si dispongono di diverse opzioni tooinstall questi strumenti multipiattaforma nel computer in uso:</span><span class="sxs-lookup"><span data-stu-id="4a49a-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="4a49a-111">**pacchetto npm** - esecuzione npm (hello package manager per JavaScript) tooinstall hello pacchetto più recente di Azure 1.0 CLI sul sistema operativo o la distribuzione di Linux.</span><span class="sxs-lookup"><span data-stu-id="4a49a-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="4a49a-112">Nel computer devono essere installati node.js e npm.</span><span class="sxs-lookup"><span data-stu-id="4a49a-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="4a49a-113">**Programma di installazione** - È possibile scaricare un programma di installazione per agevolare l'installazione in Mac o Windows.</span><span class="sxs-lookup"><span data-stu-id="4a49a-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="4a49a-114">**Contenitore docker** : iniziare a utilizzare hello CLI più recente in un contenitore Docker ready to run.</span><span class="sxs-lookup"><span data-stu-id="4a49a-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="4a49a-115">Nel computer deve essere installato l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="4a49a-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="4a49a-116">Per altre opzioni e in background, vedere repository progetto hello in [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="4a49a-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="4a49a-117">Una volta installato, hello Azure CLI 1.0 [connetterlo con la sottoscrizione di Azure](xplat-cli-connect.md) esecuzione hello e **azure** comandi dall'interfaccia della riga di comando (Bash Terminal, il prompt dei comandi e così via) toowork con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a49a-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="4a49a-118">Opzione 1: Installare un pacchetto npm</span><span class="sxs-lookup"><span data-stu-id="4a49a-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="4a49a-119">tooinstall hello CLI da un pacchetto npm, assicurarsi aver scaricato e installato hello [più recenti di Node.js e npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="4a49a-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="4a49a-120">Eseguire quindi **npm installare** pacchetto di tooinstall hello cli di azure:</span><span class="sxs-lookup"><span data-stu-id="4a49a-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="4a49a-121">Nelle distribuzioni di Linux, potrebbe essere necessario toouse **sudo** toosuccessfully eseguire hello **npm** comando, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4a49a-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="4a49a-122">Se è necessario tooinstall o aggiornare Node.js e npm sul sistema operativo o la distribuzione di Linux, è consigliabile installare hello versione di Node. js LTS più recente (4. x).</span><span class="sxs-lookup"><span data-stu-id="4a49a-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="4a49a-123">Se si usa una versione precedente, potrebbero verificarsi errori di installazione.</span><span class="sxs-lookup"><span data-stu-id="4a49a-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="4a49a-124">Se si preferisce, scaricare hello Linux più recente [file con estensione tar] [ linux-installer] per npm hello pacchetto localmente.</span><span class="sxs-lookup"><span data-stu-id="4a49a-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="4a49a-125">Quindi, installare il pacchetto di npm scaricato hello come indicato di seguito (in distribuzioni di Linux potrebbe essere necessario toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="4a49a-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="4a49a-126">Opzione 2: Usare un programma di installazione</span><span class="sxs-lookup"><span data-stu-id="4a49a-126">Option 2: Use an installer</span></span>
<span data-ttu-id="4a49a-127">Se si utilizza un computer Mac o Windows, hello seguenti programmi di installazione CLI sono disponibile per il download:</span><span class="sxs-lookup"><span data-stu-id="4a49a-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="4a49a-128">[Programma di installazione di Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="4a49a-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="4a49a-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="4a49a-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="4a49a-130">In Windows, è anche possibile scaricare hello [installazione guidata piattaforma Web](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span><span class="sxs-lookup"><span data-stu-id="4a49a-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="4a49a-131">In questo modo di programma di installazione si hello tooinstall opzione aggiuntive Azure SDK e strumenti da riga di comando dopo l'installazione di hello CLI.</span><span class="sxs-lookup"><span data-stu-id="4a49a-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="4a49a-132">Opzione 3: Usare un contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="4a49a-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="4a49a-133">Se è stato configurato il computer come un [Docker](https://docs.docker.com/engine/understanding-docker/) host, è possibile eseguire hello 1.0 CLI di Azure più recente in un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="4a49a-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="4a49a-134">Esecuzione hello il seguente comando (in distribuzioni di Linux potrebbe essere necessario toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="4a49a-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="4a49a-135">Eseguire i comandi dell'interfaccia della riga di comando 1.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="4a49a-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="4a49a-136">Dopo l'installazione hello Azure CLI 1.0, eseguire hello **azure** comando dall'interfaccia utente della riga di comando (Bash Terminal, il prompt dei comandi e così via).</span><span class="sxs-lookup"><span data-stu-id="4a49a-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="4a49a-137">Ad esempio toorun hello help comando, digitare seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4a49a-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="4a49a-138">In alcune distribuzioni Linux, è possibile che venga visualizzato un messaggio di errore simile troppo`/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="4a49a-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="4a49a-139">Questo errore è causato dalle installazioni recenti di Node.js che vengono installate in /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="4a49a-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="4a49a-140">toofix, creare un collegamento simbolico troppo/usr/bin/nodo eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="4a49a-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="4a49a-141">versione di hello toosee di hello Azure CLI 1.0 è stato installato, hello tipo seguente:</span><span class="sxs-lookup"><span data-stu-id="4a49a-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="4a49a-142">È ora possibile iniziare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4a49a-142">Now you are ready!</span></span> <span data-ttu-id="4a49a-143">tooaccess tutti hello toowork comandi CLI con le risorse, [connettersi tooyour sottoscrizione di Azure da hello Azure CLI](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="4a49a-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4a49a-144">Quando si usa CLI di Azure, viene visualizzato un messaggio che chiede se si desidera tooallow informazioni sull'utilizzo di Microsoft toocollect.</span><span class="sxs-lookup"><span data-stu-id="4a49a-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="4a49a-145">La partecipazione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="4a49a-145">Participation is voluntary.</span></span> <span data-ttu-id="4a49a-146">Se si sceglie tooparticipate, è possibile interrompere in qualsiasi momento eseguendo `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="4a49a-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="4a49a-147">la partecipazione di tooenable in qualsiasi momento, eseguire `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="4a49a-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="4a49a-148">Aggiornare hello CLI</span><span class="sxs-lookup"><span data-stu-id="4a49a-148">Update hello CLI</span></span>
<span data-ttu-id="4a49a-149">Spesso, Microsoft rilascia versioni aggiornate di hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a49a-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="4a49a-150">Reinstallare hello CLI utilizzando Installazione guidata di hello del sistema operativo, oppure eseguire il contenitore Docker più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="4a49a-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="4a49a-151">O, se si hanno hello più recenti di Node.js e npm installati, aggiornare digitando hello segue (in distribuzioni di Linux potrebbe essere necessario toouse **sudo**).</span><span class="sxs-lookup"><span data-stu-id="4a49a-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="4a49a-152">Attivare il completamento con tasto TAB</span><span class="sxs-lookup"><span data-stu-id="4a49a-152">Enable tab completion</span></span>
<span data-ttu-id="4a49a-153">Il completamento con tasto TAB dei comandi dell'interfaccia della riga di comando è supportato per Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="4a49a-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="4a49a-154">tooenable in zsh, eseguire:</span><span class="sxs-lookup"><span data-stu-id="4a49a-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="4a49a-155">tooenable in bash, eseguire:</span><span class="sxs-lookup"><span data-stu-id="4a49a-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="4a49a-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a49a-156">Next steps</span></span>
* <span data-ttu-id="4a49a-157">[Connettersi da hello CLI tooyour sottoscrizione di Azure](xplat-cli-connect.md) toocreate e gestire le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a49a-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="4a49a-158">toolearn ulteriori informazioni su hello CLI di Azure, scaricare il codice sorgente, segnalare i problemi, o collaborazione progetto toohello, visitare hello [repository GitHub per hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="4a49a-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="4a49a-159">In caso di domande sull'utilizzo di hello CLI di Azure o Azure, visitare hello [forum di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="4a49a-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
