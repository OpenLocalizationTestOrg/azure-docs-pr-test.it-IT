---
title: "Nome e chiave dell'autorità emittente in Servizi BizTalk | Microsoft Docs"
description: "Informazioni su come recuperare il nome dell'autorità emittente e la chiave dell'autorità emittente per il bus di servizio o il Servizio di controllo di accesso (ACS) in Servizi BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="64ae2-104">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="64ae2-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="64ae2-105">Servizi BizTalk di Azure utilizza il nome e la chiave dell'autorità emittente del bus di servizio e il nome e la chiave dell'autorità emittente del Controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="64ae2-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="64ae2-106">In particolare:</span><span class="sxs-lookup"><span data-stu-id="64ae2-106">Specifically:</span></span>

| <span data-ttu-id="64ae2-107">Attività</span><span class="sxs-lookup"><span data-stu-id="64ae2-107">Task</span></span> | <span data-ttu-id="64ae2-108">Nome e chiave dell'autorità emittente da utilizzare</span><span class="sxs-lookup"><span data-stu-id="64ae2-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="64ae2-109">Distribuzione dell'applicazione da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64ae2-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="64ae2-110">Nome e chiave dell'autorità emittente del Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="64ae2-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="64ae2-111">Configurazione del Portale Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="64ae2-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="64ae2-112">Nome e chiave dell'autorità emittente del Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="64ae2-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="64ae2-113">Creazione di inoltri LOB con i servizi dell'adapter di BizTalk in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64ae2-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="64ae2-114">Nome e chiave dell'autorità emittente del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="64ae2-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="64ae2-115">Questo argomento elenca i passaggi necessari per recuperare il nome e la chiave dell'autorità emittente.</span><span class="sxs-lookup"><span data-stu-id="64ae2-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="64ae2-116">Nome e chiave dell'autorità emittente del Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="64ae2-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="64ae2-117">Il nome e la chiave dell'autorità emittente del Controllo di accesso vengono utilizzati dagli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="64ae2-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="64ae2-118">Applicazione del servizio BizTalk di Azure creata in Visual Studio: per distribuire correttamente l'applicazione del servizio BizTalk in Visual Studio in Azure, immettere il nome e la chiave dell'autorità emittente del Controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="64ae2-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="64ae2-119">Portale dei servizi BizTalk di Azure: quando si crea un servizio BizTalk e si apre il portale dei servizi BizTalk, il nome e la chiave dell'autorità emittente del Controllo di accesso vengono registrati automaticamente per le distribuzioni con gli stessi valori del Controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="64ae2-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="64ae2-120">Ottenere il nome e la chiave dell'autorità emittente del Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="64ae2-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="64ae2-121">Per usare il servizio contenitore di Azure per l'autenticazione e ottenere i valori di Nome e chiave dell'autorità emittente, la procedura generale include:</span><span class="sxs-lookup"><span data-stu-id="64ae2-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="64ae2-122">[Installare i cmdlet di Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="64ae2-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="64ae2-123">Aggiungere il proprio Account Azure: `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="64ae2-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="64ae2-124">Restituire il nome della sottoscrizione: `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="64ae2-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="64ae2-125">Selezionare la propria sottoscrizione: `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="64ae2-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="64ae2-126">Creare un nuovo spazio dei nomi: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="64ae2-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="64ae2-127">Esempio:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="64ae2-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="64ae2-128">Quando viene creato il nuovo spazio dei nomi del servizio contenitore di Azure (che può richiedere alcuni minuti), nella stringa di connessione sono elencati i valori di Nome e chiave dell'autorità emittente.</span><span class="sxs-lookup"><span data-stu-id="64ae2-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="64ae2-129">Per riepilogare:</span><span class="sxs-lookup"><span data-stu-id="64ae2-129">To summarize:</span></span>  
<span data-ttu-id="64ae2-130">Nome dell'autorità emittente = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="64ae2-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="64ae2-131">Chiave dell'autorità emittente = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="64ae2-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="64ae2-132">Altre informazioni sul cmdlet [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx).</span><span class="sxs-lookup"><span data-stu-id="64ae2-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="64ae2-133">Nome e chiave dell'autorità emittente del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="64ae2-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="64ae2-134">Il nome e la chiave dell'autorità emittente del bus di servizio vengono utilizzati dai servizi dell'adapter di BizTalk.</span><span class="sxs-lookup"><span data-stu-id="64ae2-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="64ae2-135">Nel progetto di Servizi BizTalk in Visual Studio è possibile usare Servizi Adapter BizTalk per la connessione a un sistema LOB (Line-of-Business) locale.</span><span class="sxs-lookup"><span data-stu-id="64ae2-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="64ae2-136">Per effettuare la connessione, creare l'inoltro LOB e immettere i dettagli relativi al sistema LOB.</span><span class="sxs-lookup"><span data-stu-id="64ae2-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="64ae2-137">Quando si esegue questa operazione, è necessario immettere anche il nome e la chiave dell'autorità emittente del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="64ae2-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="64ae2-138">Per recuperare il nome e la chiave dell'autorità emittente del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="64ae2-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="64ae2-139">Accedere al [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="64ae2-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="64ae2-140">Nel pannello di navigazione sinistro selezionare **Bus di servizio**.</span><span class="sxs-lookup"><span data-stu-id="64ae2-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="64ae2-141">Selezionare lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="64ae2-141">Select your namespace.</span></span> <span data-ttu-id="64ae2-142">Nella barra delle applicazioni selezionare **Informazioni di connessione**.</span><span class="sxs-lookup"><span data-stu-id="64ae2-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="64ae2-143">Verranno visualizzati i valori relativi a **nome dell'autorità emittente** e **Chiave dell'autorità emittente**.</span><span class="sxs-lookup"><span data-stu-id="64ae2-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="64ae2-144">Questi valori possono essere copiati.</span><span class="sxs-lookup"><span data-stu-id="64ae2-144">Their values can be copied.</span></span>  

<span data-ttu-id="64ae2-145">Per riepilogare:</span><span class="sxs-lookup"><span data-stu-id="64ae2-145">To summarize:</span></span>  
<span data-ttu-id="64ae2-146">Nome dell'autorità di certificazione = Autorità di certificazione predefinita</span><span class="sxs-lookup"><span data-stu-id="64ae2-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="64ae2-147">Chiave autorità di certificazione = Chiave predefinita</span><span class="sxs-lookup"><span data-stu-id="64ae2-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="64ae2-148">Avanti</span><span class="sxs-lookup"><span data-stu-id="64ae2-148">Next</span></span>
<span data-ttu-id="64ae2-149">Altri argomenti relativi a Servizi BizTalk di Azure:</span><span class="sxs-lookup"><span data-stu-id="64ae2-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="64ae2-150">Installare Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="64ae2-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="64ae2-151">Servizi BizTalk: Esercitazioni ed esempi</span><span class="sxs-lookup"><span data-stu-id="64ae2-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="64ae2-152">Come iniziare a usare l'SDK di Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="64ae2-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="64ae2-153">Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="64ae2-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="64ae2-154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="64ae2-154">See Also</span></span>
* [<span data-ttu-id="64ae2-155">Procedura: Usare il servizio di gestione ACS per la configurazione delle identità del servizio</span><span class="sxs-lookup"><span data-stu-id="64ae2-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="64ae2-156">Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="64ae2-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="64ae2-157">Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="64ae2-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="64ae2-158">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="64ae2-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="64ae2-159">Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità</span><span class="sxs-lookup"><span data-stu-id="64ae2-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="64ae2-160">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="64ae2-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="64ae2-161">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="64ae2-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

