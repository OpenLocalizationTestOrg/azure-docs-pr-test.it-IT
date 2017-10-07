---
title: "aaaIssuer nome e la chiave dell'autorità di certificazione nei servizi BizTalk | Documenti Microsoft"
description: "Informazioni su come nome dell'autorità di certificazione tooretrieve e la chiave dell'autorità di certificazione per il Bus di servizio o Access Control (ACS) nei servizi BizTalk. MABS, WABS"
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
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="280a4-104">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="280a4-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="280a4-105">Servizi BizTalk di Azure Usa hello nome dell'autorità di certificazione del Bus di servizio e la chiave dell'autorità emittente e hello nome di accesso controllo dell'autorità emittente e chiave dell'autorità emittente.</span><span class="sxs-lookup"><span data-stu-id="280a4-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="280a4-106">In particolare:</span><span class="sxs-lookup"><span data-stu-id="280a4-106">Specifically:</span></span>

| <span data-ttu-id="280a4-107">Attività</span><span class="sxs-lookup"><span data-stu-id="280a4-107">Task</span></span> | <span data-ttu-id="280a4-108">Nome e chiave dell'autorità emittente da utilizzare</span><span class="sxs-lookup"><span data-stu-id="280a4-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="280a4-109">Distribuzione dell'applicazione da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="280a4-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="280a4-110">Nome e chiave dell'autorità emittente del Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="280a4-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="280a4-111">Configurazione hello portale servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="280a4-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="280a4-112">Nome e chiave dell'autorità emittente del Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="280a4-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="280a4-113">Creazione di inoltro LOB con hello servizi dell'Adapter BizTalk in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="280a4-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="280a4-114">Nome e chiave dell'autorità emittente del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="280a4-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="280a4-115">Questo argomento elenca hello passaggi tooretrieve hello nome dell'autorità emittente e chiave dell'autorità emittente.</span><span class="sxs-lookup"><span data-stu-id="280a4-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="280a4-116">Nome e chiave dell'autorità emittente del Controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="280a4-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="280a4-117">Hello nome di accesso controllo dell'autorità emittente e la chiave dell'autorità di certificazione vengono utilizzati dal seguente hello:</span><span class="sxs-lookup"><span data-stu-id="280a4-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="280a4-118">L'applicazione di servizio BizTalk di Azure creata in Visual Studio: toosuccessfully distribuire l'applicazione BizTalk Service in tooAzure di Visual Studio, si immette hello nome di accesso controllo dell'autorità emittente e chiave dell'autorità emittente.</span><span class="sxs-lookup"><span data-stu-id="280a4-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="280a4-119">Hello portale servizi BizTalk di Azure: quando si crea un BizTalk Service e apre hello portale dei servizi BizTalk, il nome di autorità di certificazione di controllo di accesso e la chiave dell'autorità di certificazione vengono registrati automaticamente per le distribuzioni con hello stessi valori di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="280a4-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="280a4-120">Ottenere hello nome di accesso controllo dell'autorità emittente e la chiave dell'autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="280a4-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="280a4-121">toouse ACS per l'autenticazione e get hello i valori di nome dell'autorità emittente e la chiave dell'autorità di certificazione, includono hello passaggi generali:</span><span class="sxs-lookup"><span data-stu-id="280a4-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="280a4-122">Installare hello [cmdlet di Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="280a4-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="280a4-123">Aggiungere il proprio Account Azure: `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="280a4-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="280a4-124">Restituire il nome della sottoscrizione: `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="280a4-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="280a4-125">Selezionare la propria sottoscrizione: `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="280a4-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="280a4-126">Creare un nuovo spazio dei nomi: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="280a4-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="280a4-127">Esempio:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="280a4-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="280a4-128">Creazione di hello nuovo spazio dei nomi ACS (che può richiedere alcuni minuti), sono elencati i valori di nome dell'autorità emittente e chiave dell'autorità emittente hello nella stringa di connessione hello:</span><span class="sxs-lookup"><span data-stu-id="280a4-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

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

<span data-ttu-id="280a4-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="280a4-129">toosummarize:</span></span>  
<span data-ttu-id="280a4-130">Nome dell'autorità emittente = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="280a4-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="280a4-131">Chiave dell'autorità emittente = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="280a4-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="280a4-132">Altre informazioni sul hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="280a4-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="280a4-133">Nome e chiave dell'autorità emittente del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="280a4-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="280a4-134">Il nome e la chiave dell'autorità emittente del bus di servizio vengono utilizzati dai servizi dell'adapter di BizTalk.</span><span class="sxs-lookup"><span data-stu-id="280a4-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="280a4-135">Nel progetto servizi BizTalk in Visual Studio, utilizzare il sistema Line-of-Business (LOB) locale tooan di hello servizi dell'Adapter BizTalk tooconnect.</span><span class="sxs-lookup"><span data-stu-id="280a4-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="280a4-136">tooconnect, si crea hello inoltro LOB e immettere i dettagli del sistema LOB.</span><span class="sxs-lookup"><span data-stu-id="280a4-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="280a4-137">In tal caso, è anche possibile immettere hello nome dell'autorità di certificazione del Bus di servizio e la chiave dell'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="280a4-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="280a4-138">hello tooretrieve nome dell'autorità di certificazione del Bus di servizio e la chiave dell'autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="280a4-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="280a4-139">Accedi toohello [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="280a4-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="280a4-140">Nel riquadro di spostamento a sinistra di hello, selezionare **Bus di servizio**.</span><span class="sxs-lookup"><span data-stu-id="280a4-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="280a4-141">Selezionare lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="280a4-141">Select your namespace.</span></span> <span data-ttu-id="280a4-142">Nella barra delle applicazioni hello, selezionare **informazioni di connessione**.</span><span class="sxs-lookup"><span data-stu-id="280a4-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="280a4-143">Consente di visualizzare hello **autorità di certificazione predefinita** (nome dell'autorità emittente) e **chiave predefinita** (chiave dell'autorità di certificazione).</span><span class="sxs-lookup"><span data-stu-id="280a4-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="280a4-144">Questi valori possono essere copiati.</span><span class="sxs-lookup"><span data-stu-id="280a4-144">Their values can be copied.</span></span>  

<span data-ttu-id="280a4-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="280a4-145">toosummarize:</span></span>  
<span data-ttu-id="280a4-146">Nome dell'autorità di certificazione = Autorità di certificazione predefinita</span><span class="sxs-lookup"><span data-stu-id="280a4-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="280a4-147">Chiave autorità di certificazione = Chiave predefinita</span><span class="sxs-lookup"><span data-stu-id="280a4-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="280a4-148">Avanti</span><span class="sxs-lookup"><span data-stu-id="280a4-148">Next</span></span>
<span data-ttu-id="280a4-149">Altri argomenti relativi a Servizi BizTalk di Azure:</span><span class="sxs-lookup"><span data-stu-id="280a4-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="280a4-150">L'installazione di hello Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="280a4-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="280a4-151">Servizi BizTalk: Esercitazioni ed esempi</span><span class="sxs-lookup"><span data-stu-id="280a4-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="280a4-152">Come è possibile utilizzare hello Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="280a4-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="280a4-153">Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="280a4-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="280a4-154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="280a4-154">See Also</span></span>
* [<span data-ttu-id="280a4-155">Procedura: tooConfigure servizio di gestione ACS di usare le identità del servizio</span><span class="sxs-lookup"><span data-stu-id="280a4-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="280a4-156">Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="280a4-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="280a4-157">Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="280a4-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="280a4-158">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="280a4-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="280a4-159">Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità</span><span class="sxs-lookup"><span data-stu-id="280a4-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="280a4-160">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="280a4-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="280a4-161">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="280a4-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

