---
title: aaaImport tooAnalytics i dati in Azure Application Insights | Documenti Microsoft
description: Importare i dati statici toojoin con dati di telemetria app oppure importare una tooquery di flusso di dati separato con Analitica.
services: application-insights
keywords: schema aperto, importazione dei dati
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>Importazione di dati in Analytics

Importare i dati tabulari in [Analitica](app-insights-analytics.md), entrambi toojoin con [Application Insights](app-insights-overview.md) telemetria dall'app, o in modo che sia possibile analizzarli come flusso separato. Analitica è un timestamp con volumi elevati flussi di query avanzate language tooanalyzing ideale di telemetria.

È possibile importare dati in Analytics usando uno schema personalizzato. Non dispone di schemi standard Application Insights toouse hello, ad esempio traccia o di richiesta.

È possibile importare i file JSON o DSV (Delimiter-Separated Values: virgola, punto e virgola o tabulazione).

Ci sono tre i casi in cui l'importazione tooAnalytics è utile:

* **Creare un join con la telemetria dell'app.** Ad esempio, è possibile importare una tabella che esegue il mapping degli URL tra i titoli di pagina leggibile toomore sito Web. In Analitica, è possibile creare un report di grafico del dashboard che mostra le pagine di più diffusi dieci hello nel sito Web. Ora consente di visualizzare hello titoli delle pagine anziché hello URL.
* **Correlare la telemetria dell'applicazione** con altre origini, ad esempio il traffico di rete, i dati del server o i file di log della rete CDN.
* **Applicare flusso dei dati distinto tooa Analitica.** Application Insights Analytics è uno strumento potente, che funziona bene con flussi di timestamp frammentati, spesso in modo più efficace di SQL. Se si dispone di tale flusso da un'altra origine, è possibile analizzarlo con Analytics.

L'invio di dati tooyour origine dati è semplice. 

1. (Una volta) Definizione di schema hello dei dati in un'origine di dati' '.
2. (Periodicamente) Caricamento dell'archiviazione dei dati tooAzure e contattarci toonotify API REST hello in attesa per l'inserimento di nuovi dati. Entro pochi minuti, dati hello sono disponibili per query in Analitica.

Hello frequenza di caricamento hello è definita dall'utente e la velocità con cui si desidera toobe i dati disponibili per le query. È più efficiente tooupload i dati in blocchi più grandi, ma non maggiore di 1GB.

> [!NOTE]
> *Hai un numero elevato di tooanalyze di origini dati?* [*È consigliabile utilizzare* logstash *tooship i dati in Application Insights.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>Prima di iniziare

Sono necessari:

1. Una risorsa di Application Insights in Microsoft Azure.

 * Se si desidera tooanalyze dati separatamente da eventuali altri dati di telemetria [creare una nuova risorsa di Application Insights](app-insights-create-new-resource.md).
 * Se si è aggiunta o il confronto dei dati con dati di telemetria da un'app è già configurata con Application Insights, è possibile utilizzare risorse hello per l'app.
 * Risorsa toothat di accesso proprietario o collaboratore.
 
2. nell'archiviazione di Azure. Caricare archiviazione tooAzure e Analitica Ottiene i dati da tale posizione. 

 * È consigliabile creare un account di archiviazione dedicato per i BLOB. Se i BLOB sono condivise con altri processi, richiede più tempo per i processi tooread i BLOB.


## <a name="define-your-schema"></a>Definire lo schema

È possibile importare dati, è necessario definire un *origine dati,* che consente di specificare schema hello dei dati.
È possibile avere fino a too50 origini di dati in una singola risorsa di Application Insights

1. Avviare Creazione guidata origine dati di hello. Usare il pulsante "Aggiungi nuova origine dati". In alternativa, fare clic sul pulsante Impostazioni nell'angolo in alto a destra e scegliere "Origini dati" nel menu a discesa.

    ![Aggiungere la nuova origine dati](./media/app-insights-analytics-import/add-new-data-source.png)

    Immettere un nome per la nuova origine dati.

2. Definire formato di file hello che verrà caricato.

    È possibile definire il formato di hello manualmente o caricare un file di esempio.

    Dati hello sono in formato CSV, hello prima riga dell'esempio hello possibile caso le intestazioni di colonna. È possibile modificare i nomi dei campi hello nel passaggio successivo hello.

    esempio Hello deve includere almeno 10 righe o record di dati.

    I nomi di colonna o di campo devono essere alfanumerici (senza spazi o punteggiatura).

    ![Caricare un file di esempio](./media/app-insights-analytics-import/sample-data-file.png)


3. Ha ottenuto schema hello revisione hello procedura guidata. Se dedotto tipi hello da un esempio, potrebbe essere tipi di hello dedotto tooadjust delle colonne di hello.

    ![Schema inferito hello revisione](./media/app-insights-analytics-import/data-source-review-schema.png)

 * Facoltativo. Caricare una definizione dello schema. Vedere hello formato riportato di seguito.

 * Selezionare un timestamp. Tutti i dati in Analytics devono avere un campo di timestamp. Il tipo deve essere `datetime`, ma non è toobe denominato 'timestamp'. Se i dati includono una colonna contenente una data e ora in formato ISO, scegliere questa opzione come colonna di tipo timestamp hello. In caso contrario, scegliere "come dati ricevuti" e il processo di importazione hello viene aggiunto un campo di timestamp.

5. Creare l'origine dati hello.

### <a name="schema-definition-file-format"></a>Formato del file di definizione dello schema

Anziché la modifica dello schema hello nell'interfaccia utente, è possibile caricare la definizione dello schema hello da un file. formato di definizione dello schema Hello è come segue: 

Formato delimitato 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

Formato JSON 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
Ogni colonna viene identificato dal tipo, nome e percorso hello. 

* Ubicazione: per formattare file delimitato è posizione hello del valore di hello mappato. Per il formato JSON, è jpath hello della chiave hello mappato.
* Nome: hello visualizzati nome della colonna hello.
* Tipo: tipo di dati hello di tale colonna.
 
Nel caso in cui è stata utilizzata una data di esempio e ha un formato di file delimitato, la definizione dello schema hello deve eseguire il mapping di tutte le colonne e aggiungere nuove colonne alla fine di hello. 

JSON consente il mapping parziale dei dati di hello, pertanto hello definizione dello schema di formato JSON non ha toomap ogni chiave è presente in dati di esempio. Anche possibile eseguire il mapping di colonne che non fanno parte di dati di esempio hello. 

## <a name="import-data"></a>Importa dati

dati tooimport, caricarlo tooAzure archiviazione, creare una chiave di accesso per tale e quindi effettuare una chiamata API REST.

![Aggiungere la nuova origine dati](./media/app-insights-analytics-import/analytics-upload-process.png)

È possibile eseguire hello seguente processo manualmente o configurare un toodo automatico di sistema, a intervalli regolari. È necessario toofollow questi passaggi per ogni blocco di dati si desidera tooimport.

1. Caricare dati hello troppo[archiviazione blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). 

 * BLOB possono essere di qualsiasi dimensione di too1GB non compressi. I BLOB di centinaia di MB sono ideali dal punto di vista delle prestazioni.
 * È possibile comprimere, con tempo di caricamento tooimprove Gzip e la latenza di hello toobe di dati disponibili per le query. Hello utilizzare `.gz` estensione del nome file.
 * A tale scopo, chiamate tooavoid dai vari servizi rallentare le prestazioni è migliore toouse un account di archiviazione separata.
 * Quando si inviano dati ad alta frequenza, ogni pochi secondi, è consigliabile toouse più di un account di archiviazione, per motivi di prestazioni.

 
2. [Creare una chiave di firma di accesso condiviso per il blob hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md). chiave di Hello deve avere un periodo di scadenza di un giorno e forniscono l'accesso in lettura.
3. Verificare un toonotify chiamata REST Application Insights in attesa di dati.

 * Endpoint: `https://dc.services.visualstudio.com/v2/track`
 * Metodo HTTP: POST
 * Payload:

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

segnaposto Hello sono:

* `Blob URI with Shared Access Key`: Questa procedura hello per la creazione di una chiave. È il blob toohello specifico.
* `Schema ID`: hello ID dello schema generato per lo schema definito. dati Hello in questo blob devono essere conformi toohello schema.
* `DateTime`: ora hello in cui hello viene inoltrata una richiesta, UTC. Vengono accettati i seguenti formati: ISO8601 (ad esempio "2016-01-01 13:45:01"); RFC822 ("mer, 14 dic 16 14:57:01 +0000"); RFC850 ("mercoledì, 14-dic-16 14:57:00 UTC"); RFC1123 ("mer, 14 dic 2016 14:57:00 +0000").
* `Instrumentation key` della risorsa di Application Insights.

dati Hello sono disponibili in Analitica dopo alcuni minuti.

## <a name="error-responses"></a>Risposte agli errori

* **400 richiesta non valida**: indica che il payload della richiesta hello è valido. Controllare:
 * Chiave di strumentazione corretta.
 * Valore dell'ora valido. Dovrebbe essere ora hello ora UTC.
 * JSON dell'evento hello conforme toohello schema.
* **403-accesso negato**: blob hello è stato inviato non è accessibile. Verificare che tale chiave di accesso condiviso hello sia valido e non sia scaduto.
* **404 - Pagina non trovata**:
 * blob Hello non esiste.
 * sourceId Hello è errato.

Informazioni più dettagliate sono disponibili nel messaggio di errore di risposta hello.


## <a name="sample-code"></a>Codice di esempio

Questo codice Usa hello [newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) pacchetto NuGet.

### <a name="classes"></a>Classi

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>Inserire dati

Usare questo codice per ogni BLOB. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>Passaggi successivi

* [Panoramica del linguaggio di query Log Analitica hello](app-insights-analytics-tour.md)
* [Utilizzare *Logstash* toosend dati tooApplication Insights](https://github.com/Microsoft/logstash-output-application-insights)
