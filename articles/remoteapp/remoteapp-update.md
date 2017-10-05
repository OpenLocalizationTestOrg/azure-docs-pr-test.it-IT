---
title: Aggiornare la raccolta di Azure RemoteApp | Microsoft Docs
description: Informazioni su come aggiornare la raccolta di Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 454d78445d6092aec9eaa383e4c50cf15195848c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="e7549-103">Aggiornare una raccolta in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e7549-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e7549-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="e7549-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e7549-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="e7549-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e7549-106">Ad un certo punto sarà necessario, inevitabilmente, aggiornare le app o l’immagine nella raccolta di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e7549-106">There will come a time, inevitably, when you need to update the apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="e7549-107">Se si usa una delle immagini incluse nella sottoscrizione di Azure RemoteApp, in una raccolta cloud o ibrida, tutti gli aggiornamenti vengono gestiti automaticamente da Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e7549-107">If you are using one of the images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="e7549-108">Tuttavia, se si utilizza un'immagine personalizzata (che è stata compilata da zero o creata modificando une delle immagini disponibili), si è responsabili della manutenzione dell'immagine e delle app.</span><span class="sxs-lookup"><span data-stu-id="e7549-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining the image and apps.</span></span> <span data-ttu-id="e7549-109">Se è necessario aggiornare l'immagine o una qualsiasi delle app all'interno, è necessario creare una nuova versione aggiornata dell'immagine e quindi sostituire l'immagine esistente nella raccolta con la nuova immagine aggiornata.</span><span class="sxs-lookup"><span data-stu-id="e7549-109">If you need to update your image or any of the apps inside it, you need to create a new, updated version of the image, and then replace the existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="e7549-110">Quindi, come si esegue l'aggiornamento della raccolta?</span><span class="sxs-lookup"><span data-stu-id="e7549-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="e7549-111">È piuttosto semplice:</span><span class="sxs-lookup"><span data-stu-id="e7549-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="e7549-112">Aggiornare l'immagine utilizzata nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="e7549-112">Update the image that you used in your collection.</span></span> <span data-ttu-id="e7549-113">Applicare le patch o gli aggiornamenti necessari e quindi salvarla con un nuovo nome.</span><span class="sxs-lookup"><span data-stu-id="e7549-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="e7549-114">[Caricare](remoteapp-uploadimage.md) o [importare](remoteapp-image-on-azurevm.md) l'immagine in RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e7549-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image to RemoteApp.</span></span>
3. <span data-ttu-id="e7549-115">A questo punto, nella pagina della raccolta, fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="e7549-115">Now, on the collection page, click **Update**.</span></span>
4. <span data-ttu-id="e7549-116">Scegliere la nuova immagine dall’elenco **Immagine modello** .</span><span class="sxs-lookup"><span data-stu-id="e7549-116">Choose the new image from the **Template Image** list.</span></span>
5. <span data-ttu-id="e7549-117">Questa è la parte più complicata, è necessario decidere come gestire gli utenti che utilizzano attualmente un'app della raccolta.</span><span class="sxs-lookup"><span data-stu-id="e7549-117">Here's the tricky part - you need to decide how to deal with any users that are currently using an app in the collection.</span></span> <span data-ttu-id="e7549-118">L'utente ha a disposizione le seguenti opzioni:</span><span class="sxs-lookup"><span data-stu-id="e7549-118">You have the following choices:</span></span>
   
   * <span data-ttu-id="e7549-119">**Concedere agli utenti 60 minuti dopo l'aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="e7549-119">**Give users 60 minutes after the update**.</span></span> <span data-ttu-id="e7549-120">Non appena completato l'aggiornamento, in Azure RemoteApp viene visualizzato un messaggio con cui viene richiesto a tutti gli utenti attivi di salvare il lavoro, disconnettersi e accedere di nuovo.</span><span class="sxs-lookup"><span data-stu-id="e7549-120">As soon as the update is finished, Azure RemoteApp will display a message to any active users telling them to save their work and log off and log back in.</span></span> <span data-ttu-id="e7549-121">Dopo 60 minuti, tutti gli utenti attivi che non si sono disconnessi vengono disconnessi automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e7549-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="e7549-122">Gli utenti possono accedere di nuovo immediatamente.</span><span class="sxs-lookup"><span data-stu-id="e7549-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="e7549-123">**Disconnettere gli utenti immediatamente**.</span><span class="sxs-lookup"><span data-stu-id="e7549-123">**Sign users out immediately**.</span></span> <span data-ttu-id="e7549-124">Non appena completato l'aggiornamento, disconnettere tutti gli utenti automaticamente senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="e7549-124">As soon as the update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="e7549-125">Se si sceglie questa opzione, gli utenti potrebbero perdere i dati.</span><span class="sxs-lookup"><span data-stu-id="e7549-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="e7549-126">Tuttavia, possano riconnettersi all'app immediatamente.</span><span class="sxs-lookup"><span data-stu-id="e7549-126">However, they can reconnect to the app immediately.</span></span>
6. <span data-ttu-id="e7549-127">Fare clic sul segno di spunta per avviare l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e7549-127">Click the check mark to start the update.</span></span>

