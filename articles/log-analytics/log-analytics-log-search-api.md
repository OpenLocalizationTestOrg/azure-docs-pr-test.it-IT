---
title: API REST di ricerca nei log di Log Analytics | Documentazione Microsoft
description: Questa guida contiene un'esercitazione di base che descrive come usare l'API REST di ricerca di Log Analytics in Operations Management Suite (OMS) e offre esempi che indicano come usare i comandi.
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
ms.openlocfilehash: 78afb2f065dde4a3e7a3ab787c939b3c52b72cc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="ffd83-103">API REST di Log Analytics per la ricerca nei log</span><span class="sxs-lookup"><span data-stu-id="ffd83-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="ffd83-104">Questa guida fornisce un'esercitazione di base, inclusi alcuni esempi, per l'uso dell'API REST di Log Analytics per la ricerca.</span><span class="sxs-lookup"><span data-stu-id="ffd83-104">This guide provides a basic tutorial, including examples, of how you can use the Log Analytics Search REST API.</span></span> <span data-ttu-id="ffd83-105">Log Analytics fa parte di Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="ffd83-105">Log Analytics is part of the Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="ffd83-106">Se l'area di lavoro è stata aggiornata al [nuovo linguaggio di query di Log Analytics](log-analytics-log-search-upgrade.md), è necessario continuare a usare il linguaggio di query legacy con l'API di ricerca log, come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ffd83-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue to use the legacy query language with the log search API as described in this article.</span></span>  <span data-ttu-id="ffd83-107">Verrà rilasciata una nuova API per le aree di lavoro aggiornate e la documentazione verrà a quel punto aggiornata.</span><span class="sxs-lookup"><span data-stu-id="ffd83-107">A new API will be released for upgraded workspaces, and the documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="ffd83-108">In precedenza Log Analytics era chiamato Operational Insights e questo è il motivo per cui questo nome viene usato nel provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="ffd83-108">Log Analytics was previously called Operational Insights, which is why it is the name used in the resource provider.</span></span>
>
>

## <a name="overview-of-the-log-search-rest-api"></a><span data-ttu-id="ffd83-109">Panoramica dell'API REST di ricerca di log</span><span class="sxs-lookup"><span data-stu-id="ffd83-109">Overview of the Log Search REST API</span></span>
<span data-ttu-id="ffd83-110">L'API REST di ricerca di Log Analytics è RESTful e accessibile tramite l'API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ffd83-110">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager API.</span></span> <span data-ttu-id="ffd83-111">Questo articolo presenta alcuni esempi di accesso all'API tramite [ARMClient](https://github.com/projectkudu/ARMClient), uno strumento da riga di comando open source che semplifica la chiamata dell'API di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ffd83-111">This article provides examples of accessing the API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="ffd83-112">L'uso di ARMClient è una delle numerose opzioni disponibili per accedere all'API di ricerca di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ffd83-112">The use of ARMClient is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="ffd83-113">Un'altra possibilità è quella di usare il modulo Azure PowerShell per OperationalInsights che include cmdlet per l'accesso alla ricerca.</span><span class="sxs-lookup"><span data-stu-id="ffd83-113">Another option is to use the Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="ffd83-114">Con questi strumenti è possibile usare l'API di Azure Resource Manager per effettuare chiamate alle aree di lavoro di OMS ed eseguire i comandi di ricerca al loro interno.</span><span class="sxs-lookup"><span data-stu-id="ffd83-114">With these tools, you can utilize the Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="ffd83-115">L'API restituisce i risultati della ricerca in formato JSON, consentendo di usare i risultati della ricerca in molti modi diversi a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="ffd83-115">The API outputs search results in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

<span data-ttu-id="ffd83-116">È possibile usare Azure Resource Manager tramite una [libreria per NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) e l'[API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="ffd83-116">The Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and the [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="ffd83-117">Per altre informazioni, vedere le pagine Web collegate.</span><span class="sxs-lookup"><span data-stu-id="ffd83-117">To learn more, review the linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="ffd83-118">Se si usa un comando di aggregazione, ad esempio `|measure count()` o `distinct`, ogni chiamata per la ricerca può restituire fino a 500.000 record.</span><span class="sxs-lookup"><span data-stu-id="ffd83-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call to search can return upto 500,000 records.</span></span> <span data-ttu-id="ffd83-119">Le ricerche che non includono un comando di aggregazione restituiscono fino a 5.000 record.</span><span class="sxs-lookup"><span data-stu-id="ffd83-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="ffd83-120">Esercitazione di base sull'API REST di ricerca di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ffd83-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="to-use-armclient"></a><span data-ttu-id="ffd83-121">Per usare ARMClient</span><span class="sxs-lookup"><span data-stu-id="ffd83-121">To use ARMClient</span></span>
1. <span data-ttu-id="ffd83-122">Installare [Chocolatey](https://chocolatey.org/), un gestore di pacchetti open source per Windows.</span><span class="sxs-lookup"><span data-stu-id="ffd83-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="ffd83-123">Aprire una finestra di prompt di comandi come amministratore ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ffd83-123">Open a command prompt window as administrator and then run the following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="ffd83-124">Installare ARMClient eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ffd83-124">Install ARMClient by running the following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="to-perform-a-search-using-armclient"></a><span data-ttu-id="ffd83-125">Per eseguire una ricerca usando ARMClient</span><span class="sxs-lookup"><span data-stu-id="ffd83-125">To perform a search using ARMClient</span></span>
1. <span data-ttu-id="ffd83-126">Effettuare l'accesso usando il proprio account Microsoft oppure l'account aziendale o dell'istituto di istruzione:</span><span class="sxs-lookup"><span data-stu-id="ffd83-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="ffd83-127">Se l’accesso viene effettuato correttamente, vengono elencate tutte le sottoscrizioni associate all'account specificato.</span><span class="sxs-lookup"><span data-stu-id="ffd83-127">A successful login lists all subscriptions tied to the given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="ffd83-128">Ottenere le aree di lavoro di Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="ffd83-128">Get the Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="ffd83-129">Una chiamata Get riuscita genera tutte le aree di lavoro associate alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ffd83-129">A successful Get call would output all workspaces tied to the subscription:</span></span>

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
3. <span data-ttu-id="ffd83-130">Creare la variabile di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ffd83-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="ffd83-131">Eseguire la ricerca usando la nuova variabile di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ffd83-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="ffd83-132">Esempi di riferimento per l'API REST di ricerca di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ffd83-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="ffd83-133">I codici di esempio seguenti mostrano come usare l’API di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ffd83-133">The following examples show you how you can use the Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="ffd83-134">Ricerca - Azione/Lettura</span><span class="sxs-lookup"><span data-stu-id="ffd83-134">Search - Action/Read</span></span>
<span data-ttu-id="ffd83-135">**Url di esempio:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="ffd83-136">**Richiesta:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-136">**Request:**</span></span>

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
<span data-ttu-id="ffd83-137">La tabella seguente descrive le proprietà disponibili.</span><span class="sxs-lookup"><span data-stu-id="ffd83-137">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="ffd83-138">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="ffd83-138">**Property**</span></span> | <span data-ttu-id="ffd83-139">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="ffd83-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="ffd83-140">top</span><span class="sxs-lookup"><span data-stu-id="ffd83-140">top</span></span> |<span data-ttu-id="ffd83-141">Il numero massimo di risultati da restituire.</span><span class="sxs-lookup"><span data-stu-id="ffd83-141">The maximum number of results to return.</span></span> |
| <span data-ttu-id="ffd83-142">highlight</span><span class="sxs-lookup"><span data-stu-id="ffd83-142">highlight</span></span> |<span data-ttu-id="ffd83-143">Contiene i parametri pre e post, in genere usati per evidenziare i campi corrispondenti</span><span class="sxs-lookup"><span data-stu-id="ffd83-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="ffd83-144">pre</span><span class="sxs-lookup"><span data-stu-id="ffd83-144">pre</span></span> |<span data-ttu-id="ffd83-145">Antepone la stringa specificata ai campi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="ffd83-145">Prefixes the given string to your matched fields.</span></span> |
| <span data-ttu-id="ffd83-146">post</span><span class="sxs-lookup"><span data-stu-id="ffd83-146">post</span></span> |<span data-ttu-id="ffd83-147">Appone la stringa specificata ai campi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="ffd83-147">Appends the given string to your matched fields.</span></span> |
| <span data-ttu-id="ffd83-148">query</span><span class="sxs-lookup"><span data-stu-id="ffd83-148">query</span></span> |<span data-ttu-id="ffd83-149">La query di ricerca usata per raccogliere e restituire i risultati.</span><span class="sxs-lookup"><span data-stu-id="ffd83-149">The search query used to collect and return results.</span></span> |
| <span data-ttu-id="ffd83-150">start</span><span class="sxs-lookup"><span data-stu-id="ffd83-150">start</span></span> |<span data-ttu-id="ffd83-151">L’inizio dell'intervallo di tempo da cui si desidera trovare risultati.</span><span class="sxs-lookup"><span data-stu-id="ffd83-151">The beginning of the time window you want results to be found from.</span></span> |
| <span data-ttu-id="ffd83-152">end</span><span class="sxs-lookup"><span data-stu-id="ffd83-152">end</span></span> |<span data-ttu-id="ffd83-153">La fine dell'intervallo di tempo da cui si desidera trovare risultati.</span><span class="sxs-lookup"><span data-stu-id="ffd83-153">The end of the time window you want results to be found from.</span></span> |

<span data-ttu-id="ffd83-154">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="ffd83-155">Ricerca/{ID} - Azione/Lettura</span><span class="sxs-lookup"><span data-stu-id="ffd83-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="ffd83-156">**Richiedere il contenuto di una ricerca salvata:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-156">**Request the contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="ffd83-157">Se la ricerca restituisce lo stato 'Sospeso', il polling dei risultati aggiornati può essere effettuato tramite questa API.</span><span class="sxs-lookup"><span data-stu-id="ffd83-157">If the search returns with a ‘Pending’ status, then polling the updated results can be done through this API.</span></span> <span data-ttu-id="ffd83-158">Dopo 6 min il risultato della ricerca verrà rimosso dalla cache e sarà restituito Http Gone.</span><span class="sxs-lookup"><span data-stu-id="ffd83-158">After 6 min, the result of the search will be dropped from the cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="ffd83-159">Se la richiesta di ricerca iniziale restituisce immediatamente lo stato di operazione riuscita, i risultati non vengono aggiunti alla cache e l'API restituisce HTTP Gone in caso di query.</span><span class="sxs-lookup"><span data-stu-id="ffd83-159">If the initial search request returns a ‘Successful’ status immediately, the results are not added to the cache causing this API to return HTTP Gone if queried.</span></span> <span data-ttu-id="ffd83-160">Il contenuto di un risultato HTTP 200 è nello stesso formato della richiesta di ricerca iniziale, ma con i valori aggiornati.</span><span class="sxs-lookup"><span data-stu-id="ffd83-160">The contents of an HTTP 200 result are in the same format as the initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="ffd83-161">Ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="ffd83-161">Saved searches</span></span>
<span data-ttu-id="ffd83-162">**Elenco di richieste delle ricerche salvate:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="ffd83-163">Metodi supportati: GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="ffd83-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="ffd83-164">Metodi di raccolta supportati: GET</span><span class="sxs-lookup"><span data-stu-id="ffd83-164">Supported collection methods: GET</span></span>

<span data-ttu-id="ffd83-165">La tabella seguente descrive le proprietà disponibili.</span><span class="sxs-lookup"><span data-stu-id="ffd83-165">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="ffd83-166">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ffd83-166">Property</span></span> | <span data-ttu-id="ffd83-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="ffd83-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ffd83-168">ID</span><span class="sxs-lookup"><span data-stu-id="ffd83-168">Id</span></span> |<span data-ttu-id="ffd83-169">Identificatore univoco.</span><span class="sxs-lookup"><span data-stu-id="ffd83-169">The unique identifier.</span></span> |
| <span data-ttu-id="ffd83-170">ETag</span><span class="sxs-lookup"><span data-stu-id="ffd83-170">Etag</span></span> |<span data-ttu-id="ffd83-171">**Obbligatoria per l'applicazione di patch**.</span><span class="sxs-lookup"><span data-stu-id="ffd83-171">**Required for Patch**.</span></span> <span data-ttu-id="ffd83-172">Aggiornata dal server a ogni scrittura.</span><span class="sxs-lookup"><span data-stu-id="ffd83-172">Updated by server on each write.</span></span> <span data-ttu-id="ffd83-173">Il valore deve essere uguale al valore archiviato attuale o a "*" per effettuare l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ffd83-173">Value must be equal to the current stored value or ‘*’ to update.</span></span> <span data-ttu-id="ffd83-174">Viene restituito il codice 409 per i valori obsoleti/non validi.</span><span class="sxs-lookup"><span data-stu-id="ffd83-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="ffd83-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="ffd83-175">properties.query</span></span> |<span data-ttu-id="ffd83-176">**Obbligatoria**.</span><span class="sxs-lookup"><span data-stu-id="ffd83-176">**Required**.</span></span> <span data-ttu-id="ffd83-177">Query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ffd83-177">The search query.</span></span> |
| <span data-ttu-id="ffd83-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="ffd83-178">properties.displayName</span></span> |<span data-ttu-id="ffd83-179">**Obbligatoria**.</span><span class="sxs-lookup"><span data-stu-id="ffd83-179">**Required**.</span></span> <span data-ttu-id="ffd83-180">Nome visualizzato della query, definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="ffd83-180">The user-defined display name of the query.</span></span> |
| <span data-ttu-id="ffd83-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="ffd83-181">properties.category</span></span> |<span data-ttu-id="ffd83-182">**Obbligatoria**.</span><span class="sxs-lookup"><span data-stu-id="ffd83-182">**Required**.</span></span> <span data-ttu-id="ffd83-183">Categoria della query, definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="ffd83-183">The user-defined category of the query.</span></span> |

> [!NOTE]
> <span data-ttu-id="ffd83-184">L'API di ricerca di Log Analytics restituisce attualmente le ricerche salvate create dall'utente quando viene eseguito il polling di ricerche salvate in un'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ffd83-184">The Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="ffd83-185">L'API non restituisce le ricerche salvate fornite dalle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="ffd83-185">The API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="ffd83-186">Creare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="ffd83-186">Create saved searches</span></span>
<span data-ttu-id="ffd83-187">**Richiesta:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="ffd83-188">Il nome per tutte le ricerche salvate, per le pianificazioni e per le azioni create con l'API Log Analytics deve essere in minuscolo.</span><span class="sxs-lookup"><span data-stu-id="ffd83-188">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="ffd83-189">Eliminare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="ffd83-189">Delete saved searches</span></span>
<span data-ttu-id="ffd83-190">**Richiesta:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="ffd83-191">Aggiornare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="ffd83-191">Update saved searches</span></span>
 <span data-ttu-id="ffd83-192">**Richiesta:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="ffd83-193">Metadati - Solo JSON</span><span class="sxs-lookup"><span data-stu-id="ffd83-193">Metadata - JSON only</span></span>
<span data-ttu-id="ffd83-194">Ecco come visualizzare i campi per tutti i tipi di log per i dati raccolti nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ffd83-194">Here’s a way to see the fields for all log types for the data collected in your workspace.</span></span> <span data-ttu-id="ffd83-195">Ad esempio, se si vuole sapere se il tipo di evento include un campo denominato Computer, questa query rappresenta uno dei modi per controllare.</span><span class="sxs-lookup"><span data-stu-id="ffd83-195">For example, if you want you know if the Event type has a field named Computer, then this query is one way to check.</span></span>

<span data-ttu-id="ffd83-196">**Richiesta di campi:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="ffd83-197">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-197">**Response:**</span></span>

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

<span data-ttu-id="ffd83-198">La tabella seguente descrive le proprietà disponibili.</span><span class="sxs-lookup"><span data-stu-id="ffd83-198">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="ffd83-199">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="ffd83-199">**Property**</span></span> | <span data-ttu-id="ffd83-200">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="ffd83-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="ffd83-201">name</span><span class="sxs-lookup"><span data-stu-id="ffd83-201">name</span></span> |<span data-ttu-id="ffd83-202">Nome del campo.</span><span class="sxs-lookup"><span data-stu-id="ffd83-202">Field name.</span></span> |
| <span data-ttu-id="ffd83-203">displayName</span><span class="sxs-lookup"><span data-stu-id="ffd83-203">displayName</span></span> |<span data-ttu-id="ffd83-204">Nome visualizzato del campo.</span><span class="sxs-lookup"><span data-stu-id="ffd83-204">The display name of the field.</span></span> |
| <span data-ttu-id="ffd83-205">type</span><span class="sxs-lookup"><span data-stu-id="ffd83-205">type</span></span> |<span data-ttu-id="ffd83-206">Tipo del valore del campo.</span><span class="sxs-lookup"><span data-stu-id="ffd83-206">The Type of the field value.</span></span> |
| <span data-ttu-id="ffd83-207">facetable</span><span class="sxs-lookup"><span data-stu-id="ffd83-207">facetable</span></span> |<span data-ttu-id="ffd83-208">Combinazione delle proprietà "indexed", "stored" e "facet" attuali.</span><span class="sxs-lookup"><span data-stu-id="ffd83-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="ffd83-209">display</span><span class="sxs-lookup"><span data-stu-id="ffd83-209">display</span></span> |<span data-ttu-id="ffd83-210">Proprietà "display" attuale.</span><span class="sxs-lookup"><span data-stu-id="ffd83-210">Current ‘display’ property.</span></span> <span data-ttu-id="ffd83-211">True se il campo è visibile nella ricerca.</span><span class="sxs-lookup"><span data-stu-id="ffd83-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="ffd83-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="ffd83-212">ownerType</span></span> |<span data-ttu-id="ffd83-213">Ridotta solo ai tipi appartenenti agli indirizzi IP caricati.</span><span class="sxs-lookup"><span data-stu-id="ffd83-213">Reduced to only Types belonging to onboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="ffd83-214">Parametri facoltativi</span><span class="sxs-lookup"><span data-stu-id="ffd83-214">Optional parameters</span></span>
<span data-ttu-id="ffd83-215">Le informazioni seguenti illustrano i parametri facoltativi disponibili.</span><span class="sxs-lookup"><span data-stu-id="ffd83-215">The following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="ffd83-216">Evidenziazione</span><span class="sxs-lookup"><span data-stu-id="ffd83-216">Highlighting</span></span>
<span data-ttu-id="ffd83-217">Il parametro "Highlight" è un parametro facoltativo che può essere usato per richiedere che il sottosistema di ricerca includa un set di marcatori nella risposta.</span><span class="sxs-lookup"><span data-stu-id="ffd83-217">The “Highlight” parameter is an optional parameter you may use to request the search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="ffd83-218">Questi marcatori indicano l'inizio e la fine del testo evidenziato che corrisponde ai termini forniti nella query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ffd83-218">These markers indicate the start and end highlighted text that matches the terms provided in your search query.</span></span>
<span data-ttu-id="ffd83-219">È possibile specificare i marcatori di inizio e di fine che vengono usati dalla ricerca per eseguire il wrapping del termine evidenziato.</span><span class="sxs-lookup"><span data-stu-id="ffd83-219">You may specify the start and end markers that are used by search to wrap the highlighted term.</span></span>

<span data-ttu-id="ffd83-220">**Query di ricerca di esempio**</span><span class="sxs-lookup"><span data-stu-id="ffd83-220">**Example search query**</span></span>

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

<span data-ttu-id="ffd83-221">**Risultati di esempio:**</span><span class="sxs-lookup"><span data-stu-id="ffd83-221">**Sample result:**</span></span>

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

<span data-ttu-id="ffd83-222">Si noti che il risultato precedente contiene un messaggio di errore con prefisso e suffisso.</span><span class="sxs-lookup"><span data-stu-id="ffd83-222">Notice that the preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="ffd83-223">Gruppi di computer</span><span class="sxs-lookup"><span data-stu-id="ffd83-223">Computer groups</span></span>
<span data-ttu-id="ffd83-224">I gruppi di computer sono ricerche salvate speciali che restituiscono un set di computer.</span><span class="sxs-lookup"><span data-stu-id="ffd83-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="ffd83-225">È possibile usare un gruppo di computer in altre query per limitare i risultati ai computer nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="ffd83-225">You can use a computer group in other queries to limit the results to the computers in the group.</span></span>  <span data-ttu-id="ffd83-226">Un gruppo di computer viene implementato come una ricerca salvata con un tag Gruppo con il valore Computer.</span><span class="sxs-lookup"><span data-stu-id="ffd83-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="ffd83-227">Di seguito viene riportata una risposta di esempio per un gruppo di computer.</span><span class="sxs-lookup"><span data-stu-id="ffd83-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="ffd83-228">Recupero dei gruppi di computer</span><span class="sxs-lookup"><span data-stu-id="ffd83-228">Retrieving computer groups</span></span>
<span data-ttu-id="ffd83-229">Per recuperare un gruppo di computer, usare il metodo Get con l'ID del gruppo.</span><span class="sxs-lookup"><span data-stu-id="ffd83-229">To retrieve a computer group, use the Get method with the group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="ffd83-230">Creazione o aggiornamento di un gruppo di computer</span><span class="sxs-lookup"><span data-stu-id="ffd83-230">Creating or updating a computer group</span></span>
<span data-ttu-id="ffd83-231">Per creare un gruppo di computer, usare il metodo Put con un ID di ricerca salvato univoco.</span><span class="sxs-lookup"><span data-stu-id="ffd83-231">To create a computer group, use the Put method with a unique saved search ID.</span></span> <span data-ttu-id="ffd83-232">Se si usa un ID di gruppo di computer esistente, tale gruppo viene modificato.</span><span class="sxs-lookup"><span data-stu-id="ffd83-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="ffd83-233">Quando si crea un gruppo di computer nel portale di Log Analytics, l'ID viene creato dal gruppo e dal nome.</span><span class="sxs-lookup"><span data-stu-id="ffd83-233">When you create a computer group in the Log Analytics portal, then the ID is created from the group and name.</span></span>

<span data-ttu-id="ffd83-234">La query usata per la definizione del gruppo deve restituire un insieme di computer per il gruppo per funzionare correttamente.</span><span class="sxs-lookup"><span data-stu-id="ffd83-234">The query used for the group definition must return a set of computers for the group to function properly.</span></span>  <span data-ttu-id="ffd83-235">È consigliabile concludere la query con `| Distinct Computer` per assicurarsi che vengano restituiti i dati corretti.</span><span class="sxs-lookup"><span data-stu-id="ffd83-235">It's recommended that you end your query with `| Distinct Computer` to ensure the correct data is returned.</span></span>

<span data-ttu-id="ffd83-236">La definizione di una ricerca salvata deve includere un tag denominato Gruppo con un valore Computer affinché la ricerca venga classificata come un gruppo di computer.</span><span class="sxs-lookup"><span data-stu-id="ffd83-236">The definition of the saved search must include a tag named Group with a value of Computer for the search to be classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="ffd83-237">Eliminazione di gruppi di computer</span><span class="sxs-lookup"><span data-stu-id="ffd83-237">Deleting computer groups</span></span>
<span data-ttu-id="ffd83-238">Per eliminare un gruppo di computer, usare il metodo Delete con l'ID del gruppo.</span><span class="sxs-lookup"><span data-stu-id="ffd83-238">To delete a computer group, use the Delete method with the group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="ffd83-239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ffd83-239">Next steps</span></span>
* <span data-ttu-id="ffd83-240">Per informazioni su come creare query usando i campi personalizzati come criteri, vedere l'articolo relativo alle [ricerche nei log](log-analytics-log-searches.md) .</span><span class="sxs-lookup"><span data-stu-id="ffd83-240">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
