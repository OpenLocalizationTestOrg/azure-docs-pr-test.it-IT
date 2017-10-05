---
title: Come codificare un asset di Azure mediante Media Encoder Standard| Microsoft Docs
description: Informazioni su come usare Media Encoder Standard per codificare contenuti multimediali in Servizi multimediali di Azure. Negli esempi di codice viene usata l'API REST.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 796f3b5a4dd56a0160986600cbbcf38faf8add56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a>Come codificare un asset mediante Media Encoder Standard
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portale](media-services-portal-encode.md)
>
>

## <a name="overview"></a>Panoramica
Per distribuire un video digitale in Internet è necessario comprimere il file multimediale. I file video digitali hanno dimensioni piuttosto elevate e possono risultare troppo grandi per la distribuzione su Internet o per la visualizzazione corretta sui dispositivi dei clienti. Mediante il processo di codifica è possibile comprimere video e audio per consentire ai clienti di visualizzare i file multimediali.

I processi di codifica sono tra le operazioni di elaborazione più frequenti in Servizi multimediali di Azure. Questi processi vengono creati per convertire i file multimediali da una codifica all'altra. Durante la codifica è possibile usare il codificatore multimediale incorporato in Servizi multimediali (Media Encoder Standard). È inoltre possibile usare un codificatore fornito da un partner di Servizi multimediali. I codificatori di terze parti sono disponibili tramite il Marketplace di Azure. È possibile specificare i dettagli relativi alle attività di codifica usando stringhe di set di impostazioni definite per il codificatore oppure file di configurazione di set di impostazioni. Per i tipi di set di impostazioni disponibili, vedere [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960) (Set di impostazioni disponibili per Media Encoder Standard).

Ogni processo può includere una o più attività in base al tipo di elaborazione che si desidera eseguire. Usando l'API REST è possibile creare i processi e le attività correlate procedendo in due modi diversi:

* Le Attività possono essere definite in linea mediante la proprietà di navigazione attività nelle entità dei processi.
* Usare l'elaborazione batch OData.

È consigliabile codificare sempre i file di origine in un set MP4 a velocità in bit adattiva e quindi convertire il set nel formato desiderato mediante la [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md).

Se l'asset di output è protetto con crittografia di archiviazione, è necessario configurare i criteri di distribuzione degli asset. Per altre informazioni, vedere [Configurazione dei criteri di distribuzione degli asset](media-services-rest-configure-asset-delivery-policy.md).

## <a name="considerations"></a>Considerazioni

Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP. Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).

Prima di iniziare a fare riferimento ai supporti multimediali, verificare di avere il corretto processore ID del supporto. Per altre informazioni, vedere [Ottenere processori di contenuti multimediali](media-services-rest-get-media-processor.md).

## <a name="connect-to-media-services"></a>Connettersi a Servizi multimediali

Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali. Le chiamate successive dovranno essere effettuate al nuovo URI.

## <a name="create-a-job-with-a-single-encoding-task"></a>Creare un processo con una singola attività di codifica
> [!NOTE]
> Quando si usa l'API REST di Servizi multimediali, tenere presenti le seguenti considerazioni:
>
> Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP. Per altre informazioni, vedere [Configurazione dello sviluppo dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).
>
> Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali. Le chiamate successive dovranno essere effettuate al nuovo URI. Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).
>
> Se si usa JSON e si specifica di usare la parola chiave **__metadata** nella richiesta (ad esempio, per fare riferimento a un oggetto collegato) è necessario impostare l'intestazione **Accetta** sul [formato JSON Verbose](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accetta: application/json;odata=verbose.
>
>

Il seguente esempio mostra come creare e pubblicare un processo con un'attività impostata per codificare un video con determinati valori di risoluzione e qualità. Quando si esegue la codifica con Media Encoder Standard, è possibile usare i set di impostazioni di attività specificati [qui](http://msdn.microsoft.com/library/mt269960).

Richiesta:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

Risposta:

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a>Impostare il nome dell'asset di output
Il seguente esempio mostra impostare l'attributo assetName:

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>Considerazioni
* Le proprietà TaskBody devono usare codice XML letterale per definire il numero di asset di input o di output che vengono usati dall'attività. L'argomento Task contiene la definizione dello schema XML per il codice XML.
* Nella definizione TaskBody ogni valore interno per <inputAsset> e <outputAsset>deve essere impostato come JobInputAsset(value) o JobOutputAsset(value).
* Un'attività può avere più asset di output. Un oggetto JobOutputAsset(x) può essere usato solo una volta come output di un'attività in un processo.
* È possibile specificare JobInputAsset o JobOutputAsset come asset di input di un'attività.
* Le attività non devono formare un ciclo.
* Il parametro del valore passato a JobInputAsset o JobOutputAsset rappresenta il valore di indice di un asset. Gli asset effettivi vengono definiti nelle proprietà di navigazione InputMediaAssets e OutputMediaAssets nella definizione dell'entità del processo.
* Poiché Servizi multimediali si basa su OData versione 3, i riferimenti ai singoli asset nelle raccolte delle proprietà di navigazione InputMediaAssets e OutputMediaAssets vengono definiti mediante una coppia nome/valore "__metadata : uri".
* InputMediaAssets è mappata a uno o più asset creati in Servizi multimediali. Le proprietà OutputMediaAssets vengono create dal sistema. Non fanno riferimento a un asset esistente.
* Per assegnare un nome a OutputMediaAssets è possibile usare l'attributo assetName. Se questo attributo non è presente, il nome della proprietà OutputMediaAssets corrisponde al valore del testo interno dell'elemento <outputAsset> preceduto dal nome o dall'ID del processo, nel caso in cui la proprietà Name non sia definita. Se ad esempio si è impostato "Sample" come valore di assetName, la proprietà Name di OutputMediaAssets sarà impostata su "Sample". Se invece non si è impostato un valore per assetName, ma si è impostato "NewJob" come nome del processo, il nome di OutputMediaAssets sarà "JobOutputAsset(value)_NewJob".

## <a name="create-a-job-with-chained-tasks"></a>Creare un processo con attività concatenate
In molti scenari di applicazione, gli sviluppatori desiderano creare una serie di attività di elaborazione. In Servizi multimediali è possibile creare una serie di attività concatenate. Ogni attività esegue diversi passaggi di elaborazione e può usare processori di contenuti multimediali differenti. Le attività concatenate possono trasferire un asset da un'attività a un'altra e consentono quindi l'esecuzione delle attività dell'asset in sequenza lineare. Tuttavia, non è necessario che le attività eseguite in un processo siano in sequenza. Quando si crea un'attività concatenata, gli oggetti **ITask** concatenati vengono creati in un singolo oggetto **IJob**.

> [!NOTE]
> Attualmente è previsto un limite di 30 attività per processo. Se è necessario concatenare più di 30 attività, creare più processi in modo da contenerle tutte.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a>Considerazioni
Per abilitare il concatenamento di attività:

* Un processo deve avere almeno due attività.
* Deve essere presente almeno un'attività il cui input viene usato come output di un'altra attività nel processo.

## <a name="use-odata-batch-processing"></a>Utilizzare l'elaborazione batch OData
Nell'esempio seguente viene illustrato come utilizzare l'elaborazione batch OData per creare un processo e un’attività. Per informazioni sull'elaborazione batch, vedere l'articolo relativo all' [elaborazione batch OData (Open Data Protocol)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a>Creare un processo tramite JobTemplate
Quando si elaborano più asset usando un set comune di attività, usare JobTemplate per specificare le impostazioni di attività predefinite o per impostare l'ordine delle attività.

L'esempio seguente mostra come creare JobTemplate con un'entità TaskTemplate definita inline. L'entità TaskTemplate usa Media Encoder Standard come entità MediaProcessor per codificare il file di asset. Tuttavia, può usare anche altre entità Mediaprocessor.

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> A differenza di altre entità di Servizi multimediali, è necessario definire un nuovo identificatore GUID per ogni entità TaskTemplate e inserirlo nel corpo della richiesta in taskTemplateId e nella proprietà Id. Lo schema di identificazione del contenuto deve seguire lo schema descritto in Identificare le entità di Servizi multimediali di Azure. Inoltre, non è possibile aggiornare le entità JobTemplate. È invece necessario crearne una nuova con le modifiche aggiornate.
>
>

Se l'esito è positivo, viene restituita la seguente risposta:

    HTTP/1.1 201 Created

    . . .


L'esempio seguente mostra come creare un processo che fa riferimento all'ID di un'entità JobTemplate:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


Se l'esito è positivo, viene restituita la seguente risposta:

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver spiegato il processo per la codifica di un asset, si può passare all'argomento [Procedura per controllare lo stato dei processi con Servizi multimediali](media-services-rest-check-job-progress.md).

## <a name="see-also"></a>Vedere anche
[Ottenere processori di contenuti multimediali](media-services-rest-get-media-processor.md)
