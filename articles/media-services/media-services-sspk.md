---
title: "Microsoft® Smooth Streaming Client Porting Kit aaaLicensing"
description: "Informazioni su come toolicensing hello Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a>Licenza per Microsoft® Smooth Streaming Client Porting Kit
## <a name="overview"></a>Panoramica
Microsoft Smooth Streaming Client Porting Kit (**SSPK** breve) è un'implementazione client Smooth Streaming ottimizzata toohelp incorporato produttori di dispositivi, via cavo e operatori di telefonia mobile, i provider di servizi di contenuto, palmari produttori di fornitori di software indipendenti (ISV) e i prodotti toocreate di provider di soluzioni e servizi per la trasmissione di flussi adattivi in formato Smooth Streaming. SSPK è un'implementazione indipendente dal dispositivo e piattaforma del client Smooth Streaming che possono essere trasferite dalla piattaforma e hello Licenziatario tooany dispositivo. 

Incluso di seguito è un'architettura di alto livello e consente di IIS Smooth Streaming Porting Kit è hello Smooth Streaming Client implementazione fornita da Microsoft e di includere tutta la logica hello core per la riproduzione del contenuto Smooth Streaming. Questa implementazione viene quindi applicata dai partner a una piattaforma o un dispositivo specifico mediante l'implementazione di interfacce appropriate. 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a>Descrizione
SSPK è concesso in licenza a condizioni che offrono un valore aziendale eccellente. Licenza SSPK fornisce settore hello con:

* Codice sorgente di Smooth Streaming Porting Kit in C++ 
  * implementa la funzionalità client di Smooth Streaming Client
  * aggiunge analisi del formato, euristica, logica di buffering e così via.
* API dell'applicazione lettore 
  * interfacce di programmazione per l'interazione con un'applicazione lettore multimediale
* Interfaccia Platform Abstraction Layer (PAL) 
  * interfacce di programmazione per l'interazione con il sistema operativo hello (thread, socket)
* Interfaccia Hardware Abstraction Layer (HAL) 
  * interfacce di programmazione per l'interazione con un decodificatore A/V hardware (decodifica, rendering)
* Interfaccia Digital Rights Management (DRM) 
  * interfacce di programmazione per la gestione di DRM tramite hello DRM Abstraction Layer (DAL)
  * Microsoft PlayReady Porting Kit viene fornito separatamente, ma si integra tramite questa interfaccia. Per altri dettagli sulle licenze Microsoft PlayReady Device, fare clic [qui](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).
* Esempi di implementazione 
  * implementazione PAL di esempio per Linux
  * implementazione HAL di esempio per GStreamer

## <a name="licensing-options"></a>Opzioni di licenza
Microsoft Smooth Streaming Client Porting Kit viene effettuata toolicensees disponibile in due contratti di licenza distinte: una per lo sviluppo di Smooth Streaming Client provvisorio prodotti e un altro per la distribuzione agli utenti di tooend Smooth Streaming Client prodotto finale.

* Per produttori chipset, integratori di sistema o software indipendenti (Vendor) che richiedono un codice di origine porting kit toodevelop provvisorio prodotti, una Microsoft Smooth Streaming Client Porting Kit **licenza del prodotto provvisorio** deve essere eseguito.
* Per i produttori di dispositivi o gli ISV che necessitano di diritti di distribuzione per gli utenti tooend Smooth Streaming Client finale prodotti, hello Microsoft Smooth Streaming Client Porting Kit **licenza del prodotto finale** deve essere eseguito.

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a>Interim Product License di Microsoft Smooth Streaming Client Porting Kit
Con questa licenza, Microsoft offre un Smooth Streaming Client Porting Kit e hello toodevelop diritti di proprietà intellettuale necessari e distribuire Smooth Streaming Client provvisorio prodotti tooother Smooth Streaming Client Porting Kit dispositivo i titolari di licenze che distribuire Smooth Streaming Client prodotto finale.

#### <a name="fee-structure"></a>Struttura tariffaria
Una quota di licenza monouso 50.000 dollari fornisce accesso toohello Smooth Streaming Client Porting Kit. 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a>Final Product License di Microsoft Smooth Streaming Client Porting Kit
In questo tipo di licenza, Microsoft offre tutte le necessarie tooreceive di diritti di proprietà intellettuale Smooth Streaming Client provvisorio prodotti da altri licenziatari Smooth Streaming Client Porting Kit e toodistribute aziendale personalizzata Smooth Streaming Client finale Utenti tooend di prodotti.

#### <a name="fee-structure"></a>Struttura tariffaria
Hello Smooth Streaming Client finale del prodotto è disponibile in un modello di royalty come in:

* USD 0,10 per ogni implementazione di dispositivo fornita
* royalty Hello è limitato a 50.000 ogni anno
* Nessun diritto per le prime 10.000 implementazioni di dispositivi ogni anno 

## <a name="licensing-procedure-and-sspk-access"></a>Procedura di gestione delle licenze e accesso a SSPK
Per domande relative alla gestione delle licenze, inviare un messaggio di posta elettronica a [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) .

Hello [portale distribuzione SSPK](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) è accessibile tooregistered licenziatari provvisorio.

I titolari di licenze provvisorio e SSPK finale possono inviare domande tecniche troppo[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a>Licenziatari di contratti Microsoft Smooth Streaming Client Interim Product
* Adroit Business Solutions, Inc
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Alticast Corporation
* Amazon Digital Services, Inc.
* Arion Technology, Inc.
* AVC Multimedia Software Co., Ltd.
* Cavium, Inc.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Fluendo S.A.
* HANDAN BroadInfoCom Co., Ltd.
* Infomir GMBH
* Irdeto USA Inc.
* iWEDIA S.A. 
* Liberty Global Services BV
* MediaTek Inc.
* MStar Co, Ltd.
* Nintendo Co., Ltd.
* OpenTV, Inc.
* Saffron Digital Limited
* Sichuan Changhong Electric Co., Ltd
* SoftAtHome
* Sony Corporation
* Tatung Technology Inc.
* TCL Technoly Electronics (Huizhou) Co., Ltd.
* Top Victory Investments, Ltd.
* Vestel Elektronik Sanayi ve Ticaret A.S.
* VisualOn, Inc.
* ZTE Corporation

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a>Licenziatari di contratti Microsoft Smooth Streaming Client Final Product
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Amazon Digital Services, Inc.
* AmTRAN Technology Co., Ltd.
* Arcadyan Technology Corporation
* Arion Technology, Inc.
* ATMACA ELEKTRONİK SAN. VE TİC. A.Ş
* British Sky Broadcasting Limited
* CastPal Technology Inc., Shenzhen
* Compal Electronics, Inc.
* Dongguan Digital AV Technology Corp., Ltd.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Filmflex Movies Limited
* Fluendo S.A.
* Gibson Innovations Limited
* Haier Information Applicantion S.R.L
* HANDAN BroadInfoCom Co., Ltd.
* Hisense International Co., Ltd. 
* Homecast Co.,Ltd
* Hon Hai Precision Industry Co., Ltd.
* Infomir GMBH
* Kaonmedia Co., Ltd.
* KDDI Corporation
* Nintendo Co., Ltd.
* Orange SA
* Saffron Digital Limited
* Sagemcom Broadband SAS
* Shenzhen Coship Electronics CO., LTD
* Shenzhen Jiuzhou Electric Co.,Ltd
* Shenzhen Skyworth Digital Technology Co., Ltd
* Sichuan Changhong Electric Co., Ltd.
* Skardin Industrial Corp.
* Sky Deutschland Fernsehen GmbH & Co. KG
* SmarDTV S.A.
* SoftAtHome
* Sony Corporation
* TCL Overseas Marketing (Macao Commercial Offshore) Limited
* Technicolor Delivery Technologies, SAS
* Tongfang Global Ltd.
* Top Victory Investments, Ltd.
* Toshiba Lifestyle Products & Services Corporation
* Universal Media Corporation /Slovakia/ s.r.o.
* VIZIO, Inc.
* Wistron Corporation
* ZTE Corporation


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

