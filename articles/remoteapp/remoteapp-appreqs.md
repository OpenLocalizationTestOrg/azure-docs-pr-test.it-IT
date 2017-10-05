---
title: Requisiti per le app di Azure RemoteApp | Documentazione Microsoft
description: Informazioni sui requisiti per le app che si desidera usare in Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 13d42df97ea2b090180f5865a4eac25945f9f34c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="app-requirements"></a><span data-ttu-id="5de6f-103">Requisiti delle app</span><span class="sxs-lookup"><span data-stu-id="5de6f-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5de6f-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="5de6f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5de6f-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="5de6f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5de6f-106">Azure RemoteApp supporta applicazioni basate su Windows a 32 bit o a 64 bit in streaming Windows da un'immagine di Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="5de6f-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="5de6f-107">La maggior parte delle applicazioni basate su Windows a 32 bit o a 64 bit vengono eseguite "così come sono" in un ambiente Azure RemoteApp (Servizi Desktop remoto, in precedenza noti come Servizi terminal).</span><span class="sxs-lookup"><span data-stu-id="5de6f-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="5de6f-108">Tuttavia, esiste una differenza tra esecuzione e corretta esecuzione: alcune applicazioni funzionano correttamente e offrono buone prestazioni, mentre altre no.</span><span class="sxs-lookup"><span data-stu-id="5de6f-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="5de6f-109">Le informazioni seguenti forniscono indicazioni per lo sviluppo di applicazioni in un ambiente di Servizi Desktop remoto e l'esecuzione di test per garantire la compatibilità.</span><span class="sxs-lookup"><span data-stu-id="5de6f-109">The following information provides guidance for developing applications in a Remote Desktop Services environment and testing to ensure compatibility.</span></span>

<span data-ttu-id="5de6f-110">Suggerimento: è in corso la creazione di alcuni esempi di app per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="5de6f-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="5de6f-111">Verranno pubblicati altri argomenti sull'uso di Microsoft Access, QuickBooks e App-V in RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5de6f-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="5de6f-112">Requisiti</span><span class="sxs-lookup"><span data-stu-id="5de6f-112">Requirements</span></span>
<span data-ttu-id="5de6f-113">Questi tre requisiti, se seguiti, contribuiscono a una corretta esecuzione dell'applicazione in RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="5de6f-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="5de6f-114">Le applicazioni che soddisfano tutti i [requisiti di certificazione per le app desktop di Windows](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) e sono conformi alle [linee guida di programmazione dei Servizi Desktop remoto](https://msdn.microsoft.com/library/aa383490.aspx) saranno totalmente compatibili con RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5de6f-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere to [Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="5de6f-115">Le applicazioni non devono mai archiviare dati localmente nell'immagine o nelle istanze di RemoteApp che possono essere perse.</span><span class="sxs-lookup"><span data-stu-id="5de6f-115">Applications should never store data locally on the image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="5de6f-116">Dopo aver creato una raccolta di RemoteApp, le istanze vengono clonate e sono senza stato; inoltre, devono contenere solo applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5de6f-116">After you create a RemoteApp collection, the instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="5de6f-117">Archiviare i dati in un'origine esterna o all'interno del profilo utente.</span><span class="sxs-lookup"><span data-stu-id="5de6f-117">Store data in an external source or within the user's profile.</span></span>
3. <span data-ttu-id="5de6f-118">Le immagini personalizzate non devono mai contenere dati che possono essere persi.</span><span class="sxs-lookup"><span data-stu-id="5de6f-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="5de6f-119">Test delle app</span><span class="sxs-lookup"><span data-stu-id="5de6f-119">Testing your apps</span></span>
<span data-ttu-id="5de6f-120">Usare questa procedura per eseguire il test delle applicazioni:</span><span class="sxs-lookup"><span data-stu-id="5de6f-120">Use these steps to testing applications:</span></span>

1. <span data-ttu-id="5de6f-121">Installare Windows Server 2012 R2 e l'applicazione</span><span class="sxs-lookup"><span data-stu-id="5de6f-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="5de6f-122">Abilitare Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="5de6f-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="5de6f-123">Creare due account utente, Utente A e Utente B, aggiungendo entrambi gli account utente al gruppo di sicurezza di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="5de6f-123">Create two user accounts, UserA and UserB, adding both user accounts to the Remote Desktop security group.</span></span>
4. <span data-ttu-id="5de6f-124">Verificare la compatibilità multisessione stabilendo due sessioni di Servizi Desktop remoto simultanee al PC durante l'avvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5de6f-124">Check multi-session compatibility by establishing two simultaneous RDS sessions to the PC while launching the application.</span></span>
5. <span data-ttu-id="5de6f-125">Convalidare il comportamento dell'app</span><span class="sxs-lookup"><span data-stu-id="5de6f-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="5de6f-126">Linee guida sullo sviluppo di applicazioni</span><span class="sxs-lookup"><span data-stu-id="5de6f-126">Application development guidelines</span></span>
<span data-ttu-id="5de6f-127">Usare le linee guida seguenti per lo sviluppo di applicazioni per RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5de6f-127">Use the following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="5de6f-128">Più utenti</span><span class="sxs-lookup"><span data-stu-id="5de6f-128">Multiple users</span></span>
* <span data-ttu-id="5de6f-129">L'installazione di un' [applicazione per un singolo utente ](https://msdn.microsoft.com/library/aa380661.aspx)può creare problemi in un ambiente multiutente.</span><span class="sxs-lookup"><span data-stu-id="5de6f-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="5de6f-130">Le applicazioni devono [archiviare le informazioni specifiche dell'utente](https://msdn.microsoft.com/library/aa383452.aspx) in percorsi specifici dell'utente, separatamente da informazioni globali che si applicano a tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="5de6f-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies to all users.</span></span>
* <span data-ttu-id="5de6f-131">RemoteApp usa più [spazi dei nomi per gli oggetti del kernel](https://msdn.microsoft.com/library/aa382954.aspx); uno spazio dei nomi globale viene usato principalmente dai servizi nelle applicazioni client/server.</span><span class="sxs-lookup"><span data-stu-id="5de6f-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="5de6f-132">Non è opportuno presupporre che il nome del computer o l' [indirizzo IP](https://msdn.microsoft.com/library/aa382942.aspx) assegnato al computer sia associato a un singolo utente poiché più utenti possono accedere contemporaneamente a un server Host sessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="5de6f-132">It is not safe to assume that the computer name or the [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned to the computer are associated with a single user because multiple users can be logged on simultaneously to a Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="5de6f-133">Prestazioni</span><span class="sxs-lookup"><span data-stu-id="5de6f-133">Performance</span></span>
* <span data-ttu-id="5de6f-134">Disabilitare gli [effetti grafici](https://msdn.microsoft.com/library/aa380822.aspx) prima di aggiungere l'app a RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="5de6f-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app to RemoteApp.</span></span>
* <span data-ttu-id="5de6f-135">Per ottimizzare la disponibilità della CPU per tutti gli utenti, disabilitare le [attività in background ](https://msdn.microsoft.com/library/aa380665.aspx) o creare attività in background efficienti che non richiedano molte risorse.</span><span class="sxs-lookup"><span data-stu-id="5de6f-135">To maximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="5de6f-136">È consigliabile ottimizzare e bilanciare l' [utilizzo del thread](https://msdn.microsoft.com/library/aa383520.aspx) dell'applicazione per un ambiente multiutente e multiprocessore.</span><span class="sxs-lookup"><span data-stu-id="5de6f-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="5de6f-137">Per ottimizzare le prestazioni, è consigliabile che le applicazioni [rilevino](https://msdn.microsoft.com/library/aa380798.aspx) se sono in esecuzione in una sessione client.</span><span class="sxs-lookup"><span data-stu-id="5de6f-137">To optimize performance, it is good practice for applications to [detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

