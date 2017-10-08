---
title: hello aaaUsing CLI di Azure in Windows | Documenti Microsoft
description: Usa hello CLI di Azure in Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="db733-103">Usa hello CLI di Azure in Windows</span><span class="sxs-lookup"><span data-stu-id="db733-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="db733-104">Hello interfaccia della riga di comando (CLI) di Azure fornisce una riga di comando e l'ambiente di scripting per la creazione e la gestione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="db733-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="db733-105">Hello CLI di Azure è disponibile per i sistemi operativi Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="db733-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="db733-106">In questi sistemi operativi, i comandi CLI hello sono identici, tuttavia la sintassi di scripting specifici del sistema operativo può essere diverso.</span><span class="sxs-lookup"><span data-stu-id="db733-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="db733-107">Questa modalità di hello dettagli documento hello CLI di Azure può essere installato ed eseguito in Windows e i dettagli requisiti sintattici per ognuno.</span><span class="sxs-lookup"><span data-stu-id="db733-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="db733-108">Per la documentazione dettagliata sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="db733-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="db733-109">Sottosistema di Windows per Linux</span><span class="sxs-lookup"><span data-stu-id="db733-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="db733-110">Hello sottosistema Windows per Linux (WSL) offre un ambiente Ubuntu Linux su anniversario di Windows 10 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="db733-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="db733-111">Quando abilitato, WSL offre un'esperienza Bash nativa, che può essere usata per la creazione e l'esecuzione di script dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="db733-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="db733-112">Dal momento che WSL fornisce un'esperienza Bash nativa, gli script dell'interfaccia della riga di comando di Azure possono essere condivisi tra macOS, Linux e Windows senza alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="db733-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="db733-113">hello toouse CLI di Azure in WSL, completare i seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="db733-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="db733-114">Attività</span><span class="sxs-lookup"><span data-stu-id="db733-114">Task</span></span> | <span data-ttu-id="db733-115">Istruzioni</span><span class="sxs-lookup"><span data-stu-id="db733-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="db733-116">Abilitare WLS</span><span class="sxs-lookup"><span data-stu-id="db733-116">Enable WSL</span></span> | [<span data-ttu-id="db733-117">Documentazione sull'installazione di WSL</span><span class="sxs-lookup"><span data-stu-id="db733-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="db733-118">Installare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="db733-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="db733-119">Installare hello CLI in WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="db733-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="db733-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="db733-120">PowerShell</span></span>

<span data-ttu-id="db733-121">Hello CLI di Azure può essere eseguito in modo nativo in Windows.</span><span class="sxs-lookup"><span data-stu-id="db733-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="db733-122">In questa configurazione, hello CLI di Azure viene installato nel sistema operativo di Windows hello e comandi possono essere eseguiti da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db733-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="db733-123">In questa configurazione, gli script e i comandi dell'interfaccia della riga di comando di Azure sono eseguibili in qualsiasi versione di Windows supportata. È tuttavia necessaria la sintassi di scripting specifica della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="db733-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="db733-124">Per questo motivo, gli script non devono necessariamente essere condivisi tra macOS, Linux e Windows senza modifiche.</span><span class="sxs-lookup"><span data-stu-id="db733-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="db733-125">hello toouse CLI di Azure in Windows, installare il pacchetto di hello usando queste istruzioni, [installazione hello CLI in Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="db733-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="db733-126">Immagine Docker</span><span class="sxs-lookup"><span data-stu-id="db733-126">Docker Image</span></span>

<span data-ttu-id="db733-127">Quando si usa Docker per Windows, può essere avviata un'immagine Docker che include hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="db733-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="db733-128">Questa immagine si basa su Linux e include un'esperienza Bash nativa.</span><span class="sxs-lookup"><span data-stu-id="db733-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="db733-129">Quando si usa Docker per Windows e l'immagine di hello CLI di Azure, toobe script condivisi tra macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="db733-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="db733-130">hello toouse CLI di Azure per Docker per Windows, assicurarsi che Docker per Windows e l'esecuzione hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="db733-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="db733-131">Una volta completato, un Bash sessione inizierà ovvero precaricato con gli strumenti di hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="db733-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db733-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="db733-132">Next Steps</span></span>

[<span data-ttu-id="db733-133">Esempio di interfaccia della riga di comando per macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="db733-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="db733-134">Esempi di interfaccia della riga di comando per App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="db733-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="db733-135">Esempi di interfaccia della riga di comando per Azure SQL</span><span class="sxs-lookup"><span data-stu-id="db733-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
