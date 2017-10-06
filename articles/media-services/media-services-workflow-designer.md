---
title: aaaCreate avanzate codifica flussi di lavoro con Progettazione flussi di lavoro | Documenti Microsoft
description: Informazioni su come toocreate avanzate codifica flussi di lavoro con Progettazione flussi di lavoro.
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 004815f2-0761-4706-87a1-675ba36e0322
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako;johndeu;anilmur
ms.openlocfilehash: 3744cde54c78bec7c7b586962ec1a8fe9529c1d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-advanced-encoding-workflows-with-workflow-designer"></a>Creazione di flussi di lavoro di codifica avanzati con Progettazione flussi di lavoro
## <a name="overview"></a>Panoramica
Hello **Progettazione flussi di lavoro** è uno strumento desktop di Windows che viene utilizzati toodesign e compilare flussi di lavoro personalizzati per la codifica con **flusso di lavoro Premium del codificatore multimediale**.
Usando l'accensione di hello hello del flusso di lavoro dello strumento di progettazione, è possibile progettare e creare flussi di lavoro complessi che verrà eseguito in **Premium del codificatore multimediale**.  

I flussi di lavoro può includere la logica delle decisioni del cliente e creazione di rami in base alle proprietà del file di origine di input hello. È possibile creare flussi di lavoro con le proprietà sottoponibile a override e i valori dinamici toomake hello anche più complessa codifica attività semplice toorepeat e personalizzare nel cloud hello.

Di seguito sono riportati alcuni flussi di lavoro di esempio che è possibile creare:

* Decisione basato su flussi di lavoro che controllano il contenuto di origine hello per la risoluzione e codificare solo tracce di output di hello desiderato.  Si tratta helfpul eliminando le tracce di hello sprecato che verrebbero generate da upscaling hello origine contenuto inavvertitamente.
* Più file di input possono essere utilizzato toosupport didascalie, sovrapposizioni e contenuto insieme unione (stitching). 

Questo strumento può anche essere toomodify utilizzato uno dei nostri [pubblicato i flussi di lavoro](media-services-workflow-designer.md#existing_workflows). 

> [!NOTE]
> la copia dello strumento di progettazione del flusso di lavoro hello, tooget, contattare mepd@microsoft.com.
> 
> 

Dopo aver creato un file del flusso di lavoro, lo strumento può essere caricato come risorsa e può quindi essere usato per la codifica di file multimediali. Per informazioni su come tooencode con **flusso di lavoro Premium del codificatore multimediale** utilizzando **.NET**, vedere [avanzate codifica con flusso di lavoro Premium del codificatore multimediale](media-services-encode-with-premium-workflow.md).

## <a id="existing_workflows"></a>Modificare flussi di lavoro esistenti
Hello predefinito [pubblicato i flussi di lavoro](media-services-workflow-designer.md#existing_workflows) può essere modificato utilizzando hello strumento di progettazione. È possibile ottenere i file del flusso di lavoro predefinito hello [qui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). cartella Hello contiene inoltre descrizione hello di questi file.

Hello video seguente viene illustrato come toouse hello finestra di progettazione.

### <a name="day-1--getting-started"></a>Giorno 1 - Introduzione
Il video del giorno 1 riguarda:

* Panoramica della finestra di progettazione
* Flussi di lavoro di base - "Hello World"
* Creazione di più file di output MP4 da usare lo streaming di Servizi multimediali di Azure

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-1/player]
> 
> 

### <a name="day-2"></a>Giorno 2
Il video del giorno 2 riguarda:

* Vari scenari di file di origine - Gestione dell'audio
* Flussi di lavoro con logica avanzata
* Fasi del grafico

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-2/player]
> 
> 

### <a name="day-3"></a>Giorno 3
Il video del giorno 3 riguarda:

* Creazione di script all'interno di flussi di lavoro/progetti
* Restrizioni con hello codificatore corrente
* Domande e risposte

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-3/player]
> 
> 

## <a name="next-step"></a>Passaggio successivo
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

Se è necessario supportare o domande sulla creazione di flussi di lavoro personalizzati in strumento di progettazione del flusso di lavoro di hello, inviare posta elettronica toomepd@microsoft.com.

## <a name="see-also"></a>Vedere anche
[Video di formazione sulla finestra di progettazione del flusso di lavoro del codificatore Premium di Azure](http://johndeutscher.com/2015/07/06/azure-premium-encoder-workflow-designer-training-videos/)

