---
title: "aaaHow tooperform live streaming con flussi di servizi multimediali di Azure toocreate più velocità in bit hello portale di Azure | Documenti Microsoft"
description: "Questa esercitazione percorsi sono illustrati i passaggi hello di creazione di un canale che riceve un flusso live a velocità in bit singola e lo codifica flusso toomulti velocità in bit usando hello portale di Azure."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>Come tooperform lo streaming live usando servizi multimediali di Azure toocreate più velocità in bit flussi con hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [API REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

In questa esercitazione illustra hello passaggi della creazione di un **canale** che riceve un flusso live a velocità in bit singola e lo codifica flusso toomulti velocità in bit.

> [!NOTE]
> Per ulteriori informazioni teoriche tooChannels correlati che sono abilitati per la codifica live, vedere [Live streaming con flussi di servizi multimediali di Azure toocreate più velocità in bit](media-services-manage-live-encoder-enabled-channels.md).
> 
> 

## <a name="common-live-streaming-scenario"></a>Scenario comune di streaming live
di seguito Hello sono passaggi generali per la creazione di applicazioni comuni di streaming in tempo reale.

> [!NOTE]
> Attualmente, hello max consigliata la durata di un evento in tempo reale è 8 ore. Se è necessario un canale toorun per lunghi periodi di tempo, contattare amslived all'indirizzo Microsoft.com.
> 
> 

1. Connettere un computer tooa videocamera. Avviare e configurare un codificatore live locale che può restituire un flusso a velocità in bit singola in uno dei seguenti protocolli hello: RTP (MPEG-TS), Smooth Streaming o RTMP. Per altre informazioni, vedere l'argomento relativo a [codificatori live e supporto RTMP di Servizi multimediali di Azure](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Questa operazione può essere eseguita anche dopo la creazione del canale.
2. Creare e avviare un canale. 
3. URL di inserimento recuperare hello del canale. 
   
    URL di inserimento Hello viene utilizzato dal codificatore live di hello toosend hello flusso toohello canale.
4. Recuperare l'URL di anteprima del canale hello. 
   
    Utilizzare questo tooverify URL che il canale riceve correttamente flusso live hello.
5. Creare un evento o un programma, l'operazione creerà anche un asset. 
6. Pubblicare l'evento hello (che verrà creato un localizzatore OnDemand per asset associato hello).    
7. Avviare eventi hello quando sei pronto toostart streaming e l'archiviazione.
8. Facoltativamente, codificatore live hello può essere segnalato toostart un annuncio. annuncio Hello viene inserito nel flusso di output di hello.
9. Interrompere hello eventi ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello.
10. Eliminare un evento di hello (e facoltativamente elimina hello asset).   

## <a name="in-this-tutorial"></a>Contenuto dell'esercitazione:
In questa esercitazione, hello portale di Azure viene utilizzato tooaccomplish hello seguenti attività: 

1. Creare un canale che rappresenta la codifica tooperform abilitato in tempo reale.
2. Get hello URL di inserimento in ordine toosupply il codificatore toolive. codificatore live Hello utilizzerà questo flusso di hello tooingest URL in hello del canale.
3. Creare un evento o un programma e un asset.
4. Pubblicare l'asset hello e ottenere l'URL di streaming.  
5. Riprodurre i contenuti.
6. Pulizia.

## <a name="prerequisites"></a>Prerequisiti
di seguito Hello sono esercitazione hello toocomplete obbligatorio.

* toocomplete questa esercitazione, è necessario un account di Azure. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. 
  Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* Account di Servizi multimediali. toocreate un account di servizi multimediali, vedere [crea Account](media-services-portal-create-account.md).
* Una webcam e un codificatore in grado di inviare un flusso live a velocità in bit singola.

## <a name="create-a-channel"></a>Creare un canale
1. In hello [portale di Azure](https://portal.azure.com/), selezionare Servizi multimediali e quindi fare clic su nome account servizi multimediali.
2. Selezionare **Streaming live**.
3. Selezionare **Creazione personalizzata**. Questa opzione permette di creare un canale abilitato per la codifica live.
   
    ![Creare un CANALE](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. Fare clic su **Impostazioni**.
   
   1. Scegliere hello **codifica Live** tipo di canale. Questo tipo di specifica che si desidera toocreate un canale che è abilitato per la codifica live. Che indica hello in arrivo velocità in bit singola flusso inviato toohello canale e codificato in un flusso a più velocità in bit usando le impostazioni del codificatore live specificato. Per ulteriori informazioni, vedere [Live streaming con flussi di servizi multimediali di Azure toocreate più velocità in bit](media-services-manage-live-encoder-enabled-channels.md). Fare clic su OK.
   2. Specificare il nome di un canale.
   3. Fare clic su OK in basso hello hello.
5. Seleziona hello **inserimento** scheda.
   
   1. In questa pagina è possibile selezionare un protocollo di streaming. Per hello **codifica Live** sono di tipo di canale, le opzioni di protocollo valido:
      
      * MP4 frammentato (Smooth Streaming) a velocità in bit singola
      * RTMP a velocità in bit singola
      * RTP (MPEG-TS): MPEG-2 Transport Stream su RTP.
        
        Per informazioni dettagliate su ogni protocollo, vedere [Live streaming con flussi di servizi multimediali di Azure toocreate più velocità in bit](media-services-manage-live-encoder-enabled-channels.md).
        
        Non è possibile modificare l'opzione di protocollo hello durante hello canale o relativi eventi/programmi sono in esecuzione. Se sono necessari protocolli diversi, è necessario creare canali separati per ciascun protocollo di streaming.  
   2. È possibile applicare restrizioni IP a hello di inserimento. 
      
       È possibile definire IP hello gli indirizzi che sono consentiti tooingest un canale toothis video. Gli indirizzi IP consentiti possono essere specificati come un singolo indirizzo IP, ad esempio '10.0.0.1', come un intervallo IP usando un indirizzo IP e una subnet mask CIDR, ad esempio '10.0.0.1/22' o come un intervallo IP usando un indirizzo IP e una subnet mask decimale puntata, ad esempio '10.0.0.1(255.255.252.0)'.
      
       Se non viene specificato alcun indirizzo IP e non è presente una definizione della regola, non sarà consentito alcun indirizzo IP. tooallow qualsiasi indirizzo IP, creare una regola e impostare 0.0.0.0/0.
6. In hello **anteprima** scheda, applicare restrizioni IP anteprima hello.
7. In hello **codifica** , specificare set di impostazioni di codifica hello. 
   
    Attualmente, hello solo sistema predefinito, è possibile selezionare è **predefinito 720p**. un oggetto personalizzato toospecify predefinito, aprire un ticket di supporto Microsoft. Quindi, immettere il nome di hello di hello predefinito creato. 

> [!NOTE]
> Attualmente, hello canale iniziale può richiedere fino a too30 minuti. Reimpostazione del canale può richiedere too5 minuti.
> 
> 

Una volta creato il canale di hello, è possibile fare clic sul canale hello e selezionare **impostazioni** in cui è possibile visualizzare le configurazioni di canali. 

Per ulteriori informazioni, vedere [Live streaming con flussi di servizi multimediali di Azure toocreate più velocità in bit](media-services-manage-live-encoder-enabled-channels.md).

## <a name="get-ingest-urls"></a>Ottenere gli URL di inserimento
Una volta creato il canale di hello, è possibile ottenere l'URL che verrà fornito codificatore live toohello di inserimento. codificatore Hello utilizza questi tooinput URL di un flusso in tempo reale.

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>Creare e gestire eventi
### <a name="overview"></a>Panoramica
Un canale è associato a eventi e i programmi che consentono la pubblicazione di hello toocontrol e l'archiviazione di segmenti in un flusso in tempo reale. Eventi e programmi sono gestiti dai canali. Hello relazione canale e il programma è molto simile tootraditional media, in cui un canale è un flusso costante di contenuto e l'evento con ambito toosome timeout su tale canale è un programma.

È possibile specificare hello numero di ore che si vuole tooretain hello registrato contenuto per evento hello, impostazione hello **finestra archivio** lunghezza. Questo valore può essere impostato da un minimo di 25 ore massimo tooa 5 minuti. Lunghezza dell'intervallo di archiviazione determina anche l'intervallo di tempo i client possono cercare indietro nel tempo dalla posizione live corrente hello massimo hello. Gli eventi è possono eseguire sul periodo di tempo specificato hello, ma il contenuto che non è sincronizzato con la lunghezza della finestra hello viene scartato in modo continuo. Questo valore di questa proprietà determina anche per quanto tempo hello client possono raggiungere i manifesti.

Ogni evento è associato a un asset. evento hello toopublish è necessario creare un localizzatore OnDemand per hello associati asset. Con questo localizzatore sarà si toobuild un URL di streaming che è possibile fornire tooyour client.

Un canale supporta fino toothree in esecuzione simultanea di eventi in modo è possibile creare più archivi di hello stesso flusso in ingresso. In questo modo toopublish e archiviare parti diverse di un evento in base alle esigenze. Ad esempio, il requisito di business è tooarchive 6 ore di un evento, ma toobroadcast solo ultimi 10 minuti. tooaccomplish, è necessario toocreate due simultanee evento. Un evento è impostato tooarchive 6 ore dell'evento hello ma hello non viene pubblicato. Hello altri evento tooarchive insieme per 10 minuti di questo programma viene pubblicato.

Non riutilizzare i programmi esistenti per nuovi eventi. Al contrario, creare e avviare un nuovo programma per ogni evento.

Avviare un programma o di evento quando si è pronti toostart streaming e l'archiviazione. Interrompere hello eventi ogni volta che si desidera toostop streaming e l'archiviazione di eventi di hello. 

contenuto toodelete archiviato, interrompere ed eliminare evento hello e quindi eliminare asset associato hello. Se viene utilizzato dall'evento hello; non è possibile eliminare un asset evento Hello deve prima essere eliminato. 

Anche dopo aver arrestato ed eliminato evento hello, hello gli utenti sarebbero in grado di toostream il contenuto archiviato come video on demand, per fino a quando non si elimina asset hello.

Se si desidera hello tooretain archiviato il contenuto, ma non è disponibile per lo streaming, eliminare hello localizzatore di streaming.

### <a name="createstartstop-events"></a>Creare, avviare o arrestare eventi
Dopo aver flusso hello propagazione nel canale hello è possibile iniziare il flusso di eventi tramite la creazione di un Asset, un programma e un localizzatore di Streaming hello. Verrà archiviare flusso hello e renderlo disponibile tooviewers tramite hello Endpoint di Streaming. 

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. 

Sono disponibili eventi di toostart due modi: 

1. Da hello **canale** pagina, premere **evento Live** tooadd un nuovo evento.
   
    Specificare il nome dell'evento, il nome dell'asset, l'intervallo di archiviazione e l'opzione di crittografia.
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    Se si lascia **pubblica questo evento in tempo reale** selezionata, verrà creata hello evento hello gli URL di pubblicazione.
   
    È possibile premere **avviare**, ogni volta che sono eventi hello toostream pronto.
   
    Dopo aver iniziato l'evento hello, è possibile premere **espressioni di controllo** toostart la riproduzione di contenuti di hello.
2. In alternativa, è possibile utilizzare un collegamento e premere **Go Live** pulsante hello **canale** pagina. In questo modo verrà creato un localizzatore predefinito di asset, programma e streaming.
   
    nome dell'evento Hello è **predefinito** e viene impostato l'intervallo di archiviazione hello too8 ore.

È possibile guardare hello evento pubblicato da hello **evento Live** pagina. 

Facendo clic su **Sospendi trasmissione**vengono arrestati tutti gli eventi live. 

## <a name="watch-hello-event"></a>Evento hello espressioni di controllo
evento hello toowatch, fare clic su **espressioni di controllo** in hello Azure portal o copia a hello URL di streaming e usare un lettore di propria scelta. 

![Data di creazione](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

Evento Live converte automaticamente il contenuto di richiesta tooon eventi all'arresto.

## <a name="clean-up"></a>Eseguire la pulizia
Se vengono eseguiti i flussi di eventi di tooclean delle risorse di hello il provisioning in precedenza, attenersi alla procedura hello.

* Arrestare il push flusso hello dal codificatore hello.
* Arrestare il canale hello. Una volta hello canale viene interrotto, non genererà eventuali addebiti. Quando è necessario toostart nuovamente, disporrà di hello stesso URL di inserimento in modo non sarà necessario tooreconfigure codificatore.
* È possibile arrestare l'Endpoint di Streaming, a meno che non si desidera l'archivio di hello tooprovide toocontinue dell'evento live come flusso su richiesta. Se il canale di hello è nello stato arrestato, non genererà eventuali addebiti.

## <a name="view-archived-content"></a>Visualizzare il contenuto archiviato
Anche dopo aver arrestato ed eliminato evento hello, hello gli utenti sarebbero in grado di toostream il contenuto archiviato come video on demand, per fino a quando non si elimina asset hello. Non è possibile eliminare un asset se è utilizzato da un evento. evento Hello deve prima essere eliminato. 

Selezionare le risorse, toomanage **impostazione** e fare clic su **asset**.

![Asset](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>Considerazioni
* Attualmente, hello max consigliata la durata di un evento in tempo reale è 8 ore. Se è necessario un canale toorun per lunghi periodi di tempo, contattare amslived all'indirizzo Microsoft.com.
* Verificare che sia di streaming dei contenuti di endpoint da cui si desidera toostream hello in hello **esecuzione** stato.

## <a name="next-step"></a>Passaggio successivo
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

