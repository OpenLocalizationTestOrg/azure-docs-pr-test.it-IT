---
title: Cenni preliminari sulla creazione dinamica dei pacchetti di servizi multimediali aaaAzure | Documenti Microsoft
description: Consente di argomento Hello e Cenni preliminari sulla creazione dinamica dei pacchetti.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>creazione dinamica dei pacchetti
## <a name="overview"></a>Panoramica
Servizi multimediali di Microsoft Azure può essere utilizzato toodeliver un'origine multimediale molti formati di file, formati di streaming multimediali e la protezione del contenuto formati tooa varie tecnologie client (ad esempio, iOS, XBOX, Silverlight, Windows 8). Questi client supportano tuttavia protocolli diversi. iOS, ad esempio, richiede un formato HTTP Live Streaming (HLS) V4, mentre Silverlight e Xbox richiedono Smooth Streaming. Se si dispone di un set di velocità in bit adattiva (più velocità in bit) MP4 file (ISO Base Media 14496-12) o un set di file Smooth Streaming a velocità in bit adattiva che si desidera tooclients tooserve che supportano contenuto MPEG DASH, HLS o Smooth Streaming, è opportuno avvalersi del supporto I servizi di creazione dinamica dei pacchetti.

Creazione di pacchetti dinamiche tutto che il necessario è toocreate un asset che contiene un set di file MP4 o file Smooth Streaming a velocità in bit adattiva. Quindi, base hello formato specificato nel manifesto hello o frammentare la richiesta, hello server ti garantisce che il flusso di hello nel protocollo hello che si è scelto di Streaming On Demand. Di conseguenza, è necessario solo toostore e pagare per i file hello in unico formato di archiviazione e servizi multimediali creerà e fornirà hello risposta appropriata in base alle richieste da un client.

Hello diagramma seguente mostra la codifica tradizionale hello e flusso di lavoro di creazione statica dei pacchetti.

![Codifica statica](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

Hello diagramma seguente mostra del flusso di lavoro di hello creazione dinamica dei pacchetti.

![Codifica dinamica](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>Scenario comune
1. Caricare un file di input (detto file in formato intermedio). Ad esempio, h. 264, MP4 o WMV (per l'elenco di hello dei formati supportati, vedere [formati supportati da Media Encoder Standard hello](media-services-media-encoder-standard-formats.md).
2. Codificare i set di velocità in bit adattiva in formato intermedio in file MP4 tooH.264.
3. Pubblicare l'asset di hello contenente hello velocità in bit adattiva set MP4 creando hello localizzatore su richiesta.
4. Compilare hello tooaccess gli URL di streaming e lo streaming del contenuto.

## <a name="preparing-assets-for-dynamic-streaming"></a>Preparazione di asset per lo streaming dinamico
tooprepare l'asset per streaming è dinamico sono disponibili due opzioni:

1. [Caricare un file master](media-services-dotnet-upload-files.md).
2. [Utilizzare set di hello Media Encoder Standard codificatore tooproduce MP4 h. 264 velocità in bit adattiva](media-services-dotnet-encode-with-media-encoder-standard.md).
3. [Trasmettere i contenuti in streaming](media-services-deliver-content-overview.md).

## <a id="unsupported_formats"></a>Formati non supportati dalla creazione dinamica dei pacchetti
Hello seguenti formati di file di origine non sono supportati dalla creazione dinamica dei pacchetti.

* File Dolby Digital MP4.
* File Dolby Digital Smooth.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

