---
title: aaaHost siti multipli con Gateway applicazione Azure | Documenti Microsoft
description: "Questa pagina fornisce istruzioni tooconfigure un gateway applicazione Azure esistente per ospitare più applicazioni web su hello stesso gateway con hello portale di Azure."
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
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="887de-103">Configurare un gateway applicazione esistente per l'hosting di più applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="887de-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="887de-104">portale di Azure</span><span class="sxs-lookup"><span data-stu-id="887de-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="887de-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="887de-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="887de-106">Hosting di più siti consente toodeploy più di una sola applicazione web su hello stesso gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="887de-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="887de-107">Si basa su presenza dell'intestazione host nella richiesta HTTP in ingresso hello, toodetermine quali listener riceve traffico.</span><span class="sxs-lookup"><span data-stu-id="887de-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="887de-108">listener di Hello indirizza quindi il pool back-end tooappropriate traffico come configurato nella definizione delle regole hello del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="887de-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="887de-109">Nelle applicazioni web SSL abilitato, i gateway applicazione si basa su hello indicazione nome Server (SNI) estensione toochoose hello corretto del listener per il traffico web hello.</span><span class="sxs-lookup"><span data-stu-id="887de-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="887de-110">Viene in genere utilizzata per l'hosting del sito più tooload bilanciamento delle richieste per i pool di server back-end web diversi domini toodifferent.</span><span class="sxs-lookup"><span data-stu-id="887de-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="887de-111">Analogamente, più sottodomini del dominio radice della stessa può essere ospitato su hello hello stesso gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="887de-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="887de-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="887de-112">Scenario</span></span>

<span data-ttu-id="887de-113">Nell'esempio seguente di hello, gateway applicazione gestisce il traffico per contoso.com e fabrikam.com con due pool di server back-end: contoso pool di server e il pool di server di fabrikam.</span><span class="sxs-lookup"><span data-stu-id="887de-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="887de-114">Il programma di installazione simile potrebbe essere sottodomini toohost usato come app.contoso.com e blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="887de-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![scenario multisito][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="887de-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="887de-116">Before you begin</span></span>

<span data-ttu-id="887de-117">Questo scenario aggiunge supporto multisito tooan gateway di applicazioni esistente.</span><span class="sxs-lookup"><span data-stu-id="887de-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="887de-118">toocomplete tooconfigure disponibile toobe è necessario questo scenario, un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="887de-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="887de-119">Visitare [creare un gateway applicazione tramite il portale di hello](application-gateway-create-gateway-portal.md) toolearn come toocreate un gateway applicazione basic nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="887de-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="887de-120">di seguito Hello sono passaggi hello necessari gateway di applicazione hello tooupdate:</span><span class="sxs-lookup"><span data-stu-id="887de-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="887de-121">Creare toouse pool back-end per ogni sito.</span><span class="sxs-lookup"><span data-stu-id="887de-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="887de-122">Creare un listener per ogni sito che viene supportato dal gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="887de-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="887de-123">Creare regole toomap ogni listener con hello appropriato back-end.</span><span class="sxs-lookup"><span data-stu-id="887de-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="887de-124">Requisiti</span><span class="sxs-lookup"><span data-stu-id="887de-124">Requirements</span></span>

* <span data-ttu-id="887de-125">**Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="887de-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="887de-126">gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="887de-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="887de-127">È possibile usare anche FQDN.</span><span class="sxs-lookup"><span data-stu-id="887de-127">FQDN can also be used.</span></span>
* <span data-ttu-id="887de-128">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="887de-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="887de-129">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="887de-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="887de-130">**Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="887de-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="887de-131">Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="887de-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="887de-132">**Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="887de-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="887de-133">Per i gateway applicazione abilitati per più siti vengono aggiunti anche indicatori SNI e nome host.</span><span class="sxs-lookup"><span data-stu-id="887de-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="887de-134">**Regola:** regola hello associa listener hello, pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="887de-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="887de-135">Le regole vengono elaborate in ordine di hello che sono elencati e il traffico verrà indirizzato tramite hello prima regola che corrisponde indipendentemente dal fatto di specificità.</span><span class="sxs-lookup"><span data-stu-id="887de-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="887de-136">Ad esempio, se si dispone di una regola di utilizzo di un listener di base e una regola di utilizzo di un listener multisito entrambi nella stessa regola di porta, hello con hello listener multisito hello deve essere elencato prima regola hello con listener di base hello affinché hello multisito regola toofunction come previsto.</span><span class="sxs-lookup"><span data-stu-id="887de-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="887de-137">**Certificati**: ogni listener richiede un certificato univoco. In questo esempio vengono creati due listener per più siti.</span><span class="sxs-lookup"><span data-stu-id="887de-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="887de-138">Due certificati PFX e password hello relativa necessario toobe creato.</span><span class="sxs-lookup"><span data-stu-id="887de-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="887de-139">Creare i pool di back-end per ogni sito</span><span class="sxs-lookup"><span data-stu-id="887de-139">Create back-end pools for each site</span></span>

<span data-ttu-id="887de-140">È necessario un pool di back-end per ogni sito che supporta il gateway applicazione. In questo caso ne vengono creati due, uno per contoso11.com e uno per fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="887de-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="887de-141">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="887de-141">Step 1</span></span>

<span data-ttu-id="887de-142">Passare tooan gateway di applicazione esistente nel portale di Azure (https://portal.azure.com) hello.</span><span class="sxs-lookup"><span data-stu-id="887de-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="887de-143">Selezionare **Pool back-end** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="887de-143">Select **Backend pools** and click **Add**</span></span>

![aggiunta di pool di back-end][7]

### <a name="step-2"></a><span data-ttu-id="887de-145">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="887de-145">Step 2</span></span>

<span data-ttu-id="887de-146">Immettere le informazioni di hello per il pool back-end hello **pool1**, l'aggiunta di indirizzi ip hello o FQDN per i server back-end hello e fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="887de-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![impostazioni del pool di back-end pool1][8]

### <a name="step-3"></a><span data-ttu-id="887de-148">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="887de-148">Step 3</span></span>

<span data-ttu-id="887de-149">Nel Pannello di pool back-end hello clic **Aggiungi** tooadd un pool back-end aggiuntivo **pool2**, l'aggiunta di indirizzi ip hello o FQDN per i server back-end hello e fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="887de-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![impostazioni del pool di back-end pool2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="887de-151">Creare listener per ogni back-end</span><span class="sxs-lookup"><span data-stu-id="887de-151">Create listeners for each back-end</span></span>

<span data-ttu-id="887de-152">Gateway applicazione si basa su HTTP 1.1 toohost intestazioni host più di un sito Web in hello stesso indirizzo IP pubblico e la porta.</span><span class="sxs-lookup"><span data-stu-id="887de-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="887de-153">listener di base Hello creato nel portale di hello non contiene questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="887de-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="887de-154">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="887de-154">Step 1</span></span>

<span data-ttu-id="887de-155">Fare clic su **listener** hello gateway applicazione esistente e fare clic su **multisito** listener prima di tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="887de-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![pannello della panoramica dei listener][1]

### <a name="step-2"></a><span data-ttu-id="887de-157">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="887de-157">Step 2</span></span>

<span data-ttu-id="887de-158">Immettere le informazioni di hello per listener hello.</span><span class="sxs-lookup"><span data-stu-id="887de-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="887de-159">In questo esempio la terminazione SSL è configurata, creare una nuova porta front-end.</span><span class="sxs-lookup"><span data-stu-id="887de-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="887de-160">Caricare toobe di certificato PFX hello utilizzato per la terminazione SSL.</span><span class="sxs-lookup"><span data-stu-id="887de-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="887de-161">Hello l'unica differenza in questo pannello listener base standard di blade confrontati toohello è hostname hello.</span><span class="sxs-lookup"><span data-stu-id="887de-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![pannello delle proprietà del listener][2]

### <a name="step-3"></a><span data-ttu-id="887de-163">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="887de-163">Step 3</span></span>

<span data-ttu-id="887de-164">Fare clic su **multisito** e creare un altro listener come descritto nel passaggio precedente di hello per secondo sito hello.</span><span class="sxs-lookup"><span data-stu-id="887de-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="887de-165">Verificare che toouse un certificato diverso per il listener secondo hello.</span><span class="sxs-lookup"><span data-stu-id="887de-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="887de-166">Hello l'unica differenza in questo pannello listener base standard di blade confrontati toohello è hostname hello.</span><span class="sxs-lookup"><span data-stu-id="887de-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="887de-167">Immettere le informazioni di hello per listener hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="887de-167">Fill out hello information for hello listener and click **OK**.</span></span>

![pannello delle proprietà del listener][3]

> [!NOTE]
> <span data-ttu-id="887de-169">La creazione di listener nel portale di Azure per il gateway applicazione hello è un'attività a esecuzione prolungata, potrebbe richiedere alcuni hello toocreate ora due listener in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="887de-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="887de-170">Quando il listener di completamento hello Visualizza nel portale di hello, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="887de-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![panoramica dei listener][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="887de-172">Creare regole di pool di toobackend toomap listener</span><span class="sxs-lookup"><span data-stu-id="887de-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="887de-173">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="887de-173">Step 1</span></span>

<span data-ttu-id="887de-174">Passare tooan gateway di applicazione esistente nel portale di Azure (https://portal.azure.com) hello.</span><span class="sxs-lookup"><span data-stu-id="887de-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="887de-175">Selezionare **regole** e scegliere regole predefinito esistente hello **rule1** e fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="887de-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="887de-176">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="887de-176">Step 2</span></span>

<span data-ttu-id="887de-177">Compilare pannello regole hello, come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="887de-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="887de-178">Listener del primo hello e primo pool e fare clic su **salvare** al completamento.</span><span class="sxs-lookup"><span data-stu-id="887de-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![modifica della regola esistente][6]

### <a name="step-3"></a><span data-ttu-id="887de-180">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="887de-180">Step 3</span></span>

<span data-ttu-id="887de-181">Fare clic su **regola base** seconda regola di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="887de-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="887de-182">Compilare il modulo di hello con pool back-end del listener e secondo secondo hello e fare clic su **OK** toosave.</span><span class="sxs-lookup"><span data-stu-id="887de-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![pannello Aggiungi regola di base][10]

<span data-ttu-id="887de-184">Questo scenario consente di completare la configurazione di un gateway applicazione esistente con il supporto di più siti tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="887de-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="887de-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="887de-185">Next steps</span></span>

<span data-ttu-id="887de-186">Informazioni su come tooprotect i siti Web con [Gateway applicazione - Firewall applicazione Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="887de-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

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
