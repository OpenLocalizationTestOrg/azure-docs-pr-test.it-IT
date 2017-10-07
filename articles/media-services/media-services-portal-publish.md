---
title: aaa"pubblicare il contenuto con hello portale di Azure | Documenti di Microsoft"
description: In questa esercitazione vengono illustrati i passaggi hello della pubblicazione del contenuto con hello portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>Pubblicare il contenuto con hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Panoramica
> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

tooprovide l'utente con un URL che possa essere utilizzati toostream o scaricare il contenuto, è innanzitutto necessario troppo "pubblica" l'asset creando un localizzatore. I localizzatori forniscono accesso toofiles contenuti in hello asset. Servizi multimediali supporta due tipi di localizzatori: 

* Streaming localizzatori (OnDemandOrigin) usati per streaming adattivo (ad esempio, toostream MPEG DASH, HLS o Smooth Streaming). toocreate un localizzatore di streaming dell'asset deve contenere un file con estensione ISM. 
* Localizzatori progressivi (SAS) usati per la distribuzione di video tramite download progressivo.

È possibile utilizzare asset Smooth Streaming tooplay un URL di streaming ha hello seguente formato.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

aggiungere toobuild un URL di streaming HLS (formato = m3u8-aapl) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

aggiungere toobuild un URL di streaming di contenuto MPEG DASH (formato = mpd-tempo-csf) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

Un URL SAS è hello seguente formato.

    {blob container name}/{asset name}/{file name}/{SAS signature}

Per altre informazioni, vedere [Panoramica della distribuzione di contenuti](media-services-deliver-content-overview.md).

> [!NOTE]
> Se si utilizza i localizzatori toocreate portale hello prima marzo 2015, sono stati creati con una data di scadenza per anno a due indicatori di posizione.  
> 
> 

tooupdate data di scadenza su un indicatore di posizione, utilizzare [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API. Si noti che quando si aggiorna la data di scadenza hello di un localizzatore SAS, hello URL viene modificato.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello portale toopublish un asset
toouse hello portale toopublish un asset, hello seguenti:

1. In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.
2. Selezionare **Impostazioni** > **Asset**.
3. Selezionare asset hello che si desidera toopublish.
4. Fare clic su hello **pubblica** pulsante.
5. Selezionare il tipo di localizzatore hello.
6. Fare clic su **Aggiungi**.
   
    ![Pubblica](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Hello URL verrà aggiunto l'elenco toohello di **URL pubblicato**.

## <a name="play-content-from-hello-portal"></a>Riprodurre il contenuto dal portale hello
portale di Azure Hello fornisce un lettore di contenuti che è possibile utilizzare tootest video.

Fare clic su video hello desiderato e quindi fare clic su hello **riprodurre** pulsante.

![Pubblica](./media/media-services-portal-vod-get-started/media-services-play.png)

Considerazioni applicabili:

* Verificare che sia stato pubblicato hello video.
* Questo **Media player** riprodotto dal valore predefinito di hello endpoint di streaming. Se si desidera tooplay da un valore non predefinito, endpoint di streaming fare clic su URL hello toocopy e usare un altro lettore. ad esempio [Lettore di Servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
* Hello da cui si utilizza il flusso di endpoint di streaming deve essere in esecuzione.  

## <a name="next-steps"></a>Passaggi successivi
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

