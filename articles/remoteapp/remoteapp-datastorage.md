---
title: Non archiviare mai dati sensibili in immagini personalizzate per Azure RemoteApp | Documentazione Microsoft
description: Informazioni sulle linee guida per l'archiviazione dei dati in immagini personalizzate in Azure RemoteApp
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
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="ed98d-103">Non archiviare mai dati sensibili in immagini personalizzate</span><span class="sxs-lookup"><span data-stu-id="ed98d-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ed98d-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="ed98d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ed98d-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="ed98d-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ed98d-106">Quando si ospita un'applicazione personalizzata in Azure RemoteApp, il primo passaggio consiste nella creazione di un'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="ed98d-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="ed98d-107">L'immagine personalizzata viene usata per creare istanze di VM che forniscono le app agli utenti.</span><span class="sxs-lookup"><span data-stu-id="ed98d-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="ed98d-108">L'immagine personalizzata deve contenere SOLTANTO applicazioni e mai dati sensibili che possano essere persi, ad esempio database SQL, file personali o file di dati speciali come i file aziendali QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="ed98d-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="ed98d-109">Tutti i dati riservati devono essere esterni ad Azure RemoteApp e trovarsi in un file server, in un'altra VM di Azure o in SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ed98d-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="ed98d-110">L'immagine deve ospitare soltanto l'applicazione che si collega all'origine dati e visualizza i dati.</span><span class="sxs-lookup"><span data-stu-id="ed98d-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="ed98d-111">Per altre informazioni vedere [Requisiti per le immagini di Azure RemoteApp](remoteapp-imagereqs.md) .</span><span class="sxs-lookup"><span data-stu-id="ed98d-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="ed98d-112">Per comprendere il motivo per cui non si devono archiviare dati sensibili, è necessario comprendere il funzionamento di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ed98d-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="ed98d-113">Quando si crea o si aggiorna una raccolta, sullo sfondo vengono creati più cloni o copie dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="ed98d-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="ed98d-114">Tutte le istanze di VM sono repliche esatte dell'immagine personalizzata. Quando gli utenti avviano le applicazioni, si collegano a una di queste istanze di VM.</span><span class="sxs-lookup"><span data-stu-id="ed98d-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="ed98d-115">Non è però garantita la stessa istanza e l'istanza non è importante perché non è permanente.</span><span class="sxs-lookup"><span data-stu-id="ed98d-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="ed98d-116">Le istanze di VM che ospitano le applicazioni non sono permanenti e possono essere eliminate o distrutte, ad esempio durante l'aggiornamento della raccolta.</span><span class="sxs-lookup"><span data-stu-id="ed98d-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="ed98d-117">Quando viene eseguito il provisioning della raccolta e gli utenti si collegano alle VM, i dati utente sono permanenti e protetti perché vengono salvati in una memoria separata all'interno di un disco rigido virtuale definito [disco profili utente](remoteapp-upd.md), ovvero il profilo utente in c:\users\<userprofile>.</span><span class="sxs-lookup"><span data-stu-id="ed98d-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="ed98d-118">Quando si avvia un'applicazione, il disco profili utente viene montato e gestito come un profilo utente locale dal sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ed98d-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="ed98d-119">Altre informazioni su come [Azure RemoteApp salva dati e impostazioni](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="ed98d-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="ed98d-120">Dati di esempio che non devono trovarsi nell'immagine:</span><span class="sxs-lookup"><span data-stu-id="ed98d-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="ed98d-121">Dati condivisi per l'accesso degli utenti</span><span class="sxs-lookup"><span data-stu-id="ed98d-121">Shared data for users to access</span></span>
* <span data-ttu-id="ed98d-122">SQL DB o QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="ed98d-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="ed98d-123">Tutti i dati in D:\\</span><span class="sxs-lookup"><span data-stu-id="ed98d-123">Any data in D:\\</span></span>

<span data-ttu-id="ed98d-124">Dati di esempio che possono trovarsi nel profilo predefinito da copiare nel disco profili utente di ogni utente:</span><span class="sxs-lookup"><span data-stu-id="ed98d-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="ed98d-125">File di configurazione di ogni utente</span><span class="sxs-lookup"><span data-stu-id="ed98d-125">Configuration files per user</span></span>
* <span data-ttu-id="ed98d-126">Script che gli utenti devono mantenere nel loro disco profili utente</span><span class="sxs-lookup"><span data-stu-id="ed98d-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="ed98d-127">Punti principali:</span><span class="sxs-lookup"><span data-stu-id="ed98d-127">Key points:</span></span>

* <span data-ttu-id="ed98d-128">Quando si crea un'immagine personalizzata, non archiviare mai nell'immagine dati sensibili che possano andare perduti.</span><span class="sxs-lookup"><span data-stu-id="ed98d-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="ed98d-129">I dati sensibili devono sempre trovarsi in un file server separato, in una VM di Azure separata o nel cloud e devono essere sempre esterni alle istanze della VM che ospita le applicazioni all'interno di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ed98d-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="ed98d-130">I dati utente vengono salvati e mantenuti nel disco profili utente.</span><span class="sxs-lookup"><span data-stu-id="ed98d-130">User data is saved and persists in the user profile disk (UPD)</span></span>

