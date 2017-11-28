---
title: gli utenti di tooindividual applicazioni aaaPublish in una raccolta RemoteApp di Azure (anteprima) | Documenti Microsoft
description: "Informazioni su come pubblicare gli utenti tooindividual App, anziché in base a gruppi, in Azure RemoteApp."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="ea01a-103">Pubblicare gli utenti tooindividual applicazioni in una raccolta RemoteApp di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="ea01a-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ea01a-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="ea01a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ea01a-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="ea01a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ea01a-106">Questo articolo viene illustrato come gli utenti di tooindividual applicazioni toopublish in una raccolta di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ea01a-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="ea01a-107">Questa è una nuova funzionalità in Azure RemoteApp, attualmente in anteprima privata e adottato disponibili tooselect solo a scopo di valutazione.</span><span class="sxs-lookup"><span data-stu-id="ea01a-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="ea01a-108">Origine RemoteApp di Azure abilitata solo una modalità di pubblicazione di applicazioni: amministratore hello pubblicare le app dall'immagine hello e saranno visibili tooall utenti nella raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="ea01a-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="ea01a-109">Uno scenario comune è tooinclude molte applicazioni in una singola immagine e la distribuzione dei costi di gestione tooreduce di ordine di una raccolta.</span><span class="sxs-lookup"><span data-stu-id="ea01a-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="ea01a-110">Spesso non tutte le applicazioni sono rilevanti tooall utenti: gli amministratori preferisce agli utenti di tooindividual App toopublish in modo non visualizzano le applicazioni non necessarie nella propria applicazione feed.</span><span class="sxs-lookup"><span data-stu-id="ea01a-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="ea01a-111">Questa operazione è ora possibile in Azure RemoteApp, attualmente disponibile come funzionalità in anteprima limitata.</span><span class="sxs-lookup"><span data-stu-id="ea01a-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="ea01a-112">Ecco un breve riepilogo delle nuove funzionalità di hello:</span><span class="sxs-lookup"><span data-stu-id="ea01a-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="ea01a-113">È possibile impostare una delle due modalità seguenti per una raccolta:</span><span class="sxs-lookup"><span data-stu-id="ea01a-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="ea01a-114">Hello originale modalità di raccolta, in cui è possono visualizzare tutti gli utenti in una raccolta di applicazioni pubblicate tutte.</span><span class="sxs-lookup"><span data-stu-id="ea01a-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="ea01a-115">Questa è una modalità predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="ea01a-115">This is hello default mode.</span></span>
   * <span data-ttu-id="ea01a-116">modalità applicazione nuova Hello, in cui gli utenti visualizzano solo le applicazioni che sono state assegnate esplicitamente toothem</span><span class="sxs-lookup"><span data-stu-id="ea01a-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="ea01a-117">Un determinato momento hello modalità applicazione hello può essere abilitata solo tramite i cmdlet PowerShell di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ea01a-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="ea01a-118">Impostare la modalità di tooapplication, assegnazione di utente nella raccolta di hello quando non può essere gestita tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea01a-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="ea01a-119">Assegnazione utente ha toobe gestite tramite cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea01a-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="ea01a-120">Gli utenti visualizzeranno solo le applicazioni di hello pubblicate direttamente toothem.</span><span class="sxs-lookup"><span data-stu-id="ea01a-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="ea01a-121">Tuttavia, è comunque possibile per un utente toolaunch hello altre applicazioni disponibili sull'immagine di hello accedendovi direttamente nel sistema operativo di hello.</span><span class="sxs-lookup"><span data-stu-id="ea01a-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="ea01a-122">Questa funzionalità non fornisce un blocco di protezione delle applicazioni. Limita solo la visibilità in un'applicazione hello feed.</span><span class="sxs-lookup"><span data-stu-id="ea01a-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="ea01a-123">Se è necessario tooisolate utenti dalle applicazioni, è necessario raccolte separate toouse a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="ea01a-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="ea01a-124">Come tooget cmdlet PowerShell di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ea01a-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="ea01a-125">tootry hello nuove funzionalità di anteprima, sarà necessario toouse cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea01a-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ea01a-126">Non è attualmente possibile toouse hello Azure tooenable portale hello nuova applicazione pubblicazione modalità di gestione.</span><span class="sxs-lookup"><span data-stu-id="ea01a-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="ea01a-127">In primo luogo, accertarsi di avere hello [modulo Azure PowerShell](/powershell/azure/overview) installato.</span><span class="sxs-lookup"><span data-stu-id="ea01a-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="ea01a-128">Avviare console di PowerShell hello in modalità amministratore e hello esecuzione seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ea01a-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="ea01a-129">Verranno richiesti il nome utente e la password di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea01a-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="ea01a-130">Una volta effettuato l'accesso, sarà in grado di toorun i cmdlet di Azure RemoteApp contro le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea01a-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="ea01a-131">Come toocheck quale modalità è in una raccolta</span><span class="sxs-lookup"><span data-stu-id="ea01a-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="ea01a-132">Eseguire hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ea01a-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Verificare la modalità di raccolta hello](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="ea01a-134">proprietà AclLevel Hello può avere hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="ea01a-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="ea01a-135">Raccolta: hello pubblicazione modalità originale.</span><span class="sxs-lookup"><span data-stu-id="ea01a-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="ea01a-136">Tutti gli utenti vedono tutte le app pubblicate.</span><span class="sxs-lookup"><span data-stu-id="ea01a-136">All users see all published apps.</span></span>
* <span data-ttu-id="ea01a-137">Dell'applicazione: modalità hello nuova pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="ea01a-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="ea01a-138">Gli utenti vedono solo le app hello pubblicato direttamente toothem.</span><span class="sxs-lookup"><span data-stu-id="ea01a-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="ea01a-139">La modalità di pubblicazione tooapplication tooswitch</span><span class="sxs-lookup"><span data-stu-id="ea01a-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="ea01a-140">Eseguire hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ea01a-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="ea01a-141">Stato di pubblicazione dell'applicazione verrà mantenuto: inizialmente tutti gli utenti visualizzino tutte le app pubblicate di hello originale.</span><span class="sxs-lookup"><span data-stu-id="ea01a-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="ea01a-142">Come gli utenti toolist chi possono visualizzare un'applicazione specifica</span><span class="sxs-lookup"><span data-stu-id="ea01a-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="ea01a-143">Eseguire hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ea01a-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="ea01a-144">Elenca tutti gli utenti possono vedere applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ea01a-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="ea01a-145">Nota: È possibile visualizzare gli alias dell'applicazione hello (denominati "alias app" nella sintassi hello) tramite l'esecuzione di Get-AzureRemoteAppProgram - NomeRaccolta <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="ea01a-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="ea01a-146">Come un utente dell'applicazione tooa tooassign</span><span class="sxs-lookup"><span data-stu-id="ea01a-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="ea01a-147">Eseguire hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ea01a-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="ea01a-148">utente Hello visualizzata applicazione hello nel client di Azure RemoteApp hello e sarà in grado di tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="ea01a-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="ea01a-149">Come tooremove un'applicazione da un utente</span><span class="sxs-lookup"><span data-stu-id="ea01a-149">How tooremove an application from a user</span></span>
<span data-ttu-id="ea01a-150">Eseguire hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ea01a-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="ea01a-151">Inviare commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ea01a-151">Providing feedback</span></span>
<span data-ttu-id="ea01a-152">Siamo lieti di ricevere commenti e suggerimenti su questa funzionalità in anteprima.</span><span class="sxs-lookup"><span data-stu-id="ea01a-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="ea01a-153">Compilare hello [sondaggio](http://www.instant.ly/s/FDdrb) toolet ci sapere cosa ne pensi.</span><span class="sxs-lookup"><span data-stu-id="ea01a-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="ea01a-154">Non ho avuto una funzionalità di anteprima di probabilità tootry hello?</span><span class="sxs-lookup"><span data-stu-id="ea01a-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="ea01a-155">Se non hanno partecipato in anteprima hello ancora, utilizzare questo [sondaggio](http://www.instant.ly/s/AY83p) toorequest accesso.</span><span class="sxs-lookup"><span data-stu-id="ea01a-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

