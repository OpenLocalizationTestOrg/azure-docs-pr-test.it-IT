---
title: Panoramica di Azure Cloud Shell (anteprima) | Microsoft Docs
description: Panoramica di Azure Cloud Shell.
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 7165633cd354eeea2e3619f839338e6af1524e56
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="904ee-103">Panoramica di Azure Cloud Shell (anteprima)</span><span class="sxs-lookup"><span data-stu-id="904ee-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="904ee-104">Azure Cloud Shell è una shell interattiva accessibile dal browser per la gestione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="904ee-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="904ee-105">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="904ee-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="904ee-106">Esperienza di shell basata su browser</span><span class="sxs-lookup"><span data-stu-id="904ee-106">Browser-based shell experience</span></span>
<span data-ttu-id="904ee-107">Cloud Shell consente l'accesso a un'esperienza di riga di comando basata su browser realizzata pensando alle attività di gestione di Azure management.</span><span class="sxs-lookup"><span data-stu-id="904ee-107">Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="904ee-108">È possibile sfruttare Cloud Shell per lavorare senza i limiti di un computer locale come solo il cloud può permettere.</span><span class="sxs-lookup"><span data-stu-id="904ee-108">Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="904ee-109">Workstation Azure preconfigurata</span><span class="sxs-lookup"><span data-stu-id="904ee-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="904ee-110">In Cloud Shell sono preinstallati i più diffusi strumenti da riga di comando e il supporto per linguaggi per poter lavorare più velocemente.</span><span class="sxs-lookup"><span data-stu-id="904ee-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="904ee-111">Vedere qui l'elenco completo di strumenti per Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="904ee-111">View the full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="904ee-112">Autenticazione automatica</span><span class="sxs-lookup"><span data-stu-id="904ee-112">Automatic authentication</span></span>
<span data-ttu-id="904ee-113">Cloud Shell esegue automaticamente l'autenticazione sicura a ogni sessione per un accesso immediato alle risorse tramite l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="904ee-113">Cloud Shell securely authenticates automatically on each session for instant access to your resources through the Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="904ee-114">Connettersi ad Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="904ee-114">Connect your Azure File storage</span></span>
<span data-ttu-id="904ee-115">I computer Cloud Shell sono temporanei e quindi è necessario montare una condivisione file di Azure come `clouddrive` per rendere persistente la directory $Home.</span><span class="sxs-lookup"><span data-stu-id="904ee-115">Cloud Shell machines are temporary and as a result require an Azure file share to be mounted as `clouddrive` to persist your $Home directory.</span></span>
<span data-ttu-id="904ee-116">Al primo avvio Cloud Shell chiede di creare un gruppo di risorse, un account di archiviazione e una condivisione file per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="904ee-116">On first launch Cloud Shell prompts to create a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="904ee-117">Questo passaggio è occasionale e verrà automaticamente collegato per tutte le sessioni.</span><span class="sxs-lookup"><span data-stu-id="904ee-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="904ee-118">Creare una nuova risorsa di archiviazione</span><span class="sxs-lookup"><span data-stu-id="904ee-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="904ee-119">Viene creato per conto dell'utente un account di archiviazione con ridondanza locale, ovvero LRS, con una condivisione file di Azure contenente un'immagine del disco da 5 GB.</span><span class="sxs-lookup"><span data-stu-id="904ee-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="904ee-120">La condivisione file viene montata come `clouddrive` per l'interazione della condivisione file stessa con l'immagine del disco utilizzata per sincronizzare e rendere persistente la directory $Home.</span><span class="sxs-lookup"><span data-stu-id="904ee-120">The file share mounts as `clouddrive` for file share interaction with the disk image being used to sync and persist your $Home directory.</span></span> <span data-ttu-id="904ee-121">Vengono applicati i normali costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="904ee-121">Regular storage costs apply.</span></span>

<span data-ttu-id="904ee-122">Verranno create tre risorse per conto dell'utente:</span><span class="sxs-lookup"><span data-stu-id="904ee-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="904ee-123">Gruppo di risorse denominato: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="904ee-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="904ee-124">Account di archiviazione denominato: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="904ee-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="904ee-125">Condivisione file denominata: `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="904ee-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="904ee-126">Tutti i file della directory $Home, come le chiavi SSH, vengono mantenuti nell'immagine del disco utente archiviato nella condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="904ee-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="904ee-127">Applicare le procedure consigliate quando si salvano i file nella directory $Home e nella condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="904ee-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="904ee-128">Usare le risorse esistenti</span><span class="sxs-lookup"><span data-stu-id="904ee-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="904ee-129">Viene data anche un'opzione avanzata che consente di associare le risorse esistenti a Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="904ee-129">An advanced option is also provided allowing you to associate existing resources to Cloud Shell.</span></span> <span data-ttu-id="904ee-130">Quando verrà richiesta l'installazione dell'archiviazione, fare clic su "Mostra impostazioni avanzate" per selezionare le opzioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="904ee-130">When presented with the storage setup prompt, click "Show advanced settings" to select additional options.</span></span> <span data-ttu-id="904ee-131">I menu a discesa vengono filtrati per le aree Cloud Shell assegnate e gli account di archiviazione ridondanti a livello locale o globale.</span><span class="sxs-lookup"><span data-stu-id="904ee-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="904ee-132">[Altre informazioni sull'archiviazione di Cloud Shell, l'aggiornamento delle condivisioni file e il caricamento e download di file.] (persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="904ee-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="904ee-133">Concetti</span><span class="sxs-lookup"><span data-stu-id="904ee-133">Concepts</span></span>
* <span data-ttu-id="904ee-134">Cloud Shell viene eseguito in un computer temporaneo disponibile per ogni sessione e per ogni utente</span><span class="sxs-lookup"><span data-stu-id="904ee-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="904ee-135">Il timeout di Cloud Shell si verifica dopo 20 minuti senza attività interattiva</span><span class="sxs-lookup"><span data-stu-id="904ee-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="904ee-136">Cloud Shell è accessibile solo con una condivisione di file collegata</span><span class="sxs-lookup"><span data-stu-id="904ee-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="904ee-137">A Cloud Shell viene assegnato un computer per ogni account utente</span><span class="sxs-lookup"><span data-stu-id="904ee-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="904ee-138">Vengono impostate le autorizzazioni per un normale utente Linux</span><span class="sxs-lookup"><span data-stu-id="904ee-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="904ee-139">Altre informazioni su tutte le funzionalità Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="904ee-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="904ee-140">esempi</span><span class="sxs-lookup"><span data-stu-id="904ee-140">Examples</span></span>
* <span data-ttu-id="904ee-141">Creare o modificare gli script per automatizzare la gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="904ee-141">Create or edit scripts to automate Azure management</span></span>
* <span data-ttu-id="904ee-142">Gestire le risorse tramite il portale di Azure e l'interfaccia della riga di comando di Azure 2.0 contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="904ee-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="904ee-143">Effettuare il test drive dell'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="904ee-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="904ee-144">Provare tutti questi esempi nella guida introduttiva a Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="904ee-144">Try out all these examples at the Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="904ee-145">Prezzi</span><span class="sxs-lookup"><span data-stu-id="904ee-145">Pricing</span></span>
<span data-ttu-id="904ee-146">Il computer che ospita Cloud Shell è gratuito, con il prerequisito di una condivisione file di Azure montata per rendere persistente la directory $Home.</span><span class="sxs-lookup"><span data-stu-id="904ee-146">The machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share to persist your $Home directory.</span></span> <span data-ttu-id="904ee-147">Vengono applicati i normali costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="904ee-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="904ee-148">Browser supportati</span><span class="sxs-lookup"><span data-stu-id="904ee-148">Supported browsers</span></span>
<span data-ttu-id="904ee-149">Cloud Shell è consigliato per Chrome, Microsoft Edge e Safari.</span><span class="sxs-lookup"><span data-stu-id="904ee-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="904ee-150">Cloud Shell è supportato per Chrome, Firefox, Safari, IE e Microsoft Edge, ma è soggetto a impostazioni specifiche del browser.</span><span class="sxs-lookup"><span data-stu-id="904ee-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject to specific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="904ee-151">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="904ee-151">Troubleshooting</span></span>
1. <span data-ttu-id="904ee-152">Quando si usa una sottoscrizione di Azure Active Directory, non è possibile creare la risorsa di archiviazione a causa dell'errore 400 DisallowedOperation.</span><span class="sxs-lookup"><span data-stu-id="904ee-152">When using an Azure Active Directory subscription, I cannot create storage due to Error: 400 DisallowedOperation.</span></span> <span data-ttu-id="904ee-153">Per risolvere questo problema, usare una sottoscrizione di Azure in grado di creare le risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="904ee-153">To resolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="904ee-154">Le sottoscrizioni di AD non sono in grado di creare le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="904ee-154">AD subscriptions are not able to create Azure resources.</span></span>

<span data-ttu-id="904ee-155">Per le limitazioni note specifiche, vedere le [limitazioni di Cloud Shell](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="904ee-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
