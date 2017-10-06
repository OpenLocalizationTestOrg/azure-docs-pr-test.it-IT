---
title: aaaOverview di Live Streaming con servizi multimediali di Azure | Documenti Microsoft
description: Questo argomento offre una panoramica dello streaming live con Servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>Panoramica dello streaming live con Servizi multimediali di Azure
## <a name="overview"></a>Panoramica
Per il recapito in tempo reale flussi di eventi con servizi multimediali di Azure hello seguenti componenti è generalmente necessari:

* Fotocamera che viene utilizzato toobroadcast un evento.
* Un codificatore video live che converte i segnali dalla toostreams fotocamera hello inviati tooa in tempo reale di servizio di streaming.

    Facoltativamente, più codificatori live con sincronizzazione dell'ora. Per alcuni eventi live critici per disponibilità elevata e la qualità di esperienza, è consigliabile codificatori ridondanti di tooemploy attivo-attivo con failover trasparente ora sincronizzazione tooachieve senza perdita di dati.
* Un servizio di streaming live che consente di hello toodo seguenti:

  * inserire contenuti live usando vari protocolli di streaming live (ad esempio RTMP o Smooth Streaming),
  * (facoltativamente) codificare il flusso per il flusso a bitrate adattivo,
  * visualizzare in anteprima il flusso live,
  * flusso di record e l'archivio contenuto hello caricamento in ordine toobe successive (video on Demand)
  * distribuire il contenuto di hello tramite protocolli di streaming comuni (ad esempio, MPEG DASH, Smooth, HLS) direttamente ai clienti di tooyour o tooa rete di contenuti (CDN) per ulteriore distribuzione.

**Servizi multimediali di Microsoft Azure** (AMS) fornisce hello tooingest possibilità, codificare, visualizzare in anteprima, archiviare e distribuire il contenuto di streaming in tempo reale.

Per il recapito del contenuto toocustomers l'obiettivo è toodeliver un toovarious video di qualità elevata per i dispositivi in condizioni di rete diverso. tooachieve, utilizzare live codificatori tooencode flusso video di flusso tooa più velocità in bit (velocità in bit adattiva).  tootake cure streaming su diversi dispositivi, usare servizi multimediali [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md) toodynamically nuovamente il protocollo toodifferent flusso del pacchetto. Servizi multimediali supporta il recapito di hello velocità in bit adattive tecnologie seguente: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.

In servizi multimediali di Azure, **canali**, **programmi**, e **StreamingEndpoints** handle hello tutti live streaming compresi inserimento, formattazione, DVR, funzionalità sicurezza, scalabilità e ridondanza.

Un **canale** rappresenta una pipeline per l'elaborazione di contenuto in streaming live. Un canale può ricevere attivo di input flussi in hello seguenti modi:

* Un codificatore live locale invia più velocità in bit **RTMP** o **Smooth Streaming** (MP4 frammentato) canale toohello configurato per **pass-through** recapito. Hello **pass-through** recapito è quando attraversano flussi hello caricamento **canale**s senza ulteriore elaborazione. È possibile utilizzare i seguenti codificatori live Smooth Streaming con più velocità in bit di output di hello: MediaExcel, Ateme, le comunicazioni immaginare, Envivio, Cisco ed elementare. Hello codificatori live seguenti generano output in RTMP: Adobe Flash multimediali Live codificatore (FMLE), Telestream Wirecast, Haivision, Teradek e transcodificatori Tricaster.  Un codificatore live può inoltre inviare una velocità in bit singola tooa il canale del flusso che non è abilitato per la codifica live, ma che non è consigliata. Quando richiesto, servizi multimediali offre toocustomers flusso hello.

  > [!NOTE]
  > Utilizzo di un metodo pass-through è hello più conveniente toodo live streaming quando si eseguono più eventi per un lungo periodo di tempo e hanno già investito in codificatori locali. Vedere i dettagli sui [prezzi](https://azure.microsoft.com/pricing/details/media-services/) .
  > 
  > 
* Un codificatore live locale invia un flusso a velocità in bit singola canale toohello tooperform abilitato live codifica con servizi multimediali in uno dei seguenti formati hello: RTMP o Smooth Streaming (MP4 frammentato). RTP (MPEG-TS) è supportata anche se si dispone di un connessione dedicata toohello data center di Azure. sono noti toowork dei canali di questo tipo di output di Hello seguenti codificatori live con RTMP: Telestream Wirecast, FMLE. Hello canale esegue quindi la codifica live di hello in arrivo velocità in bit singola flusso tooa più velocità in bit (adattivo) flusso video. Quando richiesto, servizi multimediali offre toocustomers flusso hello.

A partire dalla versione di hello 2.10 di servizi multimediali, quando si crea un canale, è possibile specificare in che modo si desidera per il flusso di input del canale tooreceive hello e se si vuole che per hello canale tooperform live codifica del flusso di lavoro. Sono disponibili due opzioni:

* **Nessuna** (pass-through): specificare questo valore, se si prevede di toouse un codificatore live locale che genera più velocità in bit flusso (flusso di pass-through). In questo caso, il flusso in ingresso di hello passati toohello output senza codifica. Questo è il comportamento di hello di una versione precedente di too2.10 canale.  
* **Standard** -scegliere questo valore, se si prevede di tooencode di servizi multimediali toouse il flusso di velocità in bit toomulti flusso live a velocità in bit singola. Questo metodo è il più vantaggioso per aumentare rapidamente le unità in caso di eventi non frequenti. Tenere presente che vi sia un impatto sulla fatturazione per la codifica live è opportuno tenere presente che se si lascia un canale di codifica live in stato "Running" hello comporterà ulteriori addebiti nella fatturazione.  È consigliabile arrestare immediatamente i canali in esecuzione dopo l'evento di streaming in tempo reale viene completato tooavoid costi extra orarie.

## <a name="comparison-of-channel-types"></a>Confronto tra tipi di canale
Nella tabella seguente viene fornita una Guida toocomparing hello due tipi di canale supportati in servizi multimediali

| Funzionalità | Canale pass-through | Canale standard |
| --- | --- | --- |
| Velocità in bit singola input viene codificato in più velocità in bit nel cloud hello |No |Sì |
| Risoluzione massima, numero di livelli |1080p, 8 livelli, oltre 60 fps |720p, 6 livelli, 30 fps |
| Protocolli di input |RTMP, Smooth Streaming |RTMP, Smooth Streaming e RTP |
| Prezzo |Vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/media-services/) e fare clic sulla scheda "Video Live" |Vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/media-services/) |
| Tempo di esecuzione massimo |24 x 7 |8 ore |
| Supporto per l'inserimento di slate |No |Sì |
| Supporto per annunci pubblicitari |No |Sì |
| Pass-through di sottotitoli CEA 608/708 |Sì |Sì |
| Possibilità toorecover da blocchi breve nel contributo feed |Sì |No (senza dati di input, il canale avvierà lo slate dopo 6 secondi) |
| Supporto per GOP di input non uniformi |Sì |No: l'input deve essere fisso (GOP di 2 secondi) |
| Supporto per input con frequenza dei fotogrammi variabile |Sì |No: l'input deve essere una frequenza di fotogrammi fissa.<br/>Sono tollerate lievi variazioni, ad esempio durante scene ad alta velocità. Ma codificatore non è possibile eliminare too10 fotogrammi al secondo. |
| Arresto automatico dei canali in caso di perdita del feed di input |No |Dopo 12 ore, nessun programma è in esecuzione |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Utilizzo di canali che ricevono il flusso live a bitrate multiplo da codificatori locali con il metodo pass-through
Hello diagramma seguente mostra hello parti principali della piattaforma hello AMS coinvolti nel hello **pass-through** flusso di lavoro.

![Flusso di lavoro live](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

Per altre informazioni, vedere l'articolo relativo all' [uso di canali che ricevono il flusso live a velocità in bit multipla da codificatori locali](media-services-live-streaming-with-onprem-encoders.md).

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Utilizzo di canali che sono abilitati tooperform in tempo reale di codifica con servizi multimediali di Azure
Hello diagramma seguente viene illustrato hello principale parti della piattaforma AMS hello coinvolti in Streaming Live del flusso di lavoro in cui un canale è abilitato tooperform in tempo reale di codifica con servizi multimediali.

![Flusso di lavoro live](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

Per ulteriori informazioni, vedere [utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md).

## <a name="description-of-a-channel-and-its-related-components"></a>Descrizione di un canale e dei relativi componenti
### <a name="channel"></a>canale
In Servizi multimediali le entità [Channel](https://docs.microsoft.com/rest/api/media/operations/channel)sono responsabili dell'elaborazione dei contenuti in streaming live. Un canale, fornisce un endpoint di input (URL di inserimento) che è quindi fornire transcodificatore live tooa. canale Hello riceve flussi di input live dal transcodificatore live hello e rende disponibili per lo streaming tramite uno o più entità Streamingendpoint. I canali forniscono inoltre un endpoint di anteprima (URL di anteprima) di utilizzare toopreview e convalidare il flusso prima di elaborarlo ulteriormente e di recapito.

È possibile ottenere hello inserimento URL e l'URL di anteprima di hello quando si crea il canale hello. tooget questi URL, il canale di hello non avere toobe nello stato avviato hello. Quando si è pronti toostart push dei dati da un transcodificatore live nel canale hello, canale hello deve essere avviati. Una volta transcodificatore live hello inizia l'inserimento di dati, è possibile visualizzare in anteprima il flusso.

Ogni account di Servizi multimediali può contenere più entità Channel, Program e StreamingEndpoint. A seconda delle esigenze di larghezza di banda e sicurezza hello, servizi StreamingEndpoint possono essere dedicato tooone o altri canali. Qualsiasi StreamingEndpoint può effettuare il pull da qualsiasi canale.

### <a name="program"></a>Programma
Oggetto [programma](https://docs.microsoft.com/rest/api/media/operations/program) consente toocontrol hello pubblicazione e l'archiviazione di segmenti in un flusso in tempo reale. I programmi sono gestiti dai canali. Hello relazione canale e il programma è molto simile tootraditional media, in cui un canale è un flusso costante di contenuto e l'evento con ambito toosome timeout su tale canale è un programma.
È possibile specificare hello numero di ore che si vuole tooretain hello registrato contenuto per il programma hello, impostazione hello **ArchiveWindowLength** proprietà. Questo valore può essere impostato da un minimo di 25 ore massimo tooa 5 minuti.

ArchiveWindowLength determina anche l'intervallo di tempo i client possono cercare indietro nel tempo dalla posizione live corrente hello massimo hello. I programmi eseguibili sul periodo di tempo specificato hello, ma il contenuto che non è sincronizzato con la lunghezza della finestra hello viene scartato in modo continuo. Questo valore di questa proprietà determina anche per quanto tempo hello client possono raggiungere i manifesti.

Ogni programma è associato a un asset. il programma di hello toopublish è necessario creare un localizzatore per hello associati asset. Con questo localizzatore sarà si toobuild un URL di streaming che è possibile fornire tooyour client.

Un canale supporta fino toothree programmi in esecuzione contemporaneamente in modo è possibile creare più archivi di hello stesso flusso in ingresso. In questo modo toopublish e archiviare parti diverse di un evento in base alle esigenze. Ad esempio, il requisito di business è tooarchive 6 ore di un programma, ma toobroadcast solo ultimi 10 minuti. tooaccomplish, è necessario toocreate due programmi in esecuzione simultanea. Un programma è impostato tooarchive 6 ore dell'evento hello ma hello non viene pubblicato. Hello altro programma è tooarchive insieme per 10 minuti e questo programma viene pubblicato.

## <a name="billing-implications"></a>Implicazioni relative alla fatturazione
Un canale inizia non appena lo stato del passa troppo "Running" tramite hello API di fatturazione.  

Hello nella tabella seguente illustra gli stati dei canali mapping stati toobilling hello API e portale di Azure. Si noti che sono leggermente diversi tra hello API e portale interfaccia hello stati Non appena un canale è nello stato "Running" hello tramite API hello o in stato di "Streaming" nel portale di Azure hello o hello "Pronto", la fatturazione sarà attiva.

Canale di hello toostop dalla fatturazione è ulteriormente, hai tooStop hello canale tramite API hello o nel portale di Azure hello.
È responsabile per l'arresto dei canali al termine con canale hello. Canale di hello toostop errore comporterà la fatturazione continua.

> [!NOTE]
> Quando si utilizzano canali Standard, AMS automaticamente arresto qualsiasi canale è ancora nello stato "In esecuzione" 12 ore dopo feed input hello viene persa e non sono presenti programmi in esecuzione. Tuttavia, verrà comunque addebitato il costo per hello ora hello che canale si trovava nello stato "Running".
>
>

### <a id="states"></a>Gli stati dei canali e modalità di mapping toohello modalità di fatturazione
stato corrente di Hello di un canale. I valori possibili sono:

* **Arrestato**. Si tratta dello stato iniziale di hello di hello canale dopo la sua creazione, (a meno che l'avvio automatico è stato selezionato nel portale di hello.) In questo stato non viene eseguita alcuna attività di fatturazione. In questo stato, le proprietà del canale hello possono essere aggiornate, ma non è consentito lo streaming.
* **Avvio in corso**. Canale Hello viene avviato. In questo stato non viene eseguita alcuna attività di fatturazione. In questo stato non è consentito alcun aggiornamento o streaming. Se si verifica un errore, hello canale restituisce toohello stato arrestato.
* **In esecuzione**. Hello canale è in grado di elaborare flussi live. La fatturazione è ora attiva. È necessario arrestare hello canale tooprevent ulteriormente di fatturazione.
* **Arresto in corso**. Canale Hello è stata interrotta. In questo stato di transizione non viene eseguita alcuna attività di fatturazione. In questo stato non è consentito alcun aggiornamento o streaming.
* **Eliminazione in corso**. Canale Hello viene eliminata. In questo stato di transizione non viene eseguita alcuna attività di fatturazione. In questo stato non è consentito alcun aggiornamento o streaming.

Hello nella tabella seguente viene illustrato come canale stati modalità di fatturazione toohello mappa.

| Stato del canale | Indicatori dell'interfaccia utente del portale | Fatturazione? |
| --- | --- | --- |
| Avvio in corso |Avvio in corso |No (stato temporaneo) |
| In esecuzione |Pronto (nessun programma in esecuzione)<br/>oppure<br/>Streaming (almeno un programma in esecuzione) |SÌ |
| Arresto in corso |Arresto in corso |No (stato temporaneo) |
| Arrestato |Arrestato |No |

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Argomenti correlati
[Specifica per l'inserimento live di un flusso MP4 frammentato con Servizi multimediali di Azure](media-services-fmp4-live-ingest-overview.md)

[Utilizzo di canali che sono Enabled tooPerform Live codifica con servizi multimediali di Azure](media-services-manage-live-encoder-enabled-channels.md)

[Uso di canali che ricevono il flusso live a più velocità in bit da codificatori locali](media-services-live-streaming-with-onprem-encoders.md)

[Quote e limitazioni](media-services-quotas-and-limitations.md).  

[Concetti su Servizi multimediali di Azure](media-services-concepts.md)
