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
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="18ca2-103">Binding di tabelle esterne in Funzioni di Azure (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="18ca2-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="18ca2-104">Questo articolo viene illustrato come toomanipulate dati tabulari su provider SaaS (ad esempio, Sharepoint, Dynamics) all'interno della funzione con associazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="18ca2-104">This article shows how toomanipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="18ca2-105">Funzioni di Azure supporta i binding di input e output per le tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="18ca2-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="18ca2-106">Connessioni API</span><span class="sxs-lookup"><span data-stu-id="18ca2-106">API Connections</span></span>

<span data-ttu-id="18ca2-107">Associazioni di tabella utilizzano tooauthenticate di connessioni esterne API con i provider SaaS di terze parti 3rd.</span><span class="sxs-lookup"><span data-stu-id="18ca2-107">Table bindings leverage external API connections tooauthenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="18ca2-108">Quando si assegna un'associazione è possibile creare una nuova API di connessione o utilizzare una connessione di API esistente all'interno di hello stesso gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="18ca2-108">When assigning a binding you can either create a new API connection or use an existing API connection within hello same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="18ca2-109">Connessioni API supportate (Tabella)</span><span class="sxs-lookup"><span data-stu-id="18ca2-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="18ca2-110">Connettore</span><span class="sxs-lookup"><span data-stu-id="18ca2-110">Connector</span></span>|<span data-ttu-id="18ca2-111">Trigger</span><span class="sxs-lookup"><span data-stu-id="18ca2-111">Trigger</span></span>|<span data-ttu-id="18ca2-112">Input</span><span class="sxs-lookup"><span data-stu-id="18ca2-112">Input</span></span>|<span data-ttu-id="18ca2-113">Output</span><span class="sxs-lookup"><span data-stu-id="18ca2-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="18ca2-114">DB2</span><span class="sxs-lookup"><span data-stu-id="18ca2-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="18ca2-115">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-115">x</span></span>|<span data-ttu-id="18ca2-116">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-116">x</span></span>
|[<span data-ttu-id="18ca2-117">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="18ca2-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="18ca2-118">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-118">x</span></span>|<span data-ttu-id="18ca2-119">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-119">x</span></span>
|[<span data-ttu-id="18ca2-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="18ca2-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="18ca2-121">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-121">x</span></span>|<span data-ttu-id="18ca2-122">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-122">x</span></span>
|[<span data-ttu-id="18ca2-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="18ca2-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="18ca2-124">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-124">x</span></span>|<span data-ttu-id="18ca2-125">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-125">x</span></span>
|[<span data-ttu-id="18ca2-126">Fogli Google</span><span class="sxs-lookup"><span data-stu-id="18ca2-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="18ca2-127">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-127">x</span></span>|<span data-ttu-id="18ca2-128">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-128">x</span></span>
|[<span data-ttu-id="18ca2-129">Informix</span><span class="sxs-lookup"><span data-stu-id="18ca2-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="18ca2-130">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-130">x</span></span>|<span data-ttu-id="18ca2-131">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-131">x</span></span>
|[<span data-ttu-id="18ca2-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="18ca2-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="18ca2-133">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-133">x</span></span>|<span data-ttu-id="18ca2-134">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-134">x</span></span>
|[<span data-ttu-id="18ca2-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="18ca2-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="18ca2-136">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-136">x</span></span>|<span data-ttu-id="18ca2-137">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-137">x</span></span>
|[<span data-ttu-id="18ca2-138">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="18ca2-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="18ca2-139">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-139">x</span></span>|<span data-ttu-id="18ca2-140">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-140">x</span></span>
|[<span data-ttu-id="18ca2-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="18ca2-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="18ca2-142">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-142">x</span></span>|<span data-ttu-id="18ca2-143">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-143">x</span></span>
|[<span data-ttu-id="18ca2-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="18ca2-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="18ca2-145">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-145">x</span></span>|<span data-ttu-id="18ca2-146">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-146">x</span></span>
|[<span data-ttu-id="18ca2-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="18ca2-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="18ca2-148">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-148">x</span></span>|<span data-ttu-id="18ca2-149">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-149">x</span></span>
|[<span data-ttu-id="18ca2-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="18ca2-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="18ca2-151">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-151">x</span></span>|<span data-ttu-id="18ca2-152">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-152">x</span></span>
|[<span data-ttu-id="18ca2-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="18ca2-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="18ca2-154">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-154">x</span></span>|<span data-ttu-id="18ca2-155">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-155">x</span></span>
|<span data-ttu-id="18ca2-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="18ca2-156">UserVoice</span></span>||<span data-ttu-id="18ca2-157">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-157">x</span></span>|<span data-ttu-id="18ca2-158">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-158">x</span></span>
|<span data-ttu-id="18ca2-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="18ca2-159">Zendesk</span></span>||<span data-ttu-id="18ca2-160">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-160">x</span></span>|<span data-ttu-id="18ca2-161">x</span><span class="sxs-lookup"><span data-stu-id="18ca2-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="18ca2-162">È possibile usare le connessioni alle tabelle esterne anche nelle [App per la logica di Azure](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="18ca2-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="18ca2-163">Creazione di una connessione API: procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="18ca2-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="18ca2-164">Creare una funzione > funzione personalizzata ![Creare una funzione personalizzata](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="18ca2-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="18ca2-165">Modello scenario `Experimental`  >  `ExternalTable-CSharp` > Creare un nuovo `External Table connection` 
 ![Scegliere il modello di input tabella](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="18ca2-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="18ca2-166">Scegliere il provider SaaS > scegliere o creare una connessione ![Configurare una connessione SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="18ca2-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="18ca2-167">Selezionare la connessione API > consente di creare la funzione hello ![creare una funzione di tabella](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="18ca2-167">Select your API connection > create hello function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="18ca2-168">Selezionare `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="18ca2-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="18ca2-169">Configurare hello connessione toouse la tabella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="18ca2-169">Configure hello connection toouse your target table.</span></span> <span data-ttu-id="18ca2-170">Queste impostazioni variano tra i provider SaaS.</span><span class="sxs-lookup"><span data-stu-id="18ca2-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="18ca2-171">Sono indicate qui di seguito in [impostazioni dell'origine dati](#datasourcesettings)
![Configura tabella](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="18ca2-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="18ca2-172">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="18ca2-172">Usage</span></span>

<span data-ttu-id="18ca2-173">In questo esempio si connette tooa tabella denominata "Contact" con le colonne di tipo Id, nome e cognome.</span><span class="sxs-lookup"><span data-stu-id="18ca2-173">This example connects tooa table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="18ca2-174">codice Hello Elenca le entità di contatto hello nella tabella hello e log hello nome e cognome.</span><span class="sxs-lookup"><span data-stu-id="18ca2-174">hello code lists hello Contact entities in hello table and logs hello first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="18ca2-175">Associazioni</span><span class="sxs-lookup"><span data-stu-id="18ca2-175">Bindings</span></span>
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
<span data-ttu-id="18ca2-176">`entityId` deve essere vuoto per i binding di tabella.</span><span class="sxs-lookup"><span data-stu-id="18ca2-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="18ca2-177">`ConnectionAppSettingsKey`Identifica l'impostazione dell'app hello che archivia una stringa di connessione hello API.</span><span class="sxs-lookup"><span data-stu-id="18ca2-177">`ConnectionAppSettingsKey` identifies hello app setting that stores hello API connection string.</span></span> <span data-ttu-id="18ca2-178">Hello impostazione dell'app viene creata automaticamente quando si aggiunge un'API connessione in hello integrare dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="18ca2-178">hello app setting is created automatically when you add an API connection in hello integrate UI.</span></span>

<span data-ttu-id="18ca2-179">Un connettore tabulare fornisce set di dati e ogni set di dati contiene tabelle.</span><span class="sxs-lookup"><span data-stu-id="18ca2-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="18ca2-180">nome di Hello del set di dati predefinito hello è "default".</span><span class="sxs-lookup"><span data-stu-id="18ca2-180">hello name of hello default data set is “default.”</span></span> <span data-ttu-id="18ca2-181">i titoli di Hello per un set di dati e una tabella in diversi provider SaaS sono elencati di seguito:</span><span class="sxs-lookup"><span data-stu-id="18ca2-181">hello titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="18ca2-182">Connettore</span><span class="sxs-lookup"><span data-stu-id="18ca2-182">Connector</span></span>|<span data-ttu-id="18ca2-183">Set di dati</span><span class="sxs-lookup"><span data-stu-id="18ca2-183">Dataset</span></span>|<span data-ttu-id="18ca2-184">Tabella</span><span class="sxs-lookup"><span data-stu-id="18ca2-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="18ca2-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="18ca2-185">**SharePoint**</span></span>|<span data-ttu-id="18ca2-186">Sito</span><span class="sxs-lookup"><span data-stu-id="18ca2-186">Site</span></span>|<span data-ttu-id="18ca2-187">Elenco SharePoint</span><span class="sxs-lookup"><span data-stu-id="18ca2-187">SharePoint List</span></span>
|<span data-ttu-id="18ca2-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="18ca2-188">**SQL**</span></span>|<span data-ttu-id="18ca2-189">Database</span><span class="sxs-lookup"><span data-stu-id="18ca2-189">Database</span></span>|<span data-ttu-id="18ca2-190">Tabella</span><span class="sxs-lookup"><span data-stu-id="18ca2-190">Table</span></span> 
|<span data-ttu-id="18ca2-191">**Fogli Google**</span><span class="sxs-lookup"><span data-stu-id="18ca2-191">**Google Sheet**</span></span>|<span data-ttu-id="18ca2-192">Foglio di calcolo</span><span class="sxs-lookup"><span data-stu-id="18ca2-192">Spreadsheet</span></span>|<span data-ttu-id="18ca2-193">Foglio di lavoro</span><span class="sxs-lookup"><span data-stu-id="18ca2-193">Worksheet</span></span> 
|<span data-ttu-id="18ca2-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="18ca2-194">**Excel**</span></span>|<span data-ttu-id="18ca2-195">File di Excel</span><span class="sxs-lookup"><span data-stu-id="18ca2-195">Excel file</span></span>|<span data-ttu-id="18ca2-196">Foglio</span><span class="sxs-lookup"><span data-stu-id="18ca2-196">Sheet</span></span> 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="18ca2-197">Utilizzo in C#</span><span class="sxs-lookup"><span data-stu-id="18ca2-197">Usage in C#</span></span> #

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

<span data-ttu-id="18ca2-198"><!--
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
## Impostazioni dell'origine dati</span><span class="sxs-lookup"><span data-stu-id="18ca2-198"><!--
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

### <a name="sql-server"></a><span data-ttu-id="18ca2-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="18ca2-199">SQL Server</span></span>

<span data-ttu-id="18ca2-200">Hello toocreate script e popolare tabella Contact hello è inferiore.</span><span class="sxs-lookup"><span data-stu-id="18ca2-200">hello script toocreate and populate hello Contact table is below.</span></span> <span data-ttu-id="18ca2-201">dataSetName è "default".</span><span class="sxs-lookup"><span data-stu-id="18ca2-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="18ca2-202">Fogli Google</span><span class="sxs-lookup"><span data-stu-id="18ca2-202">Google Sheets</span></span>
<span data-ttu-id="18ca2-203">In Documenti Google, creare un foglio di calcolo con un foglio di lavoro denominato `Contact`.</span><span class="sxs-lookup"><span data-stu-id="18ca2-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="18ca2-204">connettore Hello non è possibile utilizzare nome visualizzato del foglio di calcolo di hello.</span><span class="sxs-lookup"><span data-stu-id="18ca2-204">hello connector cannot use hello spreadsheet display name.</span></span> <span data-ttu-id="18ca2-205">nome interno di Hello (in grassetto) deve toobe utilizzate come dataSetName, ad esempio: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  aggiungere nomi di colonna hello `Id`, `LastName`, `FirstName` toohello prima riga e quindi inserire i dati in righe successive.</span><span class="sxs-lookup"><span data-stu-id="18ca2-205">hello internal name (in bold) needs toobe used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add hello column names `Id`, `LastName`, `FirstName` toohello first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="18ca2-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="18ca2-206">Salesforce</span></span>
<span data-ttu-id="18ca2-207">dataSetName è "default".</span><span class="sxs-lookup"><span data-stu-id="18ca2-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="18ca2-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="18ca2-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
