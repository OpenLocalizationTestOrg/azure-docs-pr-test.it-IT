---
title: i file in un account di servizi multimediali di Azure da Azure StorSimple aaaUpload | Documenti Microsoft
description: "Questo articolo offre una breve panoramica del gestore dati di Azure StorSimple. articolo Hello è anche possibile collegare tootutorials che mostrano come dati tooextract da StorSimple e caricare il file come asset tooan account servizi multimediali di Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="47e11-104">Caricare file in un account Servizi multimediali di Azure da Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="47e11-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="47e11-105">Questo articolo offre una breve panoramica del gestore dati di Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="47e11-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="47e11-106">articolo Hello è anche possibile collegare tootutorials che mostrano come dati tooextract da StorSimple e caricare i dati come asset tooan account servizi multimediali di Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="47e11-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="47e11-107">Il gestore dati di Azure StorSimple è attualmente in anteprima privata.</span><span class="sxs-lookup"><span data-stu-id="47e11-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="47e11-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="47e11-108">Overview</span></span>

<span data-ttu-id="47e11-109">In Servizi multimediali è possibile caricare i file digitali in un asset.</span><span class="sxs-lookup"><span data-stu-id="47e11-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="47e11-110">Hello Asset può contenere video, audio, immagini, raccolte di anteprime, testo tracce e sottotitoli file (e relativi metadati hello.) Una volta caricati i file hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso.</span><span class="sxs-lookup"><span data-stu-id="47e11-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="47e11-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) utilizza archiviazione cloud come soluzione locale di un'estensione di hello e livelli automaticamente i dati tra l'archiviazione locale hello e archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="47e11-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="47e11-112">dispositivo StorSimple Hello dedupes e comprime i dati prima di inviarlo cloud toohello rende molto efficiente per l'invio di cloud toohello file di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="47e11-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="47e11-113">Hello [StorSimple Manager dati](../storsimple/storsimple-data-manager-overview.md) servizio fornisce API che consentono di tooextract dei dati da StorSimple e visualizzarlo come risorse di sistema AMS.</span><span class="sxs-lookup"><span data-stu-id="47e11-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="47e11-114">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="47e11-114">Get started</span></span>

1. <span data-ttu-id="47e11-115">[Creare un account di servizi multimediali](media-services-portal-create-account.md) in cui si desidera asset hello tootransfer.</span><span class="sxs-lookup"><span data-stu-id="47e11-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="47e11-116">Effettuare l'iscrizione per l'anteprima di gestione dati, come descritto in hello [StorSimple Manager dati](../storsimple/storsimple-data-manager-overview.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="47e11-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="47e11-117">Creare un account del gestore dati StorSimple.</span><span class="sxs-lookup"><span data-stu-id="47e11-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="47e11-118">Creare un processo di trasformazione dei dati che, se eseguito, estrae i dati da un dispositivo StorSimple e li trasferisce come asset in un account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="47e11-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="47e11-119">Quando il processo di hello viene avviata l'esecuzione, viene creata una coda di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="47e11-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="47e11-120">Questa coda viene popolata con i messaggi relativi ai BLOB trasformati non appena pronti.</span><span class="sxs-lookup"><span data-stu-id="47e11-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="47e11-121">nome Hello di questa coda è hello corrisponde al nome hello hello della definizione del processo.</span><span class="sxs-lookup"><span data-stu-id="47e11-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="47e11-122">È possibile utilizzare questo toodetermine coda quando come asset è pronto e chiamare il desiderato toorun operazione servizi multimediali su di esso.</span><span class="sxs-lookup"><span data-stu-id="47e11-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="47e11-123">Ad esempio, è possibile utilizzare questo tootrigger coda, una funzione di Azure che include il codice di servizi multimediali necessarie hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="47e11-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="47e11-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="47e11-124">See also</span></span>

[<span data-ttu-id="47e11-125">Utilizzare hello .net SDK tootrigger processi in hello gestione dati</span><span class="sxs-lookup"><span data-stu-id="47e11-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="47e11-126">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="47e11-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="47e11-127">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="47e11-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="47e11-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47e11-128">Next steps</span></span>

<span data-ttu-id="47e11-129">Ora è possibile codificare gli asset caricati.</span><span class="sxs-lookup"><span data-stu-id="47e11-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="47e11-130">Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).</span><span class="sxs-lookup"><span data-stu-id="47e11-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
