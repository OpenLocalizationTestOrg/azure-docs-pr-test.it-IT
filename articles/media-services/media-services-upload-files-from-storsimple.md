---
title: Caricare file in un account Servizi multimediali di Azure da Azure StorSimple | Microsoft Docs
description: Questo articolo offre una breve panoramica del gestore dati di Azure StorSimple. L'articolo contiene anche collegamenti a esercitazioni che illustrano come estrarre dati da StorSimple e caricarli come asset in un account Servizi multimediali di Azure.
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
ms.openlocfilehash: 636d55c15aa383208ffb39d5224123831af962c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="e7977-104">Caricare file in un account Servizi multimediali di Azure da Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="e7977-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="e7977-105">Questo articolo offre una breve panoramica del gestore dati di Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e7977-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="e7977-106">L'articolo contiene anche collegamenti a esercitazioni che illustrano come estrarre dati da StorSimple e caricarli come asset in un account Servizi multimediali di Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="e7977-106">The article also links to tutorials that show you how to extract data from StorSimple and upload this data as assets to an Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="e7977-107">Il gestore dati di Azure StorSimple è attualmente in anteprima privata.</span><span class="sxs-lookup"><span data-stu-id="e7977-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="e7977-108">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e7977-108">Overview</span></span>

<span data-ttu-id="e7977-109">In Servizi multimediali è possibile caricare i file digitali in un asset.</span><span class="sxs-lookup"><span data-stu-id="e7977-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="e7977-110">L'asset può contenere video, audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli codificati, oltre ai metadati relativi a questi file. Dopo aver caricato i file, i contenuti vengono archiviati in modo sicuro nel cloud per altre operazioni di elaborazione e streaming.</span><span class="sxs-lookup"><span data-stu-id="e7977-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="e7977-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) usa l'archiviazione cloud come un'estensione della soluzione locale e organizza automaticamente i dati in livelli tra archiviazione locale e archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="e7977-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="e7977-112">Il dispositivo StorSimple elimina i duplicati e comprime i dati prima di inviarli al cloud, migliorando notevolmente l'efficienza dell'invio di file di grandi dimensioni nel cloud.</span><span class="sxs-lookup"><span data-stu-id="e7977-112">The StorSimple device dedupes and compresses your data before sending it to the cloud making it very efficient for sending large files to the cloud.</span></span> <span data-ttu-id="e7977-113">Il servizio [gestore dati StorSimple](../storsimple/storsimple-data-manager-overview.md) include API che consentono di estrarre dati da StorSimple e presentarli come asset di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7977-113">The [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you to extract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="e7977-114">Introduzione</span><span class="sxs-lookup"><span data-stu-id="e7977-114">Get started</span></span>

1. <span data-ttu-id="e7977-115">[Creare un account Servizi multimediali](media-services-portal-create-account.md) in cui trasferire gli asset.</span><span class="sxs-lookup"><span data-stu-id="e7977-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want to transfer the assets.</span></span>
2. <span data-ttu-id="e7977-116">Eseguire l'iscrizione per l'anteprima del gestore dati, come descritto nell'articolo relativo al [gestore dati StorSimple](../storsimple/storsimple-data-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7977-116">Sign up for Data Manager preview, as described in the [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="e7977-117">Creare un account del gestore dati StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e7977-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="e7977-118">Creare un processo di trasformazione dei dati che, se eseguito, estrae i dati da un dispositivo StorSimple e li trasferisce come asset in un account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7977-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="e7977-119">Quando si avvia l'esecuzione del processo, viene creata una coda di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e7977-119">When the job starts running, a storage queue is created.</span></span> <span data-ttu-id="e7977-120">Questa coda viene popolata con i messaggi relativi ai BLOB trasformati non appena pronti.</span><span class="sxs-lookup"><span data-stu-id="e7977-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="e7977-121">Il nome di questa coda corrisponde a quello della definizione di processo.</span><span class="sxs-lookup"><span data-stu-id="e7977-121">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="e7977-122">È possibile usare la coda per stabilire quando un asset è pronto e chiamare l'operazione di Servizi multimediali da eseguire sull'asset.</span><span class="sxs-lookup"><span data-stu-id="e7977-122">You can use this queue to determine when as asset is ready and call your desired Media Services operation to run on it.</span></span> <span data-ttu-id="e7977-123">Ad esempio, è possibile usare la coda per attivare una funzione di Azure contenente il codice di Servizi multimediali necessario.</span><span class="sxs-lookup"><span data-stu-id="e7977-123">For example, you can use this queue to trigger an Azure Function that has the necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="e7977-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e7977-124">See also</span></span>

[<span data-ttu-id="e7977-125">Usare .Net SDK per attivare processi nel gestore dati</span><span class="sxs-lookup"><span data-stu-id="e7977-125">Use the .Net SDK to trigger jobs in the Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="e7977-126">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="e7977-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e7977-127">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="e7977-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e7977-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e7977-128">Next steps</span></span>

<span data-ttu-id="e7977-129">Ora è possibile codificare gli asset caricati.</span><span class="sxs-lookup"><span data-stu-id="e7977-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="e7977-130">Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).</span><span class="sxs-lookup"><span data-stu-id="e7977-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
