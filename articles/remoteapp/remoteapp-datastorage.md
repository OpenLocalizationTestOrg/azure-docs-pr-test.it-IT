---
title: archivio aaaNever i dati sensibili nel immagini personalizzate per Azure RemoteApp | Documenti Microsoft
description: Informazioni sulle linee guida hello per l'archiviazione dei dati in immagini personalizzate in Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="1fc8c-103">Non archiviare mai dati sensibili in immagini personalizzate</span><span class="sxs-lookup"><span data-stu-id="1fc8c-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1fc8c-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1fc8c-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1fc8c-106">Quando si ospita l'applicazione in Azure RemoteApp, hello primo passaggio consiste toocreate un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="1fc8c-107">Utilizziamo che istanze VM toocreate immagine personalizzata che servono le app agli utenti di tooyour.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="1fc8c-108">immagine personalizzata Hello deve contenere solo le applicazioni e dati sensibili mai che possono essere persi, ad esempio i database SQL, file personale o file di dati speciali ad esempio i file aziendali QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="1fc8c-109">Tutti i dati sensibili devono trovarsi tooAzure esterno RemoteApp in un file server, un'altra macchina virtuale di Azure, o in SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="1fc8c-110">immagine di Hello deve semplicemente un'applicazione hello host che si connette toohello origine dei dati e presenta i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="1fc8c-111">Per altre informazioni vedere [Requisiti per le immagini di Azure RemoteApp](remoteapp-imagereqs.md) .</span><span class="sxs-lookup"><span data-stu-id="1fc8c-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="1fc8c-112">toounderstand perché è consigliabile non archiviare i dati sensibili, è necessario toounderstand funzionamento di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="1fc8c-113">Quando una raccolta viene creata o aggiornata, in background hello cloni più copie dell'immagine di hello vengono create.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="1fc8c-114">Tutte le istanze di macchina virtuale sono repliche esatte dell'immagine personalizzata hello; Quando gli utenti di avviare le applicazioni sono connessi tooone di queste istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="1fc8c-115">Ma non è garantito hello stessa istanza e non è importante perché sono non persistenti.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="1fc8c-116">Hello istanze di macchina virtuale, le applicazioni di hosting hello non sono permanenti e possono essere eliminato in modo permanente o eliminati in base, ad esempio, durante l'aggiornamento della raccolta.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="1fc8c-117">Una volta raccolta hello viene eseguito il provisioning e gli utenti avviano toohello connessione macchine virtuali, i dati utente sono persistenti e protetti poiché viene salvato in archiviazione separata all'interno di un disco rigido virtuale che si chiama un [disco (UPD)](remoteapp-upd.md), ovvero profilo utente hello in c:\users\<userprofile >.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="1fc8c-118">Avvio di un'applicazione hello UPD viene montato e considerato come un profilo utente locale dal sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="1fc8c-119">Altre informazioni su come [Azure RemoteApp salva dati e impostazioni](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="1fc8c-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="1fc8c-120">Dati di esempio che non devono trovarsi nell'immagine hello:</span><span class="sxs-lookup"><span data-stu-id="1fc8c-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="1fc8c-121">Dati condivisi per gli utenti tooaccess</span><span class="sxs-lookup"><span data-stu-id="1fc8c-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="1fc8c-122">SQL DB o QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="1fc8c-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="1fc8c-123">Tutti i dati in D:\\</span><span class="sxs-lookup"><span data-stu-id="1fc8c-123">Any data in D:\\</span></span>

<span data-ttu-id="1fc8c-124">Dati di esempio che possono risiedere in hello predefinito profilo toobe vengono copiati in UPD ogni degli utenti:</span><span class="sxs-lookup"><span data-stu-id="1fc8c-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="1fc8c-125">File di configurazione di ogni utente</span><span class="sxs-lookup"><span data-stu-id="1fc8c-125">Configuration files per user</span></span>
* <span data-ttu-id="1fc8c-126">Script che gli utenti devono mantenere nel loro disco profili utente</span><span class="sxs-lookup"><span data-stu-id="1fc8c-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="1fc8c-127">Punti principali:</span><span class="sxs-lookup"><span data-stu-id="1fc8c-127">Key points:</span></span>

* <span data-ttu-id="1fc8c-128">Non memorizzare mai dati sensibili che possono essere perso sull'immagine di hello durante la creazione di un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="1fc8c-129">Dati sensibili sempre deve risiedere in un file server separato, separare le VM di Azure, in cloud hello e toohello sempre esterno istanze della macchina virtuale che ospita le applicazioni all'interno di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1fc8c-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="1fc8c-130">Dati utente viene salvati e viene mantenuto nel disco di profilo utente hello (UDP)</span><span class="sxs-lookup"><span data-stu-id="1fc8c-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

