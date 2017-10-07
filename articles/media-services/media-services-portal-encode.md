---
title: aaaEncode un asset con Media Encoder Standard hello portale di Azure | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di codifica un asset con Media Encoder Standard hello portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>Codificare un asset con Media Encoder Standard hello portale di Azure
> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Quando si lavora con servizi multimediali di Azure offre uno degli scenari più comuni di hello client tooyour streaming velocità in bit adattiva. Servizi multimediali supporta hello velocità in bit adattive tecnologie seguente: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare i video per lo streaming a velocità in bit adattiva, è necessario tooencode l'origine video in file più velocità in bit. È consigliabile utilizzare hello **Media Encoder Standard** tooencode codificatore video.  

Servizi multimediali offre anche creazione dinamica dei pacchetti che consente di toodeliver MP4s l'asset MP4 in hello seguenti formati di streaming: MPEG DASH, HLS, Smooth Streaming, senza che sia necessario toore-package in questi formati di streaming. Con creazione dinamica dei pacchetti è necessario solo toostore e pagare per i file hello in unico formato di archiviazione e servizi multimediali creerà e fornirà hello risposta appropriata in base alle richieste da un client.

Il vantaggio di tootake creazione dinamica dei pacchetti, è necessario tooencode il file di origine in un set di file MP4 a più velocità in bit (hello codifica passaggi sono illustrati più avanti in questa sezione).

supporto tooscale l'elaborazione, vedere [questo](media-services-portal-scale-media-processing.md) argomento.

## <a name="encode-with-hello-azure-portal"></a>Codifica con hello portale di Azure
In questa sezione descrive i passaggi di hello è possibile eseguire tooencode il contenuto con Media Encoder Standard.

1. In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.
2. In hello **impostazioni** selezionare **asset**.  
3. In hello **asset** finestra, che si desidera tooencode asset di hello selezionare.
4. Hello premere **Encode** pulsante.
5. In hello **codificare un asset** finestra e processore "Media Encoder Standard" hello selezionare un set di impostazioni. Per informazioni sui set di impostazioni, vedere [Generare automaticamente un bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) e [Set di impostazioni delle attività MES](media-services-mes-presets-overview.md). Se si prevede di toocontrol viene utilizzato il set di impostazioni di codifica, questo tenere presenti: è importante hello tooselect set di impostazioni che è più appropriato per il video di input. Ad esempio, se si conosce il video di input dispone di una risoluzione di 1920x1080 pixel, è possibile utilizzare hello "H264 bitrate multiplo con risoluzione 1080p" predefinito. Se il video disponibile è a bassa risoluzione (640x360), non usare il set di impostazioni "Codec video H.264 a bitrate multiplo con risoluzione 1080p".
   
   Per facilitare la gestione, è un'opzione di modifica nome hello dell'asset di output di hello e nome hello del processo di hello.
   
   ![Codificare gli asset](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Fare clic su **Crea**.

## <a name="next-step"></a>Passaggio successivo
È possibile monitorare lo stato del processo codifica con hello portale di Azure, come descritto in [questo](media-services-portal-check-job-progress.md) articolo.  

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

