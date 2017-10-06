---
title: flusso aaaLive con codificatori locali tramite il portale di Azure hello | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di creazione di un canale configurato per un'operazione di recapito pass-through.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>Come tooperform live streaming con locale codificatori utilizzando hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

In questa esercitazione illustra i passaggi hello di hello toocreate portale Azure utilizzando un **canale** che è configurato per un'operazione di recapito pass-through. 

## <a name="prerequisites"></a>Prerequisiti
di seguito Hello sono esercitazione hello toocomplete necessarie:

* Un account Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Account di Servizi multimediali. toocreate un account di servizi multimediali, vedere [come un Account di servizi multimediali tooCreate](media-services-portal-create-account.md).
* Una webcam. Ad esempio, [codificatore Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).

Si consiglia di hello tooreview seguenti articoli:

* [Codificatori live e supporto RTMP di Servizi multimediali di Azure](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [Panoramica di Live Streaming con Servizi multimediali di Azure](media-services-manage-channels-overview.md)
* [Streaming live con codificatori locali che creano flussi a bitrate multipli](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>Scenario comune di streaming live
Hello passaggi seguenti descrivono le attività coinvolte nella creazione comuni in tempo reale lo streaming di applicazioni che utilizzano canali vengono configurati per il recapito pass-through. Questa esercitazione viene illustrato come toocreate e gestire un canale di tipo pass-through e gli eventi in tempo reale.

>[!NOTE]
>Assicurarsi che sia hello endpoint da cui si desidera toostream contenuto di streaming in hello **esecuzione** stato. 
    
1. Connettere un computer tooa videocamera. Avviare e configurare un codificatore live locale che genera un flusso in formato RTMP o MP4 frammentato a più bitrate. Per altre informazioni, vedere l'argomento relativo a [codificatori live e supporto RTMP di Servizi multimediali di Azure](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Questa operazione può essere eseguita anche dopo la creazione del canale.
2. Creare e avviare un canale pass-through.
3. URL di inserimento recuperare hello del canale. 
   
    URL di inserimento Hello viene utilizzato dal codificatore live di hello toosend hello flusso toohello canale.
4. Recuperare l'URL di anteprima del canale hello. 
   
    Utilizzare questo tooverify URL che il canale riceve correttamente flusso live hello.
5. Creare un programma o un evento live. 
   
    Quando tramite hello portale di Azure, creazione di un evento in tempo reale crea inoltre un asset. 

6. Avviare hello evento/quando sei pronto toostart streaming e l'archiviazione.
7. Facoltativamente, codificatore live hello può essere segnalato toostart un annuncio. annuncio Hello viene inserito nel flusso di output di hello.
8. Arrestare hello evento/programma ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello.
9. Eliminare evento hello/programma (e facoltativamente elimina hello asset).     

> [!IMPORTANT]
> Consultare [Live streaming con codificatori locali che creano flussi più velocità in bit](media-services-live-streaming-with-onprem-encoders.md) toolearn sui concetti e considerazioni correlate toolive streaming con codificatori locali e i canali di tipo pass-through.
> 
> 

## <a name="tooview-notifications-and-errors"></a>errori e le notifiche tooview
Se si desidera tooview notifiche e gli errori generati da hello portale di Azure, fare clic sull'icona di notifica hello.

![Notifiche](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>Creare e avviare eventi e canali pass-through
Un canale è associato a eventi e i programmi che consentono la pubblicazione di hello toocontrol e l'archiviazione di segmenti in un flusso in tempo reale. Gli eventi sono gestiti dai canali. 

È possibile specificare hello numero di ore che si vuole tooretain hello registrato contenuto per il programma hello, impostazione hello **finestra archivio** lunghezza. Questo valore può essere impostato da un minimo di 25 ore massimo tooa 5 minuti. Lunghezza dell'intervallo di archiviazione determina anche l'intervallo di tempo i client possono cercare indietro nel tempo dalla posizione live corrente hello massimo hello. Gli eventi è possono eseguire sul periodo di tempo specificato hello, ma il contenuto che non è sincronizzato con la lunghezza della finestra hello viene scartato in modo continuo. Questo valore di questa proprietà determina anche per quanto tempo hello client possono raggiungere i manifesti.

Ogni evento è associato a un asset. evento hello toopublish, è necessario creare un localizzatore OnDemand per asset hello associata. Con questo localizzatore consente si toobuild un URL di streaming che è possibile fornire tooyour client.

Un canale supporta fino toothree in esecuzione simultanea di eventi in modo è possibile creare più archivi di hello stesso flusso in ingresso. In questo modo toopublish e archiviare parti diverse di un evento in base alle esigenze. Ad esempio, il requisito di business è tooarchive 6 ore di un programma, ma toobroadcast solo ultimi 10 minuti. tooaccomplish, è necessario toocreate due programmi in esecuzione simultanea. Un programma è impostato tooarchive 6 ore dell'evento hello ma hello non viene pubblicato. Hello altro programma è tooarchive insieme per 10 minuti e questo programma viene pubblicato.

Non riutilizzare eventi live esistenti, ma creare e avviare un nuovo evento per ogni evento.

Avviare eventi hello quando sei pronto toostart streaming e l'archiviazione. Arrestare il programma hello ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello. 

contenuto toodelete archiviato, interrompere ed eliminare evento hello e quindi eliminare asset associato hello. Non è possibile eliminare un asset se è utilizzato da un evento. evento Hello deve prima essere eliminato. 

Anche dopo aver arrestato ed eliminato evento hello, hello gli utenti sarebbero in grado di toostream il contenuto archiviato come video on demand, per fino a quando non si elimina asset hello.

Se si desidera hello tooretain archiviato il contenuto, ma non è disponibile per lo streaming, eliminare hello localizzatore di streaming.

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse hello portale toocreate un canale
Questa sezione viene illustrato come hello toouse **creazione rapida** opzione toocreate un canale di tipo pass-through.

Per informazioni più dettagliate sui canali pass-through, vedere [Streaming live con codificatori locali che creano flussi a bitrate multipli](media-services-live-streaming-with-onprem-encoders.md).

1. In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.
2. In hello **impostazioni** finestra, fare clic su **Live streaming**. 
   
    ![introduttiva](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    Hello **Live streaming** verrà visualizzata la finestra.
3. Fare clic su **creazione rapida** toocreate un canale di tipo pass-through con hello RTMP protocollo di inserimento.
   
    Hello **creare un nuovo canale** verrà visualizzata la finestra.
4. Assegnare un nome di nuovo canale hello e fare clic su **crea**. 
   
    Ciò consente di creare un canale pass-through con hello protocollo di inserimento RTMP.

## <a name="create-events"></a>Creare eventi
1. Selezionare un canale toowhich desiderato tooadd un evento.
2. Premere il pulsante **Evento live** .

![Evento](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>Ottenere gli URL di inserimento
Una volta creato il canale di hello, è possibile ottenere l'URL che verrà fornito codificatore live toohello di inserimento. codificatore Hello utilizza questi tooinput URL di un flusso in tempo reale.

![Data di creazione](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>Evento hello espressioni di controllo
evento hello toowatch, fare clic su **espressioni di controllo** in hello Azure portal o copia a hello URL di streaming e usare un lettore di propria scelta. 

![Data di creazione](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

Evento Live ottengono automaticamente contenuto richiesta tooon convertito all'arresto.

## <a name="clean-up"></a>Eseguire la pulizia
Per informazioni più dettagliate sui canali pass-through, vedere [Streaming live con codificatori locali che creano flussi a bitrate multipli](media-services-live-streaming-with-onprem-encoders.md).

* Un canale può essere arrestato solo quando tutti gli eventi i programmi sul canale hello è stati arrestati.  Una volta hello canale viene interrotto, non è soggetta eventuali addebiti. Quando è necessario toostart nuovamente, disporrà di hello stesso URL di inserimento in modo non sarà necessario tooreconfigure codificatore.
* Un canale può essere eliminato solo quando sono stati eliminati tutti gli eventi in tempo reale sul canale hello.

## <a name="view-archived-content"></a>Visualizzare il contenuto archiviato
Anche dopo aver arrestato ed eliminato evento hello, hello gli utenti sarebbero in grado di toostream il contenuto archiviato come video on demand, per fino a quando non si elimina asset hello. Non è possibile eliminare un asset se è utilizzato da un evento. evento Hello deve prima essere eliminato. 

Selezionare le risorse, toomanage **impostazione** e fare clic su **asset**.

![Asset](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>Passaggio successivo
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

