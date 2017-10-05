---
title: Creare un gateway applicazione con le regole per il routing basato su URL - Interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Questa pagina fornisce istruzioni per la creazione e la configurazione di un gateway applicazione di Azure con le regole per il routing basato su URL
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
ms.openlocfilehash: 958049830d6753ec26635f18f8f8b2fabdec0733
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="718f3-103">Creare un gateway applicazione con il routing basato sul percorso con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="718f3-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="718f3-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="718f3-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="718f3-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="718f3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="718f3-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="718f3-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="718f3-107">Il routing basato sul percorso dell'URL consente di associare le route in base al percorso dell'URL di una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="718f3-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="718f3-108">Verifica se è disponibile una route per il pool back-end configurato per l'URL presentato nel gateway applicazione e invia il traffico di rete al pool back-end definito.</span><span class="sxs-lookup"><span data-stu-id="718f3-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="718f3-109">In genere il routing basato su URL viene usato per le richieste di bilanciamento del carico per diversi tipi di contenuto tra vari pool di server back-end.</span><span class="sxs-lookup"><span data-stu-id="718f3-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="718f3-110">Il routing basato su URL introduce un nuovo tipo di regola per i gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="718f3-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="718f3-111">Per il gateway applicazione sono disponibili due tipi di regole: basic e PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="718f3-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="718f3-112">Il tipo di regola basic fornisce un servizio di tipo round robin per i pool back-end, mentre la regola PathBasedRouting oltre alla distribuzione round robin tiene conto del modello di percorso dell'URL della richiesta per la scelta del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="718f3-112">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="718f3-113">Scenario</span><span class="sxs-lookup"><span data-stu-id="718f3-113">Scenario</span></span>

<span data-ttu-id="718f3-114">Nell'esempio seguente il gateway applicazione gestisce il traffico per contoso.com con due pool di server back-end: un pool di server predefinito e un pool di server immagini.</span><span class="sxs-lookup"><span data-stu-id="718f3-114">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="718f3-115">Le richieste per http://contoso.com/image* vengono indirizzate al pool di server immagini (imagesBackendPool). Se il modello del percorso non corrisponde, viene selezionato un pool di server predefinito (appGatewayBackendPool).</span><span class="sxs-lookup"><span data-stu-id="718f3-115">Requests for http://contoso.com/image* are routed to image server pool (imagesBackendPool), if the path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![route dell'URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="718f3-117">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="718f3-117">Log in to Azure</span></span>

<span data-ttu-id="718f3-118">Aprire il **prompt dei comandi di Microsoft Azure**ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="718f3-118">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="718f3-119">È anche possibile usare `az login` senza l'opzione per l'accesso del dispositivo che richiede l'immissione di un codice in aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="718f3-119">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="718f3-120">Dopo avere digitato l'esempio precedente, viene fornito un codice.</span><span class="sxs-lookup"><span data-stu-id="718f3-120">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="718f3-121">Passare a https://aka.ms/devicelogin in un browser per continuare il processo di accesso.</span><span class="sxs-lookup"><span data-stu-id="718f3-121">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![Comando che illustra l'accesso al dispositivo][1]

<span data-ttu-id="718f3-123">Nel browser immettere il codice ricevuto.</span><span class="sxs-lookup"><span data-stu-id="718f3-123">In the browser, enter the code you received.</span></span> <span data-ttu-id="718f3-124">Si verrà reindirizzati a una pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="718f3-124">You are redirected to a sign-in page.</span></span>

![Browser in cui immettere il codice][2]

<span data-ttu-id="718f3-126">Dopo avere immesso il codice ed effettuato l'accesso, chiudere il browser per continuare con lo scenario.</span><span class="sxs-lookup"><span data-stu-id="718f3-126">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![Accesso eseguito][3]

## <a name="add-a-path-based-rule-to-an-existing-application-gateway"></a><span data-ttu-id="718f3-128">Aggiungere una regola basata su percorso a un gateway applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="718f3-128">Add a path-based rule to an existing application gateway</span></span>

<span data-ttu-id="718f3-129">Creare un gateway applicazione con una regola di percorso personalizzata</span><span class="sxs-lookup"><span data-stu-id="718f3-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="718f3-130">Creare un nuovo pool back-end</span><span class="sxs-lookup"><span data-stu-id="718f3-130">Create a new back-end pool</span></span>

<span data-ttu-id="718f3-131">Configurare l'impostazione **imagesBackendPool** del gateway applicazione per il traffico di rete con carico bilanciato nel pool back-end.</span><span class="sxs-lookup"><span data-stu-id="718f3-131">Configure application gateway setting **imagesBackendPool** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="718f3-132">In questo esempio vengono configurate diverse impostazioni per il nuovo pool back-end.</span><span class="sxs-lookup"><span data-stu-id="718f3-132">In this example, you configure different back-end pool settings for the new back-end pool.</span></span> <span data-ttu-id="718f3-133">Ogni pool back-end può avere un'impostazione del pool back-end dedicata.</span><span class="sxs-lookup"><span data-stu-id="718f3-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="718f3-134">Le impostazioni HTTP back-end vengono usate dalle regole per instradare il traffico verso i membri del pool di back-end corretti.</span><span class="sxs-lookup"><span data-stu-id="718f3-134">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="718f3-135">Ciò determina il protocollo e la porta usati durante l'invio di traffico ai membri del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="718f3-135">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="718f3-136">Anche le sessioni basate sui cookie sono determinate dalle impostazioni HTTP di back-end.</span><span class="sxs-lookup"><span data-stu-id="718f3-136">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="718f3-137">Se abilitata, l'affinità di sessione basata su cookie invia traffico allo stesso back-end sotto forma di richieste precedenti per ogni pacchetto.</span><span class="sxs-lookup"><span data-stu-id="718f3-137">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="718f3-138">Creare una nuova porta front-end</span><span class="sxs-lookup"><span data-stu-id="718f3-138">Create a new front-end port</span></span>

<span data-ttu-id="718f3-139">Configurare la porta front-end per un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="718f3-139">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="718f3-140">L'oggetto di configurazione della porta front-end viene usato da un listener per definire la porta del gateway applicazione in ascolto del traffico nel listener.</span><span class="sxs-lookup"><span data-stu-id="718f3-140">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="718f3-141">Creare un nuovo listener</span><span class="sxs-lookup"><span data-stu-id="718f3-141">Create a new listener</span></span>

<span data-ttu-id="718f3-142">Configurare il listener.</span><span class="sxs-lookup"><span data-stu-id="718f3-142">Configure the listener.</span></span> <span data-ttu-id="718f3-143">Questo passaggio configura il listener per l'indirizzo IP pubblico e la porta usata per ricevere il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="718f3-143">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="718f3-144">L'esempio seguente prende in considerazione la configurazione IP front-end configurata in precedenza, la configurazione della porta front-end e un protocollo (HTTP o HTTPS) e configura il listener.</span><span class="sxs-lookup"><span data-stu-id="718f3-144">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="718f3-145">In questo esempio, il listener è in ascolto per il traffico HTTP sulla porta 82 all'indirizzo IP pubblico che è stato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="718f3-145">In this example, the listener listens to HTTP traffic on port 82 on the public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-the-url-path-map"></a><span data-ttu-id="718f3-146">Creare il mapping dei percorsi URL</span><span class="sxs-lookup"><span data-stu-id="718f3-146">Create the Url path map</span></span>

<span data-ttu-id="718f3-147">Configurare i percorsi della regola per gli URL per i pool back-end.</span><span class="sxs-lookup"><span data-stu-id="718f3-147">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="718f3-148">Questo passaggio configura il percorso relativo usato dal gateway applicazione per definire il mapping tra il percorso dell'URL e il pool back-end selezionato per gestire il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="718f3-148">This step configures the relative path used by application gateway to define the mapping between URL path and which back-end pool is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="718f3-149">Ogni percorso deve iniziare con una barra / e l'unica posizione in cui è consentito il carattere "\*" è alla fine.</span><span class="sxs-lookup"><span data-stu-id="718f3-149">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="718f3-150">Esempi validi sono /xyz, /xyz* or /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="718f3-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="718f3-151">La stringa inviata al selettore di percorsi non include alcun testo dopo il primo carattere "?" o "#" e questi caratteri non sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="718f3-151">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="718f3-152">L'esempio seguente crea una regola per il percorso "/images/*" che instrada il traffico al back-end "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="718f3-152">The following example creates one rule for "/images/*" path routing traffic to back-end "imagesBackendPool."</span></span> <span data-ttu-id="718f3-153">Questa regola assicura che il traffico per ogni set di URL venga indirizzato al back-end.</span><span class="sxs-lookup"><span data-stu-id="718f3-153">This rule ensures that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="718f3-154">Ad esempio, http://adatum.com/images/figure1.jpg passa a "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="718f3-154">For example, http://adatum.com/images/figure1.jpg goes to "imagesBackendPool."</span></span> <span data-ttu-id="718f3-155">In caso di mancata corrispondenza con le regole di percorso predefinite, la configurazione del mapping dei percorsi della regola configura anche un pool di indirizzi back-end predefinito.</span><span class="sxs-lookup"><span data-stu-id="718f3-155">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="718f3-156">Ad esempio, http://adatum.com/shoppingcart/test.html passa al pool1 definito come pool predefinito per il traffico senza corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="718f3-156">For example, http://adatum.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="718f3-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="718f3-157">Next steps</span></span>

<span data-ttu-id="718f3-158">Per informazioni sull'offload SSL (Secure Sockets Layer), vedere [Configurare un gateway applicazione per l'offload SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="718f3-158">If you want to learn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
