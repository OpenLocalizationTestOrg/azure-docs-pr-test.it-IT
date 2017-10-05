---
title: "Hosting di più siti con il gateway applicazione di Azure | Microsoft Docs"
description: "Questa pagina contiene istruzioni per configurare un gateway applicazione di Azure esistente per l'hosting di più applicazioni Web nello stesso gateway con il portale di Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 84bd62ae17b7f7ba4cd815ef1f9880679607ebce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="25365-103">Configurare un gateway applicazione esistente per l'hosting di più applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="25365-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="25365-104">portale di Azure</span><span class="sxs-lookup"><span data-stu-id="25365-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="25365-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="25365-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="25365-106">L'hosting di più siti consente di distribuire più applicazioni Web nello stesso gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25365-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="25365-107">La presenza dell'intestazione host nella richiesta HTTP in ingresso consente di determinare il listener che riceverà il traffico.</span><span class="sxs-lookup"><span data-stu-id="25365-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="25365-108">Il listener indirizza quindi il traffico al pool back-end appropriato in base alla configurazione della definizione delle regole del gateway.</span><span class="sxs-lookup"><span data-stu-id="25365-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="25365-109">Nelle applicazioni Web abilitate per SSL il gateway applicazione sceglie il listener corretto per il traffico Web in base all'estensione dell'indicazione nome server (SNI).</span><span class="sxs-lookup"><span data-stu-id="25365-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="25365-110">L'hosting di più siti viene comunemente usato per bilanciare il carico delle richieste per diversi domini Web tra vari pool di server back-end.</span><span class="sxs-lookup"><span data-stu-id="25365-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="25365-111">Analogamente, lo stesso gateway applicazione potrebbe ospitare anche più sottodomini dello stesso dominio radice.</span><span class="sxs-lookup"><span data-stu-id="25365-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="25365-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="25365-112">Scenario</span></span>

<span data-ttu-id="25365-113">Nell'esempio seguente, il gateway applicazione gestisce il traffico per contoso.com e fabrikam.com con due pool di server back-end: il pool di server contoso e il pool di server fabrikam.</span><span class="sxs-lookup"><span data-stu-id="25365-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="25365-114">Una configurazione simile potrebbe essere usata per ospitare sottodomini come app.contoso.com e blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="25365-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![scenario multisito][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="25365-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="25365-116">Before you begin</span></span>

<span data-ttu-id="25365-117">Questo scenario aggiunge il supporto multisito a un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="25365-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="25365-118">Per completare questo scenario, è necessario che un gateway applicazione esistente sia disponibile per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="25365-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="25365-119">Visitare [Creare un gateway applicazione con il portale](application-gateway-create-gateway-portal.md) per imparare a creare un gateway applicazione di base nel portale.</span><span class="sxs-lookup"><span data-stu-id="25365-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="25365-120">Per aggiornare il gateway applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="25365-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="25365-121">Creare i pool di back-end da usare per ogni sito.</span><span class="sxs-lookup"><span data-stu-id="25365-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="25365-122">Creare un listener per ogni sito che viene supportato dal gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25365-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="25365-123">Creare regole per eseguire il mapping di ogni listener con il back-end appropriato.</span><span class="sxs-lookup"><span data-stu-id="25365-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="25365-124">Requisiti</span><span class="sxs-lookup"><span data-stu-id="25365-124">Requirements</span></span>

* <span data-ttu-id="25365-125">**Pool di server back-end:** elenco di indirizzi IP dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="25365-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="25365-126">Gli indirizzi IP elencati devono appartenere alla subnet della rete virtuale o devono essere indirizzi IP/VIP pubblici.</span><span class="sxs-lookup"><span data-stu-id="25365-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="25365-127">È possibile usare anche FQDN.</span><span class="sxs-lookup"><span data-stu-id="25365-127">FQDN can also be used.</span></span>
* <span data-ttu-id="25365-128">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="25365-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="25365-129">Queste impostazioni sono associate a un pool e vengono applicate a tutti i server nel pool.</span><span class="sxs-lookup"><span data-stu-id="25365-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="25365-130">**Porta front-end:** porta pubblica aperta sul gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25365-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="25365-131">Il traffico raggiunge questa porta e quindi viene reindirizzato a uno dei server back-end.</span><span class="sxs-lookup"><span data-stu-id="25365-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="25365-132">**Listener** : ha una porta front-end, un protocollo (Http o Https, con distinzione tra maiuscole e minuscole) e il nome del certificato SSL (se si configura l'offload SSL).</span><span class="sxs-lookup"><span data-stu-id="25365-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="25365-133">Per i gateway applicazione abilitati per più siti vengono aggiunti anche indicatori SNI e nome host.</span><span class="sxs-lookup"><span data-stu-id="25365-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="25365-134">**Regola**: associa il listener e il pool di server back-end e definisce il pool di server back-end a cui deve essere indirizzato il traffico quando raggiunge un listener specifico.</span><span class="sxs-lookup"><span data-stu-id="25365-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="25365-135">Le regole vengono elaborate nell'ordine in cui sono elencate e il traffico verrà indirizzato tramite la prima regola corrispondente indipendentemente dalla specificità.</span><span class="sxs-lookup"><span data-stu-id="25365-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="25365-136">Se ad esempio si dispone di due regole, una che usa un listener di base e una che usa un listener multisito, entrambe sulla stessa porta, la regola con il listener multisito deve essere elencata prima della regola con il listener di base per funzionare come previsto.</span><span class="sxs-lookup"><span data-stu-id="25365-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="25365-137">**Certificati**: ogni listener richiede un certificato univoco. In questo esempio vengono creati due listener per più siti.</span><span class="sxs-lookup"><span data-stu-id="25365-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="25365-138">È necessario creare due certificati con estensione pfx e le relative password.</span><span class="sxs-lookup"><span data-stu-id="25365-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="25365-139">Creare i pool di back-end per ogni sito</span><span class="sxs-lookup"><span data-stu-id="25365-139">Create back-end pools for each site</span></span>

<span data-ttu-id="25365-140">È necessario un pool di back-end per ogni sito che supporta il gateway applicazione. In questo caso ne vengono creati due, uno per contoso11.com e uno per fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="25365-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="25365-141">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="25365-141">Step 1</span></span>

<span data-ttu-id="25365-142">Passare a un gateway applicazione esistente nel portale di Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25365-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="25365-143">Selezionare **Pool back-end** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="25365-143">Select **Backend pools** and click **Add**</span></span>

![aggiunta di pool di back-end][7]

### <a name="step-2"></a><span data-ttu-id="25365-145">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="25365-145">Step 2</span></span>

<span data-ttu-id="25365-146">Immettere le informazioni per il pool di back-end **pool1**, aggiungendo gli indirizzi IP o i nomi di dominio completi per i server back-end, e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="25365-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![impostazioni del pool di back-end pool1][8]

### <a name="step-3"></a><span data-ttu-id="25365-148">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="25365-148">Step 3</span></span>

<span data-ttu-id="25365-149">Nel pannello dei pool di back-end fare clic su **Aggiungi** per aggiungere un altro pool di back-end, **pool2**, aggiungendo gli indirizzi IP o i nomi di dominio completi per i server back-end, e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="25365-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![impostazioni del pool di back-end pool2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="25365-151">Creare listener per ogni back-end</span><span class="sxs-lookup"><span data-stu-id="25365-151">Create listeners for each back-end</span></span>

<span data-ttu-id="25365-152">Il gateway applicazione si basa su intestazioni host HTTP 1.1 per ospitare più siti Web nello stesso indirizzo IP pubblico e nella stessa porta.</span><span class="sxs-lookup"><span data-stu-id="25365-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="25365-153">Il listener di base creato nel portale non contiene questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="25365-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="25365-154">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="25365-154">Step 1</span></span>

<span data-ttu-id="25365-155">Fare clic su **Listener** sul gateway applicazione esistente e quindi su **Multisito** per aggiungere il primo listener.</span><span class="sxs-lookup"><span data-stu-id="25365-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![pannello della panoramica dei listener][1]

### <a name="step-2"></a><span data-ttu-id="25365-157">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="25365-157">Step 2</span></span>

<span data-ttu-id="25365-158">Immettere le informazioni relative al listener.</span><span class="sxs-lookup"><span data-stu-id="25365-158">Fill out the information for the listener.</span></span> <span data-ttu-id="25365-159">In questo esempio la terminazione SSL è configurata, creare una nuova porta front-end.</span><span class="sxs-lookup"><span data-stu-id="25365-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="25365-160">Caricare il certificato con estensione pfx da usare per la terminazione SSL.</span><span class="sxs-lookup"><span data-stu-id="25365-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="25365-161">L'unica differenza tra questo pannello e quello del listener di base è data dal nome host.</span><span class="sxs-lookup"><span data-stu-id="25365-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![pannello delle proprietà del listener][2]

### <a name="step-3"></a><span data-ttu-id="25365-163">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="25365-163">Step 3</span></span>

<span data-ttu-id="25365-164">Fare clic su **Multisito** e creare un altro listener, come descritto nel passaggio precedente, per il secondo sito.</span><span class="sxs-lookup"><span data-stu-id="25365-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="25365-165">Assicurarsi di usare un certificato diverso per il secondo listener.</span><span class="sxs-lookup"><span data-stu-id="25365-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="25365-166">L'unica differenza tra questo pannello e quello del listener di base è data dal nome host.</span><span class="sxs-lookup"><span data-stu-id="25365-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="25365-167">Immettere le informazioni relative al listener e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="25365-167">Fill out the information for the listener and click **OK**.</span></span>

![pannello delle proprietà del listener][3]

> [!NOTE]
> <span data-ttu-id="25365-169">La creazione di listener nel portale di Azure per il gateway applicazione è un'attività di lunga durata. Può essere necessario del tempo per creare i due listener in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="25365-169">Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario.</span></span> <span data-ttu-id="25365-170">Al termine della procedura, i listener vengono visualizzati nel portale, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="25365-170">When complete the listeners show in the portal as seen in the following image:</span></span>

![panoramica dei listener][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="25365-172">Creare regole per associare i listener ai pool di back-end</span><span class="sxs-lookup"><span data-stu-id="25365-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="25365-173">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="25365-173">Step 1</span></span>

<span data-ttu-id="25365-174">Passare a un gateway applicazione esistente nel portale di Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25365-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="25365-175">Selezionare **Regole**, scegliere la regola predefinita esistente **rule1** e fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="25365-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="25365-176">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="25365-176">Step 2</span></span>

<span data-ttu-id="25365-177">Immettere i dati nel pannello delle regole come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="25365-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="25365-178">Scegliere il primo listener e il primo pool e fare clic su **Salva** al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="25365-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![modifica della regola esistente][6]

### <a name="step-3"></a><span data-ttu-id="25365-180">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="25365-180">Step 3</span></span>

<span data-ttu-id="25365-181">Fare clic su **Basic rule** (Regola di base) per creare la seconda regola.</span><span class="sxs-lookup"><span data-stu-id="25365-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="25365-182">Compilare il modulo con il secondo listener e il secondo pool di back-end e fare clic su **OK** per salvare.</span><span class="sxs-lookup"><span data-stu-id="25365-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![pannello Aggiungi regola di base][10]

<span data-ttu-id="25365-184">Con questo scenario viene completata la configurazione di un gateway applicazione esistente con supporto multisito tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="25365-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25365-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25365-185">Next steps</span></span>

<span data-ttu-id="25365-186">Informazioni su come proteggere i siti Web con [Gateway applicazione: firewall applicazione Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="25365-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
