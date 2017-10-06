---
title: aaaAnalyze i supporti tramite hello portale di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come tooprocess hello di file multimediali con processori di contenuti multimediali Analitica Media (MP) utilizzando il portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Analizzare i file multimediali usando hello portale di Azure
> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Azure. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

## <a name="overview"></a>Panoramica
Azure Media Services Analitica è una raccolta di riconoscimento vocale e visione componenti (scala enterprise, conformità, sicurezza e portata globale) che rendono più semplice per aziende e organizzazioni tooderive ricavare informazioni utili dai file di video. Per una panoramica più dettagliata di Analisi Servizi multimediali, vedere [questo](media-services-analytics-overview.md) argomento. 

Questo argomento viene illustrato come tooprocess hello di file multimediali con processori di contenuti multimediali Analitica Media (MP) utilizzando il portale di Azure. I processori di contenuti multimediali di Analisi Servizi multimediali producono file MP4 o JSON. Se un processore di contenuti multimediali ha prodotto un file MP4, è possibile scaricare progressivamente file hello. Se un processore di contenuti multimediali ha prodotto un file JSON, è possibile scaricare file hello da hello archiviazione blob di Azure. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>Scegliere una risorsa che si desidera tooanalyze
1. In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.
2. In hello **impostazioni** selezionare **asset**.  
   .
    ![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. Asset selezionare hello che si desidera hello tooanalyze e premere **Analizza** pulsante.
   
    ![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. In hello **asset di file multimediali di processo con supporto Analitica** finestra, processore hello selezionare. 
   
    il resto di Hello di hello articolo spiega come e perché toouse ogni processore. 
5. Premere **crea** toohello avviare un processo.

## <a name="azure-media-indexer"></a>Azure Media Indexer
Hello **Azure Media Indexer** processore di contenuti multimediali consente di file multimediali toomake e ricerca, contenuto, nonché generare tracce sottotitoli codificate chiuse. Questa sezione offre alcuni dettagli sulle opzioni che è possibile specificare per questo Management Pack.

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>Lingua
Hello riconosciuto nel file multimediale hello toobe di linguaggio naturale. ad esempio l'inglese o lo spagnolo. 

### <a name="captions"></a>Sottotitoli
È possibile scegliere un formato di sottotitoli che verrà generato dal contenuto. Un processo di indicizzazione possa generare file di sottotitoli nel hello seguenti formati:  

* **SAMI**
* **TTML**
* **WebVTT**

Chiuso i file di didascalia (CC) in questi formati possono essere utilizzati toomake audio e video file toopeople accessibile con problemi uditivi.

### <a name="aib-file"></a>File aib
Selezionare questa opzione se si sarebbe simile toogenerate hello Audio indice Blob file per l'utilizzo con hello IFilter di Server SQL personalizzata. Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.

### <a name="keywords"></a>Parole chiave
Selezionare questa opzione se si desidera toogenerate un file XML di parole chiave. Questo file contiene parole chiave estratte da contenuti vocali hello, con la frequenza e informazioni relative all'offset.

### <a name="job-name"></a>Nome processo
Nome descrittivo che consente di identificare il processo di hello. [Questo](media-services-portal-check-job-progress.md) articolo viene descritto come è possibile monitorare lo stato di avanzamento hello di un processo. 

### <a name="output-file"></a>File di output
Nome descrittivo che consente di identificare il contenuto di output di hello. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Azure Media Hyperlapse è un processore multimediale che crea fluidi video in time-lapse da contenuti registrati in prima persona o da fotocamere d'azione.  Per altre informazioni, vedere [questo](media-services-hyperlapse-content.md) argomento. Questa sezione offre alcuni dettagli sulle opzioni che è possibile specificare per questo Management Pack.

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Velocità
Specificare la velocità di hello con cui toospeed i video di input hello. output di Hello è una copia trasformata stabilizzare e tempo trascorso di video di input hello.

### <a name="job-name"></a>Nome processo
Nome descrittivo che consente di identificare il processo di hello. [Questo](media-services-portal-check-job-progress.md) articolo viene descritto come è possibile monitorare lo stato di avanzamento hello di un processo. 

### <a name="output-file"></a>File di output
Nome descrittivo che consente di identificare il contenuto di output di hello. 

## <a name="azure-media-face-detector"></a>Rilevamento multimediale volti di Azure
Hello **Azure Media faccia Rilevatore** processore di contenuti multimediali (MP) consente di toocount, i movimenti di avanzamento e anche la partecipazione di destinatari misuratore e reazione tramite facciale. Questo servizio contiene due funzionalità: 

* **Rilevamento volti**
  
    Il Rilevamento volti rileva e monitora i volti umani all'interno di un video. Più caratteri tipografici possono essere rilevati e successivamente essere rilevate man mano che vengono spostati, con hello ora e il percorso dei metadati restituiti in un file JSON. Durante il rilevamento, verrà eseguito un tentativo toogive un toohello ID coerenza stesso faccia mentre persona hello è spostamento sullo schermo, anche se è nascosto o lasciare brevemente il frame di hello.
  
  > [!NOTE]
  > Questo servizio non esegue il riconoscimento facciale. Persona che lascia frame hello o diventa nascosto per troppo tempo verrà assegnato un nuovo ID quando viene restituita.
  > 
  > 
* **Rilevamento emozioni**
  
    Rilevamento emozioni è un componente facoltativo di hello processore di contenuti multimediali di rilevamento viso restituisce analisi su più attributi affettivi da facce hello rilevate, tra cui "Happiness", sadness, paura, anger e altro ancora. 

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Modalità di rilevamento
Una delle seguenti modalità hello può essere utilizzata da processore hello:

* rilevamento volti
* rilevamento emozioni per volto
* rilevamento emozioni aggregato

### <a name="job-name"></a>Nome processo
Nome descrittivo che consente di identificare il processo di hello. [Questo](media-services-portal-check-job-progress.md) articolo viene descritto come è possibile monitorare lo stato di avanzamento hello di un processo. 

### <a name="output-file"></a>File di output
Nome descrittivo che consente di identificare il contenuto di output di hello. 

## <a name="azure-media-motion-detector"></a>Rilevatore multimediale di movimento Azure
Hello **rilevatore di movimento di Azure Media** Abilita processore (MP) supporti tooefficiently si identificano le sezioni di interesse all'interno di un video in caso contrario lungo e procede senza interruzioni. Rilevamento del movimento utilizzabile in camera statico riprese tooidentify sezioni del video hello in cui viene effettuato lo spostamento. Genera un file JSON che contiene i metadati con i timestamp e hello delimitazione area in cui si è verificato l'evento hello.

Mirata feed video di sicurezza, questa tecnologia è in grado di toocategorize movimento in eventi rilevanti e falsi positivi, ad esempio shadows e modifiche di illuminazione. Ciò consente gli avvisi di sicurezza toogenerate dai feed di fotocamera senza viene posta indesiderata con gli eventi non rilevanti infiniti, pur essendo momenti tooextract in grado di interesse da video sorveglianza estremamente lunghi.

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Anteprime video multimediali di Azure
Questo processore consentono di creare riepiloghi dei video lunghi selezionando automaticamente interessanti frammenti video di origine hello. Ciò è utile quando si desidera tooprovide una rapida panoramica delle quali tooexpect in un video di lunga durata. Per informazioni dettagliate ed esempi, vedere [tooCreate Usa Azure Media Video miniature un riepilogo di Video](media-services-video-summarization.md)

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>Nome processo
Nome descrittivo che consente di identificare il processo di hello. [Questo](media-services-portal-check-job-progress.md) articolo viene descritto come è possibile monitorare lo stato di avanzamento hello di un processo. 

### <a name="output-file"></a>File di output
Nome descrittivo che consente di identificare il contenuto di output di hello. 

## <a name="next-steps"></a>Passaggi successivi
Visualizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

