---
title: Binding di tabelle esterne in Funzioni di Azure (Anteprima) | Microsoft Docs
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
ms.openlocfilehash: 716438e5ea490f6716999813112305499dbe61a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="ee874-103">Binding di tabelle esterne in Funzioni di Azure (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="ee874-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="ee874-104">Questo articolo illustra come gestire i dati tabulari sul provider SaaS (ad esempio, Sharepoint, Dynamics) all'interno della funzione con binding incorporati.</span><span class="sxs-lookup"><span data-stu-id="ee874-104">This article shows how to manipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="ee874-105">Funzioni di Azure supporta i binding di input e output per le tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="ee874-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="ee874-106">Connessioni API</span><span class="sxs-lookup"><span data-stu-id="ee874-106">API Connections</span></span>

<span data-ttu-id="ee874-107">I binding di tabella usano connessioni API esterne per l'autenticazione con i provider SaaS di terzi.</span><span class="sxs-lookup"><span data-stu-id="ee874-107">Table bindings leverage external API connections to authenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="ee874-108">Quando si assegna un binding è possibile creare una nuova connessione API o usare una connessione API esistente nello stesso gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="ee874-108">When assigning a binding you can either create a new API connection or use an existing API connection within the same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="ee874-109">Connessioni API supportate (Tabella)</span><span class="sxs-lookup"><span data-stu-id="ee874-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="ee874-110">Connettore</span><span class="sxs-lookup"><span data-stu-id="ee874-110">Connector</span></span>|<span data-ttu-id="ee874-111">Trigger</span><span class="sxs-lookup"><span data-stu-id="ee874-111">Trigger</span></span>|<span data-ttu-id="ee874-112">Input</span><span class="sxs-lookup"><span data-stu-id="ee874-112">Input</span></span>|<span data-ttu-id="ee874-113">Output</span><span class="sxs-lookup"><span data-stu-id="ee874-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="ee874-114">DB2</span><span class="sxs-lookup"><span data-stu-id="ee874-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="ee874-115">x</span><span class="sxs-lookup"><span data-stu-id="ee874-115">x</span></span>|<span data-ttu-id="ee874-116">x</span><span class="sxs-lookup"><span data-stu-id="ee874-116">x</span></span>
|[<span data-ttu-id="ee874-117">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="ee874-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="ee874-118">x</span><span class="sxs-lookup"><span data-stu-id="ee874-118">x</span></span>|<span data-ttu-id="ee874-119">x</span><span class="sxs-lookup"><span data-stu-id="ee874-119">x</span></span>
|[<span data-ttu-id="ee874-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="ee874-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="ee874-121">x</span><span class="sxs-lookup"><span data-stu-id="ee874-121">x</span></span>|<span data-ttu-id="ee874-122">x</span><span class="sxs-lookup"><span data-stu-id="ee874-122">x</span></span>
|[<span data-ttu-id="ee874-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="ee874-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="ee874-124">x</span><span class="sxs-lookup"><span data-stu-id="ee874-124">x</span></span>|<span data-ttu-id="ee874-125">x</span><span class="sxs-lookup"><span data-stu-id="ee874-125">x</span></span>
|[<span data-ttu-id="ee874-126">Fogli Google</span><span class="sxs-lookup"><span data-stu-id="ee874-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="ee874-127">x</span><span class="sxs-lookup"><span data-stu-id="ee874-127">x</span></span>|<span data-ttu-id="ee874-128">x</span><span class="sxs-lookup"><span data-stu-id="ee874-128">x</span></span>
|[<span data-ttu-id="ee874-129">Informix</span><span class="sxs-lookup"><span data-stu-id="ee874-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="ee874-130">x</span><span class="sxs-lookup"><span data-stu-id="ee874-130">x</span></span>|<span data-ttu-id="ee874-131">x</span><span class="sxs-lookup"><span data-stu-id="ee874-131">x</span></span>
|[<span data-ttu-id="ee874-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="ee874-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="ee874-133">x</span><span class="sxs-lookup"><span data-stu-id="ee874-133">x</span></span>|<span data-ttu-id="ee874-134">x</span><span class="sxs-lookup"><span data-stu-id="ee874-134">x</span></span>
|[<span data-ttu-id="ee874-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="ee874-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="ee874-136">x</span><span class="sxs-lookup"><span data-stu-id="ee874-136">x</span></span>|<span data-ttu-id="ee874-137">x</span><span class="sxs-lookup"><span data-stu-id="ee874-137">x</span></span>
|[<span data-ttu-id="ee874-138">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="ee874-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="ee874-139">x</span><span class="sxs-lookup"><span data-stu-id="ee874-139">x</span></span>|<span data-ttu-id="ee874-140">x</span><span class="sxs-lookup"><span data-stu-id="ee874-140">x</span></span>
|[<span data-ttu-id="ee874-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="ee874-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="ee874-142">x</span><span class="sxs-lookup"><span data-stu-id="ee874-142">x</span></span>|<span data-ttu-id="ee874-143">x</span><span class="sxs-lookup"><span data-stu-id="ee874-143">x</span></span>
|[<span data-ttu-id="ee874-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="ee874-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="ee874-145">x</span><span class="sxs-lookup"><span data-stu-id="ee874-145">x</span></span>|<span data-ttu-id="ee874-146">x</span><span class="sxs-lookup"><span data-stu-id="ee874-146">x</span></span>
|[<span data-ttu-id="ee874-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="ee874-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="ee874-148">x</span><span class="sxs-lookup"><span data-stu-id="ee874-148">x</span></span>|<span data-ttu-id="ee874-149">x</span><span class="sxs-lookup"><span data-stu-id="ee874-149">x</span></span>
|[<span data-ttu-id="ee874-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ee874-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="ee874-151">x</span><span class="sxs-lookup"><span data-stu-id="ee874-151">x</span></span>|<span data-ttu-id="ee874-152">x</span><span class="sxs-lookup"><span data-stu-id="ee874-152">x</span></span>
|[<span data-ttu-id="ee874-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="ee874-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="ee874-154">x</span><span class="sxs-lookup"><span data-stu-id="ee874-154">x</span></span>|<span data-ttu-id="ee874-155">x</span><span class="sxs-lookup"><span data-stu-id="ee874-155">x</span></span>
|<span data-ttu-id="ee874-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="ee874-156">UserVoice</span></span>||<span data-ttu-id="ee874-157">x</span><span class="sxs-lookup"><span data-stu-id="ee874-157">x</span></span>|<span data-ttu-id="ee874-158">x</span><span class="sxs-lookup"><span data-stu-id="ee874-158">x</span></span>
|<span data-ttu-id="ee874-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="ee874-159">Zendesk</span></span>||<span data-ttu-id="ee874-160">x</span><span class="sxs-lookup"><span data-stu-id="ee874-160">x</span></span>|<span data-ttu-id="ee874-161">x</span><span class="sxs-lookup"><span data-stu-id="ee874-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="ee874-162">È possibile usare le connessioni alle tabelle esterne anche nelle [App per la logica di Azure](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="ee874-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="ee874-163">Creazione di una connessione API: procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="ee874-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="ee874-164">Creare una funzione > funzione personalizzata ![Creare una funzione personalizzata](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="ee874-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="ee874-165">Modello scenario `Experimental`  >  `ExternalTable-CSharp` > Creare un nuovo `External Table connection` 
 ![Scegliere il modello di input tabella](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="ee874-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="ee874-166">Scegliere il provider SaaS > scegliere o creare una connessione ![Configurare una connessione SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="ee874-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="ee874-167">Selezionare la connessione API > creare la funzione ![funzione Crea tabella](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="ee874-167">Select your API connection > create the function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="ee874-168">Selezionare `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="ee874-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="ee874-169">Configurare la connessione per usare la tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ee874-169">Configure the connection to use your target table.</span></span> <span data-ttu-id="ee874-170">Queste impostazioni variano tra i provider SaaS.</span><span class="sxs-lookup"><span data-stu-id="ee874-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="ee874-171">Sono indicate qui di seguito in [impostazioni dell'origine dati](#datasourcesettings)
![Configura tabella](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="ee874-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="ee874-172">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="ee874-172">Usage</span></span>

<span data-ttu-id="ee874-173">Questo esempio si connette a una tabella denominata "Contatto" con le colonne Id, LastName e FirstName.</span><span class="sxs-lookup"><span data-stu-id="ee874-173">This example connects to a table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="ee874-174">Il codice elenca le entità Contatto nella tabella e registra i nomi e i cognomi.</span><span class="sxs-lookup"><span data-stu-id="ee874-174">The code lists the Contact entities in the table and logs the first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="ee874-175">Associazioni</span><span class="sxs-lookup"><span data-stu-id="ee874-175">Bindings</span></span>
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
<span data-ttu-id="ee874-176">`entityId` deve essere vuoto per i binding di tabella.</span><span class="sxs-lookup"><span data-stu-id="ee874-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="ee874-177">`ConnectionAppSettingsKey` identifica l'impostazione dell'app che memorizza la stringa di connessione dell'API.</span><span class="sxs-lookup"><span data-stu-id="ee874-177">`ConnectionAppSettingsKey` identifies the app setting that stores the API connection string.</span></span> <span data-ttu-id="ee874-178">L'impostazione dell'app viene creata automaticamente quando si aggiunge una connessione API nell'interfaccia utente integrata.</span><span class="sxs-lookup"><span data-stu-id="ee874-178">The app setting is created automatically when you add an API connection in the integrate UI.</span></span>

<span data-ttu-id="ee874-179">Un connettore tabulare fornisce set di dati e ogni set di dati contiene tabelle.</span><span class="sxs-lookup"><span data-stu-id="ee874-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="ee874-180">Il nome del set di dati predefinito è "default".</span><span class="sxs-lookup"><span data-stu-id="ee874-180">The name of the default data set is “default.”</span></span> <span data-ttu-id="ee874-181">I titoli di un set di dati e di una tabella in diversi provider SaaS sono elencati di seguito:</span><span class="sxs-lookup"><span data-stu-id="ee874-181">The titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="ee874-182">Connettore</span><span class="sxs-lookup"><span data-stu-id="ee874-182">Connector</span></span>|<span data-ttu-id="ee874-183">Set di dati</span><span class="sxs-lookup"><span data-stu-id="ee874-183">Dataset</span></span>|<span data-ttu-id="ee874-184">Tabella</span><span class="sxs-lookup"><span data-stu-id="ee874-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="ee874-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="ee874-185">**SharePoint**</span></span>|<span data-ttu-id="ee874-186">Sito</span><span class="sxs-lookup"><span data-stu-id="ee874-186">Site</span></span>|<span data-ttu-id="ee874-187">Elenco SharePoint</span><span class="sxs-lookup"><span data-stu-id="ee874-187">SharePoint List</span></span>
|<span data-ttu-id="ee874-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee874-188">**SQL**</span></span>|<span data-ttu-id="ee874-189">Database</span><span class="sxs-lookup"><span data-stu-id="ee874-189">Database</span></span>|<span data-ttu-id="ee874-190">Tabella</span><span class="sxs-lookup"><span data-stu-id="ee874-190">Table</span></span> 
|<span data-ttu-id="ee874-191">**Fogli Google**</span><span class="sxs-lookup"><span data-stu-id="ee874-191">**Google Sheet**</span></span>|<span data-ttu-id="ee874-192">Foglio di calcolo</span><span class="sxs-lookup"><span data-stu-id="ee874-192">Spreadsheet</span></span>|<span data-ttu-id="ee874-193">Foglio di lavoro</span><span class="sxs-lookup"><span data-stu-id="ee874-193">Worksheet</span></span> 
|<span data-ttu-id="ee874-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="ee874-194">**Excel**</span></span>|<span data-ttu-id="ee874-195">File di Excel</span><span class="sxs-lookup"><span data-stu-id="ee874-195">Excel file</span></span>|<span data-ttu-id="ee874-196">Foglio</span><span class="sxs-lookup"><span data-stu-id="ee874-196">Sheet</span></span> 

<!--
See the language-specific sample that copies the input file to the output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="ee874-197">Utilizzo in C#</span><span class="sxs-lookup"><span data-stu-id="ee874-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound to the incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in the source table
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

<span data-ttu-id="ee874-198"><!--
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
## Impostazioni dell'origine dati</span><span class="sxs-lookup"><span data-stu-id="ee874-198"><!--
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
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="ee874-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ee874-199">SQL Server</span></span>

<span data-ttu-id="ee874-200">Lo script per creare e popolare la tabella Contact è qui di seguito.</span><span class="sxs-lookup"><span data-stu-id="ee874-200">The script to create and populate the Contact table is below.</span></span> <span data-ttu-id="ee874-201">dataSetName è "default".</span><span class="sxs-lookup"><span data-stu-id="ee874-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="ee874-202">Fogli Google</span><span class="sxs-lookup"><span data-stu-id="ee874-202">Google Sheets</span></span>
<span data-ttu-id="ee874-203">In Documenti Google, creare un foglio di calcolo con un foglio di lavoro denominato `Contact`.</span><span class="sxs-lookup"><span data-stu-id="ee874-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="ee874-204">Il connettore non può usare il nome visualizzato del foglio di calcolo.</span><span class="sxs-lookup"><span data-stu-id="ee874-204">The connector cannot use the spreadsheet display name.</span></span> <span data-ttu-id="ee874-205">Il nome interno (in grassetto) deve essere usato come dataSetName, ad esempio: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Aggiungere i nomi di colonna `Id`, `LastName`, `FirstName` alla prima riga, quindi inserire dati nelle righe successive.</span><span class="sxs-lookup"><span data-stu-id="ee874-205">The internal name (in bold) needs to be used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add the column names `Id`, `LastName`, `FirstName` to the first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="ee874-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="ee874-206">Salesforce</span></span>
<span data-ttu-id="ee874-207">dataSetName è "default".</span><span class="sxs-lookup"><span data-stu-id="ee874-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee874-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee874-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
