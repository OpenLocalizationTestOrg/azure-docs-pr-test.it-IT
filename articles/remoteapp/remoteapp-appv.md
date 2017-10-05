---
title: Uso delle app App-V in Azure RemoteApp| Microsoft Docs
description: Informazioni sull'uso delle app App-V in Azure RemoteApp.
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
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="981b7-103">Uso delle app App-V in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="981b7-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="981b7-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="981b7-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="981b7-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="981b7-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="981b7-106">È possibile usare le applicazioni App-V in una raccolta ibrida di Azure RemoteApp, che richiede l'aggiunta al dominio.</span><span class="sxs-lookup"><span data-stu-id="981b7-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="981b7-107">Prima di iniziare, assicurarsi di installare il client App-V 5.1 con gli aggiornamenti più recenti.</span><span class="sxs-lookup"><span data-stu-id="981b7-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span></span> <span data-ttu-id="981b7-108">Sarà necessario creare un' [immagine personalizzata](remoteapp-create-custom-image.md) che include il client App-V.</span><span class="sxs-lookup"><span data-stu-id="981b7-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span></span>  

<span data-ttu-id="981b7-109">L'uso dell'infrastruttura App-V esistente con Azure RemoteApp è una procedura semplice.</span><span class="sxs-lookup"><span data-stu-id="981b7-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="981b7-110">Poiché in una rete virtuale di Azure viene distribuita una raccolta ibrida con accesso al controller di dominio e le macchine virtuali vengono aggiunte al dominio, è possibile sfruttare i vantaggi offerti dai metodi di distribuzione e dall'infrastruttura App-V esistenti per ospitare facilmente l'applicazione App-V in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="981b7-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="981b7-111">Di seguito sono riportate alcune considerazioni da tenere presenti in base al tipo di distribuzione di App-V di cui si dispone:</span><span class="sxs-lookup"><span data-stu-id="981b7-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="981b7-112">Opzioni di configurazione</span><span class="sxs-lookup"><span data-stu-id="981b7-112">Configuration options</span></span> |  | <span data-ttu-id="981b7-113">Positive</span><span class="sxs-lookup"><span data-stu-id="981b7-113">Positive</span></span> | <span data-ttu-id="981b7-114">Negative</span><span class="sxs-lookup"><span data-stu-id="981b7-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="981b7-115">Metodo di distribuzione</span><span class="sxs-lookup"><span data-stu-id="981b7-115">Delivery method</span></span> |<span data-ttu-id="981b7-116">Streaming (su richiesta)</span><span class="sxs-lookup"><span data-stu-id="981b7-116">Streaming (on-demand)</span></span> |<span data-ttu-id="981b7-117">App sempre aggiornata</span><span class="sxs-lookup"><span data-stu-id="981b7-117">App is always the latest and fresh</span></span> |<span data-ttu-id="981b7-118">Prima latenza</span><span class="sxs-lookup"><span data-stu-id="981b7-118">First time latency</span></span> |
| <span data-ttu-id="981b7-119">Montato</span><span class="sxs-lookup"><span data-stu-id="981b7-119">Mounted</span></span> |<span data-ttu-id="981b7-120">Più rapido. App già presente nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="981b7-120">Fastest; app is already present on the VM</span></span> |<span data-ttu-id="981b7-121">Bloat: occupa lo spazio dell'immagine (limite di 127 GB)</span><span class="sxs-lookup"><span data-stu-id="981b7-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="981b7-122">Archiviazione percorso app</span><span class="sxs-lookup"><span data-stu-id="981b7-122">App location storage</span></span> |<span data-ttu-id="981b7-123">Contenuto condiviso</span><span class="sxs-lookup"><span data-stu-id="981b7-123">Shared content</span></span> |<span data-ttu-id="981b7-124">App eseguita nella memoria dell'istanza di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="981b7-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="981b7-125">Usa la memoria e una buona connessione al server (file) di streaming in cui si trova l'app</span><span class="sxs-lookup"><span data-stu-id="981b7-125">Eats memory and good connection to streaming (file) server where the app resides</span></span> |
| <span data-ttu-id="981b7-126">Disco (memorizzato nella cache)</span><span class="sxs-lookup"><span data-stu-id="981b7-126">Disk (Cached)</span></span> |<span data-ttu-id="981b7-127">Esecuzione rapida.</span><span class="sxs-lookup"><span data-stu-id="981b7-127">Fast execution.</span></span> <span data-ttu-id="981b7-128">Applicazione non dipende dalla disponibilità dell'origine del contenuto</span><span class="sxs-lookup"><span data-stu-id="981b7-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="981b7-129">Bloat: occupa lo spazio dell'immagine (limite di 127 GB)</span><span class="sxs-lookup"><span data-stu-id="981b7-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="981b7-130">Destinazione</span><span class="sxs-lookup"><span data-stu-id="981b7-130">Targeting</span></span> |<span data-ttu-id="981b7-131">Utente</span><span class="sxs-lookup"><span data-stu-id="981b7-131">User</span></span> |<span data-ttu-id="981b7-132">Richiede un'infrastruttura App-V autonoma completa</span><span class="sxs-lookup"><span data-stu-id="981b7-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="981b7-133">Globale (computer)</span><span class="sxs-lookup"><span data-stu-id="981b7-133">Global (machine)</span></span> |<span data-ttu-id="981b7-134">Prepubblicazione o destinazione mediante server di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="981b7-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="981b7-135">Se si desidera aggiornare l'app (di grandi dimensioni), è necessario aggiornare l'immagine di Azure.</span><span class="sxs-lookup"><span data-stu-id="981b7-135">Need to update your Azure image if you want to update the app (huge).</span></span> <span data-ttu-id="981b7-136">Occupa spazio nell'immagine.</span><span class="sxs-lookup"><span data-stu-id="981b7-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="981b7-137">Dopo aver creato l'immagine personalizzata e la raccolta ibrida, è possibile pubblicare l'applicazione, assegnare gli utenti e usare le applicazioni App-V esistenti ospitate in Azure RemoteApp distribuite a qualsiasi dispositivo e in qualsiasi luogo.</span><span class="sxs-lookup"><span data-stu-id="981b7-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span></span>

