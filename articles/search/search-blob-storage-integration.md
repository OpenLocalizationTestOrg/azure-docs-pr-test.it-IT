---
title: Ricerca di Azure di aaaAdding tooBlob archiviazione | Documenti Microsoft
description: Creare un indice nel codice utilizzando hello API REST HTTP ricerca di Azure.
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: a3801790067bf169693b500e83799286b7387a77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Ricerca nell'archiviazione BLOB tramite Ricerca di Azure

La ricerca tra hello diversi tipi di contenuto archiviato in archiviazione Blob di Azure può essere toosolve un problema difficile. Tuttavia, è possibile indicizzare e ricerca hello contenuto del BLOB in pochi clic tramite ricerca di Azure. La ricerca nell'archiviazione BLOB richiede il provisioning di un servizio di Ricerca di Azure. Hello diversi limiti di servizio e di ricerca di Azure i livelli di prezzo sono reperibile in hello [pagina dei prezzi](https://aka.ms/azspricing).

## <a name="what-is-azure-search"></a>Che cos'è la Ricerca di Azure?
[Ricerca di Azure](https://aka.ms/whatisazsearch) è una soluzione di ricerca che rende più semplice per ricerca full-text affidabile di sviluppatori tooadd riscontra tooweb e applicazioni per dispositivi mobili. Come servizio, ricerca di Azure consente di rimuovere hello necessità toomanage qualsiasi ricerca infrastruttura offrendo al contempo un [tempi di attività pari al 99,9% SLA](https://aka.ms/azuresearchsla).

Con supporto avanzato per 56 lingue, Ricerca di Azure può analizzare il contenuto e gestire in modo intelligente i costrutti specifici di ogni lingua. Ricerca di Azure offre inoltre hello strumenti toobuild un'esperienza utente di ricerca avanzate. È semplice tooadd funzionalità quali navigazione con facet, i suggerimenti di ricerca typeahead e hit interfacce toouser evidenziazione mediante ricerca di Azure. toolearn sulle funzionalità di ricerca di Azure, è possibile leggere del servizio hello [documentazione](https://aka.ms/azsearchdocs).

## <a name="crack-open-and-search-through-hello-content-of-enterprise-document-formats"></a>Abbreviazione aperto e la ricerca tramite contenuto hello di formati di documenti aziendali
Con il supporto per [documento estrazione](https://aka.ms/azsblobindexer) nell'archiviazione Blob di Azure, ricerca di Azure è possibile indicizzare contenuto hello di vari tipi di file archiviati nel BLOB:
- PDF
- Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (messaggi di posta elettronica di Outlook)
- HTML
- File di testo normale

Tramite l'estrazione di testo e i metadati di questi tipi di file, è facile toosearch in più formati di file con i documenti più rilevanti hello toofind singola query indipendentemente dal tipo. Per l'indicizzazione dei metadati di contenuto e hello hello di documenti di Microsoft Office, file PDF e messaggi di posta elettronica, è possibile toobuild una soluzione di gestione del contenuto aziendale affidabile tramite l'archiviazione di Blob e di ricerca di Azure.

## <a name="search-through-your-blob-metadata"></a>Ricerca nei metadati dei BLOB
Uno scenario comune che rende facile toosort tramite i BLOB di qualsiasi tipo di contenuto è le proprietà di sistema di metadati del blob personalizzata definita dall'utente hello tooindex nonché hello per ognuno dei BLOB. In questo modo, le informazioni per ogni blob viene indicizzate indipendentemente dal tipo di documento in blob hello in modo semplice, è possibile ordinare e il facet di hello in tutto il contenuto di archiviazione Blob.

[Altre informazioni sull'indicizzazione dei metadati dei BLOB.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>Ricerca di immagini
Ricerca full-text di ricerca di Azure, navigazione con facet e funzionalità di ordinamento può essere applicato toohello metadati delle immagini archiviate nei blob.

Se queste immagini sono pre-elaborate utilizzando hello [Computer Vision API](https://www.microsoft.com/cognitive-services/computer-vision-api) da cognitivi servizi Microsoft, quindi è possibile tooindex hello visual sono presenti contenuti in ciascuna immagine inclusi OCR e della grafia. Stiamo lavorando sull'aggiunta di funzionalità di elaborazione immagini OCR e altri direttamente tooAzure ricerca, se è interessati a queste funzionalità, inviare una richiesta nel nostro [UserVoice](https://aka.ms/azsuv) o [e-mail](mailto:azscustquestions@microsoft.com).

## <a name="index-and-search-through-json-blobs"></a>Indicizzare e cercare contenuto in BLOB JSON
Ricerca di Azure può essere configurato tooextract strutturato contenuto blob che contengono JSON. Ricerca di Azure è possibile leggere i BLOB JSON e analisi hello strutturato contenuto nei campi appropriati di hello di un documento di ricerca di Azure. Ricerca di Azure può richiedere anche blob che contengono una matrice di oggetti JSON e di eseguire il mapping di ogni documento di ricerca di Azure separato tooa elemento.

Si noti che l'analisi di JSON non è attualmente configurabile tramite il portale di hello. [Altre informazioni sull'analisi JSON in Ricerca di Azure.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>Avvio rapido
Ricerca di Azure può essere aggiunto tooblobs direttamente dal pannello portale archiviazione Blob di hello.

![](./media/search-blob-storage-integration/blob-blade.png)

Facendo clic sull'opzione di "Ricerca di Azure aggiungere" hello, verrà avviato un flusso in cui è possibile selezionare un servizio di ricerca di Azure esistente o creare un nuovo servizio. Se si crea un nuovo servizio, non si sarà più connessi al portale dell'account di archiviazione. Sarà necessario toore-passare portale Pannello di toohello archiviazione e selezionare nuovamente l'opzione "Ricerca di Azure aggiungere" hello, in cui è possibile selezionare servizio esistente hello.

### <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello Blob indicizzatore di ricerca di Azure in hello completo [documentazione](https://aka.ms/azsblobindexer).
