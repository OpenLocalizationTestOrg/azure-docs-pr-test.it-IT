---
title: API REST di ricerca nei log Analitica aaaLog | Documenti Microsoft
description: Questa guida fornisce un'esercitazione di base che descrive come usare hello Analitica Registro ricerca API REST hello Operations Management Suite (OMS) e vengono forniti esempi che illustrano come comandi hello toouse.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>API REST di Log Analytics per la ricerca nei log
Questa guida fornisce un'esercitazione di base, inclusi gli esempi, utilizzo di API REST di ricerca di Log Analitica hello. Log Analitica fa parte di hello Operations Management Suite (OMS).

> [!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi è necessario continuare linguaggio di query legacy hello toouse con API di ricerca log hello come descritto in questo articolo.  Verrà rilasciata una nuova API per le aree di lavoro aggiornati e documentazione hello verrà aggiornata in quel momento. 

> [!NOTE]
> Log Analitica era precedentemente denominato Operational Insights, perché è il nome di hello utilizzato nel provider di risorse hello.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Panoramica dell'API REST di ricerca Log hello
API REST di ricerca di Log Analitica Hello è RESTful e accessibile tramite hello API di gestione risorse di Azure. In questo articolo vengono forniti esempi di accesso tramite API di hello [ARMClient](https://github.com/projectkudu/ARMClient), uno strumento da riga di comando open source che semplifica la chiamata hello API di gestione risorse di Azure. utilizzo di Hello di ARMClient è una delle numerose opzioni tooaccess hello API di ricerca Log Analitica. Un'altra opzione consiste modulo di Azure PowerShell hello toouse per OperationalInsights, che include i cmdlet per l'accesso a ricerca. Con questi strumenti, è possibile utilizzare le aree di lavoro di hello API di gestione risorse di Azure toomake chiamate tooOMS ed eseguire i comandi di ricerca al loro interno. Hello API restituisce i risultati della ricerca in formato JSON, che consente i risultati della ricerca toouse hello in molti modi diversi a livello di codice.

Hello Azure Resource Manager può essere utilizzato tramite un [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) hello e [API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx). toolearn, esaminare le pagine web hello collegato.

> [!NOTE]
> Se si utilizza un comando di aggregazione, ad esempio `|measure count()` o `distinct`, toosearch ogni chiamata può restituire fino a 500.000 record. Le ricerche che non includono un comando di aggregazione restituiscono fino a 5.000 record.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>Esercitazione di base sull'API REST di ricerca di Log Analytics
### <a name="toouse-armclient"></a>toouse ARMClient
1. Installare [Chocolatey](https://chocolatey.org/), un gestore di pacchetti open source per Windows. Aprire una finestra del prompt dei comandi come amministratore, quindi eseguire hello comando seguente:

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. Installare l'ARMClient eseguendo hello comando seguente:

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>tooperform una ricerca usando ARMClient
1. Effettuare l'accesso usando il proprio account Microsoft oppure l'account aziendale o dell'istituto di istruzione:

    ```
    armclient login
    ```

    Un account di accesso ha esito positivo sono elencate tutte le sottoscrizioni associate toohello, account indicato:

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Ottenere le aree di lavoro di hello Operations Management Suite:

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    Una chiamata Get riuscita genera che tutte le aree di lavoro collegata toohello sottoscrizione:

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. Creare la variabile di ricerca.

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. Eseguire la ricerca usando la nuova variabile di ricerca.

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Esempi di riferimento per l'API REST di ricerca di Log Analytics
Hello seguono esempi Mostra come usare hello API di ricerca.

### <a name="search---actionread"></a>Ricerca - Azione/Lettura
**Url di esempio:**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**Richiesta:**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
Hello nella tabella seguente vengono descritte le proprietà di hello disponibili.

| **Proprietà** | **Descrizione** |
| --- | --- |
| top |numero massimo di Hello di tooreturn risultati. |
| highlight |Contiene i parametri pre e post, in genere usati per evidenziare i campi corrispondenti |
| pre |Prefissi hello data i campi stringa tooyour corrispondente. |
| post |Accoda hello data i campi stringa tooyour corrispondente. |
| query |query di ricerca Hello utilizzato toocollect e restituire risultati. |
| start |inizio di Hello dell'intervallo di tempo hello desiderato toobe risultati trovato da. |
| end |fine di Hello dell'intervallo di tempo hello desiderato toobe risultati trovato da. |

**Risposta:**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>Ricerca/{ID} - Azione/Lettura
**Contenuto della richiesta hello di una ricerca salvata:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Se hello ricerca restituisce lo stato 'Sospeso', il polling risultati di hello aggiornato è possibile farlo tramite questa API. Dopo 6 min, hello risultato della ricerca hello verrà rimosso dalla cache di hello e sarà restituito HTTP Gone. Se la richiesta di ricerca iniziale hello restituisce immediatamente lo stato 'Riuscito', i risultati di hello non vengono aggiunti cache toohello causano questo tooreturn API HTTP Gone se eseguire una query. il contenuto di Hello di un risultato HTTP 200 è in hello stesso formato delle richiesta di ricerca iniziale hello solo con i valori aggiornati.
>
>

### <a name="saved-searches"></a>Ricerche salvate
**Elenco di richieste delle ricerche salvate:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

Metodi supportati: GET PUT DELETE

Metodi di raccolta supportati: GET

Hello nella tabella seguente vengono descritte le proprietà di hello disponibili.

| Proprietà | Descrizione |
| --- | --- |
| ID |Identificatore univoco di Hello. |
| ETag |**Obbligatoria per l'applicazione di patch**. Aggiornata dal server a ogni scrittura. Valore deve essere uguale toohello corrente archiviato o ' *' tooupdate. Viene restituito il codice 409 per i valori obsoleti/non validi. |
| properties.query |**Obbligatoria**. query di ricerca Hello. |
| properties.displayName |**Obbligatoria**. nome di visualizzazione definite dall'utente Hello di query hello. |
| properties.category |**Obbligatoria**. categoria definita dall'utente Hello di query hello. |

> [!NOTE]
> API di ricerca Log Analitica Hello attualmente restituisce creati dall'utente ricerche al polling di ricerche salvate in un'area di lavoro. Hello API non restituisce le ricerche salvate fornite dalle soluzioni.
>
>

### <a name="create-saved-searches"></a>Creare le ricerche salvate
**Richiesta:**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> nome Hello per le ricerche salvate tutte, pianificazioni e le azioni create con hello Log Analitica API deve essere in lettere minuscole.

### <a name="delete-saved-searches"></a>Eliminare le ricerche salvate
**Richiesta:**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>Aggiornare le ricerche salvate
 **Richiesta:**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>Metadati - Solo JSON
Ecco i campi di hello toosee un modo per tutti i tipi di log per i dati di hello raccolti nell'area di lavoro. Ad esempio, se si desidera che sapere se hello tipo di evento include un campo denominato Computer, questa query è un modo toocheck.

**Richiesta di campi:**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**Risposta:**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

Hello nella tabella seguente vengono descritte le proprietà di hello disponibili.

| **Proprietà** | **Descrizione** |
| --- | --- |
| name |Nome del campo. |
| displayName |nome del campo hello è visualizzato Hello. |
| type |Tipo di valore del campo hello Hello. |
| facetable |Combinazione delle proprietà "indexed", "stored" e "facet" attuali. |
| display |Proprietà "display" attuale. True se il campo è visibile nella ricerca. |
| ownerType |Tipi di tooonly ridotta appartenenti tooonboarded indirizzi IP. |

## <a name="optional-parameters"></a>Parametri facoltativi
le seguenti informazioni Hello descrive i parametri facoltativi disponibili.

### <a name="highlighting"></a>Evidenziazione
il parametro "Highlight" Hello è un parametro facoltativo, è possibile utilizzare sottosistema di ricerca hello toorequest includa un set di marcatori nella risposta.

Questi marcatori indicano hello inizio e fine del testo evidenziato che corrisponde hello termini forniti nella query di ricerca.
È possibile specificare hello inizio e fine marcatori utilizzati dal termine di ricerca toowrap hello evidenziato.

**Query di ricerca di esempio**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**Risultati di esempio:**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

Si noti che hello risultato precedente contiene un messaggio di errore con il prefisso e suffisso.

## <a name="computer-groups"></a>Gruppi di computer
I gruppi di computer sono ricerche salvate speciali che restituiscono un set di computer.  È possibile utilizzare un gruppo di computer in altri computer toohello risultati di query toolimit hello gruppo hello.  Un gruppo di computer viene implementato come una ricerca salvata con un tag Gruppo con il valore Computer.

Di seguito viene riportata una risposta di esempio per un gruppo di computer.

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>Recupero dei gruppi di computer
ID di un gruppo di computer, hello di utilizzare il metodo Get con gruppo hello tooretrieve

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>Creazione o aggiornamento di un gruppo di computer
toocreate un gruppo di computer, utilizzare il metodo Put hello con un ID univoco di ricerca salvata. Se si usa un ID di gruppo di computer esistente, tale gruppo viene modificato. Quando si crea un gruppo di computer nel portale di hello Log Analitica, hello ID viene creato dal nome e gruppo hello.

query Hello utilizzato per la definizione di gruppo hello deve restituire un set di computer per hello gruppo toofunction correttamente.  È consigliabile che si termina la query con `| Distinct Computer` tooensure hello corretto i dati vengono restituiti.

definizione di Hello di hello ricerca salvata deve includere un tag denominato gruppo con un valore del Computer per hello ricerca toobe classificati come un gruppo di computer.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>Eliminazione di gruppi di computer
ID di un gruppo di computer, hello di utilizzare il metodo Delete con gruppo hello toodelete

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [log ricerche](log-analytics-log-searches.md) toobuild query utilizzando i campi personalizzati per i criteri.
