---
title: applicazioni di lettore video aaaDevelop
description: "argomento Hello tooPlayer Framework collegamenti e i plug-in che è possibile utilizzare toodevelop proprie applicazioni client che utilizzano i flussi multimediali da servizi multimediali."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>Sviluppo di applicazioni di lettore video
## <a name="overview"></a>Panoramica
Servizi multimediali di Azure fornisce gli strumenti hello necessario toocreate completi, applicazioni di lettore client dinamiche per la maggior parte delle piattaforme, tra cui: iOS, dispositivi, i dispositivi Android, Windows, Windows Phone, Xbox e Set-top caselle. In questo argomento fornisce inoltre i collegamenti tooSDKs e Player Framework che è possibile utilizzare toodevelop proprie applicazioni client che utilizzano i flussi multimediali da servizi multimediali di Azure.

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 
 
## <a name="azure-media-player"></a>Azure Media Player
[Azure Media Player](http://aka.ms/ampinfo) un lettore video web compilato tooplay indietro i contenuti multimediali da servizi multimediali di Microsoft Azure su una vasta gamma di browser e dispositivi. Azure Media Player utilizza standard del settore, ad esempio HTML5, supporto di origine Extensions (MSE) e le estensioni di supporto crittografato (EME) tooprovide un'esperienza di streaming adattivo approfondita. Se questi standard non sono disponibili in un dispositivo o in un browser, Azure Media Player usa una tecnologia di fallback come Flash o Silverlight. Indipendentemente dalla tecnologia di riproduzione hello usata, gli sviluppatori avranno un tooaccess di interfaccia unificata JavaScript API. In questo modo per il contenuto fornito da servizi multimediali di Azure toobe riprodotto in un'ampia gamma di dispositivi e browser senza alcuno sforzo aggiuntivo.

Servizi multimediali di Microsoft Azure consente toobe contenuto fornito con DASH, Smooth Streaming e HLS tooplay formati di streaming di eseguire il contenuto. Azure Media Player prende in considerazione questi diversi formati e automaticamente svolto hello collegamento migliore in base alle funzionalità di piattaforma/browser hello. Servizi multimediali di Microsoft Azure consente inoltre la crittografia dinamica degli asset con la crittografia PlayReady o la crittografia della busta AES a 128 bit. Anche Azure Media Player consente la decrittografia di contenuti crittografati con PlayReady o AES a 128 bit, se correttamente configurati. 

Per altre informazioni:

* [Azure Media Player](http://aka.ms/ampinfo)
* [Documentazione di Azure Media Player](http://aka.ms/ampdocs) 
* [Blog di introduzione ad Azure Media Player](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [Effettuare l'iscrizione toostay backup toodate con hello più recenti da Azure Media Player](http://aka.ms/ampsignup)
* [Aggiungere richieste di nuove funzionalità, idee e commenti e suggerimenti](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>Altri strumenti per la creazione di applicazioni di lettore
È inoltre possibile utilizzare uno qualsiasi dei seguenti SDK hello:

* [Smooth Streaming Client SDK](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [App Smooth Streaming Windows Store](media-services-build-smooth-streaming-apps.md)
* [Microsoft Media Platform: Player Framework](http://playerframework.codeplex.com/) 
* [Documentazione di HTML5 Player Framework](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [Plug-in Microsoft Smooth Streaming per OSMF](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Licenza per Microsoft® Smooth Streaming Client Porting Kit](http://aka.ms/sspk) 
* [Sviluppo di applicazioni video per XBox](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>Pubblicità
Servizi multimediali di Azure fornisce il supporto per l'inserimento di annunci tramite hello Windows Media Platform: Player Framework. Player Framework con supporto per gli annunci sono disponibili per i dispositivi Windows 8, Silverlight, Windows Phone 8 e iOS. Ogni player framework contiene un codice di esempio che illustra come tooimplement un'applicazione Windows Media player. Nei file multimediali è possibile inserire tre tipi di annunci.

Lineari: annunci con frequenza massima che Pausa video principale hello

Non lineari: annunci sovrapposti visualizzati durante la riproduzione di video principale hello, in genere un logo o altra immagine statica inserito all'interno di Windows Media player hello

Complementari: annunci visualizzati all'esterno di Windows Media player hello

Gli annunci possono essere inseriti in qualsiasi punto della sequenza temporale del video principale hello. È necessario indicare quando tooplay hello Active Directory e che il lettore hello tooplay annunci. Questa operazione viene eseguita mediante una serie di file standard basati su XML: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) e Digital Video Player Ad Interface Definition (VPAID). I file VAST specificano quali toodisplay annunci. File VMAP specificano quando tooplay vari annunci e contengono XML VAST. I file MAST rappresentano un altro toosequence annunci di modo che possono contenere XML VAST. I file VPAID definiscono un'interfaccia tra lettore video hello e ad hello o un server Active Directory. Per altre informazioni, vedere [Inserimento di annunci](https://msdn.microsoft.com/library/dn387398.aspx).

Per informazioni sul supporto di sottotitoli codificati e annunci nei video in streaming live, vedere [Sottotitoli codificati supportati e standard per l'inserimento di annunci](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Integrazione di uno streaming video adattivo MPEG-DASH in un'applicazione HTML5 con DASH.js](media-services-embed-mpeg-dash-in-html5.md)

[Repository dash.js di GitHub](https://github.com/Dash-Industry-Forum/dash.js)

