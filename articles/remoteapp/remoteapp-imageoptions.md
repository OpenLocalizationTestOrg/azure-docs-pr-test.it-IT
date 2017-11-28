---
title: Creare un'immagine di Azure RemoteApp | Microsoft Docs
description: Informazioni sulle opzioni disponibili per la creazione di immagini per Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 4b8ba6f264f982e03930c5ad4ccdb2d80f2c8665
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="c431f-103">Creare un'immagine di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c431f-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c431f-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="c431f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c431f-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="c431f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c431f-106">Azure RemoteApp usa immagini per contenere le app condivise con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="c431f-106">Azure RemoteApp uses images to hold the apps that you share with your users.</span></span> <span data-ttu-id="c431f-107">(Prendiamo l'immagine e la usiamo per creare macchine virtuali, ovvero il punto raggiunto dagli utenti quando accedono a RemoteApp di Azure). Per creare una raccolta Azure RemoteApp con una scelta di applicazioni personalizzata, nel cloud o ibrida, iniziare con la creazione di un'immagine contenente le applicazioni installate.</span><span class="sxs-lookup"><span data-stu-id="c431f-107">(We take your image and use it to create VMs - that's what the users access when they sign into Azure RemoteApp.) To create an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="c431f-108">Creare quindi una raccolta che usa l'immagine, assegnare utenti alla raccolta e pubblicare le app per gli utenti desiderati.</span><span class="sxs-lookup"><span data-stu-id="c431f-108">Then, create a collection that uses that image, assign users to the collection, and publish apps to those users.</span></span>

<span data-ttu-id="c431f-109">Per creare o usare le immagini sono disponibili diverse opzioni.</span><span class="sxs-lookup"><span data-stu-id="c431f-109">You have several options for creating or using images.</span></span> <span data-ttu-id="c431f-110">Il [requisito](remoteapp-imagereqs.md) di base per un'immagine è che sia in esecuzione Windows Server 2012 R2 e che sia installato il ruolo Host sessione Desktop remoto (RDSH).</span><span class="sxs-lookup"><span data-stu-id="c431f-110">The basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have the Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="c431f-111">Sarà interessante vedere come soddisfare questo requisito.</span><span class="sxs-lookup"><span data-stu-id="c431f-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="c431f-112">Per le immagini sono disponibili le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c431f-112">You have the following options when it comes to images:</span></span>

* <span data-ttu-id="c431f-113">È possibile importare e usare un' [immagine basata su una macchina virtuale di Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="c431f-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="c431f-114">Questa opzione è utile per le applicazioni line-of-business che richiedono impostazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="c431f-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="c431f-115">È possibile personalizzare l'immagine per il funzionamento con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c431f-115">You can customize the image to work for the app.</span></span>
* <span data-ttu-id="c431f-116">È possibile [creare e caricare un'immagine personalizzata](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="c431f-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="c431f-117">Questa opzione è utile se si ha già un'immagine usata per la distribuzione locale di Servizi Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="c431f-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="c431f-118">È possibile usare una delle [immagini modello](remoteapp-images.md) incluse nella sottoscrizione di RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c431f-118">You can use one of the [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="c431f-119">Queste immagini vengono create e gestite dal team di RemoteApp e contengono alcune applicazioni standard (come le applicazioni Office) che è possibile rendere disponibili agli utenti.</span><span class="sxs-lookup"><span data-stu-id="c431f-119">These images are created and maintained by the RemoteApp team and contain some standard applications (like the Office suite) that you can make available to your users.</span></span> <span data-ttu-id="c431f-120">Si noti che in un ambiente di produzione è possibile usare solo l'immagine di Office 365 Pro Plus.</span><span class="sxs-lookup"><span data-stu-id="c431f-120">Note that only the Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="c431f-121">Indipendentemente da dove si ottiene l'immagine o da come la si crea, è opportuno verificare di avere compreso i [requisiti per le app](remoteapp-appreqs.md) per garantire il corretto funzionamento dell'app in RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c431f-121">Regardless of where you get your image or how you create it, you'll want to make sure you understand the [app requirements](remoteapp-appreqs.md) to ensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="c431f-122">Il passaggio successivo consiste nel creare una raccolta [nel cloud](remoteapp-create-cloud-deployment.md) o [ibrida](remoteapp-create-hybrid-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c431f-122">Then, the next step is to create a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

