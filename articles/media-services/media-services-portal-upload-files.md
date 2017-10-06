---
title: aaa"caricamento di file in un account di servizi multimediali tramite hello portale di Azure | Documenti di Microsoft"
description: In questa esercitazione vengono illustrati i passaggi hello di caricamento dei file in un account di servizi multimediali tramite hello portale di Azure
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a>Caricare file in un account di servizi multimediali tramite hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 


In Servizi multimediali è possibile caricare i file digitali in un asset. Hello Asset può contenere video, audio, immagini, raccolte di anteprime, testo tracce e sottotitoli file (e relativi metadati hello.) Una volta caricati i file hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso.


## <a name="upload-files"></a>Caricare file

>[!NOTE]
>È una limite toohello dimensione massima supportata per l'elaborazione in servizi multimediali. Vedere [questo](media-services-quotas-and-limitations.md) per informazioni sulla limitazione delle dimensioni del file hello.
>

1. In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.
2. In hello **impostazioni** pannello, fare clic su **asset**.
   
    ![Caricare file](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. Fare clic su hello **caricare** pulsante.
   
    Hello **caricare una risorsa video** verrà visualizzata la finestra.
   
   > [!NOTE]
   > Non esistono limiti alle dimensioni dei file.
   > 
   > 
4. Sfoglia video toohello desiderato nel computer in uso, selezionarlo e fare clic su OK.  
   
    Avvia il caricamento di Hello ed è possibile visualizzare lo stato di avanzamento hello in nome file hello.  

Una volta completato il caricamento di hello, si noterà nuovo asset hello elencati in hello **asset** finestra. 

## <a name="next-steps"></a>Passaggi successivi
Ora è possibile codificare gli asset caricati. Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).

È possibile utilizzare anche funzioni Azure tootrigger un processo di codifica in base a un file in arrivo nel contenitore hello configurato. Per altre informazioni, vedere [questo esempio](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

