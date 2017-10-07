---
title: "aaaConfigure hello Telestream Wirecast encoder toosend un flusso live a velocità in bit singola | Documenti Microsoft"
description: "Questo argomento viene illustrato come tooconfigure hello Wirecast encoder toosend una velocità in bit singola flusso tooAMS canali live che sono abilitati per la codifica live. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a>Utilizzare hello Wirecast encoder toosend un flusso live a velocità in bit singola
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Questo argomento viene illustrato come hello tooconfigure [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live codificatore toosend un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live.  Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).

Questa esercitazione vengono illustrate le modalità di servizi multimediali di Azure di toomanage (AMS) con lo strumento Azure Media Services Explorer (AMSE). Questo strumento può essere eseguito solo in PC Windows. Se si utilizza Mac o Linux, usare hello toocreate portale Azure [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).

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

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. Specificare un nome di canale, il campo di descrizione hello è facoltativo. Selezionare le impostazioni del canale, **Standard** per hello opzione di codifica Live, con hello Input protocollo impostato troppo**RTMP**. È possibile confermare tutte le altre impostazioni predefinite.

    Verificare che hello **inizio hello nuovo canale ora** è selezionata.

3. Fare clic su **Create Channel**.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> canale Hello può richiedere fino a 20 minuti toostart.
>
>

Durante l'avvio di canale hello è possibile [configurare codificatore hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).

> [!IMPORTANT]
> Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto. Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_wirecast_rtmp></a>Configurare Telestream Wirecast encoder hello
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
1. Aprire un'applicazione hello Telestream Wirecast sulla macchina hello utilizzato e impostare per lo streaming RTMP.
2. Configurare l'output di hello passando toohello **Output** scheda e selezionando **le impostazioni di Output...** .

    Verificare che hello **destinazione dell'Output** è troppo**RTMP Server**.
3. Fare clic su **OK**.
4. Nella pagina Impostazioni hello, impostare hello **destinazione** campo toobe **servizi multimediali di Azure**.

    profilo di codifica Hello è preselezionata troppo**h. 264 Azure 720 p 16:9 (1280x720)**. toocustomize queste impostazioni, selezionare hello ingranaggio icona toohello diritto di hello elenco a discesa e quindi scegliere **New Preset**.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. Configura le impostazioni predefinite del codificatore.

    Hello Nome set di impostazioni e verificare la seguente hello impostazioni consigliate:

    **Video**

   * Codificatore: MainConcept h. 264
   * Fotogrammi al secondo: 30
   * Velocità in bit media: 5000 kbit al secondo (può essere regolato in base alle limitazioni di rete)
   * Profilo: principale
   * Fotogramma chiave ogni: 60 fotogrammi

    **Audio**

   * Velocità in bit di destinazione: 192 kbit/sec
   * Frequenza di campionamento: 44,100 kHz

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. Premere **Salva**.

    campo Encoding Hello dispone ora disponibili per la selezione del profilo di hello appena creato.

    Assicurarsi che sia selezionato il nuovo profilo di hello.
7. Ottenere l'URL di input del canale hello in ordine tooassign è toohello Wirecast **RTMP Endpoint**.

    Passare strumento AMSE toohello indietro e controllare lo stato di completamento di hello del canale. Una volta hello stato è cambiato da **iniziale** troppo**esecuzione**, è possibile ottenere l'URL di input hello.

    Quando il canale hello è in esecuzione, fare clic con il pulsante destro nome canale hello, spostarsi verso il basso toohover su **Copia URL di Input tooclipboard** e quindi selezionare **URL di Input primaria**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. In hello Wirecast **le impostazioni di Output** finestra incollare queste informazioni in hello **indirizzo** campo della sezione di output di hello e di assegnare un nome di flusso.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. Selezionare **OK**.
2. In hello principale **Wirecast** verificare origini di input per video e audio sono pronti e quindi premere **flusso** nell'angolo superiore sinistro hello.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> Prima di scegliere **flusso**, si **deve** assicurarsi che il canale hello è pronto.
> Inoltre, assicurarsi che non tooleave hello canale in uno stato pronto senza un contributo input feed per più di 15 minuti di >.
>
>

## <a name="test-playback"></a>Testare la riproduzione

Passare strumento AMSE toohello e fare clic con il pulsante destro hello canale toobe testato. Dal menu di hello, passare il mouse su **hello riproduzione anteprima** e selezionare **con Azure Media Player**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

Se il flusso di hello viene visualizzato nel lettore hello, codificatore hello è stato configurato correttamente tooconnect tooAMS.

Se viene ricevuto un errore, il canale hello sarà necessario toobe reimpostazione e il codificatore le impostazioni. Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.  

## <a name="create-a-program"></a>Creare un programma.
1. Una volta che viene confermata la riproduzione del canale, creare un programma. In hello **Live** nello strumento AMSE hello, fare clic con il pulsante destro nell'area di programma hello e selezionare **creare un nuovo programma**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
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

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
