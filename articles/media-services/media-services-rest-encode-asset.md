---
title: aaaHow tooencode un asset con Media Encoder Standard Azure | Documenti Microsoft
description: Informazioni su come toouse Media Encoder Standard tooencode multimediali in servizi multimediali di Azure. Negli esempi di codice viene usata l'API REST.
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
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a>Come tooencode un asset con Media Encoder Standard
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portale](media-services-portal-encode.md)
>
>

## <a name="overview"></a>Panoramica
toodeliver video digitale su hello Internet, è necessario comprimere supporti hello. File video digitali sono di grandi dimensioni e potrebbero essere troppo grande toodeliver su hello Internet, o per toodisplay dispositivi dei clienti in modo corretto. La codifica è il processo di hello di compressione di video e audio in modo i clienti possono visualizzare i file multimediali.

I processi di codifica sono una delle operazioni di elaborazione più comune di hello in servizi multimediali di Azure. Viene creato codifica file multimediali tooconvert di processi da un tooanother codifica. Quando si codifica, è possibile utilizzare hello incorporato codificatore di servizi multimediali (Media Encoder Standard). È inoltre possibile usare un codificatore fornito da un partner di Servizi multimediali. I codificatori di terze parti sono disponibili tramite hello Azure Marketplace. È possibile specificare i dettagli di hello attività di codifica usando stringhe di set di impostazioni definite per il codificatore oppure utilizzando i file di configurazione predefinito. tipi di hello toosee dei set di impostazioni che sono disponibili, vedere [set di impostazioni di attività per supporti codificatore Standard](http://msdn.microsoft.com/library/mt269960).

Ogni processo può avere uno o più attività in base al tipo di hello di elaborazione che si desidera tooaccomplish. Tramite hello API REST, è possibile creare processi e le attività correlate in uno dei due modi:

* Le attività possono essere definite inline mediante proprietà di navigazione attività hello in entità Job.
* Usare l'elaborazione batch OData.

È consigliabile codificare sempre i file di origine in un set MP4 a velocità in bit adattiva e quindi convertire il formato desiderato hello set toohello utilizzando [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md).

Se l'asset di output è crittografato di archiviazione, è necessario configurare i criteri di distribuzione di asset hello. Per altre informazioni, vedere [Configurazione dei criteri di distribuzione degli asset](media-services-rest-configure-asset-delivery-policy.md).

## <a name="considerations"></a>Considerazioni

Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP. Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).

Prima di avviare che fanno riferimento a processori di contenuti multimediali, verificare che si sono hello corretto processore relativo ID. Per altre informazioni, vedere [Ottenere processori di contenuti multimediali](media-services-rest-get-media-processor.md).

## <a name="connect-toomedia-services"></a>Connessione dei servizi tooMedia

Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali. È necessario effettuare le chiamate successive toohello nuovo URI.

## <a name="create-a-job-with-a-single-encoding-task"></a>Creare un processo con una singola attività di codifica
> [!NOTE]
> Quando si lavora con hello API REST di servizi multimediali, hello seguenti considerazioni:
>
> Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP. Per altre informazioni, vedere [Configurazione dello sviluppo dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).
>
> Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali. È necessario effettuare le chiamate successive toohello nuovo URI. Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).
>
> Quando si utilizza JSON e specificando hello toouse **Metadata** (parola chiave) nella richiesta di hello (ad esempio, tooreferences un oggetto collegato), è necessario impostare hello **Accept** intestazione troppo[formato JSON dettagliato ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accettare: application/json; odata = verbose.
>
>

Hello di esempio seguente vengono visualizzati è come toocreate e post un processo con una sola attività tooencode un video a una risoluzione specifico e di qualità. Quando si esegue la codifica con Media Encoder Standard, è possibile usare i set di impostazioni di attività specificati [qui](http://msdn.microsoft.com/library/mt269960).

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

### <a name="set-hello-output-assets-name"></a>Impostare il nome dell'asset di output hello
Hello di esempio seguente viene illustrato come tooset hello attributo assetName:

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>Considerazioni
* Proprietà TaskBody devono usare numero hello toodefine letterale XML di input o output asset utilizzati dall'attività hello. argomento di attività Hello contiene hello definizione dello Schema XML per hello XML.
* In definizione TaskBody hello, valore di ogni interna di <inputAsset> e <outputAsset> deve essere impostato come JobInputAsset(value) o JobOutputAsset(value).
* Un'attività può avere più asset di output. Un oggetto JobOutputAsset(x) può essere usato solo una volta come output di un'attività in un processo.
* È possibile specificare JobInputAsset o JobOutputAsset come asset di input di un'attività.
* Le attività non devono formare un ciclo.
* il parametro di valore Hello passato tooJobInputAsset o JobOutputAsset rappresenta il valore di indice hello per un asset. Asset effettivi Hello sono definiti nel hello InputMediaAssets e OutputMediaAssets le proprietà di navigazione nella definizione di entità processo hello.
* Poiché servizi multimediali si basa su OData versione 3, hello ai singoli asset nelle hello InputMediaAssets e OutputMediaAssets raccolte di proprietà di navigazione vengono fatto riferimento tramite un " Metadata: uri" coppia nome-valore.
* Proprietà InputMediaAssets è mappata tooone o altre risorse create in servizi multimediali. OutputMediaAssets vengono create dal sistema di hello. Non fanno riferimento a un asset esistente.
* È possibile denominare OutputMediaAssets utilizzando l'attributo assetName hello. Se questo attributo non è presente, il nome di hello di hello Outputmediaassets indipendentemente dal valore di testo interno hello di hello <outputAsset> elemento è con un suffisso del valore del nome di processo hello o valore di Id di processo hello (in caso di hello in hello Nome proprietà non è definita). Ad esempio, se si imposta un valore per assetName troppo "Esempio", quindi hello Name di Outputmediaassets impostata troppo "Sample." Tuttavia, se si non è stato impostato un valore per assetName ma è stato impostato il nome di processo hello troppo "NewJob", quindi hello Name di Outputmediaassets sarà "JobOutputAsset (valore) newjob".

## <a name="create-a-job-with-chained-tasks"></a>Creare un processo con attività concatenate
In molti scenari di applicazione, gli sviluppatori desiderino toocreate una serie di attività di elaborazione. In Servizi multimediali è possibile creare una serie di attività concatenate. Ogni attività esegue diversi passaggi di elaborazione e può usare processori di contenuti multimediali differenti. attività Hello concatenata possono trasferire un asset da tooanother un'attività, l'esecuzione di una sequenza lineare delle attività su asset hello. Attività hello eseguite in un processo non sono tuttavia toobe richiesto in una sequenza. Quando si crea un'attività concatenata, hello concatenate **ITask** gli oggetti vengono creati in una singola **IJob** oggetto.

> [!NOTE]
> Attualmente è previsto un limite di 30 attività per processo. Se è necessario toochain più di 30 attività, creare più di un processo attività hello toocontain.
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
tooenable concatenamenti di attività:

* Un processo deve avere almeno due attività.
* Deve esserci almeno un'attività il cui input è l'output di hello di un'altra attività nel processo di hello.

## <a name="use-odata-batch-processing"></a>Utilizzare l'elaborazione batch OData
Hello di esempio seguente viene illustrato come toouse OData batch toocreate l'elaborazione di un processo e le attività. Per informazioni sull'elaborazione batch, vedere l'articolo relativo all' [elaborazione batch OData (Open Data Protocol)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

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
Quando si elabora più asset usando un set comune di attività, utilizzare che un'attività predefinita di entità JobTemplate toospecify hello predefiniti o ordine hello tooset delle attività.

Hello di esempio seguente viene illustrato come toocreate un'entità JobTemplate con un'entità TaskTemplate che viene definito inline. Hello entità TaskTemplate Usa hello Media Encoder Standard come file di asset hello tooencode hello entità MediaProcessor. Tuttavia, può usare anche altre entità Mediaprocessor.

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
> A differenza di altre entità di servizi multimediali, è necessario definire un nuovo identificatore GUID per ogni entità TaskTemplate e posizionarlo nella proprietà hello taskTemplateId e Id nel corpo della richiesta. schema di identificazione del contenuto Hello deve seguire schema hello descritto nell'identificare le entità di Azure Media Services. Inoltre, non è possibile aggiornare le entità JobTemplate. È invece necessario crearne una nuova con le modifiche aggiornate.
>
>

Se ha esito positivo, viene restituito hello seguente risposta:

    HTTP/1.1 201 Created

    . . .


Hello seguente esempio viene illustrato come un processo che fa riferimento a un Id entità JobTemplate toocreate:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


Se ha esito positivo, viene restituito hello seguente risposta:

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato appreso come toocreate tooencode un processo un asset, vedere [come toocheck processo lo stato di avanzamento con servizi multimediali](media-services-rest-check-job-progress.md).

## <a name="see-also"></a>Vedere anche
[Ottenere processori di contenuti multimediali](media-services-rest-get-media-processor.md)
