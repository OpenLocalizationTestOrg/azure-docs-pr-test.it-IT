---
title: Pubblicare applicazioni per singoli utenti in una raccolta di Azure RemoteApp (anteprima) | Documentazione Microsoft
description: Informazioni su come pubblicare app per i singoli utenti, invece di basarsi sui gruppi, in Azure RemoteApp.
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
ms.openlocfilehash: c94ffffdec3e46ed08d941ee58dcf17b432e1dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="publish-applications-to-individual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="91205-103">Pubblicare applicazioni per singoli utenti in una raccolta di Azure RemoteApp (anteprima)</span><span class="sxs-lookup"><span data-stu-id="91205-103">Publish applications to individual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="91205-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="91205-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="91205-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="91205-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="91205-106">Questo articolo illustra come pubblicare applicazioni per singoli utenti in una raccolta di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="91205-106">This article explains how to publish applications to individual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="91205-107">Si tratta di una nuova funzionalità di Azure RemoteApp, attualmente disponibile in anteprima privata e solo per alcuni utenti selezionati per finalità di valutazione.</span><span class="sxs-lookup"><span data-stu-id="91205-107">This is new functionality in Azure RemoteApp, currently in private preview and available only to select early adopters for evaluation purposes.</span></span>

<span data-ttu-id="91205-108">In origine Azure RemoteApp consentiva solo un modo per pubblicare le applicazioni: l'amministratore pubblicava le app dall'immagine e le app risultavano visibili a tutti gli utenti della raccolta.</span><span class="sxs-lookup"><span data-stu-id="91205-108">Originally Azure RemoteApp enabled only one way of publishing applications: the administrator would publish apps from the image and they would be visible to all users in the collection.</span></span>

<span data-ttu-id="91205-109">Uno scenario comune consiste nell'includere molte applicazioni in una singola immagine e distribuire una sola raccolta per ridurre i costi di gestione.</span><span class="sxs-lookup"><span data-stu-id="91205-109">A common scenario is to include many applications in a single image and deploy one collection in order to reduce management costs.</span></span> <span data-ttu-id="91205-110">Spesso non tutte le applicazioni sono rilevanti per tutti gli utenti. Gli amministratori preferirebbero pubblicare app per i singoli utenti, in modo che gli utenti non vedano applicazioni non necessari nei rispettivi feed dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="91205-110">Oftentimes not all applications are relevant to all users – administrators would prefer to publish apps to individual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="91205-111">Questa operazione è ora possibile in Azure RemoteApp, attualmente disponibile come funzionalità in anteprima limitata.</span><span class="sxs-lookup"><span data-stu-id="91205-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="91205-112">Ecco un breve riepilogo della nuova funzionalità:</span><span class="sxs-lookup"><span data-stu-id="91205-112">Here is a brief summary of the new functionality:</span></span>

1. <span data-ttu-id="91205-113">È possibile impostare una delle due modalità seguenti per una raccolta:</span><span class="sxs-lookup"><span data-stu-id="91205-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="91205-114">La modalità raccolta originale, in cui tutti gli utenti di una raccolta possono visualizzare tutte le applicazioni pubblicate.</span><span class="sxs-lookup"><span data-stu-id="91205-114">the original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="91205-115">Si tratta della modalità predefinita.</span><span class="sxs-lookup"><span data-stu-id="91205-115">This is the default mode.</span></span>
   * <span data-ttu-id="91205-116">La nuova modalità applicazione, in cui gli utenti possono visualizzare solo le applicazioni assegnate in modo esplicito a loro.</span><span class="sxs-lookup"><span data-stu-id="91205-116">the new application mode, where users only see applications that have been explicitly assigned to them</span></span>
2. <span data-ttu-id="91205-117">In questo momento è possibile abilitare la modalità applicazione solo usando i cmdlet di PowerShell di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="91205-117">At the moment the application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="91205-118">Se viene abilitata la modalità applicazione, l'assegnazione utente nella raccolta non può essere gestita tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="91205-118">When set to application mode, user assignment in the collection cannot be managed through the Azure portal.</span></span> <span data-ttu-id="91205-119">L'assegnazione utente deve essere gestita tramite cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91205-119">User assignment has to be managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="91205-120">Gli utenti potranno visualizzare solo le applicazioni pubblicate direttamente per loro.</span><span class="sxs-lookup"><span data-stu-id="91205-120">Users will only see the applications published directly to them.</span></span> <span data-ttu-id="91205-121">Un utente potrà comunque avviare le altre applicazioni disponibili nell'immagine accedendo direttamente alle applicazioni nel sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="91205-121">However, it may still be possible for a user to launch the other applications available on the image by accessing them directly in the operating system.</span></span>
   
   * <span data-ttu-id="91205-122">Questa funzionalità non offre un blocco sicuro delle applicazioni. Limita solo la visibilità nel feed dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="91205-122">This feature does not provide a secure lockdown of applications; it only limits visibility in the application feed.</span></span>
   * <span data-ttu-id="91205-123">Se è necessario isolare utenti dalle applicazioni, occorrerà usare raccolte separate.</span><span class="sxs-lookup"><span data-stu-id="91205-123">If you need to isolate users from applications, you will need to use separate collections for that.</span></span>

## <a name="how-to-get-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="91205-124">Come ottenere i cmdlet di PowerShell di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="91205-124">How to get Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="91205-125">Per provare la nuova funzionalità in anteprima, è necessario usare i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91205-125">To try the new preview functionality, you will need to use Azure PowerShell cmdlets.</span></span> <span data-ttu-id="91205-126">Non è attualmente possibile usare il portale di gestione di Azure per abilitare la nuova modalità di pubblicazione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="91205-126">It is currently not possible to use the Azure Management portal to enable the new application publishing mode.</span></span>

<span data-ttu-id="91205-127">Assicurarsi prima di tutto che il [modulo Azure PowerShell](/powershell/azure/overview) sia installato.</span><span class="sxs-lookup"><span data-stu-id="91205-127">First, make sure you have the [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="91205-128">Avviare quindi la console di PowerShell in modalità amministratore ed eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="91205-128">Then launch the PowerShell console in administrator mode and run the following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="91205-129">Verranno richiesti il nome utente e la password di Azure.</span><span class="sxs-lookup"><span data-stu-id="91205-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="91205-130">Dopo l'accesso, sarà possibile eseguire i cmdlet di Azure RemoteApp con le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="91205-130">Once signed in, you will be able to run Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-to-check-which-mode-a-collection-is-in"></a><span data-ttu-id="91205-131">Come verificare la modalità di una raccolta</span><span class="sxs-lookup"><span data-stu-id="91205-131">How to check which mode a collection is in</span></span>
<span data-ttu-id="91205-132">Eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="91205-132">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Verificare la modalità raccolta](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="91205-134">La proprietà AclLevel può avere i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="91205-134">The AclLevel property can have the following values:</span></span>

* <span data-ttu-id="91205-135">Collection: modalità di pubblicazione originale.</span><span class="sxs-lookup"><span data-stu-id="91205-135">Collection: the original publishing mode.</span></span> <span data-ttu-id="91205-136">Tutti gli utenti vedono tutte le app pubblicate.</span><span class="sxs-lookup"><span data-stu-id="91205-136">All users see all published apps.</span></span>
* <span data-ttu-id="91205-137">Application: nuova modalità di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="91205-137">Application: the new publishing mode.</span></span> <span data-ttu-id="91205-138">Gli utenti vedono solo le app pubblicate direttamente per loro.</span><span class="sxs-lookup"><span data-stu-id="91205-138">Users see only the apps published directly to them.</span></span>

## <a name="how-to-switch-to-application-publishing-mode"></a><span data-ttu-id="91205-139">Come cambiare la modalità di pubblicazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="91205-139">How to switch to application publishing mode</span></span>
<span data-ttu-id="91205-140">Eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="91205-140">Run the following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="91205-141">Lo stato di pubblicazione dell'applicazione verrà conservato. Inizialmente tutti gli utenti vedranno tutte le app pubblicate in origine.</span><span class="sxs-lookup"><span data-stu-id="91205-141">Application publishing state will be preserved: initially all users will see all of the original published apps.</span></span>

## <a name="how-to-list-users-who-can-see-a-specific-application"></a><span data-ttu-id="91205-142">Come elencare utenti che possono vedere un'applicazione specifica</span><span class="sxs-lookup"><span data-stu-id="91205-142">How to list users who can see a specific application</span></span>
<span data-ttu-id="91205-143">Eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="91205-143">Run the following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="91205-144">Vengono elencati tutti gli utenti che possono vedere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="91205-144">This lists all users who can see the application.</span></span>

<span data-ttu-id="91205-145">Nota: è possibile vedere gli alias dell'applicazione, definiti "alias app" nella sintassi precedente, eseguendo Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="91205-145">Note: You can see the application aliases (called "app alias" in the syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-to-assign-an-application-to-a-user"></a><span data-ttu-id="91205-146">Come assegnare un'applicazione a un utente</span><span class="sxs-lookup"><span data-stu-id="91205-146">How to assign an application to a user</span></span>
<span data-ttu-id="91205-147">Eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="91205-147">Run the following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="91205-148">L'utente potrà ora vedere l'applicazione nel client Azure RemoteApp e potrà connettersi all'app.</span><span class="sxs-lookup"><span data-stu-id="91205-148">The user will now see the application in the Azure RemoteApp client and will be able to connect to it.</span></span>

## <a name="how-to-remove-an-application-from-a-user"></a><span data-ttu-id="91205-149">Come rimuovere un'applicazione da un utente</span><span class="sxs-lookup"><span data-stu-id="91205-149">How to remove an application from a user</span></span>
<span data-ttu-id="91205-150">Eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="91205-150">Run the following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="91205-151">Inviare commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="91205-151">Providing feedback</span></span>
<span data-ttu-id="91205-152">Siamo lieti di ricevere commenti e suggerimenti su questa funzionalità in anteprima.</span><span class="sxs-lookup"><span data-stu-id="91205-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="91205-153">Compilare il [sondaggio](http://www.instant.ly/s/FDdrb) per condividere la propria opinione.</span><span class="sxs-lookup"><span data-stu-id="91205-153">Please fill out the [survey](http://www.instant.ly/s/FDdrb) to let us know what you think.</span></span>

## <a name="havent-had-a-chance-to-try-the-preview-feature"></a><span data-ttu-id="91205-154">Se non è stato possibile provare la funzionalità in anteprima</span><span class="sxs-lookup"><span data-stu-id="91205-154">Haven't had a chance to try the preview feature?</span></span>
<span data-ttu-id="91205-155">Se non si è ancora autorizzati a provare l'anteprima, usare questo [sondaggio](http://www.instant.ly/s/AY83p) per richiedere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="91205-155">If you have not participated in the preview yet, please use this [survey](http://www.instant.ly/s/AY83p) to request access.</span></span>

