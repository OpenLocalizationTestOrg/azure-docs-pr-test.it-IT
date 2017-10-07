---
title: App aaaUsing App-V con Azure RemoteApp | Documenti Microsoft
description: Informazioni su come App toouse App-V in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="0e5c7-103">Uso delle app App-V in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0e5c7-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0e5c7-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0e5c7-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0e5c7-106">È possibile usare le applicazioni App-V in una raccolta ibrida di Azure RemoteApp, che richiede l'aggiunta al dominio.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="0e5c7-107">Prima di iniziare, verificare che client di App-V 5.1 hello tooinstall con gli aggiornamenti più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="0e5c7-108">Sarà necessario toocreate un [immagine personalizzata](remoteapp-create-custom-image.md) che include il client App-V hello.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="0e5c7-109">È facile toouse infrastruttura App-V esistente con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="0e5c7-110">Poiché una raccolta ibrida è distribuita in una rete virtuale di Azure con controller di dominio di accesso tooyour e le macchine virtuali hello vengono aggiunti a un dominio, è possibile usare App-v dell'infrastruttura e la distribuzione metodi tooeasyily host App-V applicazione esistente in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="0e5c7-111">Di seguito sono riportate alcune considerazioni che è necessario tenere in base al tipo di hello della distribuzione di App-V che è installata:</span><span class="sxs-lookup"><span data-stu-id="0e5c7-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="0e5c7-112">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="0e5c7-112">Configuration options</span></span> |  | <span data-ttu-id="0e5c7-113">Positive</span><span class="sxs-lookup"><span data-stu-id="0e5c7-113">Positive</span></span> | <span data-ttu-id="0e5c7-114">Negative</span><span class="sxs-lookup"><span data-stu-id="0e5c7-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0e5c7-115">Metodo di distribuzione</span><span class="sxs-lookup"><span data-stu-id="0e5c7-115">Delivery method</span></span> |<span data-ttu-id="0e5c7-116">Streaming (su richiesta)</span><span class="sxs-lookup"><span data-stu-id="0e5c7-116">Streaming (on-demand)</span></span> |<span data-ttu-id="0e5c7-117">App è sempre hello nuova e più recente</span><span class="sxs-lookup"><span data-stu-id="0e5c7-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="0e5c7-118">Prima latenza</span><span class="sxs-lookup"><span data-stu-id="0e5c7-118">First time latency</span></span> |
| <span data-ttu-id="0e5c7-119">Montato</span><span class="sxs-lookup"><span data-stu-id="0e5c7-119">Mounted</span></span> |<span data-ttu-id="0e5c7-120">Più veloce; App è già presente nel hello VM</span><span class="sxs-lookup"><span data-stu-id="0e5c7-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="0e5c7-121">Bloat: occupa lo spazio dell'immagine (limite di 127 GB)</span><span class="sxs-lookup"><span data-stu-id="0e5c7-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="0e5c7-122">Archiviazione percorso app</span><span class="sxs-lookup"><span data-stu-id="0e5c7-122">App location storage</span></span> |<span data-ttu-id="0e5c7-123">Contenuto condiviso</span><span class="sxs-lookup"><span data-stu-id="0e5c7-123">Shared content</span></span> |<span data-ttu-id="0e5c7-124">App eseguita nella memoria dell'istanza di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0e5c7-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="0e5c7-125">Mostro memoria e il server di collegamento toostreaming (file) in cui risiede l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="0e5c7-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="0e5c7-126">Disco (memorizzato nella cache)</span><span class="sxs-lookup"><span data-stu-id="0e5c7-126">Disk (Cached)</span></span> |<span data-ttu-id="0e5c7-127">Esecuzione rapida.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-127">Fast execution.</span></span> <span data-ttu-id="0e5c7-128">Applicazione non dipende dalla disponibilità dell'origine del contenuto</span><span class="sxs-lookup"><span data-stu-id="0e5c7-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="0e5c7-129">Bloat: occupa lo spazio dell'immagine (limite di 127 GB)</span><span class="sxs-lookup"><span data-stu-id="0e5c7-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="0e5c7-130">Destinazione</span><span class="sxs-lookup"><span data-stu-id="0e5c7-130">Targeting</span></span> |<span data-ttu-id="0e5c7-131">Utente</span><span class="sxs-lookup"><span data-stu-id="0e5c7-131">User</span></span> |<span data-ttu-id="0e5c7-132">Richiede un'infrastruttura App-V autonoma completa</span><span class="sxs-lookup"><span data-stu-id="0e5c7-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="0e5c7-133">Globale (computer)</span><span class="sxs-lookup"><span data-stu-id="0e5c7-133">Global (machine)</span></span> |<span data-ttu-id="0e5c7-134">Prepubblicazione o destinazione mediante server di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="0e5c7-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="0e5c7-135">Necessario tooupdate l'immagine di Azure, se si desidera app hello tooupdate (grande).</span><span class="sxs-lookup"><span data-stu-id="0e5c7-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="0e5c7-136">Occupa spazio nell'immagine.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="0e5c7-137">Dopo aver creato l'immagine personalizzata e la raccolta ibrida, pubblicare l'applicazione, assegnare gli utenti e sfruttare le applicazioni App-V esistenti ospitate in Azure RemoteApp recapitati tooany dispositivo ovunque.</span><span class="sxs-lookup"><span data-stu-id="0e5c7-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

