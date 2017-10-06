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
# <a name="azure-monitoring-rest-api-walkthrough"></a>Procedura dettagliata sull'API REST di monitoraggio di Azure
In questo articolo illustra come autenticazione tooperform in modo il codice può usare hello [riferimento all'API REST di Microsoft Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Hello API di monitoraggio di Azure rende possibili tooprogrammatically recuperare hello predefinite disponibili definizioni di metrica (tipo hello di metrica, ad esempio il tempo di CPU, le richieste e così via) e granularità valori della metrica. Una volta recuperato, dati hello possono essere salvati in un archivio dati separato, ad esempio Database SQL di Azure, Azure Cosmos DB o Azure Data Lake. Da qui, se necessario, è possibile svolgere ulteriori analisi.

Oltre a funzionare con diversi punti dati di metrica, come illustrato di seguito in questo articolo, hello API monitoraggio rende le regole di avviso toolist possibili, visualizzare i log di attività e molto altro ancora. Per un elenco completo delle operazioni disponibili, vedere hello [riferimento all'API REST di Microsoft Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Autenticazione delle richieste di monitoraggio di Azure
primo passaggio Hello è richiesta hello tooauthenticate.

Tutte le attività hello eseguite sul modello l'autenticazione di hello API di monitoraggio di Azure usare hello Azure Resource Manager. Di conseguenza, tutte le richieste devono essere autenticate con Azure Active Directory (Azure AD). Applicazione di un approccio tooauthenticate hello client è toocreate un'entità servizio di Azure AD e recuperare il token di autenticazione (JWT) hello. Hello script di esempio seguente viene illustrato come creare un annuncio di Azure dell'entità servizio tramite PowerShell. Per una procedura dettagliata più dettagliata, consultare la documentazione di toohello su [utilizzando Azure PowerShell toocreate una risorse tooaccess dell'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). È inoltre possibile troppo[creare un'entità servizio tramite il portale di Azure hello](../azure-resource-manager/resource-group-create-service-principal-portal.md).

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

hello tooquery API di monitoraggio di Azure, un'applicazione hello client deve utilizzare hello creato in precedenza tooauthenticate dell'entità servizio. Hello lo script di PowerShell di esempio seguente viene illustrato un approccio, hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp ottenere token JWT di hello autenticazione. token JWT Hello viene passato come parte di un parametro di autorizzazione HTTP in toohello richieste API REST di monitoraggio di Azure.

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

Al termine del passaggio di installazione di hello autenticazione, le query possono quindi essere eseguite hello API REST di monitoraggio di Azure. Esistono due query utili:

1. Elenco di definizioni di metrica hello per una risorsa
2. Recuperare i valori della metrica hello

## <a name="retrieve-metric-definitions"></a>Recuperare le definizioni delle metriche
> [!NOTE]
> le definizioni delle metriche tooretrieve utilizzando hello API REST di monitoraggio di Azure, utilizzare "2016-03-01" hello versione API.
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
Per un'App di logica di Azure, le definizioni delle metriche hello appariranno simile toohello seguente schermata:

![Alt "Visualizzazione JSON della risposta alle definizioni delle metriche"](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Per ulteriori informazioni, vedere hello [elencare le definizioni delle metriche di hello per una risorsa nell'API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentazione.

## <a name="retrieve-metric-values"></a>Recuperare i valori delle metriche
Una volta hello disponibili le definizioni delle metriche sono noti, è quindi possibile tooretrieve hello valori metriche correlati. Utilizzo nome 'value' della metrica hello (non hello 'localizedValue') per tutte le richieste di filtro (ad esempio, recuperare hello 'CpuTime' e 'Richiede' dati di metrica punti). Se non è stato specificato alcun filtro, viene restituito metrica predefinita hello.

> [!NOTE]
> valori della metrica tooretrieve utilizzando hello API REST di monitoraggio di Azure, utilizzare "2016-06-01" hello versione API.
>
>

**Metodo**: GET

**URI richiesta**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*

Ad esempio, tooretrieve hello RunsSucceeded metrica punti dati per hello dato intervallo di tempo e per un intervallo di tempo di 1 ora, richiesta hello sarà come segue:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

risultato Hello appariranno simili toohello riportato schermata:

![Alt "Risposta JSON che mostra il valore della metrica per il tempo medio di risposta"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

tooretrieve punta più dati o un'aggregazione, aggiungere i nomi definizione metrica hello e filtro toohello dei tipi di aggregazione, come illustrato nel seguente esempio hello:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>Usare ARMClient
Un'alternativa toousing PowerShell (come illustrato in precedenza), è toouse [ARMClient](https://github.com/projectkudu/ARMClient) sul proprio computer Windows. ARMClient gestisce automaticamente l'autenticazione di hello Azure AD (e i token JWT risultante). Hello seguito viene illustrato l'uso di ARMClient per il recupero dei dati di metrica:

1. Installare [Chocolatey](https://chocolatey.org/) e [ARMClient](https://github.com/projectkudu/ARMClient).
2. In una finestra del terminale digitare *armclient.exe login*. Questo richiede toolog in tooAzure.
3. Digitare *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Digitare *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![ALT "Using ARMClient toowork con l'API REST di Azure Monitoring hello"](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Recuperare l'ID di risorsa hello
Utilizzando l'API REST di hello consente effettivamente toounderstand hello disponibili le definizioni delle metriche e granularità valori correlati. Tali informazioni sono utile quando si utilizza hello [libreria di gestione di Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Per hello codice precedente, toouse ID di risorsa hello è toohello percorso completo di hello desiderato risorse di Azure. Ad esempio, tooquery rispetto a un'App Web di Azure, ID di risorsa hello sarebbe:

*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*

Hello elenco seguente contiene alcuni esempi di formati di ID di risorsa per varie risorse di Azure:

* **Hub IoT** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*
* **Pool elastico di SQL** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*
* **Database SQL (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*
* **Bus di servizio** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*
* **Set di scalabilità VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*
* **VM** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*
* **Hub eventi** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*

Esistono metodi alternativi tooretrieving hello ID di risorsa, incluso l'utilizzo di Esplora risorse di Azure, la visualizzazione di risorse hello desiderato nel portale di Azure hello e tramite PowerShell o hello CLI di Azure.

### <a name="azure-resource-explorer"></a>Esplora risorse di Azure
ID della risorsa hello toofind per la risorsa desiderata, un approccio utile è hello toouse [Esplora inventario risorse di Azure](https://resources.azure.com) strumento. Passare risorsa toohello desiderato e quindi osservare ID hello illustrato, come illustrato di seguito schermata hello:

![Alt "Esplora risorse di Azure"](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Portale di Azure
ID di risorsa Hello anche ottenibili da hello portale di Azure. toodo in tal caso, passare risorsa toohello desiderato, quindi scegliere Proprietà. ID risorsa Hello viene visualizzato nel pannello Proprietà hello, come illustrato nella seguente schermata hello:

![ALT "ID risorsa visualizzato nel pannello Proprietà hello nel portale di Azure hello"](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
ID di risorsa Hello può essere recuperato utilizzando anche i cmdlet PowerShell di Azure. ID della risorsa hello tooobtain per un'App Web di Azure, ad esempio, eseguire cmdlet Get-AzureRmWebApp hello, come hello seguente schermata:

![Alt "ID risorsa ottenuto tramite PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
tooretrieve hello hello CLI di Azure con ID di risorsa, eseguire il comando 'webapp azure Mostra' hello, specificando hello "--json' opzione, come illustrato nella seguente schermata hello:

![Alt "ID risorsa ottenuto tramite PowerShell"](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Recuperare i dati del registro attività
In aggiunta tooworking con le definizioni delle metriche e i valori correlati, è anche possibile tooretrieve interessanti informazioni dettagliate correlate tooAzure risorse aggiuntive. Ad esempio, è possibile tooquery [log attività](https://msdn.microsoft.com/library/azure/dn931934.aspx) dati. Hello esempio seguente viene illustrato come utilizzare hello API REST di Azure monitoraggio tooquery dati del log attività all'interno di un intervallo di date specifico per una sottoscrizione di Azure:

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>Passaggi successivi
* Hello revisione [Panoramica di monitoraggio](monitoring-overview.md).
* Hello vista [metriche con Monitor di Azure supportata](monitoring-supported-metrics.md).
* Hello revisione [riferimento all'API REST di Microsoft Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Hello revisione [libreria di gestione di Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
