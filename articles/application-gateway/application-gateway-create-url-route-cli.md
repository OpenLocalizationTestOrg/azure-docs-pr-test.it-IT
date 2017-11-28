---
title: regole di un gateway applicazione utilizzando l'URL di routing - aaaCreate 2.0 CLI di Azure | Documenti Microsoft
description: Questa pagina fornisce istruzioni toocreate, configurare un gateway applicazione Azure utilizzando le regole di routing di URL
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="bd1e0-103">Creare un gateway applicazione con il routing basato sul percorso con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bd1e0-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd1e0-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bd1e0-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="bd1e0-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bd1e0-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="bd1e0-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bd1e0-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="bd1e0-107">Il routing basato sul percorso URL consente di tooassociate route in base al percorso URL hello di una richiesta Http.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="bd1e0-108">Controlla se è presente un pool di back-end tooa route configurati per l'URL di hello presentati in Gateway applicazione hello e invia toohello il traffico di rete hello è definito il pool back-end.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="bd1e0-109">Un utilizzo comune per il routing basato su URL è tooload bilanciamento delle richieste per i pool di server back-end toodifferent diversi tipi di contenuto.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="bd1e0-110">Routing basato su URL introduce un nuovo gateway tooapplication tipo di regola.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="bd1e0-111">Per il gateway applicazione sono disponibili due tipi di regole: basic e PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="bd1e0-112">Tipo di regola di base fornisce servizio round robin per hello back-end pool inoltre PathBasedRouting durante la distribuzione round robin tooround, accetta inoltre il modello del percorso dell'URL di richiesta hello in considerazione durante la scelta di pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="bd1e0-113">Scenario</span><span class="sxs-lookup"><span data-stu-id="bd1e0-113">Scenario</span></span>

<span data-ttu-id="bd1e0-114">Nell'esempio seguente di hello, Gateway applicazione gestisce il traffico per contoso.com con due pool di server back-end: un pool di server predefinito e un pool di server di immagine.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="bd1e0-115">Sono richieste per http://contoso.com/image * indirizzato il pool di server tooimage (imagesBackendPool), se hello il modello del percorso non corrisponde, viene selezionato un pool di server predefinito (appGatewayBackendPool).</span><span class="sxs-lookup"><span data-stu-id="bd1e0-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![route dell'URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="bd1e0-117">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="bd1e0-117">Log in tooAzure</span></span>

<span data-ttu-id="bd1e0-118">Aprire hello **prompt dei comandi di Microsoft Azure**ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="bd1e0-119">È inoltre possibile utilizzare `az login` senza l'opzione per l'accesso di dispositivo che richiede l'immissione di un codice di aka.ms/devicelogin hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="bd1e0-120">Una volta digitato hello sopra riportato, viene fornito un codice.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="bd1e0-121">Spostarsi in un processo di accesso browser hello toocontinue toohttps://aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![Comando che illustra l'accesso al dispositivo][1]

<span data-ttu-id="bd1e0-123">Nel browser hello immettere codice hello ricevuto.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="bd1e0-124">Si è reindirizzato tooa nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-124">You are redirected tooa sign-in page.</span></span>

![codice tooenter browser][2]

<span data-ttu-id="bd1e0-126">Dopo aver immesso il codice hello si è connessi, hello Chiudi browser toocontinue scenario hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![Accesso eseguito][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="bd1e0-128">Aggiungere un gateway di applicazione esistente tooan regola basata sul percorso</span><span class="sxs-lookup"><span data-stu-id="bd1e0-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="bd1e0-129">Creare un gateway applicazione con una regola di percorso personalizzata</span><span class="sxs-lookup"><span data-stu-id="bd1e0-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="bd1e0-130">Creare un nuovo pool back-end</span><span class="sxs-lookup"><span data-stu-id="bd1e0-130">Create a new back-end pool</span></span>

<span data-ttu-id="bd1e0-131">Configurare impostazioni del gateway applicazione **imagesBackendPool** hello con bilanciamento del carico del traffico di rete nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="bd1e0-132">In questo esempio, configurare le impostazioni del pool back-end diverso per il nuovo pool back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="bd1e0-133">Ogni pool back-end può avere un'impostazione del pool back-end dedicata.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="bd1e0-134">Le impostazioni HTTP back-end vengono utilizzate per i membri del pool back-end corretto toohello traffico tooroute regole.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="bd1e0-135">Questo parametro determina il protocollo di hello e la porta utilizzata durante l'invio di traffico toohello i membri del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="bd1e0-136">Sessioni basate su cookie sono determinate anche dalle impostazioni HTTP back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="bd1e0-137">Se abilitata, l'affinità di sessione basato su cookie invia traffico toohello stesso back-end come richieste precedenti per ogni pacchetto.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="bd1e0-138">Creare una nuova porta front-end</span><span class="sxs-lookup"><span data-stu-id="bd1e0-138">Create a new front-end port</span></span>

<span data-ttu-id="bd1e0-139">Configurare hello porta front-end per un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="bd1e0-140">oggetto di configurazione di Hello porta front-end viene utilizzato un toodefine listener cosa porta hello Gateway applicazione è in attesa del traffico listener hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="bd1e0-141">Creare un nuovo listener</span><span class="sxs-lookup"><span data-stu-id="bd1e0-141">Create a new listener</span></span>

<span data-ttu-id="bd1e0-142">Configurare il listener di hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-142">Configure hello listener.</span></span> <span data-ttu-id="bd1e0-143">Questo passaggio consente di configurare il listener hello per l'indirizzo IP pubblico hello e la porta utilizzata tooreceive il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="bd1e0-144">Hello di esempio seguente accetta la configurazione IP front-end hello configurato in precedenza, la configurazione della porta front-end e un protocollo (http o https) e configura il listener hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="bd1e0-145">In questo esempio, il listener hello è in ascolto tooHTTP traffico sulla porta 82 hello indirizzo IP pubblico è stato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="bd1e0-146">Creare una mappa del percorso Url hello</span><span class="sxs-lookup"><span data-stu-id="bd1e0-146">Create hello Url path map</span></span>

<span data-ttu-id="bd1e0-147">Configurare i percorsi di regola di URL per il pool di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="bd1e0-148">Questo passaggio consente di configurare un percorso di hello utilizzato dal gateway toodefine hello mapping tra il percorso URL e il pool back-end viene assegnato il traffico in ingresso di toohandle hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd1e0-149">Ogni percorso deve iniziare con / e hello solo un "\*" è consentita, al fine di hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="bd1e0-150">Alcuni esempi validi sono /xyz, /xyz* o /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="bd1e0-151">Hello stringa inserito toohello matcher di percorso non include alcun testo dopo hello innanzitutto "?" o "#" e tali caratteri non consentiti.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="bd1e0-152">esempio Hello crea una regola per "/ immagini / *" percorso di routing del traffico tooback-end "imagesBackendPool".</span><span class="sxs-lookup"><span data-stu-id="bd1e0-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="bd1e0-153">Questa regola assicura che il traffico per ciascun set di URL sia indirizzato toohello di back-end.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="bd1e0-154">Ad esempio, http://adatum.com/images/figure1.jpg diventa troppo "imagesBackendPool".</span><span class="sxs-lookup"><span data-stu-id="bd1e0-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="bd1e0-155">Se il percorso di hello non corrisponde a una delle regole di percorso predefinito di hello, configurazione della mappa di hello regola percorso consente di configurare anche un pool di indirizzi back-end di predefinito.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="bd1e0-156">Ad esempio, http://adatum.com/shoppingcart/test.html passa toopool1 con cui è definito come il pool predefinito hello per il traffico non corrispondente.</span><span class="sxs-lookup"><span data-stu-id="bd1e0-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a><span data-ttu-id="bd1e0-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd1e0-157">Next steps</span></span>

<span data-ttu-id="bd1e0-158">Se si desidera toolearn sull'offload Secure Sockets Layer (SSL), vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bd1e0-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
