---
title: i caratteri tipografici aaaRedact con questa procedura dettagliata Azure Media Analitica | Documenti Microsoft
description: In questo argomento viene istruzioni dettagliate su come toorun un flusso di lavoro completo redazione usando Azure Media Services Explorer (AMSE) e Azure Media Redactor visualizzatore (strumento open source).
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>Procedura dettagliata: offuscare i volti con Analisi Servizi multimediali di Azure

## <a name="overview"></a>Panoramica

**Azure Media Redactor** è un [Azure Media Analitica](media-services-analytics-overview.md) processore di contenuti multimediali (MP) che offre redazione faccia scalabile nel cloud hello. Adattamento faccia consente si toomodify video in facce tooblur ordine dei singoli utenti selezionati. È opportuno toouse hello faccia redazione servizio pubblica sicurezza e i supporti di notizie negli scenari in. Pochi minuti di riprese che contiene più caratteri tipografici possono richiedere ore tooredact manualmente, ma con questa faccia hello servizio processo di adattamento richiederà solo alcuni semplici passaggi. Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/azure-media-redactor/) blog.

Per informazioni dettagliate su **Azure Media Redactor**, vedere hello [Panoramica redazione faccia](media-services-face-redaction.md) argomento.

In questo argomento viene istruzioni dettagliate su come toorun un flusso di lavoro completo redazione usando Azure Media Services Explorer (AMSE) e Azure Media Redactor visualizzatore (strumento open source).

Hello **Azure Media Redactor** Management Pack è attualmente in anteprima. È disponibile in tutte le aree di Azure pubbliche, nonché nei data center cinesi e del governo degli USA. Al momento questa versione di anteprima è disponibile gratuitamente. Nella versione corrente di hello, è previsto un limite di 10 minuti lunghezza video elaborato.

Per altre informazioni, vedere [questo](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.

## <a name="azure-media-services-explorer-workflow"></a>Flusso di lavoro di Azure Media Services Explorer

Hello tooget modo più semplice introduttiva Redactor è toouse strumento AMSE open source di hello su github. È possibile eseguire un flusso di lavoro semplificata tramite **combinati** modalità se non è necessario accedere toohello annotazione json o hello faccia immagini jpg.

### <a name="download-and-setup"></a>Download e installazione

1. Scaricare lo strumento AMSE hello da [qui](https://github.com/Azure/Azure-Media-Services-Explorer).
1. Accedi tooyour account servizi multimediali usando la chiave del servizio.

    tooobtain hello Nome account e informazioni sulla chiave, passa toohello [portale di Azure](https://portal.azure.com/) e selezionare l'account di sistema AMS. Dopodiché, selezionare Impostazioni > Chiavi. finestre di Hello Gestisci chiavi Mostra nome hello e chiavi primarie e secondarie hello viene visualizzato. Copiare i valori del nome dell'account hello e la chiave primaria hello.

![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>Primo passaggio: modalità analisi

1. Caricare il file multimediale facendo clic su Asset -> Carica oppure trascinandolo. 
1. Fare clic sul file multimediale con il pulsante destro del mouse ed elaborarlo usando Analisi Servizi multimediali -> Azure Media Redactor -> Modalità analisi. 


![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

output di Hello includerà un file json di annotazioni con dati di posizione di carattere, nonché in formato jpg di ogni tipo di carattere rilevato. 

![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>Secondo passaggio: modalità offuscamento

1. Caricare il toohello asset video originale dal primo passaggio di hello e impostare come primario asset. 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. (Facoltativo) Caricare un file 'Dance_idlist.txt', che include un elenco di nuova riga delimitato di ID desiderato tooredact hello. 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. (Facoltativo) Verificare qualsiasi file annotations.json toohello di modifiche, ad esempio aumentando hello delimitazione i limiti di casella. 
4. Fare clic con il pulsante destro asset di output di hello dal primo passaggio di hello, selezionare hello Redactor ed eseguire con hello **Redact** modalità. 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. Scaricare o condividere asset di output finale di adattamento hello. 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Strumento open source Azure Media Redactor Visualizer

Un open-source [strumento Visualizzatore](https://github.com/Microsoft/azure-media-redactor-visualizer) è sviluppatori toohelp progettato con formato annotazioni hello con l'analisi e l'utilizzo di output di hello.

Dopo che clonare il repository di hello, nel progetto di hello toorun ordine, sarà necessario toodownload FFMPEG da loro [sito ufficiale](https://ffmpeg.org/download.html).

Se si è uno sviluppatore sta tentando di hello tooparse dati annotazione JSON, cercare all'interno di Models.MetaData esempi di codice di esempio.

### <a name="set-up-hello-tool"></a>Impostare lo strumento hello

1.  Scaricare e compilare hello intera soluzione. 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  Scaricare FFmpeg da [qui](https://ffmpeg.org/download.html). Questo progetto è stato originariamente sviluppato con la versione be1d324 (04-10-2016) con il collegamento statico. 
3.  Copiare toohello ffmpeg.exe e ffprobe.exe stessa cartella di output come AzureMediaRedactor.exe. 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. Eseguire AzureMediaRedactor.exe. 

### <a name="use-hello-tool"></a>Utilizzare lo strumento di hello

1. Elaborare video nell'account di servizi multimediali di Azure con hello Redactor MP in modalità di analisi. 
2. Scaricare file video originale hello e output di hello di hello redazione - processo di analisi. 
3. Eseguire un'applicazione hello visualizzatore e selezionare file hello sopra descritti. 

    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. Visualizzare l'anteprima del file. Selezionare rivolto si sarebbe tooblur tramite la barra laterale hello in hello destra. 
    
    ![Offuscamento dei volti](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  campo di testo Hello nella parte inferiore verrà aggiornato con faccia hello ID. Creare un file denominato "idlist.txt" contenente questi ID come elenco delimitato da nuova riga. 

    >[!NOTE]
    > Hello idlist.txt deve essere salvato in formato ANSI. È possibile utilizzare il blocco note toosave in ANSI.
    
6.  Caricare l'asset di output toohello file dal passaggio 1. Caricare hello originale toothis video asset nonché e impostare come primario asset. 
7.  Eseguire il processo di adattamento in questo asset con "Redact" modalità tooget hello redatta video finale. 

## <a name="next-steps"></a>Passaggi successivi 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Collegamenti correlati
[Panoramica di Analisi servizi multimediali di Azure](media-services-analytics-overview.md)

[Demo di Analisi servizi multimediali di Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[Presto sarà disponibile l'offuscamento dei volti per Analisi Servizi multimediali di Azure](https://azure.microsoft.com/blog/azure-media-redactor/)
