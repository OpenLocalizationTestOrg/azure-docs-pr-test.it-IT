---
title: API dell'agente di raccolta dati di HTTP Analitica aaaLog | Documenti Microsoft
description: "È possibile utilizzare hello API dell'agente di raccolta dati di Log Analitica HTTP tooadd JSON POST toohello Analitica Log repository dei dati da qualsiasi client che possono chiamare l'API REST hello. In questo articolo viene descritto come toouse hello API e vengono riportati alcuni esempi di come dati toopublish utilizzando diversi linguaggi di programmazione."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>Inviare dati tooLog Analitica con hello API dell'agente di raccolta dati di HTTP
Questo articolo illustra come toouse hello API dell'agente di raccolta dati di HTTP toosend dati tooLog Analitica da un client di API REST.  Descrive come tooformat dati raccolti dallo script o applicazione, includerlo in una richiesta e tale richiesta autorizzata dal Log Analitica.  Vengono indicati esempi per PowerShell, C# e Python.

## <a name="concepts"></a>Concetti
È possibile utilizzare l'API dell'agente di raccolta dati di HTTP toosend hello dati tooLog Analitica da qualsiasi client che è possibile chiamare un'API REST.  Potrebbe trattarsi di un runbook in automazione di Azure che raccoglie gestione dati da Azure o un altro cloud o potrebbero essere un sistema di gestione alternativo che usa tooconsolidate Log Analitica e analizzare i dati.

Tutti i dati nel repository di hello Analitica Log vengono archiviati come un record con un tipo di record specifico.  Formattare il toohello toosend dati API dell'agente di raccolta dati di HTTP come più record in JSON.  Quando si inviano dati hello, viene creato un singolo record nel repository di hello per ciascun record nel payload della richiesta hello.


![Panoramica dell'agente di raccolta dati HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Creare una richiesta
API agente di raccolta dati di toouse hello HTTP, si crea una richiesta POST che include toosend dati hello in JavaScript Object Notation (JSON).  Hello tre tabelle elenco hello che gli attributi necessari per ogni richiesta. Viene descritto ogni attributo in modo più dettagliato più avanti in articolo hello.

### <a name="request-uri"></a>URI della richiesta
| Attributo | Proprietà |
|:--- |:--- |
| Metodo |POST |
| URI |https://\<IdCliente\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| Tipo di contenuto |application/json |

### <a name="request-uri-parameters"></a>Parametri URI della richiesta
| Parametro | Description |
|:--- |:--- |
| CustomerID |Hello identificatore univoco dell'area di lavoro di hello Microsoft Operations Management Suite. |
| Risorsa |nome della risorsa API Hello: / api/logs. |
| Versione dell'API |versione di Hello del toouse hello API con questa richiesta. La versione attuale è 2016-04-01. |

### <a name="request-headers"></a>Intestazioni della richiesta
| Intestazione | Descrizione |
|:--- |:--- |
| Authorization |firma di autorizzazione Hello. Più avanti in articolo hello, è possibile leggere le procedure intestazione toocreate un HMAC-SHA256. |
| Log-Type |Specificare il tipo di record hello di dati hello viene inviati. Tipo di log hello attualmente supporta solo caratteri alfabetici. Non supporta valori numerici o caratteri speciali. |
| x-ms-date |Data di Hello in cui è stata elaborata la richiesta di hello, nel formato RFC 1123. |
| time-generated-field |nome Hello di un campo nei dati hello che contiene il timestamp di hello hello elemento dei dati. Se si specifica un campo, il relativo contenuto verrà usato per **TimeGenerated**. Se questo campo non è specificato, hello predefinito per **TimeGenerated** è ora hello che hello messaggio verrà acquisito. il contenuto di Hello del campo messaggio hello deve seguire il formato ISO 8601 hello AAAA-MM-ddTHH. |

## <a name="authorization"></a>Authorization
Qualsiasi toohello richiesta API dell'agente di raccolta dati di Log Analitica HTTP deve includere un'intestazione di autorizzazione. tooauthenticate una richiesta, è necessario firmare la richiesta di hello con hello primaria o chiave secondaria di hello per area di lavoro hello che effettua la richiesta hello. Quindi, passare la firma come parte della richiesta di hello.   

Di seguito è riportato il formato di hello per intestazione authorization hello:

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*Idareadilavoro* è hello identificatore univoco dell'area di lavoro di hello Operations Management Suite. *Firma* è un [codice HMAC (Hash-based Message Authentication Code)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) che viene costruito dalla richiesta hello e quindi calcolato utilizzando hello [algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Viene quindi codificato con la codifica Base64.

Utilizzare questo hello tooencode formato **SharedKey** stringa di firma:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

Di seguito è riportato un esempio di stringa della firma:

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

Quando si dispone di stringa di firma hello, codificarli utilizzando hello l'algoritmo HMAC-SHA256 nella stringa con codifica UTF-8 hello e quindi codificare il risultato di hello come base 64. Usare il formato seguente:

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

esempi di Hello nelle sezioni successive di hello è toohelp codice di esempio si crea un'intestazione di autorizzazione.

## <a name="request-body"></a>Corpo della richiesta
corpo del messaggio hello del Hello deve essere in JSON. Deve includere uno o più record con coppie nome / valore di proprietà hello nel formato seguente:

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

È possibile raggruppare più record in una singola richiesta usando hello seguente formato. Tutti i record di hello devono essere hello stesso tipo di record.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>Proprietà e tipo di record
Si definisce un tipo di record personalizzato quando si inviano dati tramite l'API dell'agente di raccolta dati di Log Analitica HTTP hello. Attualmente, non è possibile scrivere dati tooexisting tipi di record che sono stati creati da altri tipi di dati e soluzioni. Log Analitica legge i dati in ingresso hello e quindi crea le proprietà che corrispondono a tipi di dati di hello di valori hello immesso.

Ogni richiesta toohello Log Analitica API devono includere un **-tipo di Log** intestazione con nome hello per tipo di record di hello. suffisso Hello **_CL** toohello automaticamente aggiunte nome immesso toodistinguish da altri log tipi come un log personalizzato. Ad esempio, se si immette il nome di hello **MyNewRecordType**, Log Analitica crea un record con il tipo di hello **MyNewRecordType_CL**. È così possibile evitare conflitti tra i nomi dei tipi creati dall'utente e i nomi forniti nelle soluzioni Microsoft correnti o future.

tipo di dati di una proprietà tooidentify, Log Analitica aggiunge un nome di proprietà toohello suffisso. Se una proprietà contiene un valore null, la proprietà hello non è incluso in tale record. Questa tabella elenca il tipo di dati proprietà hello e il suffisso corrispondente:

| Tipo di dati proprietà | Suffisso |
|:--- |:--- |
| String |_s |
| Boolean |_b |
| Double |_d |
| Data/ora |_t |
| GUID |_g |

tipo di dati Hello Analitica di Log viene utilizzato per ogni proprietà dipende se il tipo di record hello per il nuovo record di hello esiste già.

* Se il tipo di record hello non esiste, Log Analitica crea uno nuovo. Log Analitica utilizza hello JSON inferenza toodetermine hello dati di tipo per ogni proprietà per il nuovo record di hello.
* Se il tipo di record hello esiste, Analitica Log tenta toocreate un nuovo record in base alle proprietà esistenti. Se hello tipo di dati per una proprietà nel nuovo record di hello non corrispondono e non può essere convertito toohello tipi esistenti o se hello record include una proprietà che non esiste, Log Analitica crea una nuova proprietà con suffisso rilevanti hello.

Questa voce di invio creerà ad esempio un record con tre proprietà, **number_d**, **boolean_b** e **string_s**:

![Esempio di record 1](media/log-analytics-data-collector-api/record-01.png)

Se questa voce successiva, è quindi inviata con tutti i valori formattati come stringhe, le proprietà di hello non modificherebbe. Questi valori possono essere tooexisting convertire i tipi di dati:

![Esempio di record 2](media/log-analytics-data-collector-api/record-02.png)

Ma, se sono state quindi questo invio successivo, Log Analitica creerebbe hello nuove proprietà **boolean_d** e **string_d**. Questi valori non possono essere convertiti:

![Esempio di record 3](media/log-analytics-data-collector-api/record-03.png)

Se è stata inviata quindi hello entrata prima della creazione di tipo di record hello, Log Analitica creerà un record con tre proprietà, **num_successi**, **boolean_s**, e **string_s**. In questa voce, ognuno dei valori iniziali hello è formattato come una stringa:

![Esempio di record 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Limiti dei dati
Esistono alcune limitazioni di racchiudere i dati di hello registrati toohello raccolta dei dati di Log Analitica API.

* Massimo di 30 MB per post tooLog l'API dell'agente di raccolta dati Analitica. Questo limite riguarda le dimensioni di ogni messaggio. Se dati hello da un messaggio che supera i 30 MB, è necessario suddividere hello dati backup toosmaller dimensioni blocchi e li inviano contemporaneamente.
* Limite di 32 KB per i valori dei campi. Se il valore di campo hello è maggiore di 32 KB, dati hello verranno troncati.
* Il numero massimo di campi consigliato per un determinato tipo è 50. Si tratta di un limite pratico dal punto di vista dell'usabilità e dell'esperienza di ricerca.  

## <a name="return-codes"></a>Codici restituiti
codice di stato HTTP 200 Hello richiesta hello che è stata ricevuta per l'elaborazione. Ciò indica che operazione hello è stata completata.

Questa tabella sono elencati i set di codici di stato che potrebbe restituire servizio hello completo hello:

| Codice | Stato | Codice di errore | Descrizione |
|:--- |:--- |:--- |:--- |
| 200 |OK | |richiesta di Hello è stato accettato. |
| 400 |Richiesta non valida |InactiveCustomer |area di lavoro Hello è stato chiuso. |
| 400 |Richiesta non valida |InvalidApiVersion |versione di Hello API specificata non è stato riconosciuto dal servizio hello. |
| 400 |Richiesta non valida |InvalidCustomerId |ID dell'area di lavoro Hello specificato non è valido. |
| 400 |Richiesta non valida |InvalidDataFormat |È stata inviato JSON non valido. corpo della risposta Hello potrebbe contenere ulteriori informazioni su come tooresolve hello errore. |
| 400 |Richiesta non valida |InvalidLogType |tipo di log Hello specificato contenuti caratteri speciali o valori numerici. |
| 400 |Richiesta non valida |MissingApiVersion |versione dell'API Hello non è stato specificato. |
| 400 |Richiesta non valida |MissingContentType |non è stato specificato il tipo di contenuto Hello. |
| 400 |Richiesta non valida |MissingLogType |Hello richiesto è stato specificato alcun tipo di valore di log. |
| 400 |Richiesta non valida |UnsupportedContentType |tipo di contenuto Hello non è stato impostato troppo**application/json**. |
| 403 |Accesso negato |InvalidAuthorization |Errore del servizio di Hello richiesta hello tooauthenticate. Verificare la chiave di connessione e l'ID dell'area di lavoro hello siano validi. |
| 404 |Non trovato | | URL di hello fornito non è corretto oppure hello richiesta è troppo grande. |
| 429 |Troppe richieste | | è presente un'elevata quantità di dati dell'account di servizio di Hello. Riprovare più tardi richiesta hello. |
| 500 |Internal Server Error |UnspecifiedError |servizio Hello ha rilevato un errore interno. Ritentare la richiesta hello. |
| 503 |Servizio non disponibile |ServiceUnavailable |servizio Hello è attualmente disponibile tooreceive richieste. Si prega di ripetere la richiesta. |

## <a name="query-data"></a>Eseguire query sui dati
dati tooquery inviati dai hello API dell'agente di raccolta dati HTTP di Analitica Log, cercare i record con **tipo** ovvero uguale toohello **LogType** valore specificato, seguito da **_CL**. Usando ad esempio **MyCustomLog** verranno restituiti tutti i record con **Type=MyCustomLog_CL**.

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>Richieste di esempio
Nelle sezioni successive di hello, sono disponibili esempi di dati di toosubmit toohello API dell'agente di raccolta dati di Log Analitica HTTP utilizzando diversi linguaggi di programmazione.

Per ogni esempio, eseguire questi passaggi variabili hello tooset per intestazione authorization hello:

1. Nel portale di Operations Management Suite hello selezionare hello **impostazioni** riquadro e quindi selezionare hello **Connected Sources** scheda.
2. toohello destra **ID area di lavoro**, selezionare l'icona di copia hello e quindi incollare hello ID come valore di hello di hello **ID cliente** variabile.
3. toohello destra **chiave primaria**, selezionare l'icona di copia hello e quindi incollare hello ID come valore di hello di hello **chiave condivisa** variabile.

In alternativa, è possibile modificare le variabili di hello per il tipo di log hello e i dati JSON.

### <a name="powershell-sample"></a>Esempio PowerShell
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>Esempio C#
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Esempio Python
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>Passaggi successivi
- Hello utilizzare [API di ricerca Log](log-analytics-log-search-api.md) tooretrieve dati dall'archivio di Log Analitica hello.
