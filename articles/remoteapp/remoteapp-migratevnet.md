---
title: toomigrate aaaHow da una rete virtuale di Azure di tooan RemoteApp VNET | Documenti Microsoft
description: Informazioni su come toomigrate da una rete virtuale di Azure di tooan RemoteApp VNET
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a><span data-ttu-id="d9d7a-103">Come una raccolta ibrida da una rete virtuale di Azure di tooan RemoteApp VNET toomigrate</span><span class="sxs-lookup"><span data-stu-id="d9d7a-103">How toomigrate a hybrid collection from a RemoteApp VNET tooan Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d9d7a-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d9d7a-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d9d7a-106">Ottime notizie!</span><span class="sxs-lookup"><span data-stu-id="d9d7a-106">Good news!</span></span> <span data-ttu-id="d9d7a-107">È stata abilitata per le raccolte di RemoteApp ibrida toodeploy direttamente in esistente Azure reti virtuali (Vnet) invece di creare reti virtuali RemoteApp specifiche.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-107">We have enabled you toodeploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="d9d7a-108">Ciò consente di sfruttare i vantaggi di hello ultime funzionalità di rete virtuale (ad esempio ExpressRoute) e concedere l'accesso tooother di ibrida raccolte diretta alla rete servizi di Azure e le macchine virtuali distribuite toothat rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-108">This lets you take advantage of hello latest VNET features (like ExpressRoute) and give your hybrid collections direct network access tooother Azure services and virtual machines deployed toothat VNET.</span></span>  <span data-ttu-id="d9d7a-109">È così possibile migliorare le prestazioni e facilitare l'installazione rispetto alle configurazioni tra reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="d9d7a-110">Si supponga di avere già creato una raccolta RemoteApp ibrida denominata *RaccoltaOriginale* con una rete virtuale RemoteApp denominata *ReteVirtualeRemoteApp*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="d9d7a-111">Di seguito sono toomigrate passaggi hello è tooa nuova rete virtuale di Azure chiamato *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-111">Here are hello steps toomigrate it tooa new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="d9d7a-112">In hello **reti** scheda hello [portale di gestione](http://manage.windowsazure.com/), creare una rete virtuale denominata *AzureVNET*tramite hello nello stesso percorso, la configurazione di DNS e lo spazio degli indirizzi (per almeno di hello *AzureVNET* subnet) come è stato utilizzato per *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-112">On hello **Networks** tab in hello [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using hello same location, DNS configuration, and address space (for at least one of hello *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="d9d7a-113">Configurare *AzureVNET* tooeither host o dispone di connettività di rete toohello distribuzione di Active Directory che *OriginalCollection* appartenga.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-113">Configure *AzureVNET* tooeither host or have network connectivity toohello Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="d9d7a-114">In hello **programmi RemoteApp** scheda, creare una nuova raccolta RemoteApp denominata *nuova raccolta*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-114">On hello **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="d9d7a-115">(Hello utilizzare **Create con una rete virtuale** opzione, non **creazione rapida**.)</span><span class="sxs-lookup"><span data-stu-id="d9d7a-115">(Use hello **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="d9d7a-116">Configurare *NewCollection* toobe distribuito subnet tooa *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-116">Configure *NewCollection* toobe deployed tooa subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="d9d7a-117">Configurare *NewCollection* toouse hello stessa immagine e le informazioni di join di dominio come è stato utilizzato per *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-117">Configure *NewCollection* toouse hello same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="d9d7a-118">Dopo alcune ore, *NuovaRaccolta* verrà visualizzata nell'elenco di raccolte con uno stato attivo.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="d9d7a-119">A questo punto, se non è necessario toomigrate le informazioni utente hello originale raccolta toohello nuova raccolta, eseguire successivamente questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d9d7a-119">Now, if you DON’T need toomigrate any user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="d9d7a-120">Eliminare *RaccoltaOriginale*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="d9d7a-121">Eliminare *ReteVirtualeRemoteApp*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="d9d7a-122">L'operazione è così completata.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-122">And, you’re done!</span></span>

<span data-ttu-id="d9d7a-123">In alternativa, se si richiedono informazioni utente toomigrate hello originale raccolta toohello nuova raccolta, eseguire successivamente questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d9d7a-123">Alternately, if you DO need toomigrate user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="d9d7a-124">Inviare un messaggio di posta elettronica troppo[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) con l'ID sottoscrizione di Azure, hello nome della raccolta originale e hello nome della raccolta di nuovo e chiedere toomigrate le informazioni sull'utente.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-124">Send an email too[remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, hello name of your original collection, and hello name of your new collection, and ask them toomigrate your user information.</span></span>
2. <span data-ttu-id="d9d7a-125">Entro 2 giorni lavorativi team RemoteApp hello sposterà elenco di accesso utente hello e tutti i documenti dell'utente e impostazioni utente da hello originale raccolta toohello nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-125">Within 2 business days hello RemoteApp team will move hello user access list and all user documents and user settings from hello original collection toohello new collection.</span></span>
3. <span data-ttu-id="d9d7a-126">Eliminare *RaccoltaOriginale*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="d9d7a-127">Eliminare *ReteVirtualeRemoteApp*.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="d9d7a-128">L'operazione è così completata.</span><span class="sxs-lookup"><span data-stu-id="d9d7a-128">And now, you’re done!</span></span>

<span data-ttu-id="d9d7a-129">In caso di domande o se è necessaria un'assistenza particolare, inviare un messaggio di posta elettronica a [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="d9d7a-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

