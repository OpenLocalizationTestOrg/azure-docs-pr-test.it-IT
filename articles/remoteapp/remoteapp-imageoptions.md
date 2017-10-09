---
title: un'immagine di Azure RemoteApp aaaCreate | Documenti Microsoft
description: Informazioni sulle opzioni di hello disponibili per la creazione di immagini per Azure RemoteApp
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
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="ec956-103">Creare un'immagine di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ec956-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ec956-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="ec956-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ec956-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="ec956-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ec956-106">Azure RemoteApp utilizza immagini toohold hello App che si condivide con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="ec956-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="ec956-107">(È acquisire l'immagine e usarlo come macchine virtuali toocreate - questo è l'accedono agli utenti di hello quando effettuano l'accesso in Azure RemoteApp.) toocreate una raccolta di Azure RemoteApp con la scelta delle applicazioni, anche se la cloud ibrida, è innanzitutto necessario creare un'immagine con le applicazioni installate.</span><span class="sxs-lookup"><span data-stu-id="ec956-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="ec956-108">Quindi, creare una raccolta che utilizza quell'immagine, assegnare gli utenti toohello insieme e pubblicare gli utenti toothose app.</span><span class="sxs-lookup"><span data-stu-id="ec956-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="ec956-109">Per creare o usare le immagini sono disponibili diverse opzioni.</span><span class="sxs-lookup"><span data-stu-id="ec956-109">You have several options for creating or using images.</span></span> <span data-ttu-id="ec956-110">Hello base [requisito](remoteapp-imagereqs.md) per un'immagine che eseguono Windows Server 2012 R2 e che hanno installato il ruolo hello sessione Desktop remoto Host ().</span><span class="sxs-lookup"><span data-stu-id="ec956-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="ec956-111">Sarà interessante vedere come soddisfare questo requisito.</span><span class="sxs-lookup"><span data-stu-id="ec956-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="ec956-112">Sono disponibili le opzioni seguenti per quanto riguarda tooimages hello:</span><span class="sxs-lookup"><span data-stu-id="ec956-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="ec956-113">È possibile importare e usare un' [immagine basata su una macchina virtuale di Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="ec956-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="ec956-114">Questa opzione è utile per le applicazioni line-of-business che richiedono impostazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="ec956-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="ec956-115">È possibile personalizzare hello immagine toowork per app hello.</span><span class="sxs-lookup"><span data-stu-id="ec956-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="ec956-116">È possibile [creare e caricare un'immagine personalizzata](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="ec956-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="ec956-117">Questa opzione è utile se si ha già un'immagine usata per la distribuzione locale di Servizi Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="ec956-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="ec956-118">È possibile utilizzare uno di hello [immagini modello](remoteapp-images.md) inclusi nella sottoscrizione di RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ec956-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="ec956-119">Queste immagini vengono create e gestiti da team RemoteApp hello e contengono alcune applicazioni standard (ad esempio applicazioni di Office hello) che è possibile rendere disponibili tooyour utenti.</span><span class="sxs-lookup"><span data-stu-id="ec956-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="ec956-120">Si noti che solo immagine di Office 365 Pro Plus hello può essere utilizzata in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ec956-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="ec956-121">Indipendentemente da dove si ottenga un'immagine o modalità di creazione, è opportuno conoscere hello toomake [requisiti delle app](remoteapp-appreqs.md) tooensure che l'app funziona bene in RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ec956-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="ec956-122">Quindi, hello è toocreate un [cloud](remoteapp-create-cloud-deployment.md) o [ibrida](remoteapp-create-hybrid-deployment.md) insieme.</span><span class="sxs-lookup"><span data-stu-id="ec956-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>

