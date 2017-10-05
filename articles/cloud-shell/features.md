---
title: "Funzionalità di Azure Cloud Shell (anteprima) | Documentazione Microsoft"
description: "Panoramica delle funzionalità di Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="21d1e-103">Funzionalità e strumenti per Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="21d1e-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="21d1e-104">Azure Cloud Shell è un'esperienza shell basata su browser per gestire e sviluppare risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="21d1e-104">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span>

<span data-ttu-id="21d1e-105">Cloud Shell offre un'esperienza shell preconfigurata accessibile tramite browser per la gestione delle risorse di Azure senza l'onere di dover installare, controllare le versioni e mantenere un computer manualmente.</span><span class="sxs-lookup"><span data-stu-id="21d1e-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="21d1e-106">Cloud Shell esegue il provisioning delle macchine sulla base delle richieste e di conseguenza lo stato della macchina non viene mantenuto tra le sessioni.</span><span class="sxs-lookup"><span data-stu-id="21d1e-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="21d1e-107">Poiché Cloud Shell è pensato per le sessioni interattive, le shell vengono terminate automaticamente dopo 20 minuti di inattività della shell stessa.</span><span class="sxs-lookup"><span data-stu-id="21d1e-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="21d1e-108">Bash in Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="21d1e-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="21d1e-109">Strumenti</span><span class="sxs-lookup"><span data-stu-id="21d1e-109">Tools</span></span>
|<span data-ttu-id="21d1e-110">Categoria</span><span class="sxs-lookup"><span data-stu-id="21d1e-110">Category</span></span>   |<span data-ttu-id="21d1e-111">Nome</span><span class="sxs-lookup"><span data-stu-id="21d1e-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="21d1e-112">Interprete shell di Linux</span><span class="sxs-lookup"><span data-stu-id="21d1e-112">Linux shell interpreter</span></span>|<span data-ttu-id="21d1e-113">Bash</span><span class="sxs-lookup"><span data-stu-id="21d1e-113">Bash</span></span><br> <span data-ttu-id="21d1e-114">sh</span><span class="sxs-lookup"><span data-stu-id="21d1e-114">sh</span></span>               |
|<span data-ttu-id="21d1e-115">Strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="21d1e-115">Azure tools</span></span>            |<span data-ttu-id="21d1e-116">[Interfaccia della riga di comando di Azure 2.0](https://github.com/Azure/azure-cli) e [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="21d1e-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="21d1e-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="21d1e-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="21d1e-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="21d1e-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="21d1e-119">Editor di testo</span><span class="sxs-lookup"><span data-stu-id="21d1e-119">Text editors</span></span>           |<span data-ttu-id="21d1e-120">vim</span><span class="sxs-lookup"><span data-stu-id="21d1e-120">vim</span></span><br> <span data-ttu-id="21d1e-121">nano</span><span class="sxs-lookup"><span data-stu-id="21d1e-121">nano</span></span><br> <span data-ttu-id="21d1e-122">emacs</span><span class="sxs-lookup"><span data-stu-id="21d1e-122">emacs</span></span>       |
|<span data-ttu-id="21d1e-123">Controllo del codice sorgente</span><span class="sxs-lookup"><span data-stu-id="21d1e-123">Source control</span></span>         |<span data-ttu-id="21d1e-124">git</span><span class="sxs-lookup"><span data-stu-id="21d1e-124">git</span></span>                    |
|<span data-ttu-id="21d1e-125">Strumenti di compilazione</span><span class="sxs-lookup"><span data-stu-id="21d1e-125">Build tools</span></span>            |<span data-ttu-id="21d1e-126">make</span><span class="sxs-lookup"><span data-stu-id="21d1e-126">make</span></span><br> <span data-ttu-id="21d1e-127">maven</span><span class="sxs-lookup"><span data-stu-id="21d1e-127">maven</span></span><br> <span data-ttu-id="21d1e-128">npm</span><span class="sxs-lookup"><span data-stu-id="21d1e-128">npm</span></span><br> <span data-ttu-id="21d1e-129">pip</span><span class="sxs-lookup"><span data-stu-id="21d1e-129">pip</span></span>         |
|<span data-ttu-id="21d1e-130">Contenitori</span><span class="sxs-lookup"><span data-stu-id="21d1e-130">Containers</span></span>             |<span data-ttu-id="21d1e-131">[Interfaccia della riga di comando Docker](https://github.com/docker/cli)/[Computer Docker](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="21d1e-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="21d1e-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="21d1e-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="21d1e-133">Bozza</span><span class="sxs-lookup"><span data-stu-id="21d1e-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="21d1e-134">Interfaccia della riga di comando DC/OS</span><span class="sxs-lookup"><span data-stu-id="21d1e-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="21d1e-135">Database</span><span class="sxs-lookup"><span data-stu-id="21d1e-135">Databases</span></span>              |<span data-ttu-id="21d1e-136">Client MySQL</span><span class="sxs-lookup"><span data-stu-id="21d1e-136">MySQL client</span></span><br> <span data-ttu-id="21d1e-137">Client PostgreSql</span><span class="sxs-lookup"><span data-stu-id="21d1e-137">PostgreSql client</span></span><br> [<span data-ttu-id="21d1e-138">Utilità sqlcmd</span><span class="sxs-lookup"><span data-stu-id="21d1e-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="21d1e-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="21d1e-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="21d1e-140">Altre</span><span class="sxs-lookup"><span data-stu-id="21d1e-140">Other</span></span>                  |<span data-ttu-id="21d1e-141">Client iPython</span><span class="sxs-lookup"><span data-stu-id="21d1e-141">iPython Client</span></span><br> [<span data-ttu-id="21d1e-142">Interfaccia della riga di comando Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="21d1e-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="21d1e-143">Supporto per le lingue</span><span class="sxs-lookup"><span data-stu-id="21d1e-143">Language support</span></span>
|<span data-ttu-id="21d1e-144">Lingua</span><span class="sxs-lookup"><span data-stu-id="21d1e-144">Language</span></span>   |<span data-ttu-id="21d1e-145">Versione</span><span class="sxs-lookup"><span data-stu-id="21d1e-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="21d1e-146">.NET</span><span class="sxs-lookup"><span data-stu-id="21d1e-146">.NET</span></span>       |<span data-ttu-id="21d1e-147">1.01</span><span class="sxs-lookup"><span data-stu-id="21d1e-147">1.01</span></span>       |
|<span data-ttu-id="21d1e-148">Go</span><span class="sxs-lookup"><span data-stu-id="21d1e-148">Go</span></span>         |<span data-ttu-id="21d1e-149">1.7</span><span class="sxs-lookup"><span data-stu-id="21d1e-149">1.7</span></span>        |
|<span data-ttu-id="21d1e-150">Java</span><span class="sxs-lookup"><span data-stu-id="21d1e-150">Java</span></span>       |<span data-ttu-id="21d1e-151">1.8</span><span class="sxs-lookup"><span data-stu-id="21d1e-151">1.8</span></span>        |
|<span data-ttu-id="21d1e-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="21d1e-152">Node.js</span></span>    |<span data-ttu-id="21d1e-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="21d1e-153">6.9.4</span></span>      |
|<span data-ttu-id="21d1e-154">Python</span><span class="sxs-lookup"><span data-stu-id="21d1e-154">Python</span></span>     |<span data-ttu-id="21d1e-155">2.7 e 3.5 (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="21d1e-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="21d1e-156">Autenticazione automatica sicura</span><span class="sxs-lookup"><span data-stu-id="21d1e-156">Secure automatic authentication</span></span>
<span data-ttu-id="21d1e-157">Cloud Shell autentica in modo sicuro e automatico l'accesso agli account per l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="21d1e-157">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="21d1e-158">Persistenza di File di Azure</span><span class="sxs-lookup"><span data-stu-id="21d1e-158">Azure Files persistence</span></span>
<span data-ttu-id="21d1e-159">Poiché Cloud Shell viene allocato su base richiesta usando un computer temporaneo, i file esterni a $Home e lo stato del computer non sono mantenuti tra le sessioni.</span><span class="sxs-lookup"><span data-stu-id="21d1e-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="21d1e-160">Per rendere persistenti i file fra le sessioni, Cloud Shell illustra come associare una condivisione file di Azure al primo avvio.</span><span class="sxs-lookup"><span data-stu-id="21d1e-160">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="21d1e-161">Al termine, Cloud Shell assocerà automaticamente lo spazio di archiviazione per tutte le sessioni future.</span><span class="sxs-lookup"><span data-stu-id="21d1e-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

<span data-ttu-id="21d1e-162">[Altre informazioni sul collegamento delle condivisioni di file di Azure a Cloud Shell](persisting-shell-storage.md).</span><span class="sxs-lookup"><span data-stu-id="21d1e-162">[Learn more about attaching Azure file shares to Cloud Shell.](persisting-shell-storage.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="21d1e-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21d1e-163">Next steps</span></span>
[<span data-ttu-id="21d1e-164">Avvio rapido di Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="21d1e-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="21d1e-165">
[Informazioni sull'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="21d1e-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>