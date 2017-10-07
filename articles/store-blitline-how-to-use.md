---
title: "aaaHow toouse Blitline per l'elaborazione di immagini - Guida alla funzionalità di Azure"
description: Informazioni su come toouse hello Blitline service tooprocess immagini all'interno di un'applicazione Azure.
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>Come toouse Blitline con Azure e archiviazione di Azure
Questa guida viene illustrato come tooaccess Blitline come toosubmit tooBlitline dei processi e servizi.

## <a name="what-is-blitline"></a>Informazioni su Blitline
Blitline è un'immagine basata su cloud servizio che consente l'elaborazione di immagini a livello enterprise a una frazione del prezzo di hello che toobuild al costo di elaborazione è manualmente.

tabelle dei fatti Hello è che l'elaborazione di immagini sia stata eseguita più volte, in genere ricreato da zero hello per ogni sito Web. Ce ne rendiamo conto perché noi stessi le abbiamo create un milione di volte. Ad un certo punto abbiamo deciso che era probabilmente arrivato il momento di farlo per tutti. È noto come toodo è veloce e in modo efficiente e salvare tutti gli utenti funziona in hello frattempo toodo.

Per ulteriori informazioni, visitare il sito [http://www.blitline.com](http://www.blitline.com).

## <a name="what-blitline-is-not"></a>Operazioni NON eseguite da Blitline
tooclarify cosa Blitline è utile per, è spesso più facile tooidentify Blitline non operazioni prima di procedere.

* Blitline non dispone di immagini di tooupload widget HTML. È necessario disporre le immagini disponibili pubblicamente o con autorizzazioni limitate per Blitline tooreach.
* Blitline NON esegue l'elaborazione delle immagini attive come Aviary.com
* Blitline non accetta un caricamento di immagini, è Impossibile eseguire il push del tooBlitline immagini direttamente. È necessario effettuare il push tooAzure archiviazione o altre posizioni che blitline supporta e quindi indicare Blitline dove toogo ottenerli.
* Blitline opera principalmente in parallelo e NON esegue alcuna elaborazione sincrona; vale a dire che l'utente deve comunicare un postback_url affinché sia possibile avvisarlo del termine dell'elaborazione.

## <a name="create-a-blitline-account"></a>Creare un account Blitline
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>Come un processo Blitline toocreate
Blitline utilizza JSON toodefine hello le azioni da tootake in un'immagine. Il codice JSON è composto da alcuni semplici campi:

Hello più semplice esempio è la seguente:

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

Qui abbiamo JSON che eseguirà un'immagine "src" "... boys.jpeg" e quindi ridimensionare too240x140 tale immagine.

ID applicazione Hello è un elemento in cui è possibile trovare il **le informazioni di connessione** o **GESTISCI** scheda in Azure. È l'identificatore di segreto che consente di processi toorun su Blitline.

Hello "Salva" parametro identifica informazioni in cui si desidera che tooput hello immagine dopo che è stata eseguita l'elaborazione. In questo caso, la posizione non è stata definita. Se non viene definita alcuna posizione, Blitline archivierà l'immagine in locale (temporaneamente) in una posizione univoca sul cloud. Si sarà in grado di tooget che percorso da hello JSON restituito dalla Blitline quando si apportata hello Blitline. identificatore "image" Hello è obbligatorio e viene restituito tooyou quando tooidentify questa particolare salvata l'immagine.

È possibile trovare ulteriori informazioni su hello *funzioni* è qui il supporto: <http://www.blitline.com/docs/functions>

È anche possibile trovare documentazione su hello qui le opzioni di processo: <http://www.blitline.com/docs/api>

Una volta ottenuto il file JSON è sufficiente toodo **POST** è troppo`http://api.blitline.com/job`

Si otterrà un codice JSON che avrà più o meno l'aspetto seguente:

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


In questo modo si Blitline ha ricevuto la richiesta, ha inserito nella coda di elaborazione e al termine dell'immagine di hello è disponibile in: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>Come toosave un tooyour immagine account di archiviazione di Azure
Se si dispone di un account di archiviazione di Azure, è possibile disporre facilmente immagini di hello elaborato push Blitline nel contenitore di Azure. Aggiungendo un "azure_destination" definire percorso hello e le autorizzazioni per toopush Blitline per.

Di seguito è fornito un esempio:

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


Compilando hello CAPITALIZED valori con valori personalizzati, è possibile inviare questa toohttp://api.blitline.com/job JSON e verrà elaborati con un filtro di sfocatura hello "src" immagine e quindi inseriti tooyou destinazione Azure.

### <a name="please-note"></a>Nota bene:
Hello SAS deve contenere l'url SAS intera hello, incluso il nome file hello del file di destinazione hello.

Esempio:

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


È inoltre possibile leggere l'edizione più recente di hello di documenti di archiviazione di Azure del Blitline [qui](http://www.blitline.com/docs/azure_storage).

## <a name="next-steps"></a>Passaggi successivi
Visitare tooread blitline.com su tutte le altre funzionalità:

* Documenti sugli endpoint API di Blitline <http://www.blitline.com/docs/api>
* Funzioni delle API di Blitline <http://www.blitline.com/docs/functions>
* Esempi delle API di Blitline <http://www.blitline.com/docs/examples>
* Libreria NuGet di terze parti <http://nuget.org/packages/Blitline.Net>

