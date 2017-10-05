---
title: Caricare un'immagine personalizzata per Azure RemoteApp | Documentazione Microsoft
description: Informazioni su come caricare un'immagine personalizzata per RemoteApp di Azure
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
ms.openlocfilehash: 5a235fac88d6e95ea294bda197641108acb4a09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="80f42-103">Caricare un'immagine personalizzata per RemoteApp di Azure</span><span class="sxs-lookup"><span data-stu-id="80f42-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="80f42-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="80f42-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="80f42-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="80f42-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="80f42-106">Dopo aver creato o aggiornato con le modifiche l'immagine modello personalizzata, è necessario caricare l'immagine nella raccolta immagini di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="80f42-106">Now that you have created your custom template image or have updated it with changes, you need to upload that image to your Azure RemoteApp image library.</span></span> <span data-ttu-id="80f42-107">Usare i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="80f42-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="80f42-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="80f42-108">Before you start</span></span>
1. <span data-ttu-id="80f42-109">Verificare che l'immagine personalizzata soddisfi i [requisiti dell'immagine](remoteapp-imagereqs.md) e i [requisiti dell'applicazione](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="80f42-109">Verify your custom image meets the [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="80f42-110">Installare il [modulo Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80f42-110">Install the [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-to-upload-custom-image"></a><span data-ttu-id="80f42-111">Istruzioni dettagliate su come caricare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="80f42-111">Step by step on how to upload custom image</span></span>
1. <span data-ttu-id="80f42-112">Aprire il portale di gestione di Azure e passare alla pagina RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="80f42-112">Open Azure Management Portal and navigate to the RemoteApp page.</span></span>
2. <span data-ttu-id="80f42-113">Nella scheda **Immagini modello** fare clic su **Carica** in fondo alla pagina.</span><span class="sxs-lookup"><span data-stu-id="80f42-113">On the **Template images** tab, click **Upload** at the bottom of the page.</span></span>
3. <span data-ttu-id="80f42-114">Immettere un nome descrittivo per l'immagine e specificare il percorso dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="80f42-114">Enter a friendly name for your image and specify the storage account location.</span></span> <span data-ttu-id="80f42-115">Verificare che il percorso sia uguale a quello della raccolta RemoteApp oppure che sia il percorso dove verrà creata una nuova raccolta.</span><span class="sxs-lookup"><span data-stu-id="80f42-115">Ensure the location is the same location as your RemoteApp collection or a location where you want to create one.</span></span>
4. <span data-ttu-id="80f42-116">Quando richiesto, scaricare lo script nel PC locale.</span><span class="sxs-lookup"><span data-stu-id="80f42-116">When prompted, download the script to your local PC.</span></span>
5. <span data-ttu-id="80f42-117">Copiare negli Appunti i parametri del comando contenuti nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="80f42-117">Copy the command parameters in the text box to your clipboard.</span></span>
6. <span data-ttu-id="80f42-118">Aprire una finestra di Windows PowerShell con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="80f42-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="80f42-119">Dalla finestra di Windows PowerShell con privilegi elevati passare alla directory in cui è stato scaricato lo script.</span><span class="sxs-lookup"><span data-stu-id="80f42-119">From the elevated Windows PowerShell window, navigate to the same directory where you downloaded the script.</span></span>
8. <span data-ttu-id="80f42-120">Incollare il comando copiato e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="80f42-120">Paste the copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="80f42-121">Viene avviato il processo di caricamento, la cui durata dipende da diversi fattori, ad esempio la velocità di rete e le dimensioni dell'immagine</span><span class="sxs-lookup"><span data-stu-id="80f42-121">The upload process will begin and duration may depend on many factors including your network speed and size of the image</span></span>
9. <span data-ttu-id="80f42-122">Se il caricamento non riesce a causa di interruzioni di rete o problemi simili, è possibile riprendere il processo di caricamento avviato in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="80f42-122">If your upload does not succeed because of network interruption or things like that, you can always resume the upload process you began.</span></span> <span data-ttu-id="80f42-123">Per riprendere il caricamento, eseguire di nuovo lo script usando la stessa riga di comando.</span><span class="sxs-lookup"><span data-stu-id="80f42-123">To resume an upload, run the script again using the same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="80f42-124">Non modificare mai lo script di caricamento.</span><span class="sxs-lookup"><span data-stu-id="80f42-124">Never modify the upload script.</span></span> <span data-ttu-id="80f42-125">Sono stati implementati controlli specifici che assicurano che l'immagine soddisfi i requisiti per l'immagine e per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80f42-125">Specific checks have been implemented to ensure that the image meets the image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="80f42-126">Problemi frequenti</span><span class="sxs-lookup"><span data-stu-id="80f42-126">Common problems</span></span>
* <span data-ttu-id="80f42-127">Assicurarsi di usare Windows PowerShell, e non Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80f42-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="80f42-128">È necessario installare il modulo Azure PowerShell perché alcuni moduli sono necessari durante il processo di caricamento.</span><span class="sxs-lookup"><span data-stu-id="80f42-128">You need to install the Azure PowerShell module because certain modules are needed during the upload process.</span></span>
* <span data-ttu-id="80f42-129">Non modificare in nessun caso lo script. Le convalide sono state applicate per semplificare l'utilizzo da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="80f42-129">Never alter the script, validations are there for your convenience.</span></span>
* <span data-ttu-id="80f42-130">Se il file VHD si blocca durante il caricamento, copiare il file o spostarlo in un nuovo percorso e riprovare il caricamento.</span><span class="sxs-lookup"><span data-stu-id="80f42-130">If the vhd file gets locked out during upload, copy the file or move it to a new location and attempt upload again.</span></span> <span data-ttu-id="80f42-131">Il caricamento potrebbe essere ostacolato da qualche processo di Windows in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="80f42-131">There might be some Windows process that is preventing upload.</span></span>  

