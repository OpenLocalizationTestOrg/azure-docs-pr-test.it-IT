---
title: Procedura dettagliata sull'API REST di Monitoraggio di Azure | Microsoft Docs
description: Come autenticare le richieste e usare l'API REST di monitoraggio di Azure.
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: 454a85c4752ec9c7522ef147d5ce594ef5992c32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="0f84d-103">Procedura dettagliata sull'API REST di monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="0f84d-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="0f84d-104">In questo articolo viene illustrato come eseguire l'autenticazione in modo che il codice possa usare le [informazioni di riferimento sulle API REST di monitoraggio di Microsoft Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f84d-104">This article shows you how to perform authentication so your code can use the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="0f84d-105">L'API di monitoraggio di Azure consente di recuperare in modo programmatico le definizioni della metrica predefinita disponibili (cioè il tipo di metrica come tempo di CPU, richieste e così via), la granularità e i valori della metrica.</span><span class="sxs-lookup"><span data-stu-id="0f84d-105">The Azure Monitor API makes it possible to programmatically retrieve the available default metric definitions (the type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="0f84d-106">Dopo essere stati recuperati, i dati possono essere salvati in un archivio dati separato come il database SQL di Azure, Azure Cosmos DB o Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0f84d-106">Once retrieved, the data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="0f84d-107">Da qui, se necessario, è possibile svolgere ulteriori analisi.</span><span class="sxs-lookup"><span data-stu-id="0f84d-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="0f84d-108">Oltre a essere compatibile con vari punti dati della metrica, come illustrato in questo articolo, l'API di monitoraggio consente di elencare le regole di avviso, di visualizzare i registri delle attività e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="0f84d-108">Besides working with various metric data points, as this article demonstrates, the Monitor API makes it possible to list alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="0f84d-109">Per un elenco completo delle operazioni disponibili, vedere le [informazioni di riferimento sulle API REST di monitoraggio di Microsoft Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f84d-109">For a full list of available operations, see the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="0f84d-110">Autenticazione delle richieste di monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="0f84d-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="0f84d-111">Innanzitutto è necessario autenticare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="0f84d-111">The first step is to authenticate the request.</span></span>

<span data-ttu-id="0f84d-112">Tutte le attività eseguite sull'API di monitoraggio di Azure usano il modello di autenticazione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0f84d-112">All the tasks executed against the Azure Monitor API use the Azure Resource Manager authentication model.</span></span> <span data-ttu-id="0f84d-113">Di conseguenza, tutte le richieste devono essere autenticate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f84d-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0f84d-114">Un approccio per autenticare l'applicazione client consiste nel creare un'entità servizio di Azure AD e recuperare il token di autenticazione (JTW).</span><span class="sxs-lookup"><span data-stu-id="0f84d-114">One approach to authenticate the client application is to create an Azure AD service principal and retrieve the authentication (JWT) token.</span></span> <span data-ttu-id="0f84d-115">Il seguente script di esempio mostra la creazione di un'entità servizio di Azure AD tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f84d-115">The following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="0f84d-116">Per una procedura più dettagliata, fare riferimento alla documentazione sull' [uso di Azure PowerShell per creare un'entità servizio per accedere alle risorse](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="0f84d-116">For a more detailed walk-through, refer to the documentation on [using Azure PowerShell to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="0f84d-117">È possibile anche [creare un'entità di sicurezza tramite il portale di Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0f84d-117">It is also possible to [create a service principal via the Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate to a specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for the service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with the designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role to the newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

<span data-ttu-id="0f84d-118">Per eseguire query nell'API di monitoraggio di Azure, l'applicazione client deve effettuare l'autenticazione usando l'entità servizio creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0f84d-118">To query the Azure Monitor API, the client application should use the previously created service principal to authenticate.</span></span> <span data-ttu-id="0f84d-119">Nel seguente esempio di script di PowerShell di esempio viene illustrato un approccio in cui viene usato [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) per ottenere il token di autenticazione JTW.</span><span class="sxs-lookup"><span data-stu-id="0f84d-119">The following example PowerShell script shows one approach, using the [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) to help get the JWT authentication token.</span></span> <span data-ttu-id="0f84d-120">Il token JTW viene trasmesso come parte di un parametro di autorizzazione HTTP nelle richieste all'API di Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f84d-120">The JWT token is passed as part of an HTTP Authorization parameter in requests to the Azure Monitor REST API.</span></span>

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

<span data-ttu-id="0f84d-121">Una volta completato il passaggio di configurazione dell'autenticazione, è possibile eseguire le query con l'API REST di monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f84d-121">Once the authentication setup step is complete, queries can then be executed against the Azure Monitor REST API.</span></span> <span data-ttu-id="0f84d-122">Esistono due query utili:</span><span class="sxs-lookup"><span data-stu-id="0f84d-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="0f84d-123">Elencare le definizioni delle metriche per una risorsa</span><span class="sxs-lookup"><span data-stu-id="0f84d-123">List the metric definitions for a resource</span></span>
2. <span data-ttu-id="0f84d-124">Recuperare i valori delle metriche</span><span class="sxs-lookup"><span data-stu-id="0f84d-124">Retrieve the metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="0f84d-125">Recuperare le definizioni delle metriche</span><span class="sxs-lookup"><span data-stu-id="0f84d-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="0f84d-126">Per recuperare le definizioni delle metriche mediante l'API REST di monitoraggio di Azure, usare "2016-03-01" come versione dell'API.</span><span class="sxs-lookup"><span data-stu-id="0f84d-126">To retrieve metric definitions using the Azure Monitor REST API, use "2016-03-01" as the API version.</span></span>
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
<span data-ttu-id="0f84d-127">Per un'app per la logica di Azure, le definizioni delle metriche avranno un aspetto simile alla schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="0f84d-127">For an Azure Logic App, the metric definitions would appear similar to the following screenshot:</span></span>

![Alt "Visualizzazione JSON della risposta alle definizioni delle metriche"](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="0f84d-129">Per ulteriori informazioni, vedere la documentazione [Elencare le definizioni delle metriche per una risorsa nell'API REST di monitoraggio di Azure](https://msdn.microsoft.com/library/azure/mt743621.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0f84d-129">For more information, see the [List the metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="0f84d-130">Recuperare i valori delle metriche</span><span class="sxs-lookup"><span data-stu-id="0f84d-130">Retrieve Metric Values</span></span>
<span data-ttu-id="0f84d-131">Una volta che le definizioni delle metriche disponibili sono note, è possibile recuperare i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="0f84d-131">Once the available metric definitions are known, it is then possible to retrieve the related metric values.</span></span> <span data-ttu-id="0f84d-132">Usare il 'valore' del nome della metrica (non ' localizedValue') per tutte le richieste di filtro (ad esempio, per recuperare i punti dati delle metriche 'CpuTime' e 'Requests').</span><span class="sxs-lookup"><span data-stu-id="0f84d-132">Use the metric’s name ‘value’ (not the ‘localizedValue’) for any filtering requests (for example, retrieve the ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="0f84d-133">Se non è specificato alcun filtro, viene restituita la metrica predefinita.</span><span class="sxs-lookup"><span data-stu-id="0f84d-133">If no filters are specified, the default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="0f84d-134">Per recuperare i valori delle metriche mediante l'API REST di monitoraggio di Azure, usare "2016-06-01" come versione dell'API.</span><span class="sxs-lookup"><span data-stu-id="0f84d-134">To retrieve metric values using the Azure Monitor REST API, use "2016-06-01" as the API version.</span></span>
>
>

<span data-ttu-id="0f84d-135">**Metodo**: GET</span><span class="sxs-lookup"><span data-stu-id="0f84d-135">**Method**: GET</span></span>

<span data-ttu-id="0f84d-136">**URI richiesta**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="0f84d-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="0f84d-137">Ad esempio, per recuperare i dati della metrica RunsSucceeded per la finestra temporale specificata e per un intervallo di tempo di 1 ora, la richiesta sarà come mostrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0f84d-137">For example, to retrieve the RunsSucceeded metric data points for the given time range and for a time grain of 1 hour, the request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="0f84d-138">Il risultato sarà simile alla seguente schermata di esempio:</span><span class="sxs-lookup"><span data-stu-id="0f84d-138">The result would appear similar to the example following screenshot:</span></span>

![Alt "Risposta JSON che mostra il valore della metrica per il tempo medio di risposta"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="0f84d-140">Per recuperare più punti dati o di aggregazione, aggiungere i nomi delle definizioni delle metriche e i tipi di aggregazione al filtro, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0f84d-140">To retrieve multiple data or aggregation points, add the metric definition names and aggregation types to the filter, as seen in the following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="0f84d-141">Usare ARMClient</span><span class="sxs-lookup"><span data-stu-id="0f84d-141">Use ARMClient</span></span>
<span data-ttu-id="0f84d-142">Un'alternativa all'uso di PowerShell (come illustrato in precedenza) consiste nell'usare [ARMClient](https://github.com/projectkudu/ARMClient) su computer Windows.</span><span class="sxs-lookup"><span data-stu-id="0f84d-142">An alternative to using PowerShell (as shown above), is to use [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="0f84d-143">ARMClient gestisce automaticamente l'autenticazione di Azure AD (e il token JTW risultante).</span><span class="sxs-lookup"><span data-stu-id="0f84d-143">ARMClient handles the Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="0f84d-144">Di seguito viene illustrato l'uso di ARMClient per recuperare i dati delle metriche:</span><span class="sxs-lookup"><span data-stu-id="0f84d-144">The following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="0f84d-145">Installare [Chocolatey](https://chocolatey.org/) e [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="0f84d-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="0f84d-146">In una finestra del terminale digitare *armclient.exe login*.</span><span class="sxs-lookup"><span data-stu-id="0f84d-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="0f84d-147">Viene richiesto di accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="0f84d-147">This prompts you to log in to Azure.</span></span>
3. <span data-ttu-id="0f84d-148">Digitare *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="0f84d-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="0f84d-149">Digitare *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="0f84d-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![Alt "Uso di ARMClient con l'API REST di monitoraggio di Azure"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-the-resource-id"></a><span data-ttu-id="0f84d-151">Recuperare l'ID risorsa</span><span class="sxs-lookup"><span data-stu-id="0f84d-151">Retrieve the Resource ID</span></span>
<span data-ttu-id="0f84d-152">L'uso dell'API REST può aiutare davvero a comprendere le definizioni delle metriche disponibili, la granularità e i valori correlati.</span><span class="sxs-lookup"><span data-stu-id="0f84d-152">Using the REST API can really help to understand the available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="0f84d-153">Tali informazioni sono utili quando si usa [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f84d-153">That information is helpful when using the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="0f84d-154">Per il codice precedente, l'ID risorsa da usare è il percorso completo verso la risorsa Azure desiderata.</span><span class="sxs-lookup"><span data-stu-id="0f84d-154">For the preceding code, the resource ID to use is the full path to the desired Azure resource.</span></span> <span data-ttu-id="0f84d-155">Ad esempio, per eseguire una query su un'App Web di Azure, l'ID risorsa potrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="0f84d-155">For example, to query against an Azure Web App, the resource ID would be:</span></span>

<span data-ttu-id="0f84d-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span><span class="sxs-lookup"><span data-stu-id="0f84d-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="0f84d-157">Il seguente elenco contiene alcuni esempi di formati di ID risorsa per le varie risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="0f84d-157">The following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="0f84d-158">**Hub IoT** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span><span class="sxs-lookup"><span data-stu-id="0f84d-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="0f84d-159">**Pool elastico di SQL** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span><span class="sxs-lookup"><span data-stu-id="0f84d-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="0f84d-160">**Database SQL (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span><span class="sxs-lookup"><span data-stu-id="0f84d-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="0f84d-161">**Bus di servizio** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span><span class="sxs-lookup"><span data-stu-id="0f84d-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="0f84d-162">**Set di scalabilità VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="0f84d-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="0f84d-163">**VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="0f84d-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="0f84d-164">**Hub eventi** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span><span class="sxs-lookup"><span data-stu-id="0f84d-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="0f84d-165">Esistono approcci alternativi per recuperare l'ID risorsa, tra cui l'uso di Esplora risorse di Azure, la visualizzazione della risorsa desiderata nel portale di Azure e tramite PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f84d-165">There are alternative approaches to retrieving the resource ID, including using Azure Resource Explorer, viewing the desired resource in the Azure portal, and via PowerShell or the Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="0f84d-166">Esplora risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="0f84d-166">Azure Resource Explorer</span></span>
<span data-ttu-id="0f84d-167">Per trovare l'ID risorsa per la risorsa desiderata, un approccio utile consiste nell'usare lo strumento [Esplora risorse di Azure](https://resources.azure.com) .</span><span class="sxs-lookup"><span data-stu-id="0f84d-167">To find the resource ID for a desired resource, one helpful approach is to use the [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="0f84d-168">Individuare la risorsa desiderata e quindi esaminare l'ID indicato, come illustrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="0f84d-168">Navigate to the desired resource and then look at the ID shown, as in the following screenshot:</span></span>

![Alt "Esplora risorse di Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="0f84d-170">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0f84d-170">Azure portal</span></span>
<span data-ttu-id="0f84d-171">L'ID risorsa può anche essere ottenuto dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f84d-171">The resource ID can also be obtained from the Azure portal.</span></span> <span data-ttu-id="0f84d-172">A tale scopo, accedere alla risorsa desiderata e scegliere Proprietà.</span><span class="sxs-lookup"><span data-stu-id="0f84d-172">To do so, navigate to the desired resource and then select Properties.</span></span> <span data-ttu-id="0f84d-173">L'ID risorsa viene visualizzato nel pannello Proprietà, come illustrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="0f84d-173">The Resource ID is displayed in the Properties blade, as seen in the following screenshot:</span></span>

![Alt "ID risorsa visualizzato nel pannello Proprietà del portale di Azure"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="0f84d-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f84d-175">Azure PowerShell</span></span>
<span data-ttu-id="0f84d-176">L'ID risorsa può essere recuperato anche tramite i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f84d-176">The resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="0f84d-177">Ad esempio, per ottenere l'ID risorsa per un'App Web di Azure, eseguire il cmdlet Get-AzureRmWebApp, come illustrato nella seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="0f84d-177">For example, to obtain the resource ID for an Azure Web App, execute the Get-AzureRmWebApp cmdlet, as in the following screenshot:</span></span>

![Alt "ID risorsa ottenuto tramite PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="0f84d-179">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0f84d-179">Azure CLI</span></span>
<span data-ttu-id="0f84d-180">Per recuperare l'ID risorsa tramite l'interfaccia della riga di comando di Azure, eseguire il comando 'azure webapp show', specificando l'opzione '-json' come mostrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="0f84d-180">To retrieve the resource ID using the Azure CLI, execute the 'azure webapp show' command, specifying the '--json' option, as shown in the following screenshot:</span></span>

![Alt "ID risorsa ottenuto tramite PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="0f84d-182">Recuperare i dati del registro attività</span><span class="sxs-lookup"><span data-stu-id="0f84d-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="0f84d-183">Oltre a lavorare con le definizioni delle metriche e i valori correlati, è anche possibile recuperare interessanti informazioni aggiuntive relative alle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f84d-183">In addition to working with metric definitions and related values, it is also possible to retrieve additional interesting insights related to Azure resources.</span></span> <span data-ttu-id="0f84d-184">Ad esempio, è possibile eseguire query sui dati del [registro attività](https://msdn.microsoft.com/library/azure/dn931934.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0f84d-184">As an example, it is possible to query [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="0f84d-185">Nell'esempio seguente viene illustrato l'uso dell'API REST di monitoraggio di Azure per eseguire query sui dati del registro attività all'interno di un intervallo di date specifico per una sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="0f84d-185">The following sample demonstrates using the Azure Monitor REST API to query activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="0f84d-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f84d-186">Next steps</span></span>
* <span data-ttu-id="0f84d-187">Esaminare la [panoramica sul monitoraggio](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f84d-187">Review the [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="0f84d-188">Visualizzare le [metriche supportate con il monitoraggio di Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0f84d-188">View the [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="0f84d-189">Esaminare le [informazioni di riferimento sulle API REST di monitoraggio di Microsoft Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f84d-189">Review the [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="0f84d-190">Esaminare [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f84d-190">Review the [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
