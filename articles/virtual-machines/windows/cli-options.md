---
title: Uso dell'interfaccia della riga di comando di Azure su Windows | Documentazione Microsoft
description: Uso dell'interfaccia della riga di comando di Azure su Windows
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
ms.openlocfilehash: be02ad0d7752cb08f092deeb5a86dcd126403237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-on-windows"></a><span data-ttu-id="2ed6c-103">Uso dell'interfaccia della riga di comando di Azure su Windows</span><span class="sxs-lookup"><span data-stu-id="2ed6c-103">Using the Azure CLI on Windows</span></span>

<span data-ttu-id="2ed6c-104">L'interfaccia della riga di comando di Azure (CLI) fornisce una riga di comando e l'ambiente di scripting per la creazione e la gestione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-104">The Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="2ed6c-105">L'interfaccia della riga di comando di Azure è disponibile per i sistemi operativi macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-105">The Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="2ed6c-106">In questi sistemi operativi i comandi dell'interfaccia della riga di comando sono identici. Tuttavia, la sintassi di scripting specifica del sistema operativo può differire.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-106">Across these operating systems, the CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="2ed6c-107">Questo documento descrive le modalità di installazione ed esecuzione dell'interfaccia della riga di comando di Azure in Windows, nonché le considerazioni sulla sintassi specifica del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-107">This document details the ways that the Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="2ed6c-108">Per la documentazione dettagliata sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2ed6c-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="2ed6c-109">Sottosistema di Windows per Linux</span><span class="sxs-lookup"><span data-stu-id="2ed6c-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="2ed6c-110">Il Sottosistema Windows per Linux (WSL) fornisce un ambiente Ubuntu Linux nell'edizione anniversario di Windows 10 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-110">The Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="2ed6c-111">Quando abilitato, WSL offre un'esperienza Bash nativa, che può essere usata per la creazione e l'esecuzione di script dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="2ed6c-112">Dal momento che WSL fornisce un'esperienza Bash nativa, gli script dell'interfaccia della riga di comando di Azure possono essere condivisi tra macOS, Linux e Windows senza alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="2ed6c-113">Per usare l'interfaccia della riga di comando di Azure in WSL, completare le operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-113">To use the Azure CLI in WSL, complete the following.</span></span>

|<span data-ttu-id="2ed6c-114">Attività</span><span class="sxs-lookup"><span data-stu-id="2ed6c-114">Task</span></span> | <span data-ttu-id="2ed6c-115">Istruzioni</span><span class="sxs-lookup"><span data-stu-id="2ed6c-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="2ed6c-116">Abilitare WLS</span><span class="sxs-lookup"><span data-stu-id="2ed6c-116">Enable WSL</span></span> | [<span data-ttu-id="2ed6c-117">Documentazione sull'installazione di WSL</span><span class="sxs-lookup"><span data-stu-id="2ed6c-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="2ed6c-118">Installare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2ed6c-118">Install the Azure CLI</span></span> |[<span data-ttu-id="2ed6c-119">Installare l'interfaccia della riga di comando su WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="2ed6c-119">Install the CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="2ed6c-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ed6c-120">PowerShell</span></span>

<span data-ttu-id="2ed6c-121">L'interfaccia della riga di comando di Azure può essere eseguita in modo nativo in Windows.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-121">The Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="2ed6c-122">In questa configurazione, il pacchetto dell'interfaccia della riga di comando di Azure è installato nel sistema operativo Windows e i comandi possono essere eseguiti da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-122">In this configuration, the Azure CLI package is installed on the Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="2ed6c-123">In questa configurazione, gli script e i comandi dell'interfaccia della riga di comando di Azure sono eseguibili in qualsiasi versione di Windows supportata. È tuttavia necessaria la sintassi di scripting specifica della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="2ed6c-124">Per questo motivo, gli script non devono necessariamente essere condivisi tra macOS, Linux e Windows senza modifiche.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="2ed6c-125">Per usare l'interfaccia della riga di comando di Azure in Windows, installare il pacchetto tramite le istruzioni contenute in [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows) (Installare l'interfaccia della riga di comando su Windows).</span><span class="sxs-lookup"><span data-stu-id="2ed6c-125">To use the Azure CLI on Windows, install the package using these instructions, [Install the CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="2ed6c-126">Immagine Docker</span><span class="sxs-lookup"><span data-stu-id="2ed6c-126">Docker Image</span></span>

<span data-ttu-id="2ed6c-127">Quando si usa Docker per Windows, è possibile avviare un'immagine Docker che include l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-127">When using Docker for Windows, a Docker image can be started that includes the Azure CLI.</span></span> <span data-ttu-id="2ed6c-128">Questa immagine si basa su Linux e include un'esperienza Bash nativa.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="2ed6c-129">Quando si usa Docker per Windows e per l'immagine dell'interfaccia della riga di comando di Azure, gli script devono essere condivisi tra macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-129">When using Docker for Windows and the Azure CLI image, scripts to be shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="2ed6c-130">Per usare l'interfaccia della riga di comando di Azure in Docker per Windows, verificare che Docker per Windows sia in esecuzione ed esegua il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-130">To use the Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run the following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="2ed6c-131">Al termine, verrà avviata una sessione Bash precaricata con gli strumenti dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ed6c-131">Once completed, a Bash session will start that is preloaded with the Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ed6c-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ed6c-132">Next Steps</span></span>

[<span data-ttu-id="2ed6c-133">Esempio di interfaccia della riga di comando per macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="2ed6c-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="2ed6c-134">Esempi di interfaccia della riga di comando per App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="2ed6c-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="2ed6c-135">Esempi di interfaccia della riga di comando per Azure SQL</span><span class="sxs-lookup"><span data-stu-id="2ed6c-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
