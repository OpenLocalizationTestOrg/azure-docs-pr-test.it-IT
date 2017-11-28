---
title: aaaUpdate la raccolta RemoteApp di Azure | Documenti Microsoft
description: Informazioni su come tooupdate raccolta di Azure RemoteApp
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
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="e3916-103">Aggiornare una raccolta in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e3916-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e3916-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="e3916-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e3916-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="e3916-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e3916-106">Non esiste, verrà un'ora, inevitabilmente, quando è necessario tooupdate hello App o l'immagine nella raccolta di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e3916-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="e3916-107">Se si utilizza una delle immagini hello incluse con la sottoscrizione di Azure RemoteApp, insieme a un cloud o ibrida, che tutti gli aggiornamenti vengono gestiti da Azure RemoteApp, pertanto è possibile posizionare semplice.</span><span class="sxs-lookup"><span data-stu-id="e3916-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="e3916-108">Tuttavia, se si utilizza un'immagine personalizzata (che è stato generato da zero o creato mediante la modifica di uno dei nostri immagini), è responsabile della gestione di App e l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="e3916-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="e3916-109">Se è necessario tooupdate un'immagine o una qualsiasi delle App hello in essa contenuti, è necessario toocreate una nuova versione aggiornata dell'immagine di hello e quindi sostituire hello esistente immagine nella raccolta con la nuova immagine aggiornata.</span><span class="sxs-lookup"><span data-stu-id="e3916-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="e3916-110">Quindi, come si esegue l'aggiornamento della raccolta?</span><span class="sxs-lookup"><span data-stu-id="e3916-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="e3916-111">È piuttosto semplice:</span><span class="sxs-lookup"><span data-stu-id="e3916-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="e3916-112">Aggiornare l'immagine di hello utilizzati nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="e3916-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="e3916-113">Applicare le patch o gli aggiornamenti necessari e quindi salvarla con un nuovo nome.</span><span class="sxs-lookup"><span data-stu-id="e3916-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="e3916-114">[Caricare](remoteapp-uploadimage.md) o [importare](remoteapp-image-on-azurevm.md) tooRemoteApp tale immagine.</span><span class="sxs-lookup"><span data-stu-id="e3916-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="e3916-115">A questo punto, nella pagina insieme hello, fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="e3916-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="e3916-116">Scegliere nuova immagine hello hello **immagine modello** elenco.</span><span class="sxs-lookup"><span data-stu-id="e3916-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="e3916-117">Di seguito è la parte più impegnativa hello, è necessario toodecide come toodeal con tutti gli utenti che attualmente utilizzano un'app nella raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="e3916-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="e3916-118">È necessario hello opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3916-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="e3916-119">**Concedi agli utenti 60 minuti dopo l'aggiornamento di hello**.</span><span class="sxs-lookup"><span data-stu-id="e3916-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="e3916-120">Non appena hello aggiornamento è completato, Azure RemoteApp verrà visualizzato un messaggio tooany gli utenti attivi informa toosave loro lavoro e log off e accedere di nuovo.</span><span class="sxs-lookup"><span data-stu-id="e3916-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="e3916-121">Dopo 60 minuti, tutti gli utenti attivi che non si sono disconnessi vengono disconnessi automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e3916-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="e3916-122">Gli utenti possono accedere di nuovo immediatamente.</span><span class="sxs-lookup"><span data-stu-id="e3916-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="e3916-123">**Disconnettere gli utenti immediatamente**.</span><span class="sxs-lookup"><span data-stu-id="e3916-123">**Sign users out immediately**.</span></span> <span data-ttu-id="e3916-124">Non appena hello aggiornamento è completato, disconnettersi da tutti gli utenti automaticamente senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="e3916-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="e3916-125">Se si sceglie questa opzione, gli utenti potrebbero perdere i dati.</span><span class="sxs-lookup"><span data-stu-id="e3916-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="e3916-126">Tuttavia, possono comunque riconnettersi app toohello immediatamente.</span><span class="sxs-lookup"><span data-stu-id="e3916-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="e3916-127">Fare clic su hello segno di spunta toostart hello aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e3916-127">Click hello check mark toostart hello update.</span></span>

