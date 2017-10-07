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
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>Caricare file in un account Servizi multimediali di Azure da Azure StorSimple

Questo articolo offre una breve panoramica del gestore dati di Azure StorSimple. articolo Hello è anche possibile collegare tootutorials che mostrano come dati tooextract da StorSimple e caricare i dati come asset tooan account servizi multimediali di Azure (AMS).

> 
> [!NOTE]
> Il gestore dati di Azure StorSimple è attualmente in anteprima privata. 
> 

## <a name="overview"></a>Panoramica

In Servizi multimediali è possibile caricare i file digitali in un asset. Hello Asset può contenere video, audio, immagini, raccolte di anteprime, testo tracce e sottotitoli file (e relativi metadati hello.) Una volta caricati i file hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso.

[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) utilizza archiviazione cloud come soluzione locale di un'estensione di hello e livelli automaticamente i dati tra l'archiviazione locale hello e archiviazione cloud. dispositivo StorSimple Hello dedupes e comprime i dati prima di inviarlo cloud toohello rende molto efficiente per l'invio di cloud toohello file di grandi dimensioni. Hello [StorSimple Manager dati](../storsimple/storsimple-data-manager-overview.md) servizio fornisce API che consentono di tooextract dei dati da StorSimple e visualizzarlo come risorse di sistema AMS.

## <a name="get-started"></a>Attività iniziali

1. [Creare un account di servizi multimediali](media-services-portal-create-account.md) in cui si desidera asset hello tootransfer.
2. Effettuare l'iscrizione per l'anteprima di gestione dati, come descritto in hello [StorSimple Manager dati](../storsimple/storsimple-data-manager-overview.md) articolo.
3. Creare un account del gestore dati StorSimple.
4. Creare un processo di trasformazione dei dati che, se eseguito, estrae i dati da un dispositivo StorSimple e li trasferisce come asset in un account Servizi multimediali di Azure. 

    Quando il processo di hello viene avviata l'esecuzione, viene creata una coda di archiviazione. Questa coda viene popolata con i messaggi relativi ai BLOB trasformati non appena pronti. nome Hello di questa coda è hello corrisponde al nome hello hello della definizione del processo. È possibile utilizzare questo toodetermine coda quando come asset è pronto e chiamare il desiderato toorun operazione servizi multimediali su di esso. Ad esempio, è possibile utilizzare questo tootrigger coda, una funzione di Azure che include il codice di servizi multimediali necessarie hello in essa contenuti.

## <a name="see-also"></a>Vedere anche

[Utilizzare hello .net SDK tootrigger processi in hello gestione dati](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Passaggi successivi

Ora è possibile codificare gli asset caricati. Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).
