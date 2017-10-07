---
title: aaaGet avviato con recapito tramite il portale di Azure hello VoD | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello dell'implementazione di un servizio di distribuzione di contenuti video on Demand (VoD) base con l'applicazione di servizi multimediali di Azure (AMS) utilizzando hello portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a>Iniziare con la distribuzione di contenuti su richiesta utilizzando hello portale di Azure
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

In questa esercitazione vengono illustrati i passaggi hello dell'implementazione di un servizio di distribuzione di contenuti video on Demand (VoD) base con l'applicazione di servizi multimediali di Azure (AMS) utilizzando hello portale di Azure.

## <a name="prerequisites"></a>Prerequisiti
di seguito Hello sono esercitazione hello toocomplete necessarie:

* Un account Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Account di Servizi multimediali. toocreate un account di servizi multimediali, vedere [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).

In questa esercitazione include hello seguenti attività:

1. Avviare l'endpoint di streaming.
2. Caricare un file video.
3. Codificare il file di origine hello in un set di file MP4 a velocità in bit adattiva.
4. Pubblicare l'asset hello e get streaming e l'URL di download progressivo.  
5. Riprodurre i contenuti.

## <a name="start-streaming-endpoints"></a>Avviare gli endpoint di streaming 

Quando si lavora con uno degli scenari più comuni di hello recapita video tramite velocità in bit adattive servizi multimediali di Azure. Servizi multimediali fornisce creazione dinamica dei pacchetti, che consente di toodeliver la velocità in bit adattiva contenuto MP4 in formato con codificata in streaming formati supportati da servizi multimediali (MPEG DASH, HLS, Smooth Streaming) just-in-time, senza che sia necessario toostore preconfezionata versioni di ciascuno di questi formati di streaming.

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 

toostart hello endpoint di streaming, hello seguenti:

1. Accedere all'indirizzo hello [portale di Azure](https://portal.azure.com/).
2. Nella finestra Impostazioni hello, fare clic su endpoint di Streaming. 
3. Fare clic su predefinito hello endpoint di streaming. 

    verrà visualizzata la finestra Dettagli dell'ENDPOINT di STREAMING predefinito Hello.

4. Fare clic sull'icona di avvio hello.
5. Fare clic su toosave pulsante di hello Salva le modifiche.

## <a name="upload-files"></a>Caricare file
toostream video tramite servizi multimediali di Azure, è necessario video di origine tooupload hello, codificarli in più velocità in bit e pubblicare i risultati di hello. in questa sezione verrà illustrata innanzitutto Hello. 

1. In hello **impostazione** finestra, fare clic su **asset**.
   
    ![Caricare file](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. Fare clic su hello **caricare** pulsante.
   
    Hello **caricare una risorsa video** verrà visualizzata la finestra.
   
   > [!NOTE]
   > Non esistono limiti alle dimensioni dei file.
   > 
   > 
3. Sfoglia video toohello desiderato nel computer in uso, selezionarlo e fare clic su OK.  
   
    Avvia il caricamento di Hello ed è possibile visualizzare lo stato di avanzamento hello in nome file hello.  

Una volta completato il caricamento di hello, viene visualizzato di nuovo asset hello elencati in hello **asset** finestra. 

## <a name="encode-assets"></a>Codificare gli asset

Quando si lavora con servizi multimediali di Azure offre uno degli scenari più comuni di hello client tooyour streaming velocità in bit adattiva. Servizi multimediali supporta hello velocità in bit adattive tecnologie seguente: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare i video per lo streaming a velocità in bit adattiva, è necessario tooencode l'origine video in file più velocità in bit. È consigliabile utilizzare hello **Media Encoder Standard** tooencode codificatore video.  

Servizi multimediali offre anche creazione dinamica dei pacchetti, che consente di toodeliver MP4s l'asset MP4 in hello seguenti formati di streaming: MPEG DASH, HLS, Smooth Streaming, senza che sia necessario toorepackage in questi formati di streaming. Con creazione dinamica dei pacchetti, è necessario solo toostore e pagare per i file hello in unico formato di archiviazione e servizi multimediali di compilazioni e opera in base alle richieste da un client la risposta appropriata hello.

Il vantaggio di tootake creazione dinamica dei pacchetti, è necessario tooencode il file di origine in un set di file MP4 a più velocità in bit (hello codifica passaggi sono illustrati più avanti in questa sezione).

### <a name="toouse-hello-portal-tooencode"></a>toouse hello portale tooencode
In questa sezione descrive i passaggi di hello è possibile eseguire tooencode il contenuto con Media Encoder Standard.

1. In hello **impostazioni** selezionare **asset**.  
2. In hello **asset** finestra, che si desidera tooencode asset di hello selezionare.
3. Hello premere **Encode** pulsante.
4. In hello **codificare un asset** finestra e processore "Media Encoder Standard" hello selezionare un set di impostazioni. Per informazioni sui set di impostazioni, vedere [Generare automaticamente un bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) e [Set di impostazioni delle attività MES](media-services-mes-presets-overview.md). Se si prevede di toocontrol viene utilizzato il set di impostazioni di codifica, questo tenere presenti: è importante hello tooselect set di impostazioni che è più appropriato per il video di input. Ad esempio, se si conosce il video di input dispone di una risoluzione di 1920x1080 pixel, è possibile utilizzare hello "H264 bitrate multiplo con risoluzione 1080p" predefinito. Se il video disponibile è a bassa risoluzione (640x360), non usare il set di impostazioni "Codec video H.264 a bitrate multiplo con risoluzione 1080p".
   
   Per facilitare la gestione, è un'opzione di modifica nome hello dell'asset di output di hello e nome hello del processo di hello.
   
   ![Codificare gli asset](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. Fare clic su **Crea**.

### <a name="monitor-encoding-job-progress"></a>Monitorare lo stato del processo di codifica
lo stato di avanzamento di toomonitor hello di hello codifica processo, fare clic su **impostazioni** (in alto hello hello pagina) e quindi selezionare **processi**.

![Processi](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a>Pubblicare contenuti
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

> [!NOTE]
> Se si utilizza i localizzatori toocreate portale hello prima marzo 2015, sono stati creati i localizzatori con una data di scadenza di due anni.  
> 
> 

tooupdate data di scadenza su un indicatore di posizione, utilizzare [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API. Quando si aggiorna la data di scadenza hello di un localizzatore SAS, hello URL cambia.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello portale toopublish un asset
toouse hello portale toopublish un asset, hello seguenti:

1. Selezionare **Impostazioni** > **Asset**.
2. Selezionare asset hello che si desidera toopublish.
3. Fare clic su hello **pubblica** pulsante.
4. Selezionare il tipo di localizzatore hello.
5. Fare clic su **Aggiungi**.
   
    ![Pubblica](./media/media-services-portal-vod-get-started/media-services-publish1.png)

URL di Hello viene aggiunto l'elenco toohello di **URL pubblicato**.

## <a name="play-content-from-hello-portal"></a>Riprodurre il contenuto dal portale hello
portale di Azure Hello fornisce un lettore di contenuti che è possibile utilizzare tootest video.

Fare clic su video hello desiderato e quindi fare clic su hello **riprodurre** pulsante.

![Pubblica](./media/media-services-portal-vod-get-started/media-services-play.png)

Considerazioni applicabili:

* toobegin streaming, avviare hello in esecuzione **predefinito** endpoint di streaming.
* Verificare che sia stato pubblicato hello video.
* Questo **Media player** riprodotto dal valore predefinito di hello endpoint di streaming. Se si desidera tooplay da un valore non predefinito, endpoint di streaming fare clic su URL hello toocopy e usare un altro lettore. ad esempio [Lettore di Servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

## <a name="next-steps"></a>Passaggi successivi
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

