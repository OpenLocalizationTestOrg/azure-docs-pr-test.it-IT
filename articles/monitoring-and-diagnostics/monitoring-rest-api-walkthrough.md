---
title: aaaAzure procedura dettagliata di monitoraggio API REST | Documenti Microsoft
description: Come tooauthenticate richiede tooand utilizzare hello API REST di monitoraggio di Azure.
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
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="24e3e-103">Procedura dettagliata sull'API REST di monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="24e3e-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="24e3e-104">In questo articolo illustra come autenticazione tooperform in modo il codice può usare hello [riferimento all'API REST di Microsoft Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="24e3e-104">This article shows you how tooperform authentication so your code can use hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="24e3e-105">Hello API di monitoraggio di Azure rende possibili tooprogrammatically recuperare hello predefinite disponibili definizioni di metrica (tipo hello di metrica, ad esempio il tempo di CPU, le richieste e così via) e granularità valori della metrica.</span><span class="sxs-lookup"><span data-stu-id="24e3e-105">hello Azure Monitor API makes it possible tooprogrammatically retrieve hello available default metric definitions (hello type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="24e3e-106">Una volta recuperato, dati hello possono essere salvati in un archivio dati separato, ad esempio Database SQL di Azure, Azure Cosmos DB o Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="24e3e-106">Once retrieved, hello data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="24e3e-107">Da qui, se necessario, è possibile svolgere ulteriori analisi.</span><span class="sxs-lookup"><span data-stu-id="24e3e-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="24e3e-108">Oltre a funzionare con diversi punti dati di metrica, come illustrato di seguito in questo articolo, hello API monitoraggio rende le regole di avviso toolist possibili, visualizzare i log di attività e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="24e3e-108">Besides working with various metric data points, as this article demonstrates, hello Monitor API makes it possible toolist alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="24e3e-109">Per un elenco completo delle operazioni disponibili, vedere hello [riferimento all'API REST di Microsoft Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="24e3e-109">For a full list of available operations, see hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="24e3e-110">Autenticazione delle richieste di monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="24e3e-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="24e3e-111">primo passaggio Hello è richiesta hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="24e3e-111">hello first step is tooauthenticate hello request.</span></span>

<span data-ttu-id="24e3e-112">Tutte le attività hello eseguite sul modello l'autenticazione di hello API di monitoraggio di Azure usare hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="24e3e-112">All hello tasks executed against hello Azure Monitor API use hello Azure Resource Manager authentication model.</span></span> <span data-ttu-id="24e3e-113">Di conseguenza, tutte le richieste devono essere autenticate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24e3e-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="24e3e-114">Applicazione di un approccio tooauthenticate hello client è toocreate un'entità servizio di Azure AD e recuperare il token di autenticazione (JWT) hello.</span><span class="sxs-lookup"><span data-stu-id="24e3e-114">One approach tooauthenticate hello client application is toocreate an Azure AD service principal and retrieve hello authentication (JWT) token.</span></span> <span data-ttu-id="24e3e-115">Hello script di esempio seguente viene illustrato come creare un annuncio di Azure dell'entità servizio tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24e3e-115">hello following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="24e3e-116">Per una procedura dettagliata più dettagliata, consultare la documentazione di toohello su [utilizzando Azure PowerShell toocreate una risorse tooaccess dell'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="24e3e-116">For a more detailed walk-through, refer toohello documentation on [using Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="24e3e-117">È inoltre possibile troppo[creare un'entità servizio tramite il portale di Azure hello](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="24e3e-117">It is also possible too[create a service principal via hello Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

<span data-ttu-id="24e3e-118">hello tooquery API di monitoraggio di Azure, un'applicazione hello client deve utilizzare hello creato in precedenza tooauthenticate dell'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="24e3e-118">tooquery hello Azure Monitor API, hello client application should use hello previously created service principal tooauthenticate.</span></span> <span data-ttu-id="24e3e-119">Hello lo script di PowerShell di esempio seguente viene illustrato un approccio, hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp ottenere token JWT di hello autenticazione.</span><span class="sxs-lookup"><span data-stu-id="24e3e-119">hello following example PowerShell script shows one approach, using hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp get hello JWT authentication token.</span></span> <span data-ttu-id="24e3e-120">token JWT Hello viene passato come parte di un parametro di autorizzazione HTTP in toohello richieste API REST di monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="24e3e-120">hello JWT token is passed as part of an HTTP Authorization parameter in requests toohello Azure Monitor REST API.</span></span>

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

<span data-ttu-id="24e3e-121">Al termine del passaggio di installazione di hello autenticazione, le query possono quindi essere eseguite hello API REST di monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="24e3e-121">Once hello authentication setup step is complete, queries can then be executed against hello Azure Monitor REST API.</span></span> <span data-ttu-id="24e3e-122">Esistono due query utili:</span><span class="sxs-lookup"><span data-stu-id="24e3e-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="24e3e-123">Elenco di definizioni di metrica hello per una risorsa</span><span class="sxs-lookup"><span data-stu-id="24e3e-123">List hello metric definitions for a resource</span></span>
2. <span data-ttu-id="24e3e-124">Recuperare i valori della metrica hello</span><span class="sxs-lookup"><span data-stu-id="24e3e-124">Retrieve hello metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="24e3e-125">Recuperare le definizioni delle metriche</span><span class="sxs-lookup"><span data-stu-id="24e3e-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="24e3e-126">le definizioni delle metriche tooretrieve utilizzando hello API REST di monitoraggio di Azure, utilizzare "2016-03-01" hello versione API.</span><span class="sxs-lookup"><span data-stu-id="24e3e-126">tooretrieve metric definitions using hello Azure Monitor REST API, use "2016-03-01" as hello API version.</span></span>
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
<span data-ttu-id="24e3e-127">Per un'App di logica di Azure, le definizioni delle metriche hello appariranno simile toohello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="24e3e-127">For an Azure Logic App, hello metric definitions would appear similar toohello following screenshot:</span></span>

![Alt "Visualizzazione JSON della risposta alle definizioni delle metriche"](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="24e3e-129">Per ulteriori informazioni, vedere hello [elencare le definizioni delle metriche di hello per una risorsa nell'API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentazione.</span><span class="sxs-lookup"><span data-stu-id="24e3e-129">For more information, see hello [List hello metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="24e3e-130">Recuperare i valori delle metriche</span><span class="sxs-lookup"><span data-stu-id="24e3e-130">Retrieve Metric Values</span></span>
<span data-ttu-id="24e3e-131">Una volta hello disponibili le definizioni delle metriche sono noti, è quindi possibile tooretrieve hello valori metriche correlati.</span><span class="sxs-lookup"><span data-stu-id="24e3e-131">Once hello available metric definitions are known, it is then possible tooretrieve hello related metric values.</span></span> <span data-ttu-id="24e3e-132">Utilizzo nome 'value' della metrica hello (non hello 'localizedValue') per tutte le richieste di filtro (ad esempio, recuperare hello 'CpuTime' e 'Richiede' dati di metrica punti).</span><span class="sxs-lookup"><span data-stu-id="24e3e-132">Use hello metric’s name ‘value’ (not hello ‘localizedValue’) for any filtering requests (for example, retrieve hello ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="24e3e-133">Se non è stato specificato alcun filtro, viene restituito metrica predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="24e3e-133">If no filters are specified, hello default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="24e3e-134">valori della metrica tooretrieve utilizzando hello API REST di monitoraggio di Azure, utilizzare "2016-06-01" hello versione API.</span><span class="sxs-lookup"><span data-stu-id="24e3e-134">tooretrieve metric values using hello Azure Monitor REST API, use "2016-06-01" as hello API version.</span></span>
>
>

<span data-ttu-id="24e3e-135">**Metodo**: GET</span><span class="sxs-lookup"><span data-stu-id="24e3e-135">**Method**: GET</span></span>

<span data-ttu-id="24e3e-136">**URI richiesta**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="24e3e-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="24e3e-137">Ad esempio, tooretrieve hello RunsSucceeded metrica punti dati per hello dato intervallo di tempo e per un intervallo di tempo di 1 ora, richiesta hello sarà come segue:</span><span class="sxs-lookup"><span data-stu-id="24e3e-137">For example, tooretrieve hello RunsSucceeded metric data points for hello given time range and for a time grain of 1 hour, hello request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="24e3e-138">risultato Hello appariranno simili toohello riportato schermata:</span><span class="sxs-lookup"><span data-stu-id="24e3e-138">hello result would appear similar toohello example following screenshot:</span></span>

![Alt "Risposta JSON che mostra il valore della metrica per il tempo medio di risposta"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="24e3e-140">tooretrieve punta più dati o un'aggregazione, aggiungere i nomi definizione metrica hello e filtro toohello dei tipi di aggregazione, come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="24e3e-140">tooretrieve multiple data or aggregation points, add hello metric definition names and aggregation types toohello filter, as seen in hello following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="24e3e-141">Usare ARMClient</span><span class="sxs-lookup"><span data-stu-id="24e3e-141">Use ARMClient</span></span>
<span data-ttu-id="24e3e-142">Un'alternativa toousing PowerShell (come illustrato in precedenza), è toouse [ARMClient](https://github.com/projectkudu/ARMClient) sul proprio computer Windows.</span><span class="sxs-lookup"><span data-stu-id="24e3e-142">An alternative toousing PowerShell (as shown above), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="24e3e-143">ARMClient gestisce automaticamente l'autenticazione di hello Azure AD (e i token JWT risultante).</span><span class="sxs-lookup"><span data-stu-id="24e3e-143">ARMClient handles hello Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="24e3e-144">Hello seguito viene illustrato l'uso di ARMClient per il recupero dei dati di metrica:</span><span class="sxs-lookup"><span data-stu-id="24e3e-144">hello following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="24e3e-145">Installare [Chocolatey](https://chocolatey.org/) e [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="24e3e-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="24e3e-146">In una finestra del terminale digitare *armclient.exe login*.</span><span class="sxs-lookup"><span data-stu-id="24e3e-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="24e3e-147">Questo richiede toolog in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="24e3e-147">This prompts you toolog in tooAzure.</span></span>
3. <span data-ttu-id="24e3e-148">Digitare *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="24e3e-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="24e3e-149">Digitare *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="24e3e-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![ALT "Using ARMClient toowork con l'API REST di Azure Monitoring hello"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a><span data-ttu-id="24e3e-151">Recuperare l'ID di risorsa hello</span><span class="sxs-lookup"><span data-stu-id="24e3e-151">Retrieve hello Resource ID</span></span>
<span data-ttu-id="24e3e-152">Utilizzando l'API REST di hello consente effettivamente toounderstand hello disponibili le definizioni delle metriche e granularità valori correlati.</span><span class="sxs-lookup"><span data-stu-id="24e3e-152">Using hello REST API can really help toounderstand hello available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="24e3e-153">Tali informazioni sono utile quando si utilizza hello [libreria di gestione di Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="24e3e-153">That information is helpful when using hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="24e3e-154">Per hello codice precedente, toouse ID di risorsa hello è toohello percorso completo di hello desiderato risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="24e3e-154">For hello preceding code, hello resource ID toouse is hello full path toohello desired Azure resource.</span></span> <span data-ttu-id="24e3e-155">Ad esempio, tooquery rispetto a un'App Web di Azure, ID di risorsa hello sarebbe:</span><span class="sxs-lookup"><span data-stu-id="24e3e-155">For example, tooquery against an Azure Web App, hello resource ID would be:</span></span>

<span data-ttu-id="24e3e-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span><span class="sxs-lookup"><span data-stu-id="24e3e-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="24e3e-157">Hello elenco seguente contiene alcuni esempi di formati di ID di risorsa per varie risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="24e3e-157">hello following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="24e3e-158">**Hub IoT** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span><span class="sxs-lookup"><span data-stu-id="24e3e-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="24e3e-159">**Pool elastico di SQL** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span><span class="sxs-lookup"><span data-stu-id="24e3e-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="24e3e-160">**Database SQL (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span><span class="sxs-lookup"><span data-stu-id="24e3e-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="24e3e-161">**Bus di servizio** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span><span class="sxs-lookup"><span data-stu-id="24e3e-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="24e3e-162">**Set di scalabilità VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="24e3e-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="24e3e-163">**VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span><span class="sxs-lookup"><span data-stu-id="24e3e-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="24e3e-164">**Hub eventi** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span><span class="sxs-lookup"><span data-stu-id="24e3e-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="24e3e-165">Esistono metodi alternativi tooretrieving hello ID di risorsa, incluso l'utilizzo di Esplora risorse di Azure, la visualizzazione di risorse hello desiderato nel portale di Azure hello e tramite PowerShell o hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="24e3e-165">There are alternative approaches tooretrieving hello resource ID, including using Azure Resource Explorer, viewing hello desired resource in hello Azure portal, and via PowerShell or hello Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="24e3e-166">Esplora risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="24e3e-166">Azure Resource Explorer</span></span>
<span data-ttu-id="24e3e-167">ID della risorsa hello toofind per la risorsa desiderata, un approccio utile è hello toouse [Esplora inventario risorse di Azure](https://resources.azure.com) strumento.</span><span class="sxs-lookup"><span data-stu-id="24e3e-167">toofind hello resource ID for a desired resource, one helpful approach is toouse hello [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="24e3e-168">Passare risorsa toohello desiderato e quindi osservare ID hello illustrato, come illustrato di seguito schermata hello:</span><span class="sxs-lookup"><span data-stu-id="24e3e-168">Navigate toohello desired resource and then look at hello ID shown, as in hello following screenshot:</span></span>

![Alt "Esplora risorse di Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="24e3e-170">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="24e3e-170">Azure portal</span></span>
<span data-ttu-id="24e3e-171">ID di risorsa Hello anche ottenibili da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="24e3e-171">hello resource ID can also be obtained from hello Azure portal.</span></span> <span data-ttu-id="24e3e-172">toodo in tal caso, passare risorsa toohello desiderato, quindi scegliere Proprietà.</span><span class="sxs-lookup"><span data-stu-id="24e3e-172">toodo so, navigate toohello desired resource and then select Properties.</span></span> <span data-ttu-id="24e3e-173">ID risorsa Hello viene visualizzato nel pannello Proprietà hello, come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="24e3e-173">hello Resource ID is displayed in hello Properties blade, as seen in hello following screenshot:</span></span>

![ALT "ID risorsa visualizzato nel pannello Proprietà hello nel portale di Azure hello"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="24e3e-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="24e3e-175">Azure PowerShell</span></span>
<span data-ttu-id="24e3e-176">ID di risorsa Hello può essere recuperato utilizzando anche i cmdlet PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="24e3e-176">hello resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="24e3e-177">ID della risorsa hello tooobtain per un'App Web di Azure, ad esempio, eseguire cmdlet Get-AzureRmWebApp hello, come hello seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="24e3e-177">For example, tooobtain hello resource ID for an Azure Web App, execute hello Get-AzureRmWebApp cmdlet, as in hello following screenshot:</span></span>

![Alt "ID risorsa ottenuto tramite PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="24e3e-179">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="24e3e-179">Azure CLI</span></span>
<span data-ttu-id="24e3e-180">tooretrieve hello hello CLI di Azure con ID di risorsa, eseguire il comando 'webapp azure Mostra' hello, specificando hello "--json' opzione, come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="24e3e-180">tooretrieve hello resource ID using hello Azure CLI, execute hello 'azure webapp show' command, specifying hello '--json' option, as shown in hello following screenshot:</span></span>

![Alt "ID risorsa ottenuto tramite PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="24e3e-182">Recuperare i dati del registro attività</span><span class="sxs-lookup"><span data-stu-id="24e3e-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="24e3e-183">In aggiunta tooworking con le definizioni delle metriche e i valori correlati, è anche possibile tooretrieve interessanti informazioni dettagliate correlate tooAzure risorse aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="24e3e-183">In addition tooworking with metric definitions and related values, it is also possible tooretrieve additional interesting insights related tooAzure resources.</span></span> <span data-ttu-id="24e3e-184">Ad esempio, è possibile tooquery [log attività](https://msdn.microsoft.com/library/azure/dn931934.aspx) dati.</span><span class="sxs-lookup"><span data-stu-id="24e3e-184">As an example, it is possible tooquery [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="24e3e-185">Hello esempio seguente viene illustrato come utilizzare hello API REST di Azure monitoraggio tooquery dati del log attività all'interno di un intervallo di date specifico per una sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="24e3e-185">hello following sample demonstrates using hello Azure Monitor REST API tooquery activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="24e3e-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="24e3e-186">Next steps</span></span>
* <span data-ttu-id="24e3e-187">Hello revisione [Panoramica di monitoraggio](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24e3e-187">Review hello [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="24e3e-188">Hello vista [metriche con Monitor di Azure supportata](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="24e3e-188">View hello [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="24e3e-189">Hello revisione [riferimento all'API REST di Microsoft Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="24e3e-189">Review hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="24e3e-190">Hello revisione [libreria di gestione di Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="24e3e-190">Review hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
