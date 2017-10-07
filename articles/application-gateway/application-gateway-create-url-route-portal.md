---
title: un percorso basato su aaaCreate regola - Gateway applicazione Azure - portale di Azure | Documenti Microsoft
description: Informazioni su come toocreate una regola basata sul percorso per un gateway applicazione utilizzando hello portale
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
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="adc1a-103">Creare una regola basata sul percorso per un gateway applicazione tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="adc1a-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="adc1a-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="adc1a-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="adc1a-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="adc1a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="adc1a-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="adc1a-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="adc1a-107">Il routing basato sul percorso URL consente di tooassociate route in base al percorso URL hello della richiesta Http.</span><span class="sxs-lookup"><span data-stu-id="adc1a-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="adc1a-108">Controlla se è presente un pool di back-end tooa route configurato per l'URL di hello elencato nel Gateway applicazione hello e invia toohello il traffico di rete hello è definito il pool back-end.</span><span class="sxs-lookup"><span data-stu-id="adc1a-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="adc1a-109">Un utilizzo comune per il routing basato su URL è tooload bilanciamento delle richieste per i pool di server back-end toodifferent diversi tipi di contenuto.</span><span class="sxs-lookup"><span data-stu-id="adc1a-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="adc1a-110">Routing basato su URL introduce un nuovo gateway tooapplication tipo di regola.</span><span class="sxs-lookup"><span data-stu-id="adc1a-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="adc1a-111">Per il gateway applicazione sono disponibili due tipi di regole: di base e basate sul percorso.</span><span class="sxs-lookup"><span data-stu-id="adc1a-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="adc1a-112">Hello il tipo di regola di base, fornisce il servizio di round robin per hello back-end pool durante il percorso basato su regole inoltre distribuzione round robin tooround, accetta inoltre il modello del percorso dell'URL di richiesta hello in considerazione durante la scelta di pool back-end appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="adc1a-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="adc1a-113">Scenario</span><span class="sxs-lookup"><span data-stu-id="adc1a-113">Scenario</span></span>

<span data-ttu-id="adc1a-114">Hello nello scenario seguente passa attraverso la creazione di una regola basata sul percorso in un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="adc1a-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="adc1a-115">Hello scenario si presuppone che siano state già seguite passaggi hello troppo[creare un Gateway applicazione](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="adc1a-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![route dell'URL][scenario]

## <span data-ttu-id="adc1a-117"><a name="createrule"></a>Crea regola di percorso basato su hello</span><span class="sxs-lookup"><span data-stu-id="adc1a-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="adc1a-118">Una regola di percorso richiede il proprio listener, prima di creare la regola hello essere tooverify che si dispone di un toouse listener disponibili.</span><span class="sxs-lookup"><span data-stu-id="adc1a-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="adc1a-119">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="adc1a-119">Step 1</span></span>

<span data-ttu-id="adc1a-120">Passare toohello [portale di Azure](http://portal.azure.com) e selezionare un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="adc1a-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="adc1a-121">Fare clic su **Regole**</span><span class="sxs-lookup"><span data-stu-id="adc1a-121">Click **Rules**</span></span>

![Panoramica del gateway applicazione][1]

### <a name="step-2"></a><span data-ttu-id="adc1a-123">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="adc1a-123">Step 2</span></span>

<span data-ttu-id="adc1a-124">Fare clic su **basato sul percorso** pulsante tooadd una nuova regola percorso.</span><span class="sxs-lookup"><span data-stu-id="adc1a-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="adc1a-125">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="adc1a-125">Step 3</span></span>

<span data-ttu-id="adc1a-126">Hello **Aggiungi regola di percorso basato su** blade dispone di due sezioni.</span><span class="sxs-lookup"><span data-stu-id="adc1a-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="adc1a-127">Hello prima sezione è in cui è definito listener hello, il nome di hello della regola hello e le impostazioni del percorso predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="adc1a-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="adc1a-128">impostazioni del percorso predefinito Hello sono per le route che non rientrano hello basato sul percorso della route personalizzato.</span><span class="sxs-lookup"><span data-stu-id="adc1a-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="adc1a-129">seconda sezione di hello Hello **Aggiungi regola di percorso basato su** blade viene usata per definire le regole basate sul percorso hello personalmente.</span><span class="sxs-lookup"><span data-stu-id="adc1a-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="adc1a-130">**Basic Settings**</span><span class="sxs-lookup"><span data-stu-id="adc1a-130">**Basic Settings**</span></span>

* <span data-ttu-id="adc1a-131">**Nome** -questo valore è una regola di toohello nome descrittivo che sia accessibile nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="adc1a-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="adc1a-132">**Listener** -questo valore è listener hello utilizzato per la regola di hello.</span><span class="sxs-lookup"><span data-stu-id="adc1a-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="adc1a-133">**Predefinito pool back-end** -questa impostazione è hello definisce hello toobe di back-end utilizzato per la regola predefinita hello</span><span class="sxs-lookup"><span data-stu-id="adc1a-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="adc1a-134">**Impostazioni HTTP predefinite** -questa impostazione è hello definisce hello HTTP impostazioni toobe utilizzato per la regola predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="adc1a-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="adc1a-135">**Regole basate sul percorso**</span><span class="sxs-lookup"><span data-stu-id="adc1a-135">**Path-based rules**</span></span>

* <span data-ttu-id="adc1a-136">**Nome** -questo valore è una regola basata su toopath nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="adc1a-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="adc1a-137">**Percorsi** -questa impostazione definisce hello percorso hello regola Cerca per l'inoltro del traffico</span><span class="sxs-lookup"><span data-stu-id="adc1a-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="adc1a-138">**Pool back-end** -questa impostazione è hello definisce hello toobe di back-end utilizzato per la regola hello</span><span class="sxs-lookup"><span data-stu-id="adc1a-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="adc1a-139">**Le impostazioni HTTP** -questa impostazione è hello definisce hello HTTP impostazioni toobe utilizzato per la regola hello.</span><span class="sxs-lookup"><span data-stu-id="adc1a-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="adc1a-140">Percorsi: elenco hello di toomatch modelli percorso.</span><span class="sxs-lookup"><span data-stu-id="adc1a-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="adc1a-141">Ogni deve iniziare con / e hello solo un "\*" è consentita al fine di hello.</span><span class="sxs-lookup"><span data-stu-id="adc1a-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="adc1a-142">Alcuni esempi validi sono /xyz, /xyz* o /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="adc1a-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Pannello Add path-based rule (Aggiungi regola basata sul percorso)][2]

<span data-ttu-id="adc1a-144">Aggiunta di una regola basata sul percorso di tooan gateway applicazione esistente è un processo semplice tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="adc1a-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="adc1a-145">Dopo aver creata una regola di percorso, può essere modificato tooadd altre regole.</span><span class="sxs-lookup"><span data-stu-id="adc1a-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![aggiunta di altre regole basate sul percorso][3]

<span data-ttu-id="adc1a-147">Questo passaggio configura una route basata sul percorso.</span><span class="sxs-lookup"><span data-stu-id="adc1a-147">This step configures a path-based route.</span></span> <span data-ttu-id="adc1a-148">È importante toounderstand che le richieste vengono riscritti non, come le richieste provengano in gateway applicazione controlla richiesta hello e basic hello url modello invia hello richiesta toohello appropriata back-end.</span><span class="sxs-lookup"><span data-stu-id="adc1a-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adc1a-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="adc1a-149">Next steps</span></span>

<span data-ttu-id="adc1a-150">toolearn tooconfigure offload SSL con Gateway applicazione Azure, vedere [configurare Offload SSL](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="adc1a-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
