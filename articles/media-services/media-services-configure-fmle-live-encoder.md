---
title: "aaaConfigure hello FMLE codificatore toosend un flusso live a velocità in bit singola | Documenti Microsoft"
description: "Questo argomento viene illustrato come tooconfigure hello toosend codificatore Flash multimediali Live codificatore (FMLE) un canali tooAMS flusso a velocità in bit singola che sono abilitati per la codifica live."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a>Utilizzare hello FMLE codificatore toosend un flusso live a velocità in bit singola
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

Questo argomento viene illustrato come hello tooconfigure [Flash Media Encoder Live](http://www.adobe.com/products/flash-media-encoder.html) toosend codificatore (FMLE) una velocità in bit singola tooAMS canali abilitati per la codifica live del flusso. Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).

Questa esercitazione vengono illustrate le modalità di servizi multimediali di Azure di toomanage (AMS) con lo strumento Azure Media Services Explorer (AMSE). Questo strumento può essere eseguito solo in PC Windows. Se si utilizza Mac o Linux, usare hello toocreate portale Azure [canali](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) e [programmi](media-services-portal-creating-live-encoder-enabled-channel.md).

Si noti che questa esercitazione descrive l'utilizzo di AAC. Tuttavia, per impostazione predefinita FMLE non supporta AAC. È necessario un plug-in per la codifica AAC toopurchase ad esempio da codec altamente ottimizzati: [AAC di plug-in](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)

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

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. Specificare un nome di canale, il campo di descrizione hello è facoltativo. Selezionare le impostazioni del canale, **Standard** per hello opzione di codifica Live, con hello Input protocollo impostato troppo**RTMP**. È possibile confermare tutte le altre impostazioni predefinite.

    Verificare che hello **inizio hello nuovo canale ora** è selezionata.

3. Fare clic su **Create Channel**.

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> canale Hello può richiedere fino a 20 minuti toostart.
>
>

Durante l'avvio di canale hello è possibile [configurare codificatore hello](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).

> [!IMPORTANT]
> Si noti che la fatturazione inizia non appena il canale passa a uno stato di pronto. Per altre informazioni, vedere [Stati del canale](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_fmle_rtmp></a>Configurare il codificatore FMLE hello
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
1. Passare toohello che Flash Live codificatore multimediale (FMLE) interfaccia sul computer hello in uso.

    interfaccia Hello è una pagina principale di impostazioni. Per prendere nota dei seguenti hello consigliati tooget impostazioni introduttiva streaming mediante FMLE.

   * Formato: Frequenza dei fotogrammi h. 264: 30,00
   * Dimensione di input: 1280 x 720
   * Velocità in bit: Kbps 5000 (può essere regolato in base alle limitazioni di rete)  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     Quando tramite interlacciata origini, il segno di spunta hello "Deinterlaccia" opzione
2. Icona chiave inglese hello selezionare tooFormat Avanti, queste impostazioni aggiuntive devono essere:

   * Profilo: principale
   * Livello: 4.0
   * Frequenza dei fotogrammi chiave: 2 secondi

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. Impostare hello impostazione audio importanti seguenti:

   * Formato: AAC
   * Frequenza di campionamento: 44100 kHz
   * Velocità in bit: 192 kbps

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. Ottenere l'URL di input del canale hello in ordine tooassign è del toohello FMLE **RTMP Endpoint**.

    Passare strumento AMSE toohello indietro e controllare lo stato di completamento di hello del canale. Una volta hello stato è cambiato da **iniziale** troppo**esecuzione**, è possibile ottenere l'URL di input hello.

    Quando il canale hello è in esecuzione, fare clic con il pulsante destro nome canale hello, spostarsi verso il basso toohover su **Copia URL di Input tooclipboard** e quindi selezionare **URL di Input primaria**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. Incollare le informazioni in hello **URL FMS** campo della sezione di output di hello e di assegnare un nome di flusso.

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    Per garantire la ridondanza aggiuntiva, ripetere questi passaggi con hello secondario URL di Input.
6. Selezionare **Connessione**.

> [!IMPORTANT]
> Prima di scegliere **Connetti**, si **deve** assicurarsi che il canale hello è pronto.
> Inoltre, assicurarsi che non tooleave hello canale in uno stato pronto senza un contributo input feed per più di 15 minuti di >.
>
>

## <a name="test-playback"></a>Testare la riproduzione

Passare strumento AMSE toohello e fare clic con il pulsante destro hello canale toobe testato. Dal menu di hello, passare il mouse su **hello riproduzione anteprima** e selezionare **con Azure Media Player**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

Se il flusso di hello viene visualizzato nel lettore hello, codificatore hello è stato configurato correttamente tooconnect tooAMS.

Se viene ricevuto un errore, il canale hello sarà necessario toobe reimpostazione e il codificatore le impostazioni. Vedere hello [risoluzione dei problemi](media-services-troubleshooting-live-streaming.md) argomento per informazioni aggiuntive.  

## <a name="create-a-program"></a>Creare un programma.
1. Una volta che viene confermata la riproduzione del canale, creare un programma. In hello **Live** nello strumento AMSE hello, fare clic con il pulsante destro nell'area di programma hello e selezionare **creare un nuovo programma**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
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
