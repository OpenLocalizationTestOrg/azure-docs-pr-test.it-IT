---
title: aaaMedia Analitica nella piattaforma di servizi multimediali hello | Documenti Microsoft
description: "Una panoramica dell'anteprima pubblica di Analisi Servizi multimediali, una serie di servizi di riconoscimento vocale e visione artificiale per scalabilità, conformità, sicurezza e copertura globale per le aziende"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a>Supporto Analitica nella piattaforma di servizi multimediali hello
## <a name="overview"></a>Panoramica
Altre organizzazioni utilizzano video come hello tootrain medium preferito ai dipendenti, coinvolgere clienti e le funzioni di business di documento. Il cloud computing offre un modo toostore, flusso e accedere a questi file multimediali di grandi dimensioni. Tuttavia, man mano che aumenta la libreria di una società di contenuto video, è necessario un altrettanto efficace di estrarre informazioni dal contenuto hello. 

tooaddress questa esigenza in crescita, servizi multimediali di Azure offre Analitica multimediali di Azure. Supporto Analitica è una raccolta di componenti di riconoscimento vocale e visione che rende più semplice per aziende e organizzazioni tooderive ricavare informazioni utili dai propri file video. Per la compilazione di componenti della piattaforma di servizi multimediali core hello, supporto Analitica può gestire media di elaborazione su larga scala il primo giorno.

Con Analisi Servizi multimediali, gli sviluppatori possono introdurre rapidamente funzionalità video avanzate nelle applicazioni. Fornisce gli ambienti aziendali con scala completo hello, conformità, sicurezza e la portata globale richiesto da organizzazioni di grandi dimensioni.

Hello seguente diagramma illustra Analitica Media e altre parti principali della piattaforma di servizi multimediali hello. 

![Flusso di lavoro VoD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

I processori di contenuti multimediali di Analisi Servizi multimediali producono file MP4 o JSON. Se un processore di contenuti multimediali produce un file MP4, è possibile scaricare progressivamente file hello. Se un processore di contenuti multimediali produce un file JSON, è possibile scaricare file hello dall'archiviazione Blob di Azure. 

## <a name="media-analytics-services"></a>Servizi di Analisi Servizi multimediali

### <a name="indexer"></a>Indexer
Azure Media Indexer consente di rendere disponibili per la ricerca i contenuti, oltre a generare tracce per i sottotitoli codificati. Versione precedente di toohello confrontati, anteprima di Azure Media Indexer 2 è una lingua più veloce l'indicizzazione e più ampia di supportare. Le lingue supportate includono inglese, spagnolo, francese, tedesco, italiano, cinese, portoghese e arabo. Per informazioni dettagliate ed esempi, vedere [Elaborare video con Azure Media Indexer 2](media-services-process-content-with-indexer2.md).
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse combina stabilizzazione video e video funzionalità personalizzando toocreate rapido, utilizzabile dal contenuto in formato esteso. Oltre a creare personalizzando video, è possibile utilizzare Hyperlapse toocreate video stabili shaky video acquisite tramite telefoni cellulari e di cineprese. Per informazioni dettagliate ed esempi, vedere [File multimediali di Hyperlapse con Azure Media Hyperlapse](media-services-hyperlapse-content.md).
### <a name="motion-detector"></a>Motion Detector
È possibile utilizzare il movimento toodetect rilevamento movimento in un video con sfondi fermo. Questo rende possibile toocheck per falsi positivi sugli eventi di movimento rilevati da telecamere di sorveglianza. Per informazioni dettagliate ed esempi, vedere [Rilevamento dei movimenti per Analisi Servizi multimediali di Azure](media-services-motion-detection.md).
### <a name="face-detector"></a>Face Detector
Grazie all'uso di Face Detector, è possibile individuare i volti delle persone e le relative emozioni, ad esempio felicità, tristezza e sorpresa. Questa funzionalità vanta numerose applicazioni utili nel settore, descritte di seguito, tra cui l'aggregazione e l'analisi delle reazioni delle persone che partecipano a un evento. Per informazioni dettagliate ed esempi, vedere [Rilevamento di volti ed emozioni per Analisi Servizi multimediali di Azure](media-services-face-and-emotion-detection.md).
### <a name="video-summarization"></a>Riepilogo video
Riepilogo video consentono di creare riepiloghi dei video lunghi selezionando automaticamente interessanti frammenti video di origine hello. Questa possibilità è utile quando si desidera tooprovide una rapida panoramica delle quali tooexpect in un video di lunga durata. Per informazioni dettagliate ed esempi, vedere [riepilogo video di usare Azure Media Video anteprime toocreate](media-services-video-summarization.md).
### <a name="optical-character-recognition"></a>Riconoscimento ottico dei caratteri
Il riconoscimento ottico dei caratteri (OCR) di Analisi Servizi multimediali di Azure consente di convertire il contenuto di testo dei file video in testo digitale modificabile e sui cui è possibile eseguire ricerche. È quindi possibile automatizzare estrazione hello dei metadati significativo da segnale video di hello dei file multimediali.
### <a name="scalable-face-redaction"></a>Offuscamento dei volti scalabile
Azure Media Redactor è un processore di contenuti multimediali Analitica supporti offre redazione faccia scalabile nel cloud hello. Tramite l'adattamento faccia, è possibile modificare i caratteri tipografici tooblur video di tutti i collaboratori. È possibile toouse hello faccia redazione servizio nel supporto di notizie o quando è coinvolto nella sicurezza pubblica. Pochi minuti di riprese che contiene più caratteri tipografici possono richiedere ore tooredact manualmente, ma con questo servizio, redazione faccia richiede solo pochi semplici passaggi. Per ulteriori informazioni, vedere hello [redigere facce con Azure Media Analitica](media-services-face-redaction.md) articolo.

## <a name="common-scenarios"></a>Scenari comuni
Analisi Servii multimediali può aiutare le organizzazioni e le aziende a scoprire nuovi orizzonti nel mondo dei video e gestire più efficacemente grandi volumi di contenuti video. Di seguito sono descritti diversi scenari:

* **Call center**. Anche con l'avvento di hello di social networking, call center semplificano ancora un'alta percentuale delle transazioni di servizio clienti. In questi dati audio codificato è una grande quantità di informazioni sui clienti che possono essere analizzati tooachieve soddisfazione del cliente. Con Media Indexer, le organizzazioni possono estrarre il testo e creare indici di ricerca e dashboard. Possono quindi estrarre informazioni su reclami comuni, origini dei reclami e altri dati rilevanti.
* **Moderazione dei contenuti generati dall'utente**. Da reparti toopolice prese di notizie, molte organizzazioni utilizzano portali pubblico che accettano supporti generati dall'utente, ad esempio immagini e video. volume Hello del contenuto può raggiungere toounexpected gli eventi di scadenza. In questi scenari, è difficile tooconduct revisioni manuale efficace di contenuto appropriato per. I clienti possono basarsi su hello servizio contenuto moderation toofocus contenuto appropriato.
* **Sorveglianza**. Aumento delle dimensioni in uso di camere hello comporta un aumento inventario del video di sorveglianza. Controllo manuale del video di sorveglianza è toohuman con utilizzo intensivo e soggetta a errore in fase di. Media Analitica fornisce servizi come il rilevamento di attività, rilevamento viso e processo di hello toomake Hyperlapse esaminare, gestire e più semplice creare derivati.

## <a name="media-analytics-media-processors"></a>Processori di contenuti multimediali di Analisi Servizi multimediali
In questa sezione vengono processori di contenuti multimediali elenchi hello supporti Analitica e Mostra come toouse .NET o REST tooget un oggetto di supporto del processore (MP).

### <a name="mp-names"></a>Nomi dei processori di contenuti multimediali
* Azure Media Indexer 2 Preview
* Azure Media Indexer
* Azure Media Hyperlapse
* Rilevamento multimediale volti di Azure
* Rilevatore multimediale di movimento Azure
* Anteprime video multimediali di Azure
* Riconoscimento ottico dei caratteri multimediale di Azure

### <a name="net"></a>.NET
Hello seguente funzione accetta uno di hello specificato MP nomi e restituisce un oggetto Management Pack.

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a>REST
Richiesta:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

Risposta:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a>Demo
Vedere le [demo di Analisi Servizi multimediali di Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).

## <a name="next-steps"></a>Passaggi successivi
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Articoli correlati
Vedere l'[annuncio di Analisi Servizi multimediali di Azure](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
