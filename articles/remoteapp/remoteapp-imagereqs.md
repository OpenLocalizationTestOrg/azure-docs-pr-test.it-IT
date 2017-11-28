---
title: requisiti immagine di RemoteApp aaaAzure | Documenti Microsoft
description: Informazioni sui requisiti di hello per la creazione di immagini toobe utilizzato con Azure RemoteApp
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
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="38274-103">Requisiti per le immagini di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="38274-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="38274-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="38274-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="38274-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="38274-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="38274-106">Azure RemoteApp utilizza un toohost immagine di Windows Server 2012 R2 tutti i programmi di hello che si desidera tooshare con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="38274-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="38274-107">toocreate un'immagine personalizzata, è possibile iniziare con un'immagine esistente o [crearne uno nuovo](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="38274-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="38274-108">Non tutti sanno che i consente di sottoscrizione di Azure RemoteApp in che accedere tooa immagine di Windows Server 2012 R2 hello raccolta di macchine Virtuali di Azure che è possibile utilizzare toocreate la propria immagine modello.</span><span class="sxs-lookup"><span data-stu-id="38274-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="38274-109">[Provare](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="38274-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="38274-110">i requisiti per l'immagine di hello che può essere caricato per l'utilizzo con Azure RemoteApp Hello sono:</span><span class="sxs-lookup"><span data-stu-id="38274-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="38274-111">Applicazioni personalizzate non archiviano i dati in locale nell'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="38274-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="38274-112">Queste immagini sono senza stato e devono contenere solo le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="38274-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="38274-113">immagine di Hello non contiene dati che possono essere persi.</span><span class="sxs-lookup"><span data-stu-id="38274-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="38274-114">dimensioni dell'immagine Hello devono essere un multiplo del numero di MB.</span><span class="sxs-lookup"><span data-stu-id="38274-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="38274-115">Se si tenta di tooupload un'immagine che non è un multiplo esatto, caricamento hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="38274-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="38274-116">dimensioni dell'immagine Hello devono essere 127 GB o più piccoli.</span><span class="sxs-lookup"><span data-stu-id="38274-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="38274-117">Deve essere inclusa in un file VHD (i file VHDX non sono attualmente supportati).</span><span class="sxs-lookup"><span data-stu-id="38274-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="38274-118">Hello disco rigido virtuale non deve essere una macchina virtuale di generazione 2.</span><span class="sxs-lookup"><span data-stu-id="38274-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="38274-119">è possibile Hello disco rigido virtuale a dimensione fissa o ad espansione dinamica.</span><span class="sxs-lookup"><span data-stu-id="38274-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="38274-120">Un disco rigido virtuale ad espansione dinamica è consigliato perché richiede meno tooAzure tooupload tempo rispetto a un file di disco rigido virtuale a dimensione fissa.</span><span class="sxs-lookup"><span data-stu-id="38274-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="38274-121">Hello disco deve essere inizializzato con stile di partizionamento hello il record di avvio principale (MBR, Master Boot Record).</span><span class="sxs-lookup"><span data-stu-id="38274-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="38274-122">Hello stile di partizione GUID partizione GPT (tabella) non è supportata.</span><span class="sxs-lookup"><span data-stu-id="38274-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="38274-123">Hello VHD deve contenere una singola installazione di Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="38274-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="38274-124">Può contenere più volumi, ma solo uno che contiene un'installazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="38274-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="38274-125">ruolo di Hello sessione Desktop remoto Host () e funzionalità esperienza Desktop hello devono essere installati.</span><span class="sxs-lookup"><span data-stu-id="38274-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="38274-126">ruolo Gestore connessione Desktop remoto Hello deve *non* installato.</span><span class="sxs-lookup"><span data-stu-id="38274-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="38274-127">Hello Encrypting File System (EFS) deve essere disabilitato.</span><span class="sxs-lookup"><span data-stu-id="38274-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="38274-128">Hello immagine deve essere preparata con Sysprep utilizzando parametri hello **/oobe /generalize /shutdown** (non utilizzare hello **/mode: VM** parametro).</span><span class="sxs-lookup"><span data-stu-id="38274-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="38274-129">Il caricamento del disco VHD da una catena di snapshot non è supportato.</span><span class="sxs-lookup"><span data-stu-id="38274-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="38274-130">Vedere [Creare un'immagine di Azure RemoteApp](remoteapp-imageoptions.md) per ulteriori informazioni sulla creazione di immagini per Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="38274-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

