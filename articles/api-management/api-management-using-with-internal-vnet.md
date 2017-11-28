---
title: aaaHow toouse gestione API di Azure con la rete virtuale interna | Documenti Microsoft
description: Informazioni su come toosetup e configurare Gestione API di Azure in rete virtuale interna.
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="7d79f-103">Uso del servizio Gestione API di Azure con una rete virtuale interna</span><span class="sxs-lookup"><span data-stu-id="7d79f-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="7d79f-104">Con reti virtuali di Azure (Vnet), gestione API possono gestire le API non è accessibile su Internet hello.</span><span class="sxs-lookup"><span data-stu-id="7d79f-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on hello Internet.</span></span> <span data-ttu-id="7d79f-105">Una serie di tecnologie VPN è connessione hello toomake disponibili e gestione API può essere distribuito in due modalità principali all'interno di hello rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="7d79f-105">A number of VPN technologies are available toomake hello connection and API Management can be deployed in two main modes inside hello VNET:</span></span>
* <span data-ttu-id="7d79f-106">Esterno</span><span class="sxs-lookup"><span data-stu-id="7d79f-106">External</span></span>
* <span data-ttu-id="7d79f-107">Interno</span><span class="sxs-lookup"><span data-stu-id="7d79f-107">Internal</span></span>

## <span data-ttu-id="7d79f-108"><a name="overview"> </a>Panoramica</span><span class="sxs-lookup"><span data-stu-id="7d79f-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="7d79f-109">Quando l'API di gestione viene distribuito in una modalità di rete virtuale interna, tutti gli endpoint servizio hello (gateway, portale per sviluppatori, portale di pubblicazione, la gestione diretta e Git) vengono solo all'interno di una rete virtuale che si controllano l'accesso a.</span><span class="sxs-lookup"><span data-stu-id="7d79f-109">When API Management is deployed in an Internal Virtual network mode, all hello service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="7d79f-110">Nessuno degli endpoint del servizio hello registrati nel Server DNS pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="7d79f-110">None of hello service endpoints are registered on hello Public DNS Server.</span></span>

<span data-ttu-id="7d79f-111">Utilizzo di gestione API in modalità interna, è possibile ottenere hello seguenti scenari</span><span class="sxs-lookup"><span data-stu-id="7d79f-111">Using API Management in Internal mode, you can achieve hello following scenarios</span></span>
* <span data-ttu-id="7d79f-112">Consentire un accesso esterno sicuro da parte di terzi alle API ospitate in un data center privato, tramite connessioni VPN da sito a sito o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7d79f-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="7d79f-113">Abilitare scenari cloud ibrid esponendo le API basate su cloud e locali tramite un gateway comune.</span><span class="sxs-lookup"><span data-stu-id="7d79f-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="7d79f-114">Gestire le API ospitate in più aree geografiche usando un singolo endpoint del gateway.</span><span class="sxs-lookup"><span data-stu-id="7d79f-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="7d79f-115"><a name="enable-vpn"> </a>Creazione di un servizio Gestione API in una rete virtuale interna</span><span class="sxs-lookup"><span data-stu-id="7d79f-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="7d79f-116">Servizio gestione API nella rete virtuale interna Hello è ospitato dietro un Balancer(ILB) carico interno.</span><span class="sxs-lookup"><span data-stu-id="7d79f-116">hello API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="7d79f-117">l'indirizzo IP del bilanciamento del carico interno hello Hello è hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) intervallo.</span><span class="sxs-lookup"><span data-stu-id="7d79f-117">hello IP Address of hello ILB is in hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="7d79f-118">Abilitare la connessione della rete virtuale usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7d79f-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="7d79f-119">Creare innanzitutto il servizio di gestione API hello seguendo i passaggi di hello [servizio Gestione API di creazione][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="7d79f-119">First create hello API Management service by following hello steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="7d79f-120">Quindi configurazione Gestione API toobe distribuiti all'interno di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d79f-120">Then set-up API Management toobe deployed inside a Virtual network.</span></span>

![Menu per la configurazione di Gestione API nella rete virtuale interna][api-management-using-internal-vnet-menu]

<span data-ttu-id="7d79f-122">Dopo il completamento della distribuzione di hello, dovrebbe essere hello interno indirizzo IP virtuale del servizio nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="7d79f-122">After hello deployment succeeds, you should see hello Internal Virtual IP Address of your service on hello dashboard.</span></span>

![Dashboard di gestione API con rete virtuale interna configurata][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="7d79f-124">Abilitare la connessione della rete virtuale usando i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d79f-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="7d79f-125">È inoltre possibile abilitare la connettività di rete virtuale utilizzando i cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7d79f-125">You can also enable VNET connectivity using hello PowerShell cmdlets.</span></span>

* <span data-ttu-id="7d79f-126">**Creare un servizio di gestione API all'interno di una rete virtuale**: utilizzare i cmdlet di hello [New AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate una gestione API di Azure del servizio all'interno di una rete virtuale e configurarlo come tipo di rete virtuale interna toouse hello.</span><span class="sxs-lookup"><span data-stu-id="7d79f-126">**Create an API Management service inside a VNET**: Use hello cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate an Azure API Management service inside a VNET and configure it toouse hello Internal VNET type.</span></span>

* <span data-ttu-id="7d79f-127">**Distribuire un servizio di gestione API esistente all'interno di una rete virtuale**: utilizzare i cmdlet di hello [aggiornamento AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove una gestione API di Azure esistente all'interno di una rete virtuale del servizio e configurarlo toouse Tipo di rete virtuale interna.</span><span class="sxs-lookup"><span data-stu-id="7d79f-127">**Deploy an existing API Management service inside a VNET**: Use hello cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove an existing Azure API Management service inside a Virtual network and configure it toouse Internal VNET type.</span></span>

## <span data-ttu-id="7d79f-128"><a name="apim-dns-configuration"></a>Configurazione del DNS</span><span class="sxs-lookup"><span data-stu-id="7d79f-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="7d79f-129">Quando si usa Gestione API in modalità di rete virtuale esterna, il DNS è gestito da Azure.</span><span class="sxs-lookup"><span data-stu-id="7d79f-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="7d79f-130">Modalità di rete virtuale interna, è possibile toomanage il proprio servizio DNS.</span><span class="sxs-lookup"><span data-stu-id="7d79f-130">For Internal Virtual network mode, you have toomanage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="7d79f-131">Servizio gestione API non è in ascolto toorequests presto agli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="7d79f-131">API Management service does not listen toorequests coming on IP addresses.</span></span> <span data-ttu-id="7d79f-132">Risponde solo toorequests toohello nome host configurato sui relativi endpoint di servizio (che include i gateway, portale per sviluppatori, server di pubblicazione portale, la gestione diretta endpoint e git).</span><span class="sxs-lookup"><span data-stu-id="7d79f-132">It only responds toorequests toohello Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="7d79f-133">Accesso ai nomi host predefiniti:</span><span class="sxs-lookup"><span data-stu-id="7d79f-133">Access on default host names:</span></span>
<span data-ttu-id="7d79f-134">Quando si crea un servizio di gestione API in un cloud pubblico di Azure, denominato "contoso", ad esempio, hello seguenti endpoint di servizio sono configurati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7d79f-134">When you create an API Management service in public Azure cloud, named "contoso" for example, hello following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="7d79f-135">Gateway o Proxy: contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7d79f-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="7d79f-136">Portale di pubblicazione portale per sviluppatori: contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7d79f-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="7d79f-137">Endpoint di gestione diretta: contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7d79f-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="7d79f-138">GIT: contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7d79f-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="7d79f-139">tooaccess questi endpoint del servizio Gestione API, è possibile creare una macchina virtuale in una rete virtuale di toohello subnet connesse in cui viene distribuito l'API di gestione.</span><span class="sxs-lookup"><span data-stu-id="7d79f-139">tooaccess these API Management service endpoints, you can create a Virtual Machine in a subnet connected toohello Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="7d79f-140">Supponendo che hello indirizzo IP virtuale interno per il servizio sia 10.0.0.5, è possibile eseguire hello mapping del file host (% SystemDrive%\drivers\etc\hosts) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7d79f-140">Assuming hello Internal Virtual IP Address for your service is 10.0.0.5, you can do hello hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="7d79f-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7d79f-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="7d79f-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7d79f-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="7d79f-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7d79f-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="7d79f-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="7d79f-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="7d79f-145">È possibile accedere tutti gli endpoint di servizio hello da hello macchina virtuale è stato creato.</span><span class="sxs-lookup"><span data-stu-id="7d79f-145">You can then access all hello service endpoints from hello Virtual Machine you created.</span></span> <span data-ttu-id="7d79f-146">Se si usa un server DNS personalizzato in una rete virtuale, è anche possibile creare record DNS A e accedere agli endpoint da qualsiasi punto nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d79f-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="7d79f-147">Accedere a nomi di dominio personalizzati:</span><span class="sxs-lookup"><span data-stu-id="7d79f-147">Access on custom domain names:</span></span>
<span data-ttu-id="7d79f-148">Se non si desidera tooaccess hello servizio Gestione API con i nomi host di hello predefiniti, è possibile configurare i nomi di dominio personalizzato per tutti gli endpoint del servizio come di seguito</span><span class="sxs-lookup"><span data-stu-id="7d79f-148">If you don’t want tooaccess hello API Management service with hello default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Configurazione di un dominio personalizzato per Gestione API][api-management-custom-domain-name]

<span data-ttu-id="7d79f-150">È quindi possibile creare un record in tooaccess il Server DNS questi endpoint che sono accessibili solo da all'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d79f-150">Then you can create A records in your DNS Server tooaccess these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="7d79f-151"><a name="related-content"></a>Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="7d79f-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="7d79f-152">[Problemi di configurazione di rete comuni durante la configurazione di Gestione API in una rete virtuale][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="7d79f-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="7d79f-153">Domande frequenti sulle reti virtuali</span><span class="sxs-lookup"><span data-stu-id="7d79f-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="7d79f-154">Creazione di un record A in DNS</span><span class="sxs-lookup"><span data-stu-id="7d79f-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
