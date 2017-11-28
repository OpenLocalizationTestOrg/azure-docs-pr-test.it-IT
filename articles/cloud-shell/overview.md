---
title: Panoramica di aaaAzure Cloud Shell (anteprima) | Documenti Microsoft
description: Panoramica di hello Shell di Cloud di Azure.
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
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="9081e-103">Panoramica di Azure Cloud Shell (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9081e-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="9081e-104">Azure Cloud Shell è una shell interattiva accessibile dal browser per la gestione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9081e-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="9081e-105">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="9081e-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="9081e-106">Esperienza di shell basata su browser</span><span class="sxs-lookup"><span data-stu-id="9081e-106">Browser-based shell experience</span></span>
<span data-ttu-id="9081e-107">Cloud Shell Abilita tooa basate su browser della riga di comando l'esperienza di accesso compilato con le attività di gestione di Azure presente.</span><span class="sxs-lookup"><span data-stu-id="9081e-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="9081e-108">Sfruttare toowork Shell Cloud illimitata da un computer locale in modo che solo i cloud hello può fornire.</span><span class="sxs-lookup"><span data-stu-id="9081e-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="9081e-109">Workstation Azure preconfigurata</span><span class="sxs-lookup"><span data-stu-id="9081e-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="9081e-110">In Cloud Shell sono preinstallati i più diffusi strumenti da riga di comando e il supporto per linguaggi per poter lavorare più velocemente.</span><span class="sxs-lookup"><span data-stu-id="9081e-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="9081e-111">Visualizzazione hello completo di strumenti elenco per Shell di Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="9081e-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="9081e-112">Autenticazione automatica</span><span class="sxs-lookup"><span data-stu-id="9081e-112">Automatic authentication</span></span>
<span data-ttu-id="9081e-113">Shell cloud in modo sicuro autentica automaticamente in ogni sessione per le risorse tooyour accesso immediato tramite hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="9081e-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="9081e-114">Connettersi ad Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="9081e-114">Connect your Azure File storage</span></span>
<span data-ttu-id="9081e-115">Cloud Shell macchine sono temporanee e pertanto richiedono un toobe di condivisione file di Azure montata come `clouddrive` toopersist $Home directory.</span><span class="sxs-lookup"><span data-stu-id="9081e-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="9081e-116">Primo avvio della Shell Cloud richiede toocreate che un gruppo di risorse, account di archiviazione e della condivisione file per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9081e-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="9081e-117">Questo passaggio è occasionale e verrà automaticamente collegato per tutte le sessioni.</span><span class="sxs-lookup"><span data-stu-id="9081e-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="9081e-118">Creare una nuova risorsa di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9081e-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="9081e-119">Viene creato per conto dell'utente un account di archiviazione con ridondanza locale, ovvero LRS, con una condivisione file di Azure contenente un'immagine del disco da 5 GB.</span><span class="sxs-lookup"><span data-stu-id="9081e-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="9081e-120">condivisione di file Hello collega come `clouddrive` per file condividono l'interazione con l'immagine del disco hello viene utilizzato toosync e mantenere la directory $Home.</span><span class="sxs-lookup"><span data-stu-id="9081e-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="9081e-121">Vengono applicati i normali costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9081e-121">Regular storage costs apply.</span></span>

<span data-ttu-id="9081e-122">Verranno create tre risorse per conto dell'utente:</span><span class="sxs-lookup"><span data-stu-id="9081e-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="9081e-123">Gruppo di risorse denominato: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="9081e-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="9081e-124">Account di archiviazione denominato: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="9081e-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="9081e-125">Condivisione file denominata: `cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="9081e-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="9081e-126">Tutti i file della directory $Home, come le chiavi SSH, vengono mantenuti nell'immagine del disco utente archiviato nella condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="9081e-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="9081e-127">Applicare le procedure consigliate quando si salvano i file nella directory $Home e nella condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="9081e-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="9081e-128">Usare le risorse esistenti</span><span class="sxs-lookup"><span data-stu-id="9081e-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="9081e-129">Un'opzione avanzata viene inoltre fornita per consentire di tooassociate esistente risorse tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="9081e-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="9081e-130">Quando verrà visualizzata con richiesta di installazione di hello archiviazione, fare clic su "Show advanced settings" tooselect ulteriori opzioni.</span><span class="sxs-lookup"><span data-stu-id="9081e-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="9081e-131">I menu a discesa vengono filtrati per le aree Cloud Shell assegnate e gli account di archiviazione ridondanti a livello locale o globale.</span><span class="sxs-lookup"><span data-stu-id="9081e-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="9081e-132">[Altre informazioni sull'archiviazione di Cloud Shell, l'aggiornamento delle condivisioni file e il caricamento e download di file.] (persisting-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="9081e-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="9081e-133">Concetti</span><span class="sxs-lookup"><span data-stu-id="9081e-133">Concepts</span></span>
* <span data-ttu-id="9081e-134">Cloud Shell viene eseguito in un computer temporaneo disponibile per ogni sessione e per ogni utente</span><span class="sxs-lookup"><span data-stu-id="9081e-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="9081e-135">Il timeout di Cloud Shell si verifica dopo 20 minuti senza attività interattiva</span><span class="sxs-lookup"><span data-stu-id="9081e-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="9081e-136">Cloud Shell è accessibile solo con una condivisione di file collegata</span><span class="sxs-lookup"><span data-stu-id="9081e-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="9081e-137">A Cloud Shell viene assegnato un computer per ogni account utente</span><span class="sxs-lookup"><span data-stu-id="9081e-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="9081e-138">Vengono impostate le autorizzazioni per un normale utente Linux</span><span class="sxs-lookup"><span data-stu-id="9081e-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="9081e-139">Altre informazioni su tutte le funzionalità Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="9081e-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="9081e-140">esempi</span><span class="sxs-lookup"><span data-stu-id="9081e-140">Examples</span></span>
* <span data-ttu-id="9081e-141">Creare o modificare gli script tooautomate gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="9081e-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="9081e-142">Gestire le risorse tramite il portale di Azure e l'interfaccia della riga di comando di Azure 2.0 contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="9081e-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="9081e-143">Effettuare il test drive dell'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9081e-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="9081e-144">Provare questi esempi in avvio rapido di hello Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="9081e-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="9081e-145">Prezzi</span><span class="sxs-lookup"><span data-stu-id="9081e-145">Pricing</span></span>
<span data-ttu-id="9081e-146">macchina Hello Shell Cloud di hosting è disponibile, con un prerequisito di un file di Azure montato condividere toopersist $Home directory.</span><span class="sxs-lookup"><span data-stu-id="9081e-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="9081e-147">Vengono applicati i normali costi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9081e-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="9081e-148">Browser supportati</span><span class="sxs-lookup"><span data-stu-id="9081e-148">Supported browsers</span></span>
<span data-ttu-id="9081e-149">Cloud Shell è consigliato per Chrome, Microsoft Edge e Safari.</span><span class="sxs-lookup"><span data-stu-id="9081e-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="9081e-150">Sebbene Shell Cloud è supportata per Chrome, Firefox, Safari, Internet Explorer e bordo, Cloud Shell è le impostazioni del browser toospecific soggetto.</span><span class="sxs-lookup"><span data-stu-id="9081e-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9081e-151">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9081e-151">Troubleshooting</span></span>
1. <span data-ttu-id="9081e-152">Quando si utilizza una sottoscrizione di Azure Active Directory, non è possibile creare Archiviazione scadenza tooError: DisallowedOperation 400.</span><span class="sxs-lookup"><span data-stu-id="9081e-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="9081e-153">tooresolve, utilizzare una sottoscrizione di Azure in grado di creare le risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9081e-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="9081e-154">Le sottoscrizioni di Active Directory è toocreate non in grado di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9081e-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="9081e-155">Per le limitazioni note specifiche, vedere le [limitazioni di Cloud Shell](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9081e-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
