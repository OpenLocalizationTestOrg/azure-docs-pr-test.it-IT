---
title: aaaUse esistente lettori tooplayback contenuti - Azure | Documenti Microsoft
description: "Questo argomento elenca i lettori esistenti che è possibile utilizzare tooplayback il contenuto."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 54817345a19a9d3b18f1e7b352c3342043a569b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="playing-your-content-with-existing-players"></a>Riproduzione di contenuti con i lettori esistenti
Servizi multimediali di Azure supporta molti formati di streaming noti, ad esempio Smooth Streaming, HTTP Live Streaming (HLS) e MPEG-DASH. Questo argomento vengono elencati i lettori tooexisting che è possibile utilizzare tootest i flussi.

### <a name="hello-azure-portal-media-services-content-player"></a>il portale di Azure Media Services Hello contenuto Windows Media player
Hello **Azure** portal fornisce un lettore di contenuti che è possibile utilizzare tootest video.

Fare clic su hello desiderato video (verificare sia stato [pubblicati](media-services-portal-publish.md)) e fare clic su hello **riprodurre** pulsante nella parte inferiore di hello del portale hello.

Considerazioni applicabili:

* Hello **servizi LETTORE** riprodotto dal valore predefinito di hello endpoint di streaming. Se si desidera tooplay da un endpoint di streaming non predefinito, utilizzare un altro lettore. ad esempio [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure Media Player
Utilizzare [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback il contenuto in uno dei seguenti formati hello (crittografato o protetto):

* Smooth Streaming
* MPEG DASH
* HLS
* MP4 progressivo

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>Con crittografia AES con token
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Lettori Silverlight
#### <a name="monitoring"></a>Monitoraggio
[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady con token
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>Lettori DASH
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>Altre
è inoltre possibile utilizzare gli URL di HLS tootest:

* **Safari** in un dispositivo iOS o
* **Lettore HLS 3ivx** in un dispositivo Windows.

## <a name="developing-video-players"></a>Sviluppo di lettori video
Per informazioni su come toodevelop lettori personalizzati, vedere [sviluppare lettori video](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
