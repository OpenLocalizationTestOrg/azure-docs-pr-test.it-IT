---
title: Come usare Gestione API di Azure con le reti virtuali interne | Microsoft Docs
description: Informazioni su come installare e configurare Gestione API di Azure in una rete virtuale interna.
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
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="b1841-103">Uso del servizio Gestione API di Azure con una rete virtuale interna</span><span class="sxs-lookup"><span data-stu-id="b1841-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="b1841-104">Grazie alle reti virtuali di Azure, Gestione API è in grado di gestire API che non hanno accesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="b1841-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="b1841-105">È disponibile una serie di tecnologie VPN per effettuare tale connessione; Gestione API può essere installato in due modi principali all'interno della rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="b1841-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="b1841-106">Esterno</span><span class="sxs-lookup"><span data-stu-id="b1841-106">External</span></span>
* <span data-ttu-id="b1841-107">Interno</span><span class="sxs-lookup"><span data-stu-id="b1841-107">Internal</span></span>

## <span data-ttu-id="b1841-108"><a name="overview"> </a>Panoramica</span><span class="sxs-lookup"><span data-stu-id="b1841-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="b1841-109">Quando Gestione API viene installato in modalità di rete virtuale interna, tutti gli endpoint di servizio, ovvero gateway, portale per sviluppatori, portale di pubblicazione, gestione diretta e GIT, sono visibili solo all'interno di una rete virtuale i cui accessi sono gestiti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="b1841-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="b1841-110">Nessuno degli endpoint di servizio è registrato nel server DNS pubblico.</span><span class="sxs-lookup"><span data-stu-id="b1841-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="b1841-111">Usando Gestione API in modalità interna è possibile riscontrare gli scenari seguenti</span><span class="sxs-lookup"><span data-stu-id="b1841-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="b1841-112">Consentire un accesso esterno sicuro da parte di terzi alle API ospitate in un data center privato, tramite connessioni VPN da sito a sito o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b1841-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="b1841-113">Abilitare scenari cloud ibrid esponendo le API basate su cloud e locali tramite un gateway comune.</span><span class="sxs-lookup"><span data-stu-id="b1841-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="b1841-114">Gestire le API ospitate in più aree geografiche usando un singolo endpoint del gateway.</span><span class="sxs-lookup"><span data-stu-id="b1841-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="b1841-115"><a name="enable-vpn"> </a>Creazione di un servizio Gestione API in una rete virtuale interna</span><span class="sxs-lookup"><span data-stu-id="b1841-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="b1841-116">Il servizio Gestione API in una rete virtuale interna viene ospitato dietro un servizio di bilanciamento del carico interno (ILB).</span><span class="sxs-lookup"><span data-stu-id="b1841-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="b1841-117">L'indirizzo IP del servizio di bilanciamento del carico interno si trova nell'intervallo [RFC1918](http://www.faqs.org/rfcs/rfc1918.html).</span><span class="sxs-lookup"><span data-stu-id="b1841-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="b1841-118">Abilitare la connessione della rete virtuale usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b1841-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="b1841-119">Creare innanzitutto il servizio Gestione API, attenendosi alla procedura [Creare un servizio Gestione API][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="b1841-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="b1841-120">Quindi configurare Gestione API per la distribuzione all'interno di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b1841-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![Menu per la configurazione di Gestione API nella rete virtuale interna][api-management-using-internal-vnet-menu]

<span data-ttu-id="b1841-122">Una volta completata la distribuzione, nel dashboard dovrebbe essere visualizzato l'indirizzo IP virtuale interno del servizio.</span><span class="sxs-lookup"><span data-stu-id="b1841-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![Dashboard di gestione API con rete virtuale interna configurata][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="b1841-124">Abilitare la connessione della rete virtuale usando i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1841-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="b1841-125">È inoltre possibile abilitare la connettività della rete virtuale utilizzando i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1841-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="b1841-126">**Creare un servizio Gestione API all'interno di una rete virtuale**: usare il cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) per creare e un servizio Gestione API di Azure all'interno di una rete virtuale e configurarlo per usare il tipo di rete virtuale interna.</span><span class="sxs-lookup"><span data-stu-id="b1841-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="b1841-127">**Distribuire un servizio Gestione API esistente all'interno di una rete virtuale**: usare il cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) per spostare un servizio Gestione API di Azure esistente all'interno di una rete virtuale e configurarlo per usare il tipo di rete virtuale interna.</span><span class="sxs-lookup"><span data-stu-id="b1841-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <span data-ttu-id="b1841-128"><a name="apim-dns-configuration"></a>Configurazione del DNS</span><span class="sxs-lookup"><span data-stu-id="b1841-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="b1841-129">Quando si usa Gestione API in modalità di rete virtuale esterna, il DNS è gestito da Azure.</span><span class="sxs-lookup"><span data-stu-id="b1841-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="b1841-130">Per la modalità di rete virtuale interna, è necessario gestire un proprio DNS.</span><span class="sxs-lookup"><span data-stu-id="b1841-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="b1841-131">Il servizio Gestione API non ascolta le richieste in arrivo agli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="b1841-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="b1841-132">Risponde solo alle richieste inviate al nome host configurato sui relativi endpoint di servizio, che includono gateway, portale per sviluppatori, portale di pubblicazione, endpoint di gestione diretta e GIT.</span><span class="sxs-lookup"><span data-stu-id="b1841-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="b1841-133">Accesso ai nomi host predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b1841-133">Access on default host names:</span></span>
<span data-ttu-id="b1841-134">Quando si crea un servizio Gestione API nel Cloud Azure pubblico, denominato ad esempio "contoso", vengono configurati i seguenti endpoint di servizio per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b1841-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="b1841-135">Gateway o Proxy: contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b1841-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="b1841-136">Portale di pubblicazione portale per sviluppatori: contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b1841-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="b1841-137">Endpoint di gestione diretta: contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b1841-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="b1841-138">GIT: contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b1841-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="b1841-139">Per accedere a questi endpoint del servizio Gestione API è possibile creare una macchina virtuale in una subnet connessa alla rete virtuale in cui viene distribuito Gestione API.</span><span class="sxs-lookup"><span data-stu-id="b1841-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="b1841-140">Supponendo che l'indirizzo IP virtuale interno per il servizio sia 10.0.0.5, è possibile eseguire il mapping del file host (%SystemDrive%\drivers\etc\hosts) come segue:</span><span class="sxs-lookup"><span data-stu-id="b1841-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="b1841-141">10.0.0.5    contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b1841-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="b1841-142">10.0.0.5    contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b1841-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="b1841-143">10.0.0.5    contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b1841-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="b1841-144">10.0.0.5    contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="b1841-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="b1841-145">È quindi possibile accedere tutti gli endpoint di servizio dalla macchina virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="b1841-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="b1841-146">Se si usa un server DNS personalizzato in una rete virtuale, è anche possibile creare record DNS A e accedere agli endpoint da qualsiasi punto nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b1841-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="b1841-147">Accedere a nomi di dominio personalizzati:</span><span class="sxs-lookup"><span data-stu-id="b1841-147">Access on custom domain names:</span></span>
<span data-ttu-id="b1841-148">Se non si desidera accedere al servizio Gestione API con i nomi host predefiniti, è possibile configurare nomi di dominio personalizzati per tutti gli endpoint di servizio come mostrato di seguito</span><span class="sxs-lookup"><span data-stu-id="b1841-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Configurazione di un dominio personalizzato per Gestione API][api-management-custom-domain-name]

<span data-ttu-id="b1841-150">È quindi possibile creare record A nel server DNS per accedere a questi endpoint. Si noti che gli endpoint sono accessibili solo dall'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b1841-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="b1841-151"><a name="related-content"> </a>Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="b1841-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="b1841-152">[Problemi di configurazione di rete comuni durante la configurazione di Gestione API in una rete virtuale][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="b1841-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="b1841-153">Domande frequenti sulle reti virtuali</span><span class="sxs-lookup"><span data-stu-id="b1841-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="b1841-154">Creazione di un record A in DNS</span><span class="sxs-lookup"><span data-stu-id="b1841-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
