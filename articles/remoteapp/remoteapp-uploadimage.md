---
title: un'immagine personalizzata per Azure RemoteApp aaaUpload | Documenti Microsoft
description: Informazioni su come tooupload immagine di un oggetto personalizzato per Azure RemoteApp
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="83e6a-103">Caricare un'immagine personalizzata per RemoteApp di Azure</span><span class="sxs-lookup"><span data-stu-id="83e6a-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="83e6a-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="83e6a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="83e6a-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="83e6a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="83e6a-106">Dopo aver creato l'immagine modello personalizzato o lo abbia aggiornato con le modifiche, è necessario tooupload tale libreria di immagini immagine tooyour Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="83e6a-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="83e6a-107">Usare i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="83e6a-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="83e6a-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="83e6a-108">Before you start</span></span>
1. <span data-ttu-id="83e6a-109">Verificare che l'immagine personalizzata soddisfi hello [requisiti dell'immagine](remoteapp-imagereqs.md) e [requisiti dell'applicazione](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="83e6a-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="83e6a-110">Installare hello [modulo Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="83e6a-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="83e6a-111">Procedura dettagliata su come immagine personalizzata tooupload</span><span class="sxs-lookup"><span data-stu-id="83e6a-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="83e6a-112">Aprire il portale di gestione di Azure e passare toohello RemoteApp pagina.</span><span class="sxs-lookup"><span data-stu-id="83e6a-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="83e6a-113">In hello **immagini modello** scheda, fare clic su **caricare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="83e6a-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="83e6a-114">Immettere un nome descrittivo per l'immagine e specificare una posizione dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="83e6a-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="83e6a-115">Verificare che il percorso di hello è hello stesso percorso la raccolta RemoteApp o in un percorso in cui si desidera toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="83e6a-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="83e6a-116">Quando richiesto, scaricare hello script tooyour PC locale.</span><span class="sxs-lookup"><span data-stu-id="83e6a-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="83e6a-117">Copiare i parametri del comando hello negli Appunti tooyour casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="83e6a-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="83e6a-118">Aprire una finestra di Windows PowerShell con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="83e6a-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="83e6a-119">Da hello finestra Windows PowerShell con privilegi elevati passare toohello stessa directory in cui è stato scaricato script hello.</span><span class="sxs-lookup"><span data-stu-id="83e6a-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="83e6a-120">Hello Incolla copiati comando e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="83e6a-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="83e6a-121">verrà avviato il processo di caricamento Hello e durata può dipendere da molti fattori, tra cui la velocità di rete e le dimensioni dell'immagine di hello</span><span class="sxs-lookup"><span data-stu-id="83e6a-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="83e6a-122">Se il caricamento non riesce a causa di interruzioni di rete o elementi simili, è sempre possibile riprendere il processo di caricamento hello che è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="83e6a-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="83e6a-123">tooresume un'operazione di caricamento, eseguire script hello utilizzando hello stessa riga di comando.</span><span class="sxs-lookup"><span data-stu-id="83e6a-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="83e6a-124">Non modificare mai script caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="83e6a-124">Never modify hello upload script.</span></span> <span data-ttu-id="83e6a-125">Controlli specifici sono stati implementati tooensure che hello immagine soddisfa i requisiti di immagine hello e requisiti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="83e6a-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="83e6a-126">Problemi frequenti</span><span class="sxs-lookup"><span data-stu-id="83e6a-126">Common problems</span></span>
* <span data-ttu-id="83e6a-127">Assicurarsi di usare Windows PowerShell, e non Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83e6a-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="83e6a-128">Modulo di Azure PowerShell tooinstall hello è necessario perché alcuni moduli sono necessari durante il processo di caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="83e6a-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="83e6a-129">Non modificare script hello, le convalide sono disponibili per comodità.</span><span class="sxs-lookup"><span data-stu-id="83e6a-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="83e6a-130">Se il file di disco rigido virtuale hello Ottiene bloccato durante il caricamento, copiare il file hello o spostarlo tooa nuovo percorso e il tentativo di caricare nuovamente.</span><span class="sxs-lookup"><span data-stu-id="83e6a-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="83e6a-131">Il caricamento potrebbe essere ostacolato da qualche processo di Windows in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="83e6a-131">There might be some Windows process that is preventing upload.</span></span>  

