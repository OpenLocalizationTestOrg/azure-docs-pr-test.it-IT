---
title: aaaUsing PowerShell toomanage Traffic Manager in Azure | Documenti Microsoft
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
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="0ccc5-103">Utilizzo di PowerShell toomanage Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0ccc5-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="0ccc5-104">Gestione risorse di Azure è l'interfaccia di gestione Preferiti hello per servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="0ccc5-105">I profili di Gestione traffico di Azure possono ora essere gestiti usando le API e gli strumenti basati su Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="0ccc5-106">Modello di risorsa</span><span class="sxs-lookup"><span data-stu-id="0ccc5-106">Resource model</span></span>

<span data-ttu-id="0ccc5-107">Gestione traffico di Azure viene configurato utilizzando una serie di impostazioni denominate "profilo di Gestione traffico".</span><span class="sxs-lookup"><span data-stu-id="0ccc5-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="0ccc5-108">Il profilo contiene le impostazioni DNS, le impostazioni del routing del traffico, le impostazioni di monitoraggio degli endpoint e viene indirizzato un elenco di traffico toowhich gli endpoint del servizio.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="0ccc5-109">Ogni profilo di Gestione traffico è rappresentato da una risorsa di tipo "TrafficManagerProfiles".</span><span class="sxs-lookup"><span data-stu-id="0ccc5-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="0ccc5-110">A livello di API REST di hello, hello URI per ogni profilo è il seguente:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="0ccc5-111">Configurazione di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ccc5-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="0ccc5-112">In queste istruzioni viene usato Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="0ccc5-113">Hello articolo seguente viene illustrato come tooinstall e configurare Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="0ccc5-114">Come tooinstall e configurare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ccc5-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="0ccc5-115">esempi di Hello in questo articolo presuppongono che sia disponibile un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="0ccc5-116">È possibile creare un gruppo di risorse utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="0ccc5-117">Azure Resource Manager richiede che tutti i gruppi di risorse specifichino un percorso,</span><span class="sxs-lookup"><span data-stu-id="0ccc5-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="0ccc5-118">Questo percorso viene utilizzato come valore predefinito di hello per le risorse create in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="0ccc5-119">Tuttavia, poiché le risorse di profilo di gestione traffico globale e non regionali, scelta hello del percorso del gruppo di risorse ha alcun impatto su Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="0ccc5-120">Creazione di un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="0ccc5-121">toocreate un profilo di Traffic Manager, utilizzare hello `New-AzureRmTrafficManagerProfile` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="0ccc5-122">Hello nella tabella seguente vengono descritti i parametri di hello:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="0ccc5-123">.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-123">Parameter</span></span> | <span data-ttu-id="0ccc5-124">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0ccc5-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0ccc5-125">Nome</span><span class="sxs-lookup"><span data-stu-id="0ccc5-125">Name</span></span> |<span data-ttu-id="0ccc5-126">nome della risorsa Hello hello risorse profilo di Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="0ccc5-127">I profili in hello stesso gruppo di risorse deve avere nomi univoci.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="0ccc5-128">Questo nome è separato dal nome DNS hello per le query DNS.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="0ccc5-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="0ccc5-129">ResourceGroupName</span></span> |<span data-ttu-id="0ccc5-130">nome Hello di hello gruppo contenitore hello profilo risorsa.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="0ccc5-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="0ccc5-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="0ccc5-132">Specifica hello routing del traffico utilizzato toodetermine endpoint a cui viene restituito in risposta a una query DNS.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="0ccc5-133">I valori possibili sono "Performance", "'Weighted" e "Priority".</span><span class="sxs-lookup"><span data-stu-id="0ccc5-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="0ccc5-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="0ccc5-134">RelativeDnsName</span></span> |<span data-ttu-id="0ccc5-135">Specifica porzione hostname di hello del nome DNS hello fornito da questo profilo di Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="0ccc5-136">Questo valore viene combinato con il nome di dominio DNS hello utilizzato da Gestione traffico di Azure tooform hello Nome dominio completo (FQDN) del profilo di hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="0ccc5-137">Ad esempio, impostare il valore di hello del 'contoso' diventa 'contoso.trafficmanager.net'.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="0ccc5-138">TTL</span><span class="sxs-lookup"><span data-stu-id="0ccc5-138">TTL</span></span> |<span data-ttu-id="0ccc5-139">Specifica hello DNS Time-to-Live (TTL), in secondi.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="0ccc5-140">Questa durata TTL indica ai resolver DNS locali hello e i client DNS tempo delle risposte DNS toocache per questo profilo di Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="0ccc5-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="0ccc5-141">MonitorProtocol</span></span> |<span data-ttu-id="0ccc5-142">Specifica l'integrità dell'endpoint toomonitor toouse protocollo hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="0ccc5-143">I valori possibili sono "HTTP" e "HTTPS".</span><span class="sxs-lookup"><span data-stu-id="0ccc5-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="0ccc5-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="0ccc5-144">MonitorPort</span></span> |<span data-ttu-id="0ccc5-145">Specifica la porta TCP hello toomonitor integrità dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="0ccc5-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="0ccc5-146">MonitorPath</span></span> |<span data-ttu-id="0ccc5-147">Specifica nome di dominio dell'endpoint di hello percorso relativo toohello utilizzato tooprobe per lo stato di endpoint.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="0ccc5-148">Hello cmdlet crea un profilo di Traffic Manager in Azure e restituisce un corrispondente tooPowerShell oggetto profilo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="0ccc5-149">A questo punto, hello profilo non contiene alcun endpoint.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="0ccc5-150">Per ulteriori informazioni sull'aggiunta del profilo di Traffic Manager tooa endpoint, vedere [aggiunta di endpoint di gestione traffico](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="0ccc5-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="0ccc5-151">Visualizzazione di un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="0ccc5-152">tooretrieve un oggetto profilo di gestione traffico esistente, utilizzare hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="0ccc5-153">Questo cmdlet restituisce un oggetto profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="0ccc5-154">Aggiornare un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="0ccc5-155">La modifica dei profili di Gestione traffico prevede un processo in 3 passaggi:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="0ccc5-156">Recuperare hello profilo utilizzando `Get-AzureRmTrafficManagerProfile` oppure utilizzare il profilo di hello restituito da `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="0ccc5-157">Modificare il profilo di hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-157">Modify hello profile.</span></span> <span data-ttu-id="0ccc5-158">È possibile aggiungere e rimuovere endpoint o modificare i parametri dell'endpoint o del profilo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="0ccc5-159">Queste modifiche sono operazioni offline.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-159">These changes are off-line operations.</span></span> <span data-ttu-id="0ccc5-160">Si sta modificando solo oggetto locale di hello in memoria che rappresenta il profilo di hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="0ccc5-161">Salvare le modifiche utilizzando hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="0ccc5-162">Tutte le proprietà di profilo possono essere modificate, ad eccezione RelativeDnsName del profilo hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="0ccc5-163">toochange hello RelativeDnsName, è necessario eliminare profilo e un nuovo profilo con un nuovo nome.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="0ccc5-164">Hello di esempio seguente viene illustrato come toochange hello durata (TTL) del profilo:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="0ccc5-165">Sono disponibili tre tipi di endpoint di Gestione traffico:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="0ccc5-166">I servizi **Endpoint di Azure** sono ospitati hosting in Azure</span><span class="sxs-lookup"><span data-stu-id="0ccc5-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="0ccc5-167">I servizi **Endpoint esterni** sono ospitati all'esterno di Azure</span><span class="sxs-lookup"><span data-stu-id="0ccc5-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="0ccc5-168">**Annidati endpoint** gerarchie utilizzate tooconstruct annidati di profili di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="0ccc5-169">Gli endpoint annidati consentono configurazioni avanzate del routing del traffico per applicazioni complesse.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="0ccc5-170">In tutti e tre i casi è possibile aggiungere gli endpoint in due modi:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="0ccc5-171">Usando il processo in 3 passaggi descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="0ccc5-172">Il vantaggio di Hello di questo metodo è che possono essere apportate molte modifiche di endpoint in un singolo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="0ccc5-173">Utilizzo di cmdlet New-AzureRmTrafficManagerEndpoint hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="0ccc5-174">Questo cmdlet aggiunge un profilo di Traffic Manager endpoint tooan esistente in un'unica operazione.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="0ccc5-175">Aggiunta di endpoint di Azure</span><span class="sxs-lookup"><span data-stu-id="0ccc5-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="0ccc5-176">Gli endpoint di Azure fanno riferimento ai servizi ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="0ccc5-177">Sono attualmente supportati due tipi di endpoint di Azure:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="0ccc5-178">App Web di Azure </span><span class="sxs-lookup"><span data-stu-id="0ccc5-178">Azure Web Apps</span></span>
2. <span data-ttu-id="0ccc5-179">PublicIpAddress le risorse di Azure (che possono essere collegato tooa bilanciamento del carico o una scheda di rete di macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="0ccc5-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="0ccc5-180">Hello PublicIpAddress deve avere un nome DNS assegnato toobe utilizzato in Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="0ccc5-181">In ogni caso:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-181">In each case:</span></span>

* <span data-ttu-id="0ccc5-182">servizio Hello viene specificato utilizzando il parametro 'ID risorsa di destinazione' hello di `Add-AzureRmTrafficManagerEndpointConfig` o `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="0ccc5-183">Hello 'Target' e 'EndpointLocation' impliciti di hello ID risorsa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="0ccc5-184">Hello 'Peso' è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="0ccc5-185">I pesi vengono usati solo se il profilo di hello è metodo di routing del traffico toouse configurato hello 'Weighted'.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="0ccc5-186">In caso contrario, vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="0ccc5-187">Se specificato, il valore di hello deve essere un numero compreso tra 1 e 1000.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="0ccc5-188">valore predefinito di Hello è '1'.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-188">hello default value is '1'.</span></span>
* <span data-ttu-id="0ccc5-189">Hello specificando 'Priority' è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="0ccc5-190">Le priorità vengono utilizzate solo se il profilo di hello è metodo di routing del traffico configurate toouse hello 'Priority'.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="0ccc5-191">In caso contrario, vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="0ccc5-192">I valori validi sono da 1 too1000 con i valori più bassi, che indica una priorità più alta.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="0ccc5-193">Se si specifica questo valore per un endpoint, sarà necessario specificarlo per tutti gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="0ccc5-194">Se omesso, vengono applicati i valori predefiniti a partire da '1' in ordine di hello sono elencati gli endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="0ccc5-195">Esempio 1: Aggiunta di endpoint di App Web usando `Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="0ccc5-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="0ccc5-196">In questo esempio, creare un profilo di gestione traffico e aggiungere due endpoint di App Web utilizzando hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="0ccc5-197">Esempio 2: Aggiunta di un endpoint publicIpAddress usando `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="0ccc5-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="0ccc5-198">In questo esempio, una risorsa di indirizzo IP pubblica viene aggiunto il profilo di gestione traffico toohello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="0ccc5-199">indirizzo IP pubblico Hello deve avere un nome DNS configurato e può essere associata una scheda NIC di bilanciamento del carico macchina virtuale o tooa toohello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="0ccc5-200">Aggiunta di endpoint esterni</span><span class="sxs-lookup"><span data-stu-id="0ccc5-200">Adding External Endpoints</span></span>

<span data-ttu-id="0ccc5-201">Il traffico di gestione utilizza gli endpoint esterni toodirect traffico tooservices ospitato all'esterno di Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="0ccc5-202">Come con gli endpoint di Azure, gli endpoint esterni possono essere aggiunti usando `Add-AzureRmTrafficManagerEndpointConfig` seguito da `Set-AzureRmTrafficManagerProfile` o `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="0ccc5-203">Quando si specificano endpoint esterni:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="0ccc5-204">nome di dominio di Hello endpoint deve essere specificata utilizzando il parametro 'Target' hello</span><span class="sxs-lookup"><span data-stu-id="0ccc5-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="0ccc5-205">Se viene utilizzato il metodo di routing del traffico "Prestazioni" hello, hello 'EndpointLocation' è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="0ccc5-206">In caso contrario, è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-206">Otherwise it is optional.</span></span> <span data-ttu-id="0ccc5-207">il valore di Hello deve essere un [nome dell'area di Azure valido](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="0ccc5-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="0ccc5-208">Hello 'Peso' e 'Priority' sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="0ccc5-209">Esempio 1: Aggiunta di endpoint esterni usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="0ccc5-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="0ccc5-210">In questo esempio è creare un profilo di Traffic Manager, aggiungere due endpoint esterni e commit delle modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="0ccc5-211">Esempio 2: Aggiunta di endpoint esterni usando `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="0ccc5-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="0ccc5-212">In questo esempio, si aggiunge un profilo esistente di endpoint esterni tooan.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="0ccc5-213">profilo Hello è specificato utilizzando i nomi di gruppi di profili e risorse hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="0ccc5-214">Aggiunta di endpoint 'annidati'</span><span class="sxs-lookup"><span data-stu-id="0ccc5-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="0ccc5-215">Ciascun profilo di Gestione traffico specifica un solo metodo di routing del traffico.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="0ccc5-216">Esistono tuttavia scenari che richiedono più sofisticato il routing del traffico di routing hello fornito da un unico profilo di Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="0ccc5-217">È possibile nidificare i vantaggi di gestione traffico profili toocombine hello di più di un metodo di routing del traffico.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="0ccc5-218">Profili nidificati consentono toooverride hello predefinito Traffic Manager comportamento toosupport maggiori e le distribuzioni di applicazioni più complesse.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="0ccc5-219">Per esempi più dettagliati, vedere [Profili annidati di Gestione traffico](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="0ccc5-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="0ccc5-220">Gli endpoint annidati sono configurati nel profilo padre hello, utilizzando un tipo di endpoint specifico, 'NestedEndpoints'.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="0ccc5-221">Quando si specificano endpoint annidati:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="0ccc5-222">endpoint Hello deve essere specificata utilizzando il parametro 'ID risorsa di destinazione' hello</span><span class="sxs-lookup"><span data-stu-id="0ccc5-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="0ccc5-223">Se viene utilizzato il metodo di routing del traffico "Prestazioni" hello, hello 'EndpointLocation' è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="0ccc5-224">In caso contrario, è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-224">Otherwise it is optional.</span></span> <span data-ttu-id="0ccc5-225">il valore di Hello deve essere un [nome dell'area di Azure valido](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="0ccc5-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="0ccc5-226">Hello 'Peso' e 'Priority' sono facoltativi, come endpoint di Azure.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="0ccc5-227">parametro 'MinChildEndpoints' Hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="0ccc5-228">valore predefinito di Hello è '1'.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-228">hello default value is '1'.</span></span> <span data-ttu-id="0ccc5-229">Se hello degli endpoint disponibile scende sotto questa soglia, profilo padre hello considera profilo figlio hello 'danneggiato' e la trasferisce traffico toohello altri endpoint nel profilo padre hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="0ccc5-230">Esempio 1: Aggiunta di endpoint annidati usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="0ccc5-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="0ccc5-231">In questo esempio, è creare padre e figlio di Traffic Manager nuovi profili Aggiungi figlio hello come padre toohello endpoint annidati e commit delle modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="0ccc5-232">Per brevità, in questo esempio, non è stato aggiunto qualsiasi altro endpoint toohello padre o figlio profilo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="0ccc5-233">Esempio 2: Aggiunta di endpoint annidati usando `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="0ccc5-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="0ccc5-234">In questo esempio è aggiungere un profilo figlio esistente come un profilo padre esistente tooan endpoint annidati.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="0ccc5-235">profilo Hello è specificato utilizzando i nomi di gruppi di profili e risorse hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="0ccc5-236">Aggiornare un endpoint di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="0ccc5-237">Esistono due modi tooupdate un endpoint di gestione traffico esistente:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="0ccc5-238">Profilo di Traffic Manager hello tramite `Get-AzureRmTrafficManagerProfile`, aggiornare le proprietà endpoint hello nel profilo hello e salvare le modifiche di hello utilizzando `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="0ccc5-239">Questo metodo presenta il vantaggio di hello di essere in grado di tooupdate più di un endpoint in un'unica operazione.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="0ccc5-240">Ottenere l'endpoint di gestione traffico hello utilizzando `Get-AzureRmTrafficManagerEndpoint`, aggiornare le proprietà endpoint hello e salvare le modifiche di hello utilizzando `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="0ccc5-241">Questo metodo è più semplice, poiché non richiede l'indicizzazione in una matrice di endpoint hello nel profilo hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="0ccc5-242">Esempio 1: Aggiornamento di endpoint usando `Get-AzureRmTrafficManagerProfile` e `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="0ccc5-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="0ccc5-243">In questo esempio viene modificata la priorità di hello in due endpoint all'interno di un profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="0ccc5-244">Esempio 2: Aggiornamento di un endpoint usando `Get-AzureRmTrafficManagerEndpoint` e `Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="0ccc5-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="0ccc5-245">In questo esempio è modificare il peso di hello di un singolo endpoint in un profilo esistente.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="0ccc5-246">Abilitazione e disabilitazione di endpoint e profili</span><span class="sxs-lookup"><span data-stu-id="0ccc5-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="0ccc5-247">Gestione traffico consente singoli endpoint toobe abilitati e disabilitati, oltre a consentire l'abilitazione e disabilitazione dei profili interi.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="0ccc5-248">Queste modifiche possono essere apportate dalle risorse hello ottenimento o l'aggiornamento o l'impostazione di endpoint o un profilo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="0ccc5-249">toostreamline queste operazioni comuni, sono anche supportate tramite cmdlet dedicati.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="0ccc5-250">Esempio 1: Abilitazione e disabilitazione di un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="0ccc5-251">Utilizzare un profilo di Traffic Manager, tooenable `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="0ccc5-252">è possibile specificare il profilo di Hello utilizzando un oggetto profilo.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="0ccc5-253">Hello oggetto profilo può essere passato tramite la pipeline hello o utilizzando hello '-TrafficManagerProfile' parametro.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="0ccc5-254">In questo esempio, si specifica il profilo di hello dal nome del gruppo di risorse e profilo di hello.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="0ccc5-255">toodisable un profilo di gestione traffico:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="0ccc5-256">cmdlet Disable-AzureRmTrafficManagerProfile Hello chiesta la conferma.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="0ccc5-257">Questo messaggio può essere soppresso mediante hello '-Force' parametro.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="0ccc5-258">Esempio 2: Abilitazione e disabilitazione di un endpoint di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="0ccc5-259">tooenable un endpoint di Traffic Manager, utilizzare `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="0ccc5-260">Esistono due endpoint di hello toospecify modi</span><span class="sxs-lookup"><span data-stu-id="0ccc5-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="0ccc5-261">Utilizzando un oggetto TrafficManagerEndpoint passato tramite la pipeline hello o hello '-TrafficManagerEndpoint' parametro</span><span class="sxs-lookup"><span data-stu-id="0ccc5-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="0ccc5-262">Utilizzando il nome dell'endpoint hello, tipo di endpoint, nome del profilo e nome del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="0ccc5-263">Analogamente, toodisable un endpoint di gestione traffico:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="0ccc5-264">Come con `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet chiesta la conferma.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="0ccc5-265">Questo messaggio può essere soppresso mediante hello '-Force' parametro.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="0ccc5-266">Eliminare un endpoint di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="0ccc5-267">tooremove singoli endpoint, utilizzare hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="0ccc5-268">Il cmdlet richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="0ccc5-269">Questo messaggio può essere soppresso mediante hello '-Force' parametro.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="0ccc5-270">Eliminare un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="0ccc5-271">toodelete un profilo di Traffic Manager, utilizzare hello `Remove-AzureRmTrafficManagerProfile` specificando nomi di gruppi di profili e risorse hello:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="0ccc5-272">Il cmdlet richiede una conferma.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="0ccc5-273">Questo messaggio può essere soppresso mediante hello '-Force' parametro.</span><span class="sxs-lookup"><span data-stu-id="0ccc5-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="0ccc5-274">Hello profilo toobe eliminato è possibile specificare anche utilizzando un oggetto profilo:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="0ccc5-275">Questa sequenza può anche essere inoltrata tramite pipe:</span><span class="sxs-lookup"><span data-stu-id="0ccc5-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="0ccc5-276">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0ccc5-276">Next steps</span></span>

[<span data-ttu-id="0ccc5-277">Monitoraggio di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="0ccc5-278">Considerazioni sulle prestazioni di gestione traffico</span><span class="sxs-lookup"><span data-stu-id="0ccc5-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
