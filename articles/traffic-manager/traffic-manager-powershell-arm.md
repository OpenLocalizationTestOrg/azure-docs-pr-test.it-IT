---
title: Uso di PowerShell per Gestione traffico in Azure | Microsoft Docs
description: Uso di PowerShell per Gestione traffico con Azure Resource Manager
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 1cd7bd7e32c96398d72c7cd3b51e2b456d60f01d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="using-powershell-to-manage-traffic-manager"></a><span data-ttu-id="78b47-103">Uso di PowerShell per Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-103">Using PowerShell to manage Traffic Manager</span></span>

<span data-ttu-id="78b47-104">Azure Resource Manager è l'interfaccia di gestione preferita dei servizi in Azure.</span><span class="sxs-lookup"><span data-stu-id="78b47-104">Azure Resource Manager is the preferred management interface for services in Azure.</span></span> <span data-ttu-id="78b47-105">I profili di Gestione traffico di Azure possono ora essere gestiti usando le API e gli strumenti basati su Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="78b47-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="78b47-106">Modello di risorsa</span><span class="sxs-lookup"><span data-stu-id="78b47-106">Resource model</span></span>

<span data-ttu-id="78b47-107">Gestione traffico di Azure viene configurato utilizzando una serie di impostazioni denominate "profilo di Gestione traffico".</span><span class="sxs-lookup"><span data-stu-id="78b47-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="78b47-108">Questo profilo include le impostazioni DNS, di routing del traffico, di monitoraggio dell'endpoint e un elenco degli endpoint di servizio a cui viene indirizzato il traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints to which traffic is routed.</span></span>

<span data-ttu-id="78b47-109">Ogni profilo di Gestione traffico è rappresentato da una risorsa di tipo "TrafficManagerProfiles".</span><span class="sxs-lookup"><span data-stu-id="78b47-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="78b47-110">A livello di API REST, l'URI per ogni profilo è analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="78b47-110">At the REST API level, the URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="78b47-111">Configurazione di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="78b47-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="78b47-112">In queste istruzioni viene usato Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78b47-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="78b47-113">L'articolo seguente illustra come installare e configurare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78b47-113">The following article explains how to install and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="78b47-114">Come installare e configurare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="78b47-114">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="78b47-115">Negli esempi inclusi in questo articolo si presuppone che esista un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="78b47-115">The examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="78b47-116">È possibile creare un gruppo di risorse usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="78b47-116">You can create a resource group using the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="78b47-117">Azure Resource Manager richiede che tutti i gruppi di risorse specifichino un percorso,</span><span class="sxs-lookup"><span data-stu-id="78b47-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="78b47-118">che viene usato come percorso predefinito per le risorse create in questo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="78b47-118">This location is used as the default for resources created in that resource group.</span></span> <span data-ttu-id="78b47-119">Tuttavia, dal momento che tutte le risorse del profilo di Gestione traffico sono globali (non locali), la scelta del percorso relativo al gruppo di risorse non ha alcun impatto sul servizio Gestione traffico di Azure.</span><span class="sxs-lookup"><span data-stu-id="78b47-119">However, since Traffic Manager profile resources are global, not regional, the choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="78b47-120">Creazione di un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="78b47-121">Per creare un profilo di Gestione traffico, usare il cmdlet `New-AzureRmTrafficManagerProfile`:</span><span class="sxs-lookup"><span data-stu-id="78b47-121">To create a Traffic Manager profile, use the `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="78b47-122">La tabella seguente descrive i parametri:</span><span class="sxs-lookup"><span data-stu-id="78b47-122">The following table describes the parameters:</span></span>

| <span data-ttu-id="78b47-123">Parametro</span><span class="sxs-lookup"><span data-stu-id="78b47-123">Parameter</span></span> | <span data-ttu-id="78b47-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="78b47-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="78b47-125">Nome</span><span class="sxs-lookup"><span data-stu-id="78b47-125">Name</span></span> |<span data-ttu-id="78b47-126">Il nome della risorsa per la risorsa del profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-126">The resource name for the Traffic Manager profile resource.</span></span> <span data-ttu-id="78b47-127">I profili dello stesso gruppo di risorse devono disporre di nomi univoci.</span><span class="sxs-lookup"><span data-stu-id="78b47-127">Profiles in the same resource group must have unique names.</span></span> <span data-ttu-id="78b47-128">Tale nome è diverso rispetto a quello DNS utilizzato per le query DNS.</span><span class="sxs-lookup"><span data-stu-id="78b47-128">This name is separate from the DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="78b47-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="78b47-129">ResourceGroupName</span></span> |<span data-ttu-id="78b47-130">Il nome del gruppo di risorse che include la risorsa del profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-130">The name of the resource group containing the profile resource.</span></span> |
| <span data-ttu-id="78b47-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="78b47-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="78b47-132">Indica il metodo di routing del traffico usato per determinare quale endpoint viene restituito in risposta alle query DNS.</span><span class="sxs-lookup"><span data-stu-id="78b47-132">Specifies the traffic-routing method used to determine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="78b47-133">I valori possibili sono "Performance", "'Weighted" e "Priority".</span><span class="sxs-lookup"><span data-stu-id="78b47-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="78b47-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="78b47-134">RelativeDnsName</span></span> |<span data-ttu-id="78b47-135">Indica la parte hostname del nome DNS fornito da questo profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-135">Specifies the hostname portion of the DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="78b47-136">Questo valore viene combinato con il nome del dominio DNS usato da Gestione traffico di Azure per formare il nome di dominio completo del profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-136">This value is combined with the DNS domain name used by Azure Traffic Manager to form the fully qualified domain name (FQDN) of the profile.</span></span> <span data-ttu-id="78b47-137">Ad esempio, l'impostazione del valore di "contoso" diventa "contoso.trafficmanager.net".</span><span class="sxs-lookup"><span data-stu-id="78b47-137">For example, setting the value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="78b47-138">TTL</span><span class="sxs-lookup"><span data-stu-id="78b47-138">TTL</span></span> |<span data-ttu-id="78b47-139">Specifica la durata (TTL) DNS in secondi.</span><span class="sxs-lookup"><span data-stu-id="78b47-139">Specifies the DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="78b47-140">In questo modo, i resolver locali e i client DNS sono informati sulla durata della memorizzazione nella cache delle risposte DNS per il profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-140">This TTL informs the Local DNS resolvers and DNS clients how long to cache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="78b47-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="78b47-141">MonitorProtocol</span></span> |<span data-ttu-id="78b47-142">Indica il protocollo da usare per monitorare lo stato di integrità dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="78b47-142">Specifies the protocol to use to monitor endpoint health.</span></span> <span data-ttu-id="78b47-143">I valori possibili sono "HTTP" e "HTTPS".</span><span class="sxs-lookup"><span data-stu-id="78b47-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="78b47-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="78b47-144">MonitorPort</span></span> |<span data-ttu-id="78b47-145">Indica la porta TCP da usare per monitorare lo stato di integrità dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="78b47-145">Specifies the TCP port used to monitor endpoint health.</span></span> |
| <span data-ttu-id="78b47-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="78b47-146">MonitorPath</span></span> |<span data-ttu-id="78b47-147">Indica il percorso relativo al nome di dominio dell'endpoint usato per verificare l'integrità dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="78b47-147">Specifies the path relative to the endpoint domain name used to probe for endpoint health.</span></span> |

<span data-ttu-id="78b47-148">Il cmdlet consente di creare un profilo di Gestione traffico in Azure e restituisce un oggetto di profilo corrispondente a PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78b47-148">The cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object to PowerShell.</span></span> <span data-ttu-id="78b47-149">A questo punto, il profilo non contiene endpoint.</span><span class="sxs-lookup"><span data-stu-id="78b47-149">At this point, the profile does not contain any endpoints.</span></span> <span data-ttu-id="78b47-150">Per altre informazioni sull'aggiunta di endpoint a un profilo di Gestione traffico, vedere [Aggiunta di endpoint a Gestione traffico](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="78b47-150">For more information about adding endpoints to a Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="78b47-151">Visualizzazione di un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="78b47-152">Per recuperare un oggetto profilo di Gestione traffico esistente, usare il cmdlet `Get-AzureRmTrafficManagerProfle`:</span><span class="sxs-lookup"><span data-stu-id="78b47-152">To retrieve an existing Traffic Manager profile object, use the `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="78b47-153">Questo cmdlet restituisce un oggetto profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="78b47-154">Aggiornare un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="78b47-155">La modifica dei profili di Gestione traffico prevede un processo in 3 passaggi:</span><span class="sxs-lookup"><span data-stu-id="78b47-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="78b47-156">Recuperare il profilo usando `Get-AzureRmTrafficManagerProfile` oppure usare il profilo restituito da `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="78b47-156">Retrieve the profile using `Get-AzureRmTrafficManagerProfile` or use the profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="78b47-157">Modificare il profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-157">Modify the profile.</span></span> <span data-ttu-id="78b47-158">È possibile aggiungere e rimuovere endpoint o modificare i parametri dell'endpoint o del profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="78b47-159">Queste modifiche sono operazioni offline.</span><span class="sxs-lookup"><span data-stu-id="78b47-159">These changes are off-line operations.</span></span> <span data-ttu-id="78b47-160">Si sta modificando solo l'oggetto locale in memoria che rappresenta il profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-160">You are only changing the local object in memory that represents the profile.</span></span>
3. <span data-ttu-id="78b47-161">Confermare le modifiche usando il cmdlet `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="78b47-161">Commit your changes using the `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="78b47-162">Tutte le proprietà del profilo possono essere modificate, ad eccezione del valore RelativeDnsName del profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-162">All profile properties can be changed except the profile's RelativeDnsName.</span></span> <span data-ttu-id="78b47-163">Per modificare RelativeDnsName, è necessario eliminare il profilo e creare un nuovo profilo con un nuovo nome.</span><span class="sxs-lookup"><span data-stu-id="78b47-163">To change the RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="78b47-164">L'esempio seguente illustra come cambiare la durata (TTL) del profilo:</span><span class="sxs-lookup"><span data-stu-id="78b47-164">The following example demonstrates how to change the profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="78b47-165">Sono disponibili tre tipi di endpoint di Gestione traffico:</span><span class="sxs-lookup"><span data-stu-id="78b47-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="78b47-166">I servizi **Endpoint di Azure** sono ospitati hosting in Azure</span><span class="sxs-lookup"><span data-stu-id="78b47-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="78b47-167">I servizi **Endpoint esterni** sono ospitati all'esterno di Azure</span><span class="sxs-lookup"><span data-stu-id="78b47-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="78b47-168">Gli **endpoint annidati** vengono usati per creare gerarchie annidate dei profili di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-168">**Nested endpoints** are used to construct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="78b47-169">Gli endpoint annidati consentono configurazioni avanzate del routing del traffico per applicazioni complesse.</span><span class="sxs-lookup"><span data-stu-id="78b47-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="78b47-170">In tutti e tre i casi è possibile aggiungere gli endpoint in due modi:</span><span class="sxs-lookup"><span data-stu-id="78b47-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="78b47-171">Usando il processo in 3 passaggi descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="78b47-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="78b47-172">Il vantaggio di questo metodo consiste nel fatto che è possibile apportare diverse modifiche agli endpoint in un singolo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="78b47-172">The advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="78b47-173">Mediante il cmdlet New-AzureRmTrafficManagerEndpoint.</span><span class="sxs-lookup"><span data-stu-id="78b47-173">Using the New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="78b47-174">Questo cmdlet aggiunge un endpoint a un profilo di Gestione traffico esistente in una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="78b47-174">This cmdlet adds an endpoint to an existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="78b47-175">Aggiunta di endpoint di Azure</span><span class="sxs-lookup"><span data-stu-id="78b47-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="78b47-176">Gli endpoint di Azure fanno riferimento ai servizi ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="78b47-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="78b47-177">Sono attualmente supportati due tipi di endpoint di Azure:</span><span class="sxs-lookup"><span data-stu-id="78b47-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="78b47-178">App Web di Azure </span><span class="sxs-lookup"><span data-stu-id="78b47-178">Azure Web Apps</span></span>
2. <span data-ttu-id="78b47-179">Risorse di tipo publicIpAddress di Azure, che possono essere associate a un servizio di bilanciamento del carico o a una scheda di interfaccia di rete di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="78b47-179">Azure PublicIpAddress resources (which can be attached to a load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="78b47-180">La risorsa di tipo PublicIpAddress deve avere un nome DNS assegnato da usare in Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-180">The PublicIpAddress must have a DNS name assigned to be used in Traffic Manager.</span></span>

<span data-ttu-id="78b47-181">In ogni caso:</span><span class="sxs-lookup"><span data-stu-id="78b47-181">In each case:</span></span>

* <span data-ttu-id="78b47-182">Il servizio viene specificato usando il parametro "targetResourceId" di `Add-AzureRmTrafficManagerEndpointConfig` o `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="78b47-182">The service is specified using the 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="78b47-183">TargetResourceId usa in modo implicito "Target" ed "EndpointLocation".</span><span class="sxs-lookup"><span data-stu-id="78b47-183">The 'Target' and 'EndpointLocation' are implied by the TargetResourceId.</span></span>
* <span data-ttu-id="78b47-184">"Weight" è facoltativo ed è possibile scegliere se specificarlo.</span><span class="sxs-lookup"><span data-stu-id="78b47-184">Specifying the 'Weight' is optional.</span></span> <span data-ttu-id="78b47-185">I pesi vengono usati solo se il profilo è configurato per l'uso del metodo di routing del traffico "Weighted".</span><span class="sxs-lookup"><span data-stu-id="78b47-185">Weights are only used if the profile is configured to use the 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="78b47-186">In caso contrario, vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="78b47-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="78b47-187">Il valore deve essere un numero compreso tra 1 e 1000.</span><span class="sxs-lookup"><span data-stu-id="78b47-187">If specified, the value must be a number between 1 and 1000.</span></span> <span data-ttu-id="78b47-188">Il valore predefinito è "1".</span><span class="sxs-lookup"><span data-stu-id="78b47-188">The default value is '1'.</span></span>
* <span data-ttu-id="78b47-189">"Priority" è facoltativo ed è possibile scegliere se specificarlo.</span><span class="sxs-lookup"><span data-stu-id="78b47-189">Specifying the 'Priority' is optional.</span></span> <span data-ttu-id="78b47-190">Le priorità vengono usate solo se il profilo è configurato per l'uso del metodo di routing del traffico "Priority".</span><span class="sxs-lookup"><span data-stu-id="78b47-190">Priorities are only used if the profile is configured to use the 'Priority' traffic-routing method.</span></span> <span data-ttu-id="78b47-191">In caso contrario, vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="78b47-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="78b47-192">I valori validi sono compresi tra 1 e 1000 con i valori più bassi che indicano una priorità più alta.</span><span class="sxs-lookup"><span data-stu-id="78b47-192">Valid values are from 1 to 1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="78b47-193">Se si specifica questo valore per un endpoint, sarà necessario specificarlo per tutti gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="78b47-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="78b47-194">Se questo valore viene omesso, verranno applicati i valori predefiniti a partire da "1" nell'ordine in cui sono elencati gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="78b47-194">If omitted, default values starting from '1' are applied in the order that the endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="78b47-195">Esempio 1: Aggiunta di endpoint di App Web usando `Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="78b47-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="78b47-196">In questo esempio viene creato un profilo di Gestione traffico e vengono aggiunti due endpoint di App Web usando il cmdlet `Add-AzureRmTrafficManagerEndpointConfig`.</span><span class="sxs-lookup"><span data-stu-id="78b47-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using the `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="78b47-197">Esempio 2: Aggiunta di un endpoint publicIpAddress usando `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="78b47-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="78b47-198">In questo esempio viene aggiunta una risorsa indirizzo IP pubblico al profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-198">In this example, a public IP address resource is added to the Traffic Manager profile.</span></span> <span data-ttu-id="78b47-199">L'indirizzo IP pubblico deve avere un nome DNS configurato e può essere associato alla NIC di una VM o a un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="78b47-199">The public IP address must have a DNS name configured, and can be bound either to the NIC of a VM or to a load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="78b47-200">Aggiunta di endpoint esterni</span><span class="sxs-lookup"><span data-stu-id="78b47-200">Adding External Endpoints</span></span>

<span data-ttu-id="78b47-201">Gestione traffico usa endpoint esterni per indirizzare il traffico ai servizi ospitati all'esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="78b47-201">Traffic Manager uses external endpoints to direct traffic to services hosted outside of Azure.</span></span> <span data-ttu-id="78b47-202">Come con gli endpoint di Azure, gli endpoint esterni possono essere aggiunti usando `Add-AzureRmTrafficManagerEndpointConfig` seguito da `Set-AzureRmTrafficManagerProfile` o `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="78b47-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="78b47-203">Quando si specificano endpoint esterni:</span><span class="sxs-lookup"><span data-stu-id="78b47-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="78b47-204">Il nome di dominio dell'endpoint deve essere specificato con il parametro "Target"</span><span class="sxs-lookup"><span data-stu-id="78b47-204">The endpoint domain name must be specified using the 'Target' parameter</span></span>
* <span data-ttu-id="78b47-205">"EndpointLocation" è obbligatorio se viene usato il metodo di routing del traffico "Performance".</span><span class="sxs-lookup"><span data-stu-id="78b47-205">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span></span> <span data-ttu-id="78b47-206">In caso contrario, è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="78b47-206">Otherwise it is optional.</span></span> <span data-ttu-id="78b47-207">Il valore deve essere un [nome di area di Azure valido](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="78b47-207">The value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="78b47-208">I parametri "Weight" e "Priority" sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="78b47-208">The 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="78b47-209">Esempio 1: Aggiunta di endpoint esterni usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="78b47-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="78b47-210">In questo esempio viene creato un profilo di Gestione traffico, vengono aggiunti due endpoint esterni e viene eseguito il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="78b47-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit the changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="78b47-211">Esempio 2: Aggiunta di endpoint esterni usando `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="78b47-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="78b47-212">In questo esempio si aggiunge un endpoint esterno a un profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="78b47-212">In this example, we add an external endpoint to an existing profile.</span></span> <span data-ttu-id="78b47-213">Il profilo viene specificato usando i nomi del gruppo di risorse e del profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-213">The profile is specified using the profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="78b47-214">Aggiunta di endpoint 'annidati'</span><span class="sxs-lookup"><span data-stu-id="78b47-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="78b47-215">Ciascun profilo di Gestione traffico specifica un solo metodo di routing del traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="78b47-216">Esistono scenari che tuttavia richiedono un sistema di routing del traffico più avanzato anziché il routing fornito da un singolo profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-216">However, there are scenarios that require more sophisticated traffic routing than the routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="78b47-217">È possibile annidare i profili di Gestione traffico per combinare i vantaggi offerti da più metodi di routing del traffico.</span><span class="sxs-lookup"><span data-stu-id="78b47-217">You can nest Traffic Manager profiles to combine the benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="78b47-218">I profili annidati consentono di ignorare il comportamento predefinito di Gestione traffico per supportare distribuzioni di dimensioni maggiori e più complesse.</span><span class="sxs-lookup"><span data-stu-id="78b47-218">Nested profiles allow you to override the default Traffic Manager behavior to support larger and more complex application deployments.</span></span> <span data-ttu-id="78b47-219">Per esempi più dettagliati, vedere [Profili annidati di Gestione traffico](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="78b47-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="78b47-220">Endpoint annidati vengono configurati nel profilo padre tramite un tipo di endpoint specifico, 'NestedEndpoints'.</span><span class="sxs-lookup"><span data-stu-id="78b47-220">Nested endpoints are configured at the parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="78b47-221">Quando si specificano endpoint annidati:</span><span class="sxs-lookup"><span data-stu-id="78b47-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="78b47-222">L'endpoint deve essere specificato usando il parametro "targetResourceId"</span><span class="sxs-lookup"><span data-stu-id="78b47-222">The endpoint must be specified using the 'targetResourceId' parameter</span></span>
* <span data-ttu-id="78b47-223">"EndpointLocation" è obbligatorio se viene usato il metodo di routing del traffico "Performance".</span><span class="sxs-lookup"><span data-stu-id="78b47-223">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span></span> <span data-ttu-id="78b47-224">In caso contrario, è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="78b47-224">Otherwise it is optional.</span></span> <span data-ttu-id="78b47-225">Il valore deve essere un [nome di area di Azure valido](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="78b47-225">The value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="78b47-226">I parametri "Weight" e "Priority" sono facoltativi, come per gli endpoint di Azure.</span><span class="sxs-lookup"><span data-stu-id="78b47-226">The 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="78b47-227">Il parametro "MinChildEndpoints" è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="78b47-227">The 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="78b47-228">Il valore predefinito è "1".</span><span class="sxs-lookup"><span data-stu-id="78b47-228">The default value is '1'.</span></span> <span data-ttu-id="78b47-229">Se il numero di endpoint disponibili scende sotto questa soglia, il profilo padre considera il profilo figlio "degradato" con conseguente deviazione del traffico agli altri endpoint del profilo padre.</span><span class="sxs-lookup"><span data-stu-id="78b47-229">If the number of available endpoints falls below this threshold, the parent profile considers the child profile 'degraded' and diverts traffic to the other endpoints in the parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="78b47-230">Esempio 1: Aggiunta di endpoint annidati usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="78b47-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="78b47-231">In questo esempio vengono creati un nuovo profilo padre e un nuovo profilo figlio di Gestione traffico, il profilo figlio viene aggiunto come endpoint annidato nel profilo padre, quindi vengono confermate le modifiche.</span><span class="sxs-lookup"><span data-stu-id="78b47-231">In this example, we create new Traffic Manager child and parent profiles, add the child as a nested endpoint to the parent, and commit the changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="78b47-232">Per brevità, in questo esempio, non sono stati aggiunti altri endpoint al profilo padre o figlio.</span><span class="sxs-lookup"><span data-stu-id="78b47-232">For brevity in this example, we did not add any other endpoints to the child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="78b47-233">Esempio 2: Aggiunta di endpoint annidati usando `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="78b47-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="78b47-234">In questo esempio viene aggiunto un profilo figlio esistente come endpoint annidato in un profilo padre esistente.</span><span class="sxs-lookup"><span data-stu-id="78b47-234">In this example, we add an existing child profile as a nested endpoint to an existing parent profile.</span></span> <span data-ttu-id="78b47-235">Il profilo viene specificato usando i nomi del gruppo di risorse e del profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-235">The profile is specified using the profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="78b47-236">Aggiornare un endpoint di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="78b47-237">È possibile aggiornare un endpoint di Gestione traffico esistente in due modi:</span><span class="sxs-lookup"><span data-stu-id="78b47-237">There are two ways to update an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="78b47-238">Ottenere il profilo di Gestione traffico mediante `Get-AzureRmTrafficManagerProfile`, aggiornare le proprietà dell'endpoint nel profilo ed eseguire il commit delle modifiche mediante `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="78b47-238">Get the Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update the endpoint properties within the profile, and commit the changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="78b47-239">Il vantaggio di questo metodo consiste nella possibilità di aggiornare più endpoint in una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="78b47-239">This method has the advantage of being able to update more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="78b47-240">Ottenere l'endpoint di Gestione traffico mediante `Get-AzureRmTrafficManagerEndpoint`, aggiornare le proprietà dell'endpoint ed eseguire il commit delle modifiche mediante `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="78b47-240">Get the Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update the endpoint properties, and commit the changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="78b47-241">Questo metodo è più semplice, perché non richiede l'indicizzazione nella matrice Endpoints nel profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-241">This method is simpler, since it does not require indexing into the Endpoints array in the profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="78b47-242">Esempio 1: Aggiornamento di endpoint usando `Get-AzureRmTrafficManagerProfile` e `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="78b47-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="78b47-243">In questo esempio viene modificata la priorità di due endpoint in un profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="78b47-243">In this example, we modify the priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="78b47-244">Esempio 2: Aggiornamento di un endpoint usando `Get-AzureRmTrafficManagerEndpoint` e `Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="78b47-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="78b47-245">In questo esempio viene modificato il peso di un singolo endpoint in un profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="78b47-245">In this example, we modify the weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="78b47-246">Abilitazione e disabilitazione di endpoint e profili</span><span class="sxs-lookup"><span data-stu-id="78b47-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="78b47-247">Gestione traffico consente l'abilitazione e la disabilitazione dei singoli endpoint, oltre a consentire l'abilitazione e la disabilitazione di interi profili.</span><span class="sxs-lookup"><span data-stu-id="78b47-247">Traffic Manager allows individual endpoints to be enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="78b47-248">Queste modifiche possono essere apportate ottenendo/aggiornando/impostando l'endpoint o le risorse del profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-248">These changes can be made by getting/updating/setting the endpoint or profile resources.</span></span> <span data-ttu-id="78b47-249">Per semplificare queste operazioni comuni, le modifiche sono supportate anche tramite cmdlet dedicati.</span><span class="sxs-lookup"><span data-stu-id="78b47-249">To streamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="78b47-250">Esempio 1: Abilitazione e disabilitazione di un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="78b47-251">Per abilitare un profilo di Gestione traffico, usare `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="78b47-251">To enable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="78b47-252">Il profilo può essere specificato usando un oggetto profilo.</span><span class="sxs-lookup"><span data-stu-id="78b47-252">The profile can be specified using a profile object.</span></span> <span data-ttu-id="78b47-253">L'oggetto profilo può essere passato tramite la pipeline o usando il parametro '-TrafficManagerProfile'.</span><span class="sxs-lookup"><span data-stu-id="78b47-253">The profile object can be passed via the pipeline or by using the '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="78b47-254">In questo esempio abbiamo specificato il profilo in base al nome del gruppo di risorse e profili.</span><span class="sxs-lookup"><span data-stu-id="78b47-254">In this example, we specify the profile by the profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="78b47-255">Per disabilitare un profilo di Gestione traffico:</span><span class="sxs-lookup"><span data-stu-id="78b47-255">To disable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="78b47-256">Il cmdlet Disable-AzureRmTrafficManagerProfile chiede la conferma.</span><span class="sxs-lookup"><span data-stu-id="78b47-256">The Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="78b47-257">Questo messaggio può essere soppresso mediante il parametro "-Force".</span><span class="sxs-lookup"><span data-stu-id="78b47-257">This prompt can be suppressed using the '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="78b47-258">Esempio 2: Abilitazione e disabilitazione di un endpoint di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="78b47-259">Per abilitare un endpoint di Gestione traffico, usare `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="78b47-259">To enable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="78b47-260">È possibile specificare l'endpoint in due modi:</span><span class="sxs-lookup"><span data-stu-id="78b47-260">There are two ways to specify the endpoint</span></span>

1. <span data-ttu-id="78b47-261">Usando un oggetto TrafficManagerEndpoint passato tramite la pipeline o usando il parametro "-TrafficManagerEndpoint"</span><span class="sxs-lookup"><span data-stu-id="78b47-261">Using a TrafficManagerEndpoint object passed via the pipeline or using the '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="78b47-262">Usando il nome dell'endpoint, il tipo di endpoint, il nome del profilo e il nome del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="78b47-262">Using the endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="78b47-263">Analogamente, per disabilitare un endpoint di Gestione traffico:</span><span class="sxs-lookup"><span data-stu-id="78b47-263">Similarly, to disable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="78b47-264">Come con `Disable-AzureRmTrafficManagerProfile`, il cmdlet `Disable-AzureRmTrafficManagerEndpoint` richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="78b47-264">As with `Disable-AzureRmTrafficManagerProfile`, the `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="78b47-265">Questo messaggio può essere soppresso mediante il parametro "-Force".</span><span class="sxs-lookup"><span data-stu-id="78b47-265">This prompt can be suppressed using the '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="78b47-266">Eliminare un endpoint di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="78b47-267">Per rimuovere singoli endpoint, usare il cmdlet `Remove-AzureRmTrafficManagerEndpoint`:</span><span class="sxs-lookup"><span data-stu-id="78b47-267">To remove individual endpoints, use the `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="78b47-268">Il cmdlet richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="78b47-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="78b47-269">Questo messaggio può essere soppresso mediante il parametro "-Force".</span><span class="sxs-lookup"><span data-stu-id="78b47-269">This prompt can be suppressed using the '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="78b47-270">Eliminare un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="78b47-271">Per eliminare un profilo di Gestione traffico, usare il cmdlet `Remove-AzureRmTrafficManagerProfile`, specificando il nome del profilo e del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="78b47-271">To delete a Traffic Manager profile, use the `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying the profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="78b47-272">Il cmdlet richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="78b47-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="78b47-273">Questo messaggio può essere soppresso mediante il parametro "-Force".</span><span class="sxs-lookup"><span data-stu-id="78b47-273">This prompt can be suppressed using the '-Force' parameter.</span></span>

<span data-ttu-id="78b47-274">Inoltre, il profilo da eliminare può essere specificato utilizzando un oggetto di profilo:</span><span class="sxs-lookup"><span data-stu-id="78b47-274">The profile to be deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="78b47-275">Questa sequenza può anche essere inoltrata tramite pipe:</span><span class="sxs-lookup"><span data-stu-id="78b47-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="78b47-276">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78b47-276">Next steps</span></span>

[<span data-ttu-id="78b47-277">Monitoraggio di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="78b47-278">Considerazioni sulle prestazioni di gestione traffico</span><span class="sxs-lookup"><span data-stu-id="78b47-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
