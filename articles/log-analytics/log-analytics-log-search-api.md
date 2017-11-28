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
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="9316d-103">API REST di Log Analytics per la ricerca nei log</span><span class="sxs-lookup"><span data-stu-id="9316d-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="9316d-104">Questa guida fornisce un'esercitazione di base, inclusi gli esempi, utilizzo di API REST di ricerca di Log Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="9316d-105">Log Analitica fa parte di hello Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="9316d-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="9316d-106">Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi è necessario continuare linguaggio di query legacy hello toouse con API di ricerca log hello come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9316d-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="9316d-107">Verrà rilasciata una nuova API per le aree di lavoro aggiornati e documentazione hello verrà aggiornata in quel momento.</span><span class="sxs-lookup"><span data-stu-id="9316d-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="9316d-108">Log Analitica era precedentemente denominato Operational Insights, perché è il nome di hello utilizzato nel provider di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="9316d-109">Panoramica dell'API REST di ricerca Log hello</span><span class="sxs-lookup"><span data-stu-id="9316d-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="9316d-110">API REST di ricerca di Log Analitica Hello è RESTful e accessibile tramite hello API di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9316d-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="9316d-111">In questo articolo vengono forniti esempi di accesso tramite API di hello [ARMClient](https://github.com/projectkudu/ARMClient), uno strumento da riga di comando open source che semplifica la chiamata hello API di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9316d-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="9316d-112">utilizzo di Hello di ARMClient è una delle numerose opzioni tooaccess hello API di ricerca Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="9316d-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="9316d-113">Un'altra opzione consiste modulo di Azure PowerShell hello toouse per OperationalInsights, che include i cmdlet per l'accesso a ricerca.</span><span class="sxs-lookup"><span data-stu-id="9316d-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="9316d-114">Con questi strumenti, è possibile utilizzare le aree di lavoro di hello API di gestione risorse di Azure toomake chiamate tooOMS ed eseguire i comandi di ricerca al loro interno.</span><span class="sxs-lookup"><span data-stu-id="9316d-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="9316d-115">Hello API restituisce i risultati della ricerca in formato JSON, che consente i risultati della ricerca toouse hello in molti modi diversi a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="9316d-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="9316d-116">Hello Azure Resource Manager può essere utilizzato tramite un [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) hello e [API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="9316d-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="9316d-117">toolearn, esaminare le pagine web hello collegato.</span><span class="sxs-lookup"><span data-stu-id="9316d-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="9316d-118">Se si utilizza un comando di aggregazione, ad esempio `|measure count()` o `distinct`, toosearch ogni chiamata può restituire fino a 500.000 record.</span><span class="sxs-lookup"><span data-stu-id="9316d-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="9316d-119">Le ricerche che non includono un comando di aggregazione restituiscono fino a 5.000 record.</span><span class="sxs-lookup"><span data-stu-id="9316d-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="9316d-120">Esercitazione di base sull'API REST di ricerca di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9316d-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="9316d-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="9316d-121">toouse ARMClient</span></span>
1. <span data-ttu-id="9316d-122">Installare [Chocolatey](https://chocolatey.org/), un gestore di pacchetti open source per Windows.</span><span class="sxs-lookup"><span data-stu-id="9316d-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="9316d-123">Aprire una finestra del prompt dei comandi come amministratore, quindi eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9316d-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="9316d-124">Installare l'ARMClient eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9316d-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="9316d-125">tooperform una ricerca usando ARMClient</span><span class="sxs-lookup"><span data-stu-id="9316d-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="9316d-126">Effettuare l'accesso usando il proprio account Microsoft oppure l'account aziendale o dell'istituto di istruzione:</span><span class="sxs-lookup"><span data-stu-id="9316d-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="9316d-127">Un account di accesso ha esito positivo sono elencate tutte le sottoscrizioni associate toohello, account indicato:</span><span class="sxs-lookup"><span data-stu-id="9316d-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="9316d-128">Ottenere le aree di lavoro di hello Operations Management Suite:</span><span class="sxs-lookup"><span data-stu-id="9316d-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="9316d-129">Una chiamata Get riuscita genera che tutte le aree di lavoro collegata toohello sottoscrizione:</span><span class="sxs-lookup"><span data-stu-id="9316d-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

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
3. <span data-ttu-id="9316d-130">Creare la variabile di ricerca.</span><span class="sxs-lookup"><span data-stu-id="9316d-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="9316d-131">Eseguire la ricerca usando la nuova variabile di ricerca.</span><span class="sxs-lookup"><span data-stu-id="9316d-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="9316d-132">Esempi di riferimento per l'API REST di ricerca di Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9316d-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="9316d-133">Hello seguono esempi Mostra come usare hello API di ricerca.</span><span class="sxs-lookup"><span data-stu-id="9316d-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="9316d-134">Ricerca - Azione/Lettura</span><span class="sxs-lookup"><span data-stu-id="9316d-134">Search - Action/Read</span></span>
<span data-ttu-id="9316d-135">**Url di esempio:**</span><span class="sxs-lookup"><span data-stu-id="9316d-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="9316d-136">**Richiesta:**</span><span class="sxs-lookup"><span data-stu-id="9316d-136">**Request:**</span></span>

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
<span data-ttu-id="9316d-137">Hello nella tabella seguente vengono descritte le proprietà di hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="9316d-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="9316d-138">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="9316d-138">**Property**</span></span> | <span data-ttu-id="9316d-139">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9316d-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="9316d-140">top</span><span class="sxs-lookup"><span data-stu-id="9316d-140">top</span></span> |<span data-ttu-id="9316d-141">numero massimo di Hello di tooreturn risultati.</span><span class="sxs-lookup"><span data-stu-id="9316d-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="9316d-142">highlight</span><span class="sxs-lookup"><span data-stu-id="9316d-142">highlight</span></span> |<span data-ttu-id="9316d-143">Contiene i parametri pre e post, in genere usati per evidenziare i campi corrispondenti</span><span class="sxs-lookup"><span data-stu-id="9316d-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="9316d-144">pre</span><span class="sxs-lookup"><span data-stu-id="9316d-144">pre</span></span> |<span data-ttu-id="9316d-145">Prefissi hello data i campi stringa tooyour corrispondente.</span><span class="sxs-lookup"><span data-stu-id="9316d-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="9316d-146">post</span><span class="sxs-lookup"><span data-stu-id="9316d-146">post</span></span> |<span data-ttu-id="9316d-147">Accoda hello data i campi stringa tooyour corrispondente.</span><span class="sxs-lookup"><span data-stu-id="9316d-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="9316d-148">query</span><span class="sxs-lookup"><span data-stu-id="9316d-148">query</span></span> |<span data-ttu-id="9316d-149">query di ricerca Hello utilizzato toocollect e restituire risultati.</span><span class="sxs-lookup"><span data-stu-id="9316d-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="9316d-150">start</span><span class="sxs-lookup"><span data-stu-id="9316d-150">start</span></span> |<span data-ttu-id="9316d-151">inizio di Hello dell'intervallo di tempo hello desiderato toobe risultati trovato da.</span><span class="sxs-lookup"><span data-stu-id="9316d-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="9316d-152">end</span><span class="sxs-lookup"><span data-stu-id="9316d-152">end</span></span> |<span data-ttu-id="9316d-153">fine di Hello dell'intervallo di tempo hello desiderato toobe risultati trovato da.</span><span class="sxs-lookup"><span data-stu-id="9316d-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="9316d-154">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="9316d-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="9316d-155">Ricerca/{ID} - Azione/Lettura</span><span class="sxs-lookup"><span data-stu-id="9316d-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="9316d-156">**Contenuto della richiesta hello di una ricerca salvata:**</span><span class="sxs-lookup"><span data-stu-id="9316d-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="9316d-157">Se hello ricerca restituisce lo stato 'Sospeso', il polling risultati di hello aggiornato è possibile farlo tramite questa API.</span><span class="sxs-lookup"><span data-stu-id="9316d-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="9316d-158">Dopo 6 min, hello risultato della ricerca hello verrà rimosso dalla cache di hello e sarà restituito HTTP Gone.</span><span class="sxs-lookup"><span data-stu-id="9316d-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="9316d-159">Se la richiesta di ricerca iniziale hello restituisce immediatamente lo stato 'Riuscito', i risultati di hello non vengono aggiunti cache toohello causano questo tooreturn API HTTP Gone se eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="9316d-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="9316d-160">il contenuto di Hello di un risultato HTTP 200 è in hello stesso formato delle richiesta di ricerca iniziale hello solo con i valori aggiornati.</span><span class="sxs-lookup"><span data-stu-id="9316d-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="9316d-161">Ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="9316d-161">Saved searches</span></span>
<span data-ttu-id="9316d-162">**Elenco di richieste delle ricerche salvate:**</span><span class="sxs-lookup"><span data-stu-id="9316d-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="9316d-163">Metodi supportati: GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="9316d-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="9316d-164">Metodi di raccolta supportati: GET</span><span class="sxs-lookup"><span data-stu-id="9316d-164">Supported collection methods: GET</span></span>

<span data-ttu-id="9316d-165">Hello nella tabella seguente vengono descritte le proprietà di hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="9316d-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="9316d-166">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9316d-166">Property</span></span> | <span data-ttu-id="9316d-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9316d-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9316d-168">ID</span><span class="sxs-lookup"><span data-stu-id="9316d-168">Id</span></span> |<span data-ttu-id="9316d-169">Identificatore univoco di Hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-169">hello unique identifier.</span></span> |
| <span data-ttu-id="9316d-170">ETag</span><span class="sxs-lookup"><span data-stu-id="9316d-170">Etag</span></span> |<span data-ttu-id="9316d-171">**Obbligatoria per l'applicazione di patch**.</span><span class="sxs-lookup"><span data-stu-id="9316d-171">**Required for Patch**.</span></span> <span data-ttu-id="9316d-172">Aggiornata dal server a ogni scrittura.</span><span class="sxs-lookup"><span data-stu-id="9316d-172">Updated by server on each write.</span></span> <span data-ttu-id="9316d-173">Valore deve essere uguale toohello corrente archiviato o ' *' tooupdate.</span><span class="sxs-lookup"><span data-stu-id="9316d-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="9316d-174">Viene restituito il codice 409 per i valori obsoleti/non validi.</span><span class="sxs-lookup"><span data-stu-id="9316d-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="9316d-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="9316d-175">properties.query</span></span> |<span data-ttu-id="9316d-176">**Obbligatoria**.</span><span class="sxs-lookup"><span data-stu-id="9316d-176">**Required**.</span></span> <span data-ttu-id="9316d-177">query di ricerca Hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-177">hello search query.</span></span> |
| <span data-ttu-id="9316d-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="9316d-178">properties.displayName</span></span> |<span data-ttu-id="9316d-179">**Obbligatoria**.</span><span class="sxs-lookup"><span data-stu-id="9316d-179">**Required**.</span></span> <span data-ttu-id="9316d-180">nome di visualizzazione definite dall'utente Hello di query hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="9316d-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="9316d-181">properties.category</span></span> |<span data-ttu-id="9316d-182">**Obbligatoria**.</span><span class="sxs-lookup"><span data-stu-id="9316d-182">**Required**.</span></span> <span data-ttu-id="9316d-183">categoria definita dall'utente Hello di query hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="9316d-184">API di ricerca Log Analitica Hello attualmente restituisce creati dall'utente ricerche al polling di ricerche salvate in un'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9316d-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="9316d-185">Hello API non restituisce le ricerche salvate fornite dalle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="9316d-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="9316d-186">Creare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="9316d-186">Create saved searches</span></span>
<span data-ttu-id="9316d-187">**Richiesta:**</span><span class="sxs-lookup"><span data-stu-id="9316d-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="9316d-188">nome Hello per le ricerche salvate tutte, pianificazioni e le azioni create con hello Log Analitica API deve essere in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="9316d-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="9316d-189">Eliminare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="9316d-189">Delete saved searches</span></span>
<span data-ttu-id="9316d-190">**Richiesta:**</span><span class="sxs-lookup"><span data-stu-id="9316d-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="9316d-191">Aggiornare le ricerche salvate</span><span class="sxs-lookup"><span data-stu-id="9316d-191">Update saved searches</span></span>
 <span data-ttu-id="9316d-192">**Richiesta:**</span><span class="sxs-lookup"><span data-stu-id="9316d-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="9316d-193">Metadati - Solo JSON</span><span class="sxs-lookup"><span data-stu-id="9316d-193">Metadata - JSON only</span></span>
<span data-ttu-id="9316d-194">Ecco i campi di hello toosee un modo per tutti i tipi di log per i dati di hello raccolti nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9316d-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="9316d-195">Ad esempio, se si desidera che sapere se hello tipo di evento include un campo denominato Computer, questa query è un modo toocheck.</span><span class="sxs-lookup"><span data-stu-id="9316d-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="9316d-196">**Richiesta di campi:**</span><span class="sxs-lookup"><span data-stu-id="9316d-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="9316d-197">**Risposta:**</span><span class="sxs-lookup"><span data-stu-id="9316d-197">**Response:**</span></span>

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

<span data-ttu-id="9316d-198">Hello nella tabella seguente vengono descritte le proprietà di hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="9316d-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="9316d-199">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="9316d-199">**Property**</span></span> | <span data-ttu-id="9316d-200">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="9316d-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="9316d-201">name</span><span class="sxs-lookup"><span data-stu-id="9316d-201">name</span></span> |<span data-ttu-id="9316d-202">Nome del campo.</span><span class="sxs-lookup"><span data-stu-id="9316d-202">Field name.</span></span> |
| <span data-ttu-id="9316d-203">displayName</span><span class="sxs-lookup"><span data-stu-id="9316d-203">displayName</span></span> |<span data-ttu-id="9316d-204">nome del campo hello è visualizzato Hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="9316d-205">type</span><span class="sxs-lookup"><span data-stu-id="9316d-205">type</span></span> |<span data-ttu-id="9316d-206">Tipo di valore del campo hello Hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="9316d-207">facetable</span><span class="sxs-lookup"><span data-stu-id="9316d-207">facetable</span></span> |<span data-ttu-id="9316d-208">Combinazione delle proprietà "indexed", "stored" e "facet" attuali.</span><span class="sxs-lookup"><span data-stu-id="9316d-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="9316d-209">display</span><span class="sxs-lookup"><span data-stu-id="9316d-209">display</span></span> |<span data-ttu-id="9316d-210">Proprietà "display" attuale.</span><span class="sxs-lookup"><span data-stu-id="9316d-210">Current ‘display’ property.</span></span> <span data-ttu-id="9316d-211">True se il campo è visibile nella ricerca.</span><span class="sxs-lookup"><span data-stu-id="9316d-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="9316d-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="9316d-212">ownerType</span></span> |<span data-ttu-id="9316d-213">Tipi di tooonly ridotta appartenenti tooonboarded indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="9316d-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="9316d-214">Parametri facoltativi</span><span class="sxs-lookup"><span data-stu-id="9316d-214">Optional parameters</span></span>
<span data-ttu-id="9316d-215">le seguenti informazioni Hello descrive i parametri facoltativi disponibili.</span><span class="sxs-lookup"><span data-stu-id="9316d-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="9316d-216">Evidenziazione</span><span class="sxs-lookup"><span data-stu-id="9316d-216">Highlighting</span></span>
<span data-ttu-id="9316d-217">il parametro "Highlight" Hello è un parametro facoltativo, è possibile utilizzare sottosistema di ricerca hello toorequest includa un set di marcatori nella risposta.</span><span class="sxs-lookup"><span data-stu-id="9316d-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="9316d-218">Questi marcatori indicano hello inizio e fine del testo evidenziato che corrisponde hello termini forniti nella query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="9316d-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="9316d-219">È possibile specificare hello inizio e fine marcatori utilizzati dal termine di ricerca toowrap hello evidenziato.</span><span class="sxs-lookup"><span data-stu-id="9316d-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="9316d-220">**Query di ricerca di esempio**</span><span class="sxs-lookup"><span data-stu-id="9316d-220">**Example search query**</span></span>

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

<span data-ttu-id="9316d-221">**Risultati di esempio:**</span><span class="sxs-lookup"><span data-stu-id="9316d-221">**Sample result:**</span></span>

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

<span data-ttu-id="9316d-222">Si noti che hello risultato precedente contiene un messaggio di errore con il prefisso e suffisso.</span><span class="sxs-lookup"><span data-stu-id="9316d-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="9316d-223">Gruppi di computer</span><span class="sxs-lookup"><span data-stu-id="9316d-223">Computer groups</span></span>
<span data-ttu-id="9316d-224">I gruppi di computer sono ricerche salvate speciali che restituiscono un set di computer.</span><span class="sxs-lookup"><span data-stu-id="9316d-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="9316d-225">È possibile utilizzare un gruppo di computer in altri computer toohello risultati di query toolimit hello gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="9316d-226">Un gruppo di computer viene implementato come una ricerca salvata con un tag Gruppo con il valore Computer.</span><span class="sxs-lookup"><span data-stu-id="9316d-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="9316d-227">Di seguito viene riportata una risposta di esempio per un gruppo di computer.</span><span class="sxs-lookup"><span data-stu-id="9316d-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="9316d-228">Recupero dei gruppi di computer</span><span class="sxs-lookup"><span data-stu-id="9316d-228">Retrieving computer groups</span></span>
<span data-ttu-id="9316d-229">ID di un gruppo di computer, hello di utilizzare il metodo Get con gruppo hello tooretrieve</span><span class="sxs-lookup"><span data-stu-id="9316d-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="9316d-230">Creazione o aggiornamento di un gruppo di computer</span><span class="sxs-lookup"><span data-stu-id="9316d-230">Creating or updating a computer group</span></span>
<span data-ttu-id="9316d-231">toocreate un gruppo di computer, utilizzare il metodo Put hello con un ID univoco di ricerca salvata.</span><span class="sxs-lookup"><span data-stu-id="9316d-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="9316d-232">Se si usa un ID di gruppo di computer esistente, tale gruppo viene modificato.</span><span class="sxs-lookup"><span data-stu-id="9316d-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="9316d-233">Quando si crea un gruppo di computer nel portale di hello Log Analitica, hello ID viene creato dal nome e gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="9316d-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="9316d-234">query Hello utilizzato per la definizione di gruppo hello deve restituire un set di computer per hello gruppo toofunction correttamente.</span><span class="sxs-lookup"><span data-stu-id="9316d-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="9316d-235">È consigliabile che si termina la query con `| Distinct Computer` tooensure hello corretto i dati vengono restituiti.</span><span class="sxs-lookup"><span data-stu-id="9316d-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="9316d-236">definizione di Hello di hello ricerca salvata deve includere un tag denominato gruppo con un valore del Computer per hello ricerca toobe classificati come un gruppo di computer.</span><span class="sxs-lookup"><span data-stu-id="9316d-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="9316d-237">Eliminazione di gruppi di computer</span><span class="sxs-lookup"><span data-stu-id="9316d-237">Deleting computer groups</span></span>
<span data-ttu-id="9316d-238">ID di un gruppo di computer, hello di utilizzare il metodo Delete con gruppo hello toodelete</span><span class="sxs-lookup"><span data-stu-id="9316d-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="9316d-239">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9316d-239">Next steps</span></span>
* <span data-ttu-id="9316d-240">Informazioni su [log ricerche](log-analytics-log-searches.md) toobuild query utilizzando i campi personalizzati per i criteri.</span><span class="sxs-lookup"><span data-stu-id="9316d-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
