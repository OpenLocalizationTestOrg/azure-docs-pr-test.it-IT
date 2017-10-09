---
title: associazione di tabella esterna funzioni aaaAzure (anteprima) | Documenti Microsoft
description: Uso di binding di tabelle esterne in Funzioni di Azure
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a>Binding di tabelle esterne in Funzioni di Azure (Anteprima)
Questo articolo viene illustrato come toomanipulate dati tabulari su provider SaaS (ad esempio, Sharepoint, Dynamics) all'interno della funzione con associazioni predefinite. Funzioni di Azure supporta i binding di input e output per le tabelle esterne.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a>Connessioni API

Associazioni di tabella utilizzano tooauthenticate di connessioni esterne API con i provider SaaS di terze parti 3rd. 

Quando si assegna un'associazione è possibile creare una nuova API di connessione o utilizzare una connessione di API esistente all'interno di hello stesso gruppo di risorse

### <a name="supported-api-connections-tables"></a>Connessioni API supportate (Tabella)

|Connettore|Trigger|Input|Output|
|:-----|:---:|:---:|:---:|
|[DB2](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||x|x
|[Dynamics 365 for Operations](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||x|x
|[Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[Dynamics NAV](https://msdn.microsoft.com/library/gg481835.aspx)||x|x
|[Fogli Google](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||x|x
|[Informix](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||x|x
|[Dynamics 365 for Financials](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[MySQL](https://docs.microsoft.com/azure/store-php-create-mysql-database)||x|x
|[Oracle Database](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||x|x
|[Common Data Service](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||x|x
|[Salesforce](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||x|x
|[SharePoint](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||x|x
|[SQL Server](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||x|x
|[Teradata](http://www.teradata.com/products-and-services/azure/products/)||x|x
|UserVoice||x|x
|Zendesk||x|x


> [!NOTE]
> È possibile usare le connessioni alle tabelle esterne anche nelle [App per la logica di Azure](https://docs.microsoft.com/azure/connectors/apis-list)

### <a name="creating-an-api-connection-step-by-step"></a>Creazione di una connessione API: procedura dettagliata

1. Creare una funzione > funzione personalizzata ![Creare una funzione personalizzata](./media/functions-bindings-storage-table/create-custom-function.jpg)
1. Modello scenario `Experimental`  >  `ExternalTable-CSharp` > Creare un nuovo `External Table connection` 
 ![Scegliere il modello di input tabella](./media/functions-bindings-storage-table/create-template-table.jpg)
1. Scegliere il provider SaaS > scegliere o creare una connessione ![Configurare una connessione SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)
1. Selezionare la connessione API > consente di creare la funzione hello ![creare una funzione di tabella](./media/functions-bindings-storage-table/table-template-options.jpg)
1. Selezionare `Integrate` > `External Table`
    1. Configurare hello connessione toouse la tabella di destinazione. Queste impostazioni variano tra i provider SaaS. Sono indicate qui di seguito in [impostazioni dell'origine dati](#datasourcesettings)
![Configura tabella](./media/functions-bindings-storage-table/configure-API-connection.jpg)

## <a name="usage"></a>Utilizzo

In questo esempio si connette tooa tabella denominata "Contact" con le colonne di tipo Id, nome e cognome. codice Hello Elenca le entità di contatto hello nella tabella hello e log hello nome e cognome.

### <a name="bindings"></a>Associazioni
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
`entityId` deve essere vuoto per i binding di tabella.

`ConnectionAppSettingsKey`Identifica l'impostazione dell'app hello che archivia una stringa di connessione hello API. Hello impostazione dell'app viene creata automaticamente quando si aggiunge un'API connessione in hello integrare dell'interfaccia utente.

Un connettore tabulare fornisce set di dati e ogni set di dati contiene tabelle. nome di Hello del set di dati predefinito hello è "default". i titoli di Hello per un set di dati e una tabella in diversi provider SaaS sono elencati di seguito:

|Connettore|Set di dati|Tabella|
|:-----|:---|:---| 
|**SharePoint**|Sito|Elenco SharePoint
|**SQL**|Database|Tabella 
|**Fogli Google**|Foglio di calcolo|Foglio di lavoro 
|**Excel**|File di Excel|Foglio 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a>Utilizzo in C# #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
## Impostazioni dell'origine dati

### <a name="sql-server"></a>SQL Server

Hello toocreate script e popolare tabella Contact hello è inferiore. dataSetName è "default".

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a>Fogli Google
In Documenti Google, creare un foglio di calcolo con un foglio di lavoro denominato `Contact`. connettore Hello non è possibile utilizzare nome visualizzato del foglio di calcolo di hello. nome interno di Hello (in grassetto) deve toobe utilizzate come dataSetName, ad esempio: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  aggiungere nomi di colonna hello `Id`, `LastName`, `FirstName` toohello prima riga e quindi inserire i dati in righe successive.

### <a name="salesforce"></a>Salesforce
dataSetName è "default".

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
