---
title: Creare una regola basata sul percorso - Gateway applicazione di Azure - Portale di Azure | Microsoft Docs
description: Informazioni su come creare una regola basata sul percorso per un gateway applicazione tramite il portale
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: c184e94a04cfbdedcae70ed154aeb7dd134d1baf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-the-portal"></a><span data-ttu-id="05d92-103">Creare una regola basata sul percorso per un gateway applicazione usando il portale</span><span class="sxs-lookup"><span data-stu-id="05d92-103">Create a Path-based rule for an application gateway by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="05d92-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="05d92-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="05d92-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05d92-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="05d92-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="05d92-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="05d92-107">Il routing basato sul percorso dell'URL consente di associare le route in base al percorso dell'URL della richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="05d92-107">URL Path-based routing enables you to associate routes based on the URL path of Http request.</span></span> <span data-ttu-id="05d92-108">Verifica se è disponibile una route per il pool back-end configurato per l'URL elencato nel gateway applicazione e invia il traffico di rete al pool back-end definito.</span><span class="sxs-lookup"><span data-stu-id="05d92-108">It checks if there is a route to a back-end pool configured for the URL listed in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="05d92-109">In genere il routing basato su URL viene usato per le richieste di bilanciamento del carico per diversi tipi di contenuto tra vari pool di server back-end.</span><span class="sxs-lookup"><span data-stu-id="05d92-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="05d92-110">Il routing basato su URL introduce un nuovo tipo di regola per i gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="05d92-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="05d92-111">Per il gateway applicazione sono disponibili due tipi di regole: di base e basate sul percorso.</span><span class="sxs-lookup"><span data-stu-id="05d92-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="05d92-112">Il tipo di regola di base fornisce un servizio di tipo round robin per i pool back-end, mentre le regole basate sul percorso, oltre alla distribuzione round robin, tengono conto del modello di percorso dell'URL della richiesta per la scelta del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="05d92-112">The basic rule type, provides round-robin service for the back-end pools while path-based rules in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="05d92-113">Scenario</span><span class="sxs-lookup"><span data-stu-id="05d92-113">Scenario</span></span>

<span data-ttu-id="05d92-114">Lo scenario seguente illustra la creazione di una regola basata sul percorso in un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="05d92-114">The following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="05d92-115">Lo scenario presuppone che sia già stata seguita la procedura per [creare un gateway applicazione](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="05d92-115">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![route dell'URL][scenario]

## <span data-ttu-id="05d92-117"><a name="createrule"></a>Creare la regola basata sul percorso</span><span class="sxs-lookup"><span data-stu-id="05d92-117"><a name="createrule"></a>Create the Path-based rule</span></span>

<span data-ttu-id="05d92-118">Una regola basata sul percorso richiede un proprio listener. Prima di creare la regola, verificare di avere un listener disponibile all'uso.</span><span class="sxs-lookup"><span data-stu-id="05d92-118">A Path-based rule requires its own listener, before creating the rule be sure to verify you have an available listener to use.</span></span>

### <a name="step-1"></a><span data-ttu-id="05d92-119">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="05d92-119">Step 1</span></span>

<span data-ttu-id="05d92-120">Passare al [portale di Azure](http://portal.azure.com) e selezionare un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="05d92-120">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="05d92-121">Fare clic su **Regole**</span><span class="sxs-lookup"><span data-stu-id="05d92-121">Click **Rules**</span></span>

![Panoramica del gateway applicazione][1]

### <a name="step-2"></a><span data-ttu-id="05d92-123">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="05d92-123">Step 2</span></span>

<span data-ttu-id="05d92-124">Fare clic sul pulsante **Basata sul percorso** per aggiungere una nuova regola di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="05d92-124">Click **Path-based** button to add a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="05d92-125">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="05d92-125">Step 3</span></span>

<span data-ttu-id="05d92-126">Il pannello **Add path-based rule** (Aggiungi regola basata sul percorso) contiene due sezioni.</span><span class="sxs-lookup"><span data-stu-id="05d92-126">The **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="05d92-127">La prima è la sezione in cui sono stati definiti il listener, il nome della regola e le impostazioni del percorso predefinito.</span><span class="sxs-lookup"><span data-stu-id="05d92-127">The first section is where you defined the listener, the name of the rule and the default path settings.</span></span> <span data-ttu-id="05d92-128">Le impostazioni del percorso predefinite sono per le route che non rientrano nella route personalizzata basata sul percorso.</span><span class="sxs-lookup"><span data-stu-id="05d92-128">The default path settings are for routes that do not fall under the custom path-based route.</span></span> <span data-ttu-id="05d92-129">La seconda sezione dl pannello **Add path-based rule** (Aggiungi regola basata sul percorso) viene usata per definire le regole stesse basate sul percorso.</span><span class="sxs-lookup"><span data-stu-id="05d92-129">The second section of the **Add path-based rule** blade is where you define the path-based rules themselves.</span></span>

<span data-ttu-id="05d92-130">**Basic Settings**</span><span class="sxs-lookup"><span data-stu-id="05d92-130">**Basic Settings**</span></span>

* <span data-ttu-id="05d92-131">**Nome**: nome descrittivo della regola accessibile nel portale.</span><span class="sxs-lookup"><span data-stu-id="05d92-131">**Name** - This value is a friendly name to the rule that is accessible in the portal.</span></span>
* <span data-ttu-id="05d92-132">**Listener** : questo valore è il listener usato per la regola.</span><span class="sxs-lookup"><span data-stu-id="05d92-132">**Listener** - This value is the listener that is used for the rule.</span></span>
* <span data-ttu-id="05d92-133">**Default backend pool** (Pool back-end predefinito): questa impostazione definisce il back-end da usare per la regola predefinita.</span><span class="sxs-lookup"><span data-stu-id="05d92-133">**Default backend pool** - This setting is the setting that defines the back-end to be used for the default rule</span></span>
* <span data-ttu-id="05d92-134">**Default HTTP settings** (Impostazioni HTTP predefinite ): questa impostazione definisce le impostazioni HTTP da usare per la regola predefinita.</span><span class="sxs-lookup"><span data-stu-id="05d92-134">**Default HTTP settings** - This setting is the setting that defines the HTTP settings to be used for the default rule.</span></span>

<span data-ttu-id="05d92-135">**Regole basate sul percorso**</span><span class="sxs-lookup"><span data-stu-id="05d92-135">**Path-based rules**</span></span>

* <span data-ttu-id="05d92-136">**Nome**: questo valore è un nome descrittivo della regola basata sul percorso.</span><span class="sxs-lookup"><span data-stu-id="05d92-136">**Name** - This value is a friendly name to path-based rule.</span></span>
* <span data-ttu-id="05d92-137">**Percorsi** : questa impostazione definisce il percorso cercato dalla regola per l'inoltro del traffico.</span><span class="sxs-lookup"><span data-stu-id="05d92-137">**Paths** - This setting defines the path the rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="05d92-138">**Pool back-end** : questa impostazione definisce il back-end da usare per la regola.</span><span class="sxs-lookup"><span data-stu-id="05d92-138">**Backend Pool** - This setting is the setting that defines the back-end to be used for the rule</span></span>
* <span data-ttu-id="05d92-139">**Impostazione HTTP** : questa impostazione definisce le impostazioni HTTP da usare per la regola.</span><span class="sxs-lookup"><span data-stu-id="05d92-139">**HTTP setting** - This setting is the setting that defines the HTTP settings to be used for the rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05d92-140">Percorsi: elenco dei modelli di percorso usati per la corrispondenza.</span><span class="sxs-lookup"><span data-stu-id="05d92-140">Paths: The list of path patterns to match.</span></span> <span data-ttu-id="05d92-141">Ognuno deve iniziare con una barra / e l'unica posizione in cui è consentito il carattere "\*" è alla fine.</span><span class="sxs-lookup"><span data-stu-id="05d92-141">Each must start with / and the only place a "\*" is allowed is at the end.</span></span> <span data-ttu-id="05d92-142">Alcuni esempi validi sono /xyz, /xyz* o /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="05d92-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Pannello Add path-based rule (Aggiungi regola basata sul percorso)][2]

<span data-ttu-id="05d92-144">L'aggiunta di una regola basata sul percorso a un gateway applicazione esistente è un processo semplice con il portale.</span><span class="sxs-lookup"><span data-stu-id="05d92-144">Adding a path-based rule to an existing application gateway is an easy process through the portal.</span></span> <span data-ttu-id="05d92-145">Dopo aver creato una regola basata sul percorso, è possibile modificarla per aggiungere altre regole.</span><span class="sxs-lookup"><span data-stu-id="05d92-145">After a path-based rule has been created, it can be edited to add additional rules.</span></span> 

![aggiunta di altre regole basate sul percorso][3]

<span data-ttu-id="05d92-147">Questo passaggio configura una route basata sul percorso.</span><span class="sxs-lookup"><span data-stu-id="05d92-147">This step configures a path-based route.</span></span> <span data-ttu-id="05d92-148">È importante comprendere che le richieste non vengono scritte di nuovo: quando arriva una richiesta, il gateway applicazione la controlla e quindi la regola di base sul modello di URL la invia al back-end appropriato.</span><span class="sxs-lookup"><span data-stu-id="05d92-148">It is important to understand that requests are not rewritten, as requests come in application gateway inspects the request and basic on the url pattern sends the request to the appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05d92-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05d92-149">Next steps</span></span>

<span data-ttu-id="05d92-150">Per informazioni su come configurare l'offload SSL con un gateway applicazione di Azure, vedere [Configurare un gateway applicazione per l'offload SSL con il portale](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="05d92-150">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
