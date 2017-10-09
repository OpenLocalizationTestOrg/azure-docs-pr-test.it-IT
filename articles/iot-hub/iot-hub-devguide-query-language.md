---
title: hello aaaUnderstand linguaggio di query IoT Hub di Azure | Documenti Microsoft
description: Guida per sviluppatori - descrizione del linguaggio di query simile a SQL IoT Hub hello utilizzata tooretrieve informazioni gemelli di dispositivo e l'hub IoT dei processi.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>Riferimento: linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing di messaggi

IoT Hub è un potente linguaggio simile a SQL tooretrieve relative [gemelli dispositivo] [ lnk-twins] e [processi][lnk-jobs]e [il routing dei messaggi][lnk-devguide-messaging-routes]. Questo articolo contiene:

* Un'introduzione toohello principali funzionalità del linguaggio di query IoT Hub, hello e
* Hello descrizione dettagliata del linguaggio hello.

## <a name="get-started-with-device-twin-queries"></a>Introduzione alle query dei dispositivi gemelli
I [dispositivi gemelli][lnk-twins] possono contenere oggetti JSON arbitrari come tag e proprietà. IoT Hub consente tooquery gemelli di dispositivo come un singolo documento JSON contenente tutte le informazioni di disponibilità di una copia di dispositivo.
Supponga, ad esempio, che il gemelli di dispositivo IoT hub hello seguente struttura:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

IoT Hub espone gemelli di hello dispositivo come una raccolta di documenti denominata **dispositivi**.
Pertanto hello seguente query recupera set intero di hello di gemelli di dispositivo:

```sql
SELECT * FROM devices
```

> [!NOTE]
> Gli [SDK dell'hub IoT][lnk-hub-sdks] supportano il paging di risultati di grandi dimensioni.

IoT Hub consente gemelli dispositivo tooretrieve filtri con condizioni arbitrarie. Ad esempio,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

Recupera hello gemelli di dispositivi con hello **location.region** tag impostato troppo**US**.
Sono supportati anche gli operatori booleani e confronti aritmetici, ad esempio

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

Recupera tutti gemelli dispositivo si trova in hello ci configurato toosend telemetria minore spesso ogni minuto. Per maggiore praticità, è anche possibile toouse costanti di matrice con hello **IN** e **/NIN** operatori (non in). Ad esempio,

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

recupera tutti i dispositivi gemelli che hanno segnalato una connettività WiFi o cablata. Si è spesso necessario tooidentify tutti gemelli di dispositivi che contengono una proprietà specifica. IoT Hub supporta la funzione hello `is_defined()` a questo scopo. Ad esempio,

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

recuperare tutti i gemelli di dispositivo che definiscono hello `connectivity` segnalati proprietà. Fare riferimento toohello [clausola WHERE] [ lnk-query-where] sezione per informazioni di riferimento complete hello di hello funzionalità di filtro.

Sono supportati anche il raggruppamento e le aggregazioni. Ad esempio,

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Restituisce il numero di hello di dispositivi hello in ogni stato di configurazione di telemetria.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

Hello esempio precedente viene illustrata una situazione in tre dispositivi segnalati configurazione ha esito positivo, due sono comunque l'applicazione di configurazione di hello e uno ha segnalato un errore.

### <a name="c-example"></a>Esempio in C#
la funzionalità di query Hello è esposto dal hello [servizio c# SDK] [ lnk-hub-sdks] in hello **RegistryManager** classe.
Ecco un esempio di una query semplice:

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

Si noti come hello **query** viene creata un'istanza di oggetto con una dimensione di pagina (backup too1000) e quindi più pagine possono essere recuperate tramite chiamata hello **GetNextAsTwinAsync** metodi più volte.
Si noti che l'oggetto query hello espone più **Avanti\***, a seconda opzione deserializzazione hello necessarie hello query, ad esempio gli oggetti processo o un doppio dispositivo, o normale toobe JSON quando si utilizzano le proiezioni.

### <a name="nodejs-example"></a>Esempio di Node. js
la funzionalità di query Hello è esposto dal hello [servizio IoT di Azure SDK per Node.js] [ lnk-hub-sdks] in hello **Registro di sistema** oggetto.
Ecco un esempio di una query semplice:

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

Si noti come hello **query** viene creata un'istanza di oggetto con una dimensione di pagina (backup too1000) e quindi più pagine possono essere recuperate tramite chiamata hello **nextAsTwin** metodi più volte.
Si noti che l'oggetto query hello espone più **Avanti\***, a seconda opzione deserializzazione hello necessarie hello query, ad esempio gli oggetti processo o un doppio dispositivo, o normale toobe JSON quando si utilizzano le proiezioni.

### <a name="limitations"></a>Limitazioni
> [!IMPORTANT]
> Risultati della query possono contenere alcuni minuti di ritardo con i valori più recenti di toohello riguardo gemelli di dispositivo. Se la query gemelli di singoli dispositivi in base all'id, è sempre preferibile toouse hello recuperare dispositivo doppi API, che contiene i valori più recenti di hello sempre e ha limitazioni superiore.

I confronti sono attualmente supportati solo tra tipi primitivi (non oggetti), ad esempio `... WHERE properties.desired.config = properties.reported.config` è supportato solo se tali proprietà hanno valori primitivi.

## <a name="get-started-with-jobs-queries"></a>Introduzione alle query dei processi
[I processi] [ lnk-jobs] forniscono un modo tooexecute operazioni su set di dispositivi. Ogni coppia di dispositivo contiene informazioni hello dei processi di hello di cui fa parte di una raccolta denominata di **processi**.
La struttura logica è la seguente.

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

Questa raccolta è attualmente disponibile per query come **devices.jobs** nel linguaggio di query IoT Hub hello.

> [!IMPORTANT]
> Attualmente, proprietà processi hello non viene mai restituito quando si eseguono query gemelli di dispositivo (ovvero, query che contiene 'dai dispositivi'). È possibile accedervi direttamente solo con le query che usano `FROM devices.jobs`.
>
>

Ad esempio, tooget tutti i processi (ultime e pianificati) che interessano un singolo dispositivo, è possibile utilizzare hello seguente query:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Si noti come questa query fornisce lo stato specifico del dispositivo hello (ed eventualmente risposta dirette del metodo hello) di ogni processo restituito.
È inoltre possibile toofilter con condizioni Boolean arbitrarie in tutte le proprietà oggetto hello **devices.jobs** insieme.
Ad esempio, hello query riportata di seguito:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

recupera tutti i processi di aggiornamento del dispositivo gemello completati per il dispositivo **myDeviceId** e creati dopo settembre 2016.

È anche risultati di ogni dispositivo hello tooretrieve possibili di un singolo processo.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>Limitazioni
Attualmente le query su **devices.jobs** non supportano:

* Proiezioni, quindi è possibile solo `SELECT *`.
* Condizioni che fanno riferimento a un doppio dispositivo toohello nelle proprietà toojob di addizione (vedere la precedente sezione hello).
* Esecuzione di aggregazioni, ad esempio count, avg, group by.

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>Introduzione a espressioni di query per route di messaggi da dispositivo a cloud

Utilizzando [route da dispositivo a cloud][lnk-devguide-messaging-routes], è possibile configurare l'IoT Hub toodispatch dispositivo a cloud messaggi endpoint toodifferent basate su espressioni valutate dai singoli messaggi.

route Hello [condizione] [ lnk-query-expressions] utilizza hello stesso linguaggio di query di IoT Hub come condizioni nelle query doppi e processo. Condizioni di route vengono valutate nel corpo e intestazioni del messaggio hello. L'espressione di query routing potrebbe riguardare solo le intestazioni dei messaggi, solo corpo del messaggio hello, o entrambe le intestazioni dei messaggi e corpo del messaggio. IoT Hub presuppone uno schema specifico per le intestazioni di hello e corpo del messaggio nei messaggi di ordine tooroute e hello le sezioni seguenti descrivono ciò che è richiesto per la route tooproperly IoT Hub:

### <a name="routing-on-message-headers"></a>Routing delle intestazioni dei messaggi

IoT Hub presuppone hello rappresentazione JSON di intestazioni di messaggio per il routing dei messaggi seguenti:

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

Proprietà di sistema di messaggi sono precedute da hello `'$'` simbolo.
Alle proprietà utente si accede sempre con il relativo nome. Se il nome di una proprietà utente avviene toocoincide con una proprietà di sistema (ad esempio `$to`), proprietà utente hello verrà recuperato con hello `$to` espressione.
È sempre possibile accedere a proprietà di sistema hello utilizzando le parentesi `{}`: ad esempio, è possibile utilizzare l'espressione hello `{$to}` tooaccess hello proprietà di sistema `to`. I nomi di proprietà tra parentesi quadre recuperano sempre la proprietà di sistema corrispondente hello.

Si ricordi che nei nomi delle proprietà viene fatta distinzione tra maiuscole e minuscole.

> [!NOTE]
> Tutte le proprietà dei messaggi sono stringhe. Proprietà di sistema, come descritto in hello [Guida per sviluppatori][lnk-devguide-messaging-format], non sono attualmente disponibili toouse nelle query.
>

Ad esempio, se si utilizza un `messageType` proprietà, è possibile tooroute endpoint di tooone tutti i dati di telemetria ed endpoint di tooanother tutti gli avvisi. È possibile scrivere hello telemetria di hello tooroute espressione seguente:

```sql
messageType = 'telemetry'
```

E hello seguendo i messaggi di avviso hello tooroute espressione:

```sql
messageType = 'alert'
```

Sono supportate anche le espressioni e le funzione booleane. Questa funzionalità consente toodistinguish tra il livello di gravità, ad esempio:

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

Fare riferimento toohello [espressione e le condizioni] [ lnk-query-expressions] sezione per l'elenco completo di hello di funzioni e operatori supportati.

### <a name="routing-on-message-bodies"></a>Routing del corpo dei messaggi

IoT Hub è possibile instradare solo in base a corpo del messaggio contenuto se il corpo del messaggio hello viene correttamente formato JSON con codificata UTF-8, UTF-16 o UTF-32. È necessario impostare tipo di contenuto del messaggio hello hello troppo`application/json` e hello tooone codifica del contenuto di hello supportate codifiche UTF in tooallow intestazioni di messaggio hello messaggio hello di IoT Hub tooroute basato sul contenuto del corpo hello. Se una delle intestazioni di hello viene omesso, l'IoT Hub non tenterà tooevaluate qualsiasi espressione di query che include il corpo di hello rispetto al messaggio hello. Se il messaggio non è un messaggio JSON, o se il messaggio hello non specifica il tipo di contenuto hello e la codifica del contenuto, è comunque possibile usare il messaggio hello tooroute in base alle intestazioni di messaggio hello di routing dei messaggi.

È possibile utilizzare `$body` nel messaggio hello di hello query espressione tooroute. È possibile utilizzare un riferimento semplice corpo, riferimento a una matrice corpo o più riferimenti corpo nell'espressione di query hello. L'espressione di query può anche combinare un riferimento al corpo con un riferimento all'intestazione del messaggio. Ad esempio, di seguito hello sono tutte le espressioni di query valida:

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>Nozioni di base di una query dell'hub IoT
Ogni query dell'hub IoT è costituita da una clausola SELECT e da una clausola FROM e dalle clausole facoltative WHERE e GROUP BY. Ogni query viene eseguita su una raccolta di documenti JSON, ad esempio dispositivi gemelli. clausola FROM Hello indica hello documento raccolta toobe iterato su (**dispositivi** o **devices.jobs**). Quindi, hello filtro hello dove clausola viene applicata. Con le aggregazioni, vengono raggruppati i risultati di hello di questo passaggio come hello specificato nella clausola GROUP BY e, per ogni gruppo, viene generata una riga come specificato nella clausola SELECT hello.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>Clausola FROM
Hello **da < from_specification >** clausola può assumere solo due valori: **dai dispositivi**, gemelli dispositivo tooquery, o **da devices.jobs**, processo tooquery per dispositivo informazioni dettagliate.

## <a name="where-clause"></a>Clausola WHERE
Hello **dove < filter_condition >** clausola è facoltativa. Specifica una o più condizioni che documenti JSON hello nella raccolta di hello FROM devono soddisfare toobe incluso come parte del risultato hello. Deve restituire un documento JSON hello specificato condizioni troppo "true" toobe inclusa nel risultato hello.

Hello consentito condizioni sono descritte nella sezione [espressioni e condizioni][lnk-query-expressions].

## <a name="select-clause"></a>Clausola SELECT
clausola SELECT Hello (**selezionare < select_list >**) è obbligatorio e specifica quali valori vengono recuperati dalla query hello. Specifica hello JSON valori toobe utilizzato toogenerate di nuovi oggetti JSON.
Per ogni elemento di hello subset filtrato (e facoltativamente raggruppati) della raccolta da hello, la fase di proiezione hello genera un nuovo oggetto JSON, costruito con i valori hello specificati nella clausola SELECT hello.

Di seguito è grammatica hello della clausola SELECT hello:

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

dove **attribute_name** fa riferimento la proprietà tooany del documento JSON hello nella raccolta di hello FROM. Alcuni esempi di clausole SELECT sono reperibile in hello [Guida introduttiva a query doppi dispositivo] [ lnk-query-getstarted] sezione.

Attualmente le clausole di selezione diverse da **SELECT \*** sono supportate solo nelle query aggregate sui dispositivi gemelli.

## <a name="group-by-clause"></a>Clausola GROUP BY
Hello **GROUP BY < group_specification >** clausola è un passaggio facoltativo che può essere eseguito dopo il filtro hello specificato in hello clausola WHERE e prima di proiezione hello specificata in hello Seleziona. Raggruppa documenti in base al valore di hello di un attributo. Questi gruppi vengono utilizzati toogenerate aggregati i valori come specificato nella clausola SELECT hello.

Ecco un esempio di query che usa GROUP BY:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Hello formali sintassi GROUP BY è:

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

dove **attribute_name** fa riferimento la proprietà tooany del documento JSON hello nella raccolta di hello FROM.

Clausola GROUP BY hello è attualmente supportata solo quando si eseguono query gemelli di dispositivo.

## <a name="expressions-and-conditions"></a>Espressioni e condizioni
In generale, un'*espressione*:

* Restituisce l'istanza di tooan di un tipo JSON (ad esempio, valore booleano, numero, stringa, matrice o oggetto), e
* Viene definito mediante la modifica di dati provenienti dal documento JSON di dispositivo hello e costanti utilizzando le funzioni e operatori incorporati.

*Condizioni* sono espressioni che restituiscono tooa valore booleano. Una costante diversa da un valore booleano **true** viene considerato come **false** (inclusi **null**, **definito**, qualsiasi istanza di oggetto o una matrice, qualsiasi stringa e chiaramente hello booleano **false**).

sintassi di Hello per le espressioni è:

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

dove:

| Simbolo | Definizione |
| --- | --- |
| attribute_name | Qualsiasi proprietà del documento JSON hello in hello **FROM** insieme. |
| binary_operator | Qualsiasi operatore binario elencati in hello [operatori](#operators) sezione. |
| function_name| Qualsiasi funzione elencata in hello [funzioni](#functions) sezione. |
| decimal_literal |Float espresso in una notazione decimale. |
| hexadecimal_literal |Un numero espresso dalla stringa hello "0x" seguito da una stringa di cifre esadecimali. |
| string_literal |I valori letterali stringa sono stringhe Unicode rappresentate da una sequenza di zero o più caratteri Unicode o sequenze di escape. I valori letterali stringa sono racchiusi tra virgolette singole (apostrofo: ') o virgolette doppie (virgolette inglesi: "). Caratteri di escape consentiti: `\'`, `\"`, `\\`, `\uXXXX` per i caratteri Unicode definiti da 4 cifre esadecimali. |

### <a name="operators"></a>Operatori
Hello dopo gli operatori è supportato:

| Famiglia | Operatori |
| --- | --- |
| Aritmetico |+,-,*,/,% |
| Logico |AND, OR, NOT |
| Confronto |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>Funzioni
Quando si eseguono query gemelli e processi hello è supportato solo funzione è:

| Funzione | Descrizione |
| -------- | ----------- |
| IS_DEFINED(proprietà) | Restituisce un valore booleano che indica se è stato assegnato un valore di proprietà hello (inclusi `null`). |

In condizioni di route, hello funzioni matematiche seguenti è supportato:

| Funzione | Descrizione |
| -------- | ----------- |
| ABS(x) | Restituisce hello assoluto (positivo) il valore di hello specificato espressione numerica. |
| EXP(x) | Hello restituisce il valore esponenziale di hello specificato espressione numerica (e ^ x). |
| POWER(x,y) | Valore di hello specificato di hello restituisce espressione toohello potenza specificata (x ^ y).|
| SQUARE(x) | Hello restituisce quadrato di hello specificato valore numerico. |
| CEILING(x) | Restituisce hello più piccolo valore integer maggiore di o uguale a, hello espressione numerica specificata. |
| FLOOR(x) | Restituisce l'intero più grande hello minore o uguale toohello specificato espressione numerica. |
| SIGN(x) | Restituisce hello positivo (+ 1), zero (0) o negativo (-1) segno di hello specificato espressione numerica.|
| SQRT(x) | Hello restituisce quadrato di hello specificato valore numerico. |

In condizioni di route, hello dopo il tipo di controllo e le funzioni cast è supportato:

| Funzione | Descrizione |
| -------- | ----------- |
| AS_NUMBER | Converte hello stringa di input tooa numero. `noop` se l'input è un numero, `Undefined` se la stringa non rappresenta un numero.|
| IS_ARRAY | Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è una matrice. |
| IS_BOOL | Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un valore booleano. |
| IS_DEFINED | Restituisce un valore booleano che indica se la proprietà hello è stata assegnata un valore. |
| IS_NULL | Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è null. |
| IS_NUMBER | Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un numero. |
| IS_OBJECT | Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un oggetto JSON. |
| IS_PRIMITIVE | Restituisce un valore booleano che indica se il tipo di hello di hello specificato espressione è una primitiva (stringa, booleano, numerico o `null`). |
| IS_STRING | Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è una stringa. |

In condizioni di route, hello funzioni stringa seguenti è supportato:

| Funzione | Descrizione |
| -------- | ----------- |
| CONCAT(x, …) | Restituisce una stringa che rappresenta il risultato di hello del concatenamento di due o più valori di stringa. |
| LENGTH(x) | Restituisce il numero di caratteri di hello hello specificato espressione stringa.|
| LOWER(x) | Restituisce un'espressione stringa dopo aver convertito i caratteri maiuscoli in caratteri toolowercase di dati. |
| UPPER(x) | Restituisce un'espressione stringa dopo la conversione toouppercase di dati carattere minuscolo. |
| SUBSTRING (stringa, avvio [, lunghezza]) | Restituisce parte di un'espressione stringa a partire da hello posizione in base zero del carattere specificata e continua toohello specificato, lunghezza o alla fine di toohello della stringa hello. |
| INDEX_OF(stringa, frammento) | Restituisce hello a partire dalla posizione della prima occorrenza di hello della seconda espressione stringa hello all'hello prima espressione stringa specificata oppure -1 se la stringa hello non viene trovata.|
| STARTS_WITH(x, y) | Restituisce un valore booleano che indica se prima espressione di stringa hello inizia con hello secondo. |
| ENDS_WITH(x, y) | Restituisce un valore booleano che indica se prima espressione di stringa hello termina con hello secondo. |
| CONTAINS(x,y) | Restituisce un valore booleano che indica se prima espressione di stringa hello contiene hello secondo. |

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come viene eseguita una query tooexecute nelle App usando [Azure IoT SDK][lnk-hub-sdks].

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
