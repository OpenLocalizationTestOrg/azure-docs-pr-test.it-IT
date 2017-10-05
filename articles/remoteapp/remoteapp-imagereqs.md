---
title: Requisiti delle immagini di Azure RemoteApp | Documentazione Microsoft
description: Informazioni sui requisiti per la creazione di immagini da usare con Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="c8e6b-103">Requisiti per le immagini di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="c8e6b-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c8e6b-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="c8e6b-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="c8e6b-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="c8e6b-106">Azure RemoteApp usa un'immagine di Windows Server 2012 R2 per ospitare tutti i programmi da condividere con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-106">Azure RemoteApp uses a Windows Server 2012 R2 image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="c8e6b-107">Per creare un’immagine personalizzata, è possibile iniziare con un’immagine esistente oppure [crearne una nuova](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="c8e6b-107">To create a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="c8e6b-108">Non tutti sanno che la sottoscrizione di Azure RemoteApp consente di accedere a un'immagine di Windows Server 2012 R2 nella raccolta di VM di Azure che è possibile usare per creare la propria immagine modello.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-108">Did you know that your Azure RemoteApp subscription gives you access to a Windows Server 2012 R2 image in the Azure VM gallery that you can use to create your own template image?</span></span> <span data-ttu-id="c8e6b-109">[Provare](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="c8e6b-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="c8e6b-110">I requisiti per l'immagine che possono essere caricati e usati con l'app Azure RemoteApp sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="c8e6b-110">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="c8e6b-111">Le applicazioni personalizzate non archiviano dati in locale nell'immagine.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-111">Custom applications don’t store data locally on the image.</span></span> <span data-ttu-id="c8e6b-112">Queste immagini sono senza stato e devono contenere solo le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="c8e6b-113">L'immagine non contiene dati che possono essere persi.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-113">The image does not contain data that can be lost.</span></span>
* <span data-ttu-id="c8e6b-114">La dimensione dell'immagine dev'essere un multiplo di MB.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-114">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="c8e6b-115">Se si prova a caricare un'immagine che non è un multiplo esatto, l'operazione non andrà a buon fine.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-115">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="c8e6b-116">L'immagine deve avere una dimensione massima di 127 GB.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-116">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="c8e6b-117">Deve essere inclusa in un file VHD (i file VHDX non sono attualmente supportati).</span><span class="sxs-lookup"><span data-stu-id="c8e6b-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="c8e6b-118">Il file VHD non deve essere una macchina virtuale di seconda generazione.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-118">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="c8e6b-119">Il file VHD può essere di dimensioni fisse o a espansione dinamica.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-119">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="c8e6b-120">È consigliabile un file VHD a espansione dinamica perché i tempi di caricamento di questo file in Azure sono inferiori rispetto a uno di dimensioni disse.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-120">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="c8e6b-121">Il disco deve essere inizializzato con lo stile di partizione MBR (Master Boot Record).</span><span class="sxs-lookup"><span data-stu-id="c8e6b-121">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="c8e6b-122">Lo stile di partizione basato sulla tabella di partizione GUID (GPT) non è supportato.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-122">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="c8e6b-123">Il file VHD deve contenere una singola installazione di Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-123">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="c8e6b-124">Può contenere più volumi, ma solo uno che contiene un'installazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="c8e6b-125">È necessario installare il ruolo Host sessione Desktop remoto e la funzionalità Esperienza desktop.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-125">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="c8e6b-126">Il ruolo Gestore connessione Desktop remoto *non* deve essere installato.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-126">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="c8e6b-127">EFS (Encrypting File System) deve essere disabilitato.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-127">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="c8e6b-128">L'immagine deve essere preparata con SYSPREP usando i parametri **/oobe /generalize /shutdown** (NON usare il parametro **/mode:vm**).</span><span class="sxs-lookup"><span data-stu-id="c8e6b-128">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="c8e6b-129">Il caricamento del disco VHD da una catena di snapshot non è supportato.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="c8e6b-130">Vedere [Creare un'immagine di Azure RemoteApp](remoteapp-imageoptions.md) per ulteriori informazioni sulla creazione di immagini per Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="c8e6b-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

