---
title: "aaaConfigure hello NewTek TriCaster codificatore toosend un flusso live a velocità in bit singola | Documenti Microsoft"
description: "Questo argomento viene illustrato come hello tooconfigure Tricaster toosend codificatore una velocità in bit singola flusso tooAMS canali live che sono abilitati per la codifica live."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a>Utilizzare hello NewTek TriCaster codificatore toosend un flusso live a velocità in bit singola
> [!div class="op_single_selector"]
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Questo argomento viene illustrato come hello tooconfigure [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live codificatore toosend un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live. Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).

Questa esercitazione vengono illustrate le modalità di servizi multimediali di Azure di toomanage (AMS) con lo strumento Azure Media Services Explorer (AMSE). Questo strumento può essere eseguito solo in PC Windows. Se si utilizza Mac o Linux, usare hello toocreate portale Azure [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).

> [!NOTE]
> Quando tramite Tricaster per l'invio di un contributo feed tooAMS canali abilitati per la codifica live, potrebbe essere necessario anomalie di video o audio nell'evento in tempo reale Se si utilizzano determinate funzionalità di Tricaster, ad esempio rapido Taglia tra feed o il passaggio a/da Slate . Hello AMS team lavora in corretto questi problemi, fino a quel momento, è consigliabile non toouse queste funzionalità.
>
>

## <a name="prerequisites"></a>Prerequisiti
* [Creare un account Servizi multimediali di Azure](media-services-portal-create-account.md)
* Verificare che sia presente un endpoint di streaming in esecuzione. Per altre informazioni, vedere [Gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md)
* Installare una versione più recente di hello di hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) strumento.
* Avviare lo strumento hello e tooyour sistema AMS di account di connessione.

## <a name="tips"></a>Suggerimenti
* Se possibile, usare una connessione a Internet con cablaggio fisico.
* Una buona regola pratica per determinare i requisiti di larghezza di banda è hello toodouble streaming a velocità in bit. Sebbene non sia un requisito obbligatorio, questo risulterà utile ridurre l'impatto di hello congestione della rete.
* Se si usano codificatori basati su software, chiudere tutti i programmi non necessari.

## <a name="create-a-channel"></a>Creare un canale
1. Nello strumento AMSE hello passare toohello **Live** scheda e fare clic con il pulsante destro nell'area di canale hello. Scegliere **Create channel** dal menu di hello.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. Specificare un nome di canale, il campo di descrizione hello è facoltativo. Selezionare le impostazioni del canale, **Standard** per hello opzione di codifica Live, con hello Input protocollo impostato troppo**RTMP**. È possibile confermare tutte le altre impostazioni predefinite.

    Verificare che hello **inizio hello nuovo canale ora** è selezionata.

3. Fare clic su **Create Channel**.

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> canale Hello può richiedere fino a 20 minuti toostart.
>
>

Durante l'avvio di canale hello è possibile [configurare codificatore hello](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).

> [!IMPORTANT]
> Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto. Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_tricaster_rtmp></a>Configurare hello NewTek TriCaster codificatore
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

### <a name="configuration-steps"></a>Procedura di configurazione
1. Creare un nuovo progetto **NewTek TriCaster** in base a quale origine di input del video si sta utilizzando.
2. Una volta all'interno di tale progetto, cercare hello **flusso** pulsante e fare clic su hello ingranaggio icona Avanti tooit tooaccess hello flusso menu configurazione.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. Se il menu di hello è aperta, fare clic su **New** titolo connessione hello. Quando richiesto per il tipo di connessione hello, selezionare **Adobe Flash**.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. Fare clic su **OK**.
5. Un profilo FMLE può ora essere importato facendo clic sulla freccia sotto a discesa hello **profilo Streaming** e la navigazione troppo**Sfoglia**.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. Passare toowhere hello configurato FMLE profilo è stato salvato.
7. Selezionarlo e premere **OK**.

    Una volta caricato il profilo di hello, procedere toohello successivo.
8. Ottenere l'URL di input del canale hello in ordine tooassign è toohello Tricaster **RTMP Endpoint**.

    Passare strumento AMSE toohello indietro e controllare lo stato di completamento di hello del canale. Una volta hello stato è cambiato da **iniziale** troppo**esecuzione**, è possibile ottenere l'URL di input hello.

    Quando il canale hello è in esecuzione, fare clic con il pulsante destro nome canale hello, spostarsi verso il basso toohover su **Copia URL di Input tooclipboard** e quindi selezionare **URL di Input primaria**.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. Incollare le informazioni in hello **percorso** campo **Flash Server** all'interno di progetto di hello Tricaster. Assegnare un nome di flusso in hello **ID flusso** campo.

    Se le informazioni di flusso è stato aggiunto il profilo FMLE toohello, anche possibile importare toothis sezione facendo **importare le impostazioni**, passando profilo FMLE toohello salvato e fare clic su **OK**. campi Flash Server rilevanti Hello devono popolare con le informazioni di hello di FMLE.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. Al termine, fare clic su **OK** in basso hello hello. Quando gli input audio e video in hello Tricaster pronti, iniziare lo streaming tooAMS facendo hello **flusso** pulsante.

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> Prima di scegliere **flusso**, si **deve** assicurarsi che il canale hello è pronto.
> Inoltre, assicurarsi che non tooleave hello canale in uno stato pronto senza un contributo input feed per più di 15 minuti di >.
>
>

## <a name="test-playback"></a>Testare la riproduzione
Passare strumento AMSE toohello e fare clic con il pulsante destro hello canale toobe testato. Dal menu di hello, passare il mouse su **hello riproduzione anteprima** e selezionare **con Azure Media Player**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

Se il flusso di hello viene visualizzato nel lettore hello, codificatore hello è stato configurato correttamente tooconnect tooAMS.

Se viene ricevuto un errore, il canale hello sarà necessario toobe reimpostazione e il codificatore le impostazioni. Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.  

## <a name="create-a-program"></a>Creare un programma.
1. Una volta che viene confermata la riproduzione del canale, creare un programma. In hello **Live** nello strumento AMSE hello, fare clic con il pulsante destro nell'area di programma hello e selezionare **creare un nuovo programma**.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. Nome programma hello e, se necessario, modificare hello **lunghezza dell'intervallo di archivio** (le impostazioni predefinite too4 ore). È inoltre possibile specificare un percorso di archiviazione o lasciare hello predefinite.  
3. Controllare hello **ora inizio hello programma** casella.
4. Fare clic su **Create Program**.  

    >[!NOTE]
    >La creazione di un programma richiede meno tempo rispetto alla creazione del canale.
        
5. Quando è in esecuzione il programma hello, confermare la riproduzione facendo clic con il pulsante destro programma hello e passando troppo**riproduzione hello programmi** e quindi selezionando **con Azure Media Player**.  
6. Una volta confermato, fare clic nuovamente il programma hello e scegliere **copiare tooClipboard URL di Output di hello** (o recuperare queste informazioni da hello **informazioni e le impostazioni del programma** opzione dal menu di hello).

flusso Hello è ora pronto toobe incorporato in un lettore o destinatari tooan distribuita per live visualizzazione.  

## <a name="troubleshooting"></a>Risoluzione dei problemi
Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.

## <a name="next-step"></a>Passaggio successivo
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
