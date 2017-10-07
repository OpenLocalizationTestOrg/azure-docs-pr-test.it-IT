---
title: "funzionalità della Shell di Cloud (anteprima) aaaAzure | Documenti Microsoft"
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
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="24acb-103">Funzionalità e strumenti per Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="24acb-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="24acb-104">Shell Cloud Azure è un toomanage esperienza di shell basata su browser e sviluppare le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="24acb-104">Azure Cloud Shell is a browser-based shell experience toomanage and develop Azure resources.</span></span>

<span data-ttu-id="24acb-105">Cloud Shell offre un browser accessibile, preconfigurato esperienza di shell per la gestione delle risorse di Azure senza il sovraccarico di hello di installazione, il controllo delle versioni e gestire un computer manualmente.</span><span class="sxs-lookup"><span data-stu-id="24acb-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without hello overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="24acb-106">Cloud Shell esegue il provisioning delle macchine sulla base delle richieste e di conseguenza lo stato della macchina non viene mantenuto tra le sessioni.</span><span class="sxs-lookup"><span data-stu-id="24acb-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="24acb-107">Poiché Cloud Shell è pensato per le sessioni interattive, le shell vengono terminate automaticamente dopo 20 minuti di inattività della shell stessa.</span><span class="sxs-lookup"><span data-stu-id="24acb-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="24acb-108">Bash in Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="24acb-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="24acb-109">Strumenti</span><span class="sxs-lookup"><span data-stu-id="24acb-109">Tools</span></span>
|<span data-ttu-id="24acb-110">Categoria</span><span class="sxs-lookup"><span data-stu-id="24acb-110">Category</span></span>   |<span data-ttu-id="24acb-111">Nome</span><span class="sxs-lookup"><span data-stu-id="24acb-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="24acb-112">Interprete shell di Linux</span><span class="sxs-lookup"><span data-stu-id="24acb-112">Linux shell interpreter</span></span>|<span data-ttu-id="24acb-113">Bash</span><span class="sxs-lookup"><span data-stu-id="24acb-113">Bash</span></span><br> <span data-ttu-id="24acb-114">sh</span><span class="sxs-lookup"><span data-stu-id="24acb-114">sh</span></span>               |
|<span data-ttu-id="24acb-115">Strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="24acb-115">Azure tools</span></span>            |<span data-ttu-id="24acb-116">[Interfaccia della riga di comando di Azure 2.0](https://github.com/Azure/azure-cli) e [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="24acb-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="24acb-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="24acb-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="24acb-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="24acb-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="24acb-119">Editor di testo</span><span class="sxs-lookup"><span data-stu-id="24acb-119">Text editors</span></span>           |<span data-ttu-id="24acb-120">vim</span><span class="sxs-lookup"><span data-stu-id="24acb-120">vim</span></span><br> <span data-ttu-id="24acb-121">nano</span><span class="sxs-lookup"><span data-stu-id="24acb-121">nano</span></span><br> <span data-ttu-id="24acb-122">emacs</span><span class="sxs-lookup"><span data-stu-id="24acb-122">emacs</span></span>       |
|<span data-ttu-id="24acb-123">Controllo del codice sorgente</span><span class="sxs-lookup"><span data-stu-id="24acb-123">Source control</span></span>         |<span data-ttu-id="24acb-124">git</span><span class="sxs-lookup"><span data-stu-id="24acb-124">git</span></span>                    |
|<span data-ttu-id="24acb-125">Strumenti di compilazione</span><span class="sxs-lookup"><span data-stu-id="24acb-125">Build tools</span></span>            |<span data-ttu-id="24acb-126">make</span><span class="sxs-lookup"><span data-stu-id="24acb-126">make</span></span><br> <span data-ttu-id="24acb-127">maven</span><span class="sxs-lookup"><span data-stu-id="24acb-127">maven</span></span><br> <span data-ttu-id="24acb-128">npm</span><span class="sxs-lookup"><span data-stu-id="24acb-128">npm</span></span><br> <span data-ttu-id="24acb-129">pip</span><span class="sxs-lookup"><span data-stu-id="24acb-129">pip</span></span>         |
|<span data-ttu-id="24acb-130">Contenitori</span><span class="sxs-lookup"><span data-stu-id="24acb-130">Containers</span></span>             |<span data-ttu-id="24acb-131">[Interfaccia della riga di comando Docker](https://github.com/docker/cli)/[Computer Docker](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="24acb-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="24acb-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="24acb-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="24acb-133">Bozza</span><span class="sxs-lookup"><span data-stu-id="24acb-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="24acb-134">Interfaccia della riga di comando DC/OS</span><span class="sxs-lookup"><span data-stu-id="24acb-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="24acb-135">Database</span><span class="sxs-lookup"><span data-stu-id="24acb-135">Databases</span></span>              |<span data-ttu-id="24acb-136">Client MySQL</span><span class="sxs-lookup"><span data-stu-id="24acb-136">MySQL client</span></span><br> <span data-ttu-id="24acb-137">Client PostgreSql</span><span class="sxs-lookup"><span data-stu-id="24acb-137">PostgreSql client</span></span><br> [<span data-ttu-id="24acb-138">Utilità sqlcmd</span><span class="sxs-lookup"><span data-stu-id="24acb-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="24acb-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="24acb-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="24acb-140">Altre</span><span class="sxs-lookup"><span data-stu-id="24acb-140">Other</span></span>                  |<span data-ttu-id="24acb-141">Client iPython</span><span class="sxs-lookup"><span data-stu-id="24acb-141">iPython Client</span></span><br> [<span data-ttu-id="24acb-142">Interfaccia della riga di comando Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="24acb-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="24acb-143">Supporto per le lingue</span><span class="sxs-lookup"><span data-stu-id="24acb-143">Language support</span></span>
|<span data-ttu-id="24acb-144">Lingua</span><span class="sxs-lookup"><span data-stu-id="24acb-144">Language</span></span>   |<span data-ttu-id="24acb-145">Versione</span><span class="sxs-lookup"><span data-stu-id="24acb-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="24acb-146">.NET</span><span class="sxs-lookup"><span data-stu-id="24acb-146">.NET</span></span>       |<span data-ttu-id="24acb-147">1.01</span><span class="sxs-lookup"><span data-stu-id="24acb-147">1.01</span></span>       |
|<span data-ttu-id="24acb-148">Go</span><span class="sxs-lookup"><span data-stu-id="24acb-148">Go</span></span>         |<span data-ttu-id="24acb-149">1.7</span><span class="sxs-lookup"><span data-stu-id="24acb-149">1.7</span></span>        |
|<span data-ttu-id="24acb-150">Java</span><span class="sxs-lookup"><span data-stu-id="24acb-150">Java</span></span>       |<span data-ttu-id="24acb-151">1.8</span><span class="sxs-lookup"><span data-stu-id="24acb-151">1.8</span></span>        |
|<span data-ttu-id="24acb-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="24acb-152">Node.js</span></span>    |<span data-ttu-id="24acb-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="24acb-153">6.9.4</span></span>      |
|<span data-ttu-id="24acb-154">Python</span><span class="sxs-lookup"><span data-stu-id="24acb-154">Python</span></span>     |<span data-ttu-id="24acb-155">2.7 e 3.5 (impostazione predefinita)</span><span class="sxs-lookup"><span data-stu-id="24acb-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="24acb-156">Autenticazione automatica sicura</span><span class="sxs-lookup"><span data-stu-id="24acb-156">Secure automatic authentication</span></span>
<span data-ttu-id="24acb-157">Shell cloud in modo sicuro e automaticamente autentica account di accesso per hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="24acb-157">Cloud Shell securely and automatically authenticates account access for hello Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="24acb-158">Persistenza di File di Azure</span><span class="sxs-lookup"><span data-stu-id="24acb-158">Azure Files persistence</span></span>
<span data-ttu-id="24acb-159">Poiché Cloud Shell viene allocato su base richiesta usando un computer temporaneo, i file esterni a $Home e lo stato del computer non sono mantenuti tra le sessioni.</span><span class="sxs-lookup"><span data-stu-id="24acb-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="24acb-160">file toopersist tra le sessioni, si interromperanno Shell Cloud tramite l'aggiunta di un file di Azure condividono primo avvio.</span><span class="sxs-lookup"><span data-stu-id="24acb-160">toopersist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="24acb-161">Al termine, Cloud Shell assocerà automaticamente lo spazio di archiviazione per tutte le sessioni future.</span><span class="sxs-lookup"><span data-stu-id="24acb-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="24acb-162">Ulteriori informazioni sul collegamento di condivisioni di file di Azure tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="24acb-162">Learn more about attaching Azure file shares tooCloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="24acb-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="24acb-163">Next steps</span></span>
[<span data-ttu-id="24acb-164">Avvio rapido di Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="24acb-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="24acb-165">
[Informazioni sull'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="24acb-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>