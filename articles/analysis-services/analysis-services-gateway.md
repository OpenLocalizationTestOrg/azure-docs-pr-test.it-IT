---
title: Gateway dati locale | Microsoft Docs
description: "Un gateway locale è necessario se il server Analysis Services di Azure si connette a origini dati locali."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: 514b5404e8cbfa0baa657eb41736e20cad502638
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connecting-to-on-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="a9414-103">Connessione a origini dati locali con Gateway dati locale di Azure</span><span class="sxs-lookup"><span data-stu-id="a9414-103">Connecting to on-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="a9414-104">Il gateway dati locale svolge la funzione di ponte, garantendo il trasferimento sicuro dei dati tra le origini dati locali e i server Azure Analysis Services nel cloud.</span><span class="sxs-lookup"><span data-stu-id="a9414-104">The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in the cloud.</span></span> <span data-ttu-id="a9414-105">Oltre a lavorare con più server Azure Analysis Services nella stessa area, la versione più recente del gateway funziona anche con Microsoft Flow, Power BI, app Power e App per la logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9414-105">In addition to working with multiple Azure Analysis Services servers in the same region, the latest version of the gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="a9414-106">È possibile associare più servizi nella stessa area con un singolo gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-106">You can associate multiple services in the same region with a single gateway.</span></span> 

 <span data-ttu-id="a9414-107">Azure Analysis Services richiede una risorsa gateway nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="a9414-107">Azure Analysis Services requires a gateway resource in the same region.</span></span> <span data-ttu-id="a9414-108">Ad esempio, se si dispone di server di Analysis Services di Azure nell'area Stati Uniti orientali 2, è necessario una risorsa gateway nell'area Stati Uniti orientali 2.</span><span class="sxs-lookup"><span data-stu-id="a9414-108">For example, if you have Azure Analysis Services servers in the East US 2 region, you need a gateway resource in the East US 2 region.</span></span> <span data-ttu-id="a9414-109">Più server in Stati Uniti orientali 2 possono utilizzare lo stesso gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-109">Multiple servers in East US 2 can use the same gateway.</span></span>

<span data-ttu-id="a9414-110">Ottenere il programma di installazione con il gateway la prima volta consiste in un processo in quattro parti:</span><span class="sxs-lookup"><span data-stu-id="a9414-110">Getting setup with the gateway the first time is a four-part process:</span></span>

- <span data-ttu-id="a9414-111">**Scaricare ed eseguire il programma di installazione**: questo passaggio consente di installare un servizio gateway su un computer all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a9414-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="a9414-112">**Registrare il gateway**: in questo passaggio, si specifica un nome e la chiave di ripristino per il gateway e si seleziona un'area, si registra il gateway con il servizio Cloud Gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with the Gateway Cloud Service.</span></span>

- <span data-ttu-id="a9414-113">**Creare una risorsa per il gateway in Azure**: in questo passaggio, si crea una risorsa per il gateway nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9414-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="a9414-114">**Connettere i server per la risorsa per il gateway**: dopo aver creato una risorsa per il gateway nella sottoscrizione, è possibile iniziare a connettere i server.</span><span class="sxs-lookup"><span data-stu-id="a9414-114">**Connect your servers to your gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers to it.</span></span>

<span data-ttu-id="a9414-115">Dopo aver configurato una risorsa per il gateway per la sottoscrizione, è possibile connettere più server e altri servizi ad esso.</span><span class="sxs-lookup"><span data-stu-id="a9414-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services to it.</span></span> <span data-ttu-id="a9414-116">È sufficiente installare un gateway diverso e creare risorse aggiuntive per il gateway se si dispone di server o altri servizi in un'area diversa.</span><span class="sxs-lookup"><span data-stu-id="a9414-116">You only need to install a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="a9414-117">Per iniziare subito, vedere [Installare e configurare il gateway dati locale](analysis-services-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="a9414-117">To get started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="a9414-118"><a name="how-it-works"> </a>Funzionamento</span><span class="sxs-lookup"><span data-stu-id="a9414-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="a9414-119">Il gateway installato su un computer dell'organizzazione viene eseguito come servizio Windows, **Gateway dati locale**.</span><span class="sxs-lookup"><span data-stu-id="a9414-119">The gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="a9414-120">Il servizio locale è registrato con il servizio Cloud Gateway tramite il bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9414-120">This local service is registered with the Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="a9414-121">È quindi possibile creare una servizio Cloud della risorsa per il gateway per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9414-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="a9414-122">I server di Azure Analysis Services quindi sono connessi alla risorsa per il gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-122">Your Azure Analysis Services servers are then connected to your gateway resource.</span></span> <span data-ttu-id="a9414-123">Quando i modelli nel server devono connettersi ai dati locali di origine per le query o l'elaborazione, un flusso di dati e query attraversa la risorsa del gateway, il bus di servizio di Azure, il servizio gateway dati locale e le origini dati.</span><span class="sxs-lookup"><span data-stu-id="a9414-123">When models on your server need to connect to your on-premises data sources for queries or processing, a query and data flow traverses the gateway resource, Azure Service Bus, the local on-premises data gateway service, and your data sources.</span></span> 

![Funzionamento](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="a9414-125">Query e flusso di dati:</span><span class="sxs-lookup"><span data-stu-id="a9414-125">Queries and data flow:</span></span>

1. <span data-ttu-id="a9414-126">Il servizio cloud crea una query con le credenziali crittografate per l'origine dati locale.</span><span class="sxs-lookup"><span data-stu-id="a9414-126">A query is created by the cloud service with the encrypted credentials for the on-premises data source.</span></span> <span data-ttu-id="a9414-127">La query viene inviata a una coda per l'elaborazione da parte del gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-127">It's then sent to a queue for the gateway to process.</span></span>
2. <span data-ttu-id="a9414-128">Il servizio cloud del gateway analizza la query e inserisce la richiesta nel [bus di servizio di Azure](https://azure.microsoft.com/documentation/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="a9414-128">The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="a9414-129">Il gateway dati locale esegue il polling del bus di servizio per le richieste in sospeso.</span><span class="sxs-lookup"><span data-stu-id="a9414-129">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="a9414-130">Il gateway riceve la query, decrittografa le credenziali e si connette alle origini dati usando tali credenziali.</span><span class="sxs-lookup"><span data-stu-id="a9414-130">The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.</span></span>
5. <span data-ttu-id="a9414-131">Invia quindi la query all'origine dati per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a9414-131">The gateway sends the query to the data source for execution.</span></span>
6. <span data-ttu-id="a9414-132">I risultati vengono inviati dall'origine dati al gateway e quindi al servizio cloud e al server.</span><span class="sxs-lookup"><span data-stu-id="a9414-132">The results are sent from the data source, back to the gateway, and then onto the cloud service and your server.</span></span>

## <span data-ttu-id="a9414-133"><a name="windows-service-account"> </a>Account del servizio Windows</span><span class="sxs-lookup"><span data-stu-id="a9414-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="a9414-134">Il gateway dati locale è configurato per usare *NT SERVICE\PBIEgwService* come credenziale di accesso al servizio Windows.</span><span class="sxs-lookup"><span data-stu-id="a9414-134">The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential.</span></span> <span data-ttu-id="a9414-135">Per impostazione predefinita, dispone del diritto di accesso come servizio nel contesto del computer in cui viene installato il gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-135">By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on.</span></span> <span data-ttu-id="a9414-136">Questa credenziale non coincide con l'account usato per la connessione alle origini dati locali o con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="a9414-136">This credential is not the same account used to connect to on-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="a9414-137">Se si verificano problemi di autenticazione con il server proxy, può essere necessario trasformare l'account del servizio Windows nell'account di un utente del dominio o nell'account di un servizio gestito.</span><span class="sxs-lookup"><span data-stu-id="a9414-137">If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.</span></span>

## <span data-ttu-id="a9414-138"><a name="ports"> </a>Porte</span><span class="sxs-lookup"><span data-stu-id="a9414-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="a9414-139">Il gateway crea una connessione in uscita al bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9414-139">The gateway creates an outbound connection to Azure Service Bus.</span></span> <span data-ttu-id="a9414-140">Comunica sulle porte in uscita seguenti: TCP 443 (impostazione predefinita), 5671, 5672 e da 9350 a 9354.</span><span class="sxs-lookup"><span data-stu-id="a9414-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="a9414-141">Non sono richieste porte in ingresso.</span><span class="sxs-lookup"><span data-stu-id="a9414-141">The gateway does not require inbound ports.</span></span>

<span data-ttu-id="a9414-142">È consigliabile inserire nell'elenco degli elementi consentiti gli indirizzi IP per l'area dati del firewall.</span><span class="sxs-lookup"><span data-stu-id="a9414-142">We recommend you whitelist the IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="a9414-143">È possibile scaricare l'[elenco degli indirizzi IP dei data center di Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="a9414-143">You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="a9414-144">L'elenco viene aggiornato ogni settimana.</span><span class="sxs-lookup"><span data-stu-id="a9414-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="a9414-145">Gli indirizzi IP inclusi nell'elenco degli indirizzi IP dei data center di Azure sono nella notazione CIDR.</span><span class="sxs-lookup"><span data-stu-id="a9414-145">The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="a9414-146">Ad esempio, 10.0.0.0/24 non significa da 10.0.0.0 a 10.0.0.24.</span><span class="sxs-lookup"><span data-stu-id="a9414-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="a9414-147">Per altre informazioni, vedere [CIDR notation](http://whatismyipaddress.com/cidr) (Notazione CIDR).</span><span class="sxs-lookup"><span data-stu-id="a9414-147">Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="a9414-148">Di seguito sono indicati i nomi di dominio completi usati dal gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-148">The following are the fully qualified domain names used by the gateway.</span></span>

| <span data-ttu-id="a9414-149">Nomi di dominio</span><span class="sxs-lookup"><span data-stu-id="a9414-149">Domain names</span></span> | <span data-ttu-id="a9414-150">Porte in uscita</span><span class="sxs-lookup"><span data-stu-id="a9414-150">Outbound ports</span></span> | <span data-ttu-id="a9414-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a9414-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9414-152">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="a9414-152">*.powerbi.com</span></span> |<span data-ttu-id="a9414-153">80</span><span class="sxs-lookup"><span data-stu-id="a9414-153">80</span></span> |<span data-ttu-id="a9414-154">HTTP usato per scaricare il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="a9414-154">HTTP used to download the installer.</span></span> |
| <span data-ttu-id="a9414-155">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="a9414-155">*.powerbi.com</span></span> |<span data-ttu-id="a9414-156">443</span><span class="sxs-lookup"><span data-stu-id="a9414-156">443</span></span> |<span data-ttu-id="a9414-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a9414-157">HTTPS</span></span> |
| <span data-ttu-id="a9414-158">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="a9414-158">*.analysis.windows.net</span></span> |<span data-ttu-id="a9414-159">443</span><span class="sxs-lookup"><span data-stu-id="a9414-159">443</span></span> |<span data-ttu-id="a9414-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a9414-160">HTTPS</span></span> |
| <span data-ttu-id="a9414-161">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="a9414-161">*.login.windows.net</span></span> |<span data-ttu-id="a9414-162">443</span><span class="sxs-lookup"><span data-stu-id="a9414-162">443</span></span> |<span data-ttu-id="a9414-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a9414-163">HTTPS</span></span> |
| <span data-ttu-id="a9414-164">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="a9414-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="a9414-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="a9414-165">5671-5672</span></span> |<span data-ttu-id="a9414-166">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="a9414-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="a9414-167">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="a9414-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="a9414-168">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="a9414-168">443, 9350-9354</span></span> |<span data-ttu-id="a9414-169">Listener in Inoltro del Bus di servizio su TCP (richiede 443 per l'acquisizione del token di Controllo di accesso)</span><span class="sxs-lookup"><span data-stu-id="a9414-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="a9414-170">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="a9414-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="a9414-171">443</span><span class="sxs-lookup"><span data-stu-id="a9414-171">443</span></span> |<span data-ttu-id="a9414-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a9414-172">HTTPS</span></span> |
| <span data-ttu-id="a9414-173">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="a9414-173">*.core.windows.net</span></span> |<span data-ttu-id="a9414-174">443</span><span class="sxs-lookup"><span data-stu-id="a9414-174">443</span></span> |<span data-ttu-id="a9414-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a9414-175">HTTPS</span></span> |
| <span data-ttu-id="a9414-176">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a9414-176">login.microsoftonline.com</span></span> |<span data-ttu-id="a9414-177">443</span><span class="sxs-lookup"><span data-stu-id="a9414-177">443</span></span> |<span data-ttu-id="a9414-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="a9414-178">HTTPS</span></span> |
| <span data-ttu-id="a9414-179">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="a9414-179">*.msftncsi.com</span></span> |<span data-ttu-id="a9414-180">443</span><span class="sxs-lookup"><span data-stu-id="a9414-180">443</span></span> |<span data-ttu-id="a9414-181">Usato per testare la connettività a Internet se il gateway non è raggiungibile dal servizio Power BI.</span><span class="sxs-lookup"><span data-stu-id="a9414-181">Used to test internet connectivity if the gateway is unreachable by the Power BI service.</span></span> |
| <span data-ttu-id="a9414-182">*.microsoftonline-p.com</span><span class="sxs-lookup"><span data-stu-id="a9414-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="a9414-183">443</span><span class="sxs-lookup"><span data-stu-id="a9414-183">443</span></span> |<span data-ttu-id="a9414-184">Usato per l'autenticazione, a seconda della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a9414-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="a9414-185"><a name="force-https"></a>Forzare la comunicazione HTTPS con il bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="a9414-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="a9414-186">È possibile forzare il gateway a comunicare con il bus di servizio di Azure usando HTTPS anziché TCP diretto. Questa operazione, tuttavia, può ridurre le prestazioni in misura significativa.</span><span class="sxs-lookup"><span data-stu-id="a9414-186">You can force the gateway to communicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="a9414-187">È necessario modificare il file *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* modificando il valore da `AutoDetect` in `Https`.</span><span class="sxs-lookup"><span data-stu-id="a9414-187">You can modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing the value from `AutoDetect` to `Https`.</span></span> <span data-ttu-id="a9414-188">Questo file si trova solitamente in *C:\Programmi\On-premises data gateway*.</span><span class="sxs-lookup"><span data-stu-id="a9414-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="a9414-189"><a name="faq"></a>Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="a9414-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="a9414-190">Generale</span><span class="sxs-lookup"><span data-stu-id="a9414-190">General</span></span>

<span data-ttu-id="a9414-191">**D**: È necessario un gateway per le origini dati nel cloud, ad esempio il database SQL di Azure?</span><span class="sxs-lookup"><span data-stu-id="a9414-191">**Q**: Do I need a gateway for data sources in the cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="a9414-192">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="a9414-192">
**A**: No.</span></span> <span data-ttu-id="a9414-193">Il gateway si connette solo alle origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="a9414-193">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="a9414-194">**D**: Il gateway deve essere installato nello stesso computer dell'origine dati?</span><span class="sxs-lookup"><span data-stu-id="a9414-194">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="a9414-195">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="a9414-195">
**A**: No.</span></span> <span data-ttu-id="a9414-196">Il gateway si connette all'origine dati tramite le informazioni di connessione fornite.</span><span class="sxs-lookup"><span data-stu-id="a9414-196">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="a9414-197">In questo senso il gateway può essere paragonato a un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="a9414-197">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="a9414-198">Il gateway deve solo potersi connettere al nome del server specificato, in genere nella stessa rete.</span><span class="sxs-lookup"><span data-stu-id="a9414-198">The gateway just needs the capability to connect to the server name that was provided, typically on the same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="a9414-199">**D**: Perché è necessario utilizzare un account aziendale o dell'istituto di istruzione per accedere?</span><span class="sxs-lookup"><span data-stu-id="a9414-199">**Q**: Why do I need to use a work or school account to sign in?</span></span> <br/><span data-ttu-id="a9414-200">
**R**: È possibile usare solo un account di Azure aziendale o dell'istituto di istruzione quando si installa il gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="a9414-200">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="a9414-201">L'account di accesso viene archiviato in un tenant gestito da Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9414-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a9414-202">Il nome dell'entità utente (UPN) dell'account di Azure AD in genere corrisponde all'indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a9414-202">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="a9414-203">**D**: Dove sono archiviate le credenziali?</span><span class="sxs-lookup"><span data-stu-id="a9414-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="a9414-204">
**R**: Le credenziali immesse per un'origine dati vengono crittografate e archiviate nel servizio cloud del gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-204">
**A**: The credentials that you enter for a data source are encrypted and stored in the Gateway Cloud Service.</span></span> <span data-ttu-id="a9414-205">Le credenziali vengono quindi decrittografate nel gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="a9414-205">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="a9414-206">**D**: Sono previsti requisiti per la larghezza di banda della rete?</span><span class="sxs-lookup"><span data-stu-id="a9414-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="a9414-207">
**R**: È consigliabile che la connessione di rete abbia una buona velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="a9414-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="a9414-208">Ogni ambiente è diverso e la quantità di dati inviati influisce sui risultati.</span><span class="sxs-lookup"><span data-stu-id="a9414-208">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="a9414-209">L'uso di ExpressRoute può contribuire a garantire un livello di velocità effettiva tra i data center di Azure e quelli locali.</span><span class="sxs-lookup"><span data-stu-id="a9414-209">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="a9414-210">Lo strumenti di terze parti Azure Speed Test può aiutare a valutare la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="a9414-210">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="a9414-211">**D**: Qual è la latenza per l'esecuzione di query a un'origine dati dal gateway?</span><span class="sxs-lookup"><span data-stu-id="a9414-211">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="a9414-212">Qual è l'architettura ottimale?</span><span class="sxs-lookup"><span data-stu-id="a9414-212">What is the best architecture?</span></span> <br/><span data-ttu-id="a9414-213">
**R**: Per ridurre la latenza di rete è consigliabile installare il gateway il più vicino possibile all'origine dati.</span><span class="sxs-lookup"><span data-stu-id="a9414-213">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="a9414-214">Installando il gateway nell'origine dati effettiva, la latenza introdotta risulterà ridotta al minimo grazie a questa prossimità.</span><span class="sxs-lookup"><span data-stu-id="a9414-214">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="a9414-215">Si considerino anche i data center.</span><span class="sxs-lookup"><span data-stu-id="a9414-215">Consider the datacenters too.</span></span> <span data-ttu-id="a9414-216">Se, ad esempio, il servizio usa il data center degli Stati Uniti occidentali e SQL Server è ospitato in una macchina virtuale di Azure, è opportuno che anche la macchina virtuale di Azure sia ubicata negli Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="a9414-216">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="a9414-217">Grazie a questa prossimità la latenza è ridotta al minimo e si evitano addebiti relativi ai dati in uscita sulla macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9414-217">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="a9414-218">**D**: In che modo i risultati vengono inviati al cloud?</span><span class="sxs-lookup"><span data-stu-id="a9414-218">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="a9414-219">
**R**: I risultati vengono inviati tramite il Bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9414-219">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="a9414-220">**D**: Esistono connessioni in ingresso al gateway dal cloud?</span><span class="sxs-lookup"><span data-stu-id="a9414-220">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="a9414-221">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="a9414-221">
**A**: No.</span></span> <span data-ttu-id="a9414-222">Il gateway usa le connessioni in uscita al bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9414-222">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="a9414-223">**D**: Cosa accade se si bloccano le connessioni in uscita?</span><span class="sxs-lookup"><span data-stu-id="a9414-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="a9414-224">Cosa fare per sbloccarle?</span><span class="sxs-lookup"><span data-stu-id="a9414-224">What do I need to open?</span></span> <br/><span data-ttu-id="a9414-225">
**R**: Visualizzare le porte e gli host usati dal gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-225">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="a9414-226">**D**: Come viene chiamato il servizio Windows effettivo?</span><span class="sxs-lookup"><span data-stu-id="a9414-226">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="a9414-227">
**R**: Nei servizi, il gateway è denominato servizio Gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="a9414-227">
**A**: In Services, the gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="a9414-228">**D**: Il servizio gateway di Windows può essere eseguito con un account Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9414-228">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="a9414-229">
**R**: No.</span><span class="sxs-lookup"><span data-stu-id="a9414-229">
**A**: No.</span></span> <span data-ttu-id="a9414-230">Il servizio Windows deve disporre di un account Windows valido.</span><span class="sxs-lookup"><span data-stu-id="a9414-230">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="a9414-231">Per impostazione predefinita, il sevizio viene eseguito con il SID servizio NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="a9414-231">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="a9414-232"><a name="high-availability"></a>Disponibilità elevata e ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="a9414-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="a9414-233">**D**: Quali opzioni sono disponibili per il ripristino di emergenza?</span><span class="sxs-lookup"><span data-stu-id="a9414-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="a9414-234">
**R**: È possibile usare la chiave di ripristino per ripristinare o spostare un gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-234">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="a9414-235">La chiave di ripristino viene specificata al momento dell'installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="a9414-235">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="a9414-236">**D**: Qual è il vantaggio della chiave di ripristino?</span><span class="sxs-lookup"><span data-stu-id="a9414-236">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="a9414-237">
**R**: La chiave di ripristino consente di eseguire la migrazione o di ripristinare le impostazioni del gateway in caso di emergenza.</span><span class="sxs-lookup"><span data-stu-id="a9414-237">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="a9414-238"><a name="troubleshooting"> </a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="a9414-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="a9414-239">**D**: Come è possibile visualizzare le query inviate all'origine dati locale?</span><span class="sxs-lookup"><span data-stu-id="a9414-239">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="a9414-240">
**R**: È possibile abilitare la funzione di tracciamento delle query, che include le query inviate.</span><span class="sxs-lookup"><span data-stu-id="a9414-240">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="a9414-241">Dopo aver risolto il problema, ripristinare il valore originale per il tracciamento delle query.</span><span class="sxs-lookup"><span data-stu-id="a9414-241">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="a9414-242">Se il tracciamento delle query non viene disabilitato, si creeranno dei log più grandi.</span><span class="sxs-lookup"><span data-stu-id="a9414-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="a9414-243">È anche possibile usare gli strumenti per il tracciamento delle query di cui è dotata l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="a9414-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="a9414-244">Ad esempio, è possibile usare Eventi estesi o SQL Profiler per SQL Server e Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="a9414-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="a9414-245">**D**: Dove si trovano i log del gateway?</span><span class="sxs-lookup"><span data-stu-id="a9414-245">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="a9414-246">
**R**: Vedere la sezione Registri più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="a9414-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="a9414-247"><a name="update"></a>Aggiornare alla versione più recente</span><span class="sxs-lookup"><span data-stu-id="a9414-247"><a name="update"></a>Update to the latest version</span></span>

<span data-ttu-id="a9414-248">Quando la versione del gateway non è aggiornata, possono emergere numerosi problemi.</span><span class="sxs-lookup"><span data-stu-id="a9414-248">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="a9414-249">Come buona pratica, assicurarsi di usare la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="a9414-249">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="a9414-250">Se il gateway non è stato aggiornato per un mese o più è consigliabile installarne la versione più recente e verificare se è possibile riprodurre il problema.</span><span class="sxs-lookup"><span data-stu-id="a9414-250">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="a9414-251">Errore: Impossibile aggiungere l'utente al gruppo.</span><span class="sxs-lookup"><span data-stu-id="a9414-251">Error: Failed to add user to group.</span></span> <span data-ttu-id="a9414-252">(Utenti log delle prestazioni -2147463168 PBIEgwService)</span><span class="sxs-lookup"><span data-stu-id="a9414-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="a9414-253">Questo errore viene visualizzato se si sta tentando di installare il gateway in un controller di dominio, un'operazione non consentita.</span><span class="sxs-lookup"><span data-stu-id="a9414-253">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="a9414-254">Assicurarsi di distribuire il gateway in un computer che non sia un controller di dominio.</span><span class="sxs-lookup"><span data-stu-id="a9414-254">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="a9414-255"><a name="logs"></a>Log</span><span class="sxs-lookup"><span data-stu-id="a9414-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="a9414-256">I file di log sono di fondamentale importanza per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="a9414-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="a9414-257">Log del servizio gateway Enterprise</span><span class="sxs-lookup"><span data-stu-id="a9414-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="a9414-258">Log di configurazione</span><span class="sxs-lookup"><span data-stu-id="a9414-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="a9414-259">Log eventi</span><span class="sxs-lookup"><span data-stu-id="a9414-259">Event logs</span></span>

<span data-ttu-id="a9414-260">I log di Gateway di gestione dati e PowerBIGateway sono reperibili in **Registri applicazioni e servizi**.</span><span class="sxs-lookup"><span data-stu-id="a9414-260">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="a9414-261"><a name="telemetry"></a>Telemetria</span><span class="sxs-lookup"><span data-stu-id="a9414-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="a9414-262">La telemetria può essere usata per il monitoraggio e la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="a9414-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="a9414-263">Per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="a9414-263">By default</span></span>

<span data-ttu-id="a9414-264">**Per attivare la telemetria**</span><span class="sxs-lookup"><span data-stu-id="a9414-264">**To turn on telemetry**</span></span>

1.  <span data-ttu-id="a9414-265">Verificare la directory del client gateway dati locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="a9414-265">Check the On-premises data gateway client directory on the computer.</span></span> <span data-ttu-id="a9414-266">In genere è **%unitàsistema%\Programmi\Gateway dati locale**.</span><span class="sxs-lookup"><span data-stu-id="a9414-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="a9414-267">Oppure è possibile aprire una console dei servizi e verificare il percorso al file eseguibile, una proprietà del servizio gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="a9414-267">Or, you can open a Services console and check the Path to executable: A property of the On-premises data gateway service.</span></span>
2.  <span data-ttu-id="a9414-268">Nel file Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config nella directory del client</span><span class="sxs-lookup"><span data-stu-id="a9414-268">In the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="a9414-269">modificare l'impostazione SendTelemetry su true.</span><span class="sxs-lookup"><span data-stu-id="a9414-269">Change the SendTelemetry setting to true.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="a9414-270">Salvare le modifiche e riavviare il servizio Windows gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="a9414-270">Save your changes and restart the Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="a9414-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9414-271">Next steps</span></span>
* [<span data-ttu-id="a9414-272">Gestire Analysis Services</span><span class="sxs-lookup"><span data-stu-id="a9414-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="a9414-273">Ottenere dati da Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="a9414-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
