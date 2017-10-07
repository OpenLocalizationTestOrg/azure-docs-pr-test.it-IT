---
title: "aaaConfigure hello toosend di codificatore Live elementare un flusso live a velocità in bit singola | Documenti Microsoft"
description: "Questo argomento viene illustrato come tooconfigure hello toosend di codificatore Live elementare un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a>Utilizzare hello Live elementare codificatore toosend un flusso live a velocità in bit singola
> [!div class="op_single_selector"]
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Questo argomento viene illustrato come hello tooconfigure [Live elementare](http://www.elementaltechnologies.com/products/elemental-live) codificatore toosend una velocità in bit singola tooAMS canali abilitati per la codifica live del flusso.  Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).

Questa esercitazione vengono illustrate le modalità di servizi multimediali di Azure di toomanage (AMS) con lo strumento Azure Media Services Explorer (AMSE). Questo strumento può essere eseguito solo in PC Windows. Se si utilizza Mac o Linux, usare hello toocreate portale Azure [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Prerequisiti
* Deve avere una conoscenza di utilizzo di Live elementare web interfaccia toocreate eventi in tempo reale.
* [Creare un account Servizi multimediali di Azure](media-services-portal-create-account.md)
* Verificare che sia presente un endpoint di streaming in esecuzione. Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md).
* Installare una versione più recente di hello di hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) strumento.
* Avviare lo strumento hello e tooyour sistema AMS di account di connessione.

## <a name="tips"></a>Suggerimenti
* Se possibile, usare una connessione a Internet con cablaggio fisico.
* Una buona regola pratica per determinare i requisiti di larghezza di banda è hello toodouble streaming a velocità in bit. Sebbene non sia un requisito obbligatorio, questo risulterà utile ridurre l'impatto di hello congestione della rete.
* Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.

## <a name="elemental-live-with-rtp-ingest"></a>Elemental Live con inserimento RTP
In questa sezione viene illustrato come tooconfigure hello elementare codificatore Live che invia una velocità in bit singola flusso live su RTP.  Per altre informazioni, vedere [Flusso MPEG-TS su RTP](media-services-manage-live-encoder-enabled-channels.md#channel).

### <a name="create-a-channel"></a>Creare un canale

1. Nello strumento AMSE hello passare toohello **Live** scheda e fare clic con il pulsante destro nell'area di canale hello. Scegliere **Create channel** dal menu di hello.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. Specificare un nome di canale, il campo di descrizione hello è facoltativo. Selezionare le impostazioni del canale, **Standard** per hello opzione di codifica Live, con hello Input protocollo impostato troppo**RTP (MPEG-TS)**. È possibile confermare tutte le altre impostazioni predefinite.

    Verificare che hello **inizio hello nuovo canale ora** è selezionata.

3. Fare clic su **Create Channel**.

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> canale Hello può richiedere fino a 20 minuti toostart.
>
>

Durante l'avvio di canale hello è possibile [configurare codificatore hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).

> [!IMPORTANT]
> Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto. Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

### <a id=configure_elemental_rtp></a>Configurazione del codificatore Live elementare hello
In questa esercitazione hello vengono utilizzate le seguenti impostazioni di output. Hello in questa sezione descrive in dettaglio i passaggi di configurazione.

**Video**:

* Codec: H.264
* Profilo: alto (livello 4.0)
* Velocità in bit: 5000 kbps
* Fotogramma chiave: 2 secondi (60 secondi)
* Frequenza dei fotogrammi: 30

**Audio**:

* Codec: AAC (LC)
* Velocità in bit: 192 kbps
* Frequenza di campionamento: 44,1 kHz

#### <a name="configuration-steps"></a>Procedura di configurazione
1. Passare toohello **Live elementare** interfaccia web e impostare il codificatore hello per **UDP/Servizi terminal** streaming.
2. Dopo aver creato un nuovo evento, scorrere verso il basso dei gruppi di output toohello e aggiungere hello **UDP/Servizi terminal** gruppo di output.
3. Creare un nuovo output selezionando **Nuovo flusso** e quindi facendo clic su **Aggiungi output**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > È consigliabile che l'evento elementare hello disponga timecode hello impostato troppo codificatore di hello toohelp "Orologio di sistema" riconnessione in caso di hello di un errore di flusso.
   >
   >
4. Ora che hello Output è stato creato, fare clic su **aggiungere flusso**. le impostazioni di output di Hello possono ora essere configurate.
5. Scorrere verso il basso toohello "Stream 1" è stato appena creato, fare clic su hello **Video** scheda hello sinistra ed espandere hello **avanzate** sezione Impostazioni.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    Mentre Live elementare ha un'ampia gamma di personalizzazione disponibili, hello seguente si consigliano le impostazioni per iniziare a usare tooAMS di streaming.

   * Risoluzione: 1280 x 720
   * Frequenza fotogrammi: 30
   * Dimensioni GOP: 60 fotogrammi
   * Modalità interlacciamento: progressivo
   * Velocità in bit: 5000000 bit/s (regolabile in base alle limitazioni di rete)

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. Ottenere l'URL di input del canale hello.

    Passare strumento AMSE toohello indietro e controllare lo stato di completamento di hello del canale. Una volta hello stato è cambiato da **iniziale** troppo**esecuzione**, è possibile ottenere l'URL di input hello.

    Quando il canale hello è in esecuzione, fare clic con il pulsante destro nome canale hello, spostarsi verso il basso toohover su **Copia URL di Input tooclipboard** e quindi selezionare **URL di Input primaria**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. Incollare le informazioni in hello **destinazione principale** campo hello elementare. Tutte le altre impostazioni possono rimanere predefinito hello.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    Per garantire la ridondanza aggiuntiva, ripetere questi passaggi con hello secondario URL di Input mediante la creazione di una scheda separata di "Output" per lo Streaming UDP/Servizi terminal.
3. Fare clic su **crea** (se è stato creato un nuovo evento) o **aggiornamento** (se la modifica di un evento di pre-esistente) e quindi procedere codificatore hello toostart.

> [!IMPORTANT]
> Prima di scegliere **avviare** nell'interfaccia web Live elementare di hello è **deve** assicurarsi che il canale hello è pronto.
> Inoltre, assicurarsi che non tooleave hello canale in uno stato pronto senza un evento per più di 15 minuti di >.
>
>

Dopo il flusso di hello è stata eseguita per 30 secondi, passare la riproduzione dello strumento e test AMSE toohello indietro.  

### <a name="test-playback"></a>Testare la riproduzione

Passare strumento AMSE toohello e fare clic con il pulsante destro hello canale toobe testato. Dal menu di hello, passare il mouse su **hello riproduzione anteprima** e selezionare **con Azure Media Player**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

Se il flusso di hello viene visualizzato nel lettore hello, codificatore hello è stato configurato correttamente tooconnect tooAMS.

Se viene ricevuto un errore, il canale hello sarà necessario toobe reimpostazione e il codificatore le impostazioni. Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.   

### <a name="create-a-program"></a>Creare un programma.
1. Una volta che viene confermata la riproduzione del canale, creare un programma. In hello **Live** nello strumento AMSE hello, fare clic con il pulsante destro nell'area di programma hello e selezionare **creare un nuovo programma**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. Nome programma hello e, se necessario, modificare hello **lunghezza dell'intervallo di archivio** (le impostazioni predefinite too4 ore). È inoltre possibile specificare un percorso di archiviazione o lasciare hello predefinite.  
3. Controllare hello **ora inizio hello programma** casella.
4. Fare clic su **Create Program**.  

    >[!NOTE]
    > La creazione di un programma richiede meno tempo rispetto alla creazione del canale.   
      
5. Quando è in esecuzione il programma hello, confermare la riproduzione facendo clic con il pulsante destro programma hello e passando troppo**riproduzione hello programmi** e quindi selezionando **con Azure Media Player**.  
6. Una volta confermato, fare clic nuovamente il programma hello e scegliere **copiare tooClipboard URL di Output di hello** (o recuperare queste informazioni da hello **informazioni e le impostazioni del programma** opzione dal menu di hello).

flusso Hello è ora pronto toobe incorporato in un lettore o destinatari tooan distribuita per live visualizzazione.  

## <a name="troubleshooting"></a>Risoluzione dei problemi
Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
